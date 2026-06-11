# Lab 10 — Robustness Battery v2: One-Command Submission-Grade Appendix

Week 8 ended with a robustness suite that ran. It produced a specification curve, a wild-cluster bootstrap, an Oster $\delta$, a placebo, and a Bonferroni-adjusted heterogeneity table — six artifacts called by `make robust`, defending the paper against the average referee on the average day. Week 9 put that paper in front of a *real* audience and the audience asked harder questions. Three of the four comments your Chapter 10.1 triage flagged as **Required** were robustness questions disguised as substantive ones: *is the effect the same across market regimes? does the mechanism survive once you instrument the mediator? would the estimate transport to a population the discussant cares about?* The honest answer to all three is "Week 8's battery does not yet address that." Lab 10 is where the battery becomes the one that does.

The discipline this lab drills separates a working paper from a *submission*. **A submission-grade battery is not a longer list of tests; it is a tighter list, wired into a single Makefile target that regenerates every appendix table from raw bytes in one command, with each test answering a *named* threat from your Chapter 7.5 table and producing an artifact your paper `\input{}`s rather than an output you copy-paste.** A referee who clones your repo and types `make appendix` should see the same five appendix tables that appear in the PDF, rebuilt from scratch, no manual steps. That is the bar.

Nothing in Lab 10 requires the internet at run time; the licensed pulls were frozen in Lab 7 and the analysis runs on local Parquet snapshots. The five new tests — Romano-Wolf step-down, causal-forest CATE with honest inference, mediation via the Acharya-Blackwell-Sen controlled-direct-effect estimator, Oster bounds at $R_{\max}$ swept, and transportability reweighting — are all CPU-bound. Plan for 15-25 minutes end-to-end on a fresh clone.

---

## Learning goals

By the end of this lab you will be able to:

1. **Architect a robustness pipeline as a DAG of `make` targets**, each target producing exactly one `.tex` table or `.pdf` figure that the paper `\input{}`s — no copy-paste, no manual steps, no orphan outputs.
2. **Operationalize Chapter 10.2's Romano-Wolf step-down** as a Python module that takes a coefficient family and a residual-bootstrap function and returns FWER-adjusted p-values, then wire it into the heterogeneity appendix.
3. **Fit a causal forest CATE on a *pre-registered* feature list** with Athey-Wager honest inference, ship the CATE histogram and the GATE-by-quintile plot to the paper, and write the pre-registration footnote that keeps the analysis honest.
4. **Run an Acharya-Blackwell-Sen sequential-g controlled-direct-effect (CDE) mediation audit** on a candidate channel, comparing the CDE to the biased Baron-Kenny estimate so the appendix shows the gap.
5. **Compute Oster $\delta$ at a swept range of $R_{\max}$ values** with the assumption made explicit, plot the bound curve, and report the result as a sensitivity interval rather than a single number.
6. **Apply transportability reweighting** that maps the in-sample ATT to a named target population (the one the discussant cared about) and reports the bound on how far the estimate could move.
7. **Wire all five tests behind a single `make appendix` target** whose `manifest.json` lists each output's SHA-256, and verify that `make clean && make appendix` reproduces every byte on a fresh clone.

---

## Setup

You already have the Week 8 capstone repository with the Lab 8 `Makefile`, the Lab 9 `bundle/`, and the Week 10 revision branch that Chapter 10.1's triage memo lives on. Lab 10 needs three additions: a `src/robust2/` Python package for the new estimators, an `appendix/` LaTeX folder for the new tables, and an updated `Makefile` whose `appendix` target wires them together.

Probe what is present before you start:

```bash
python -c "import econml, statsmodels, linearmodels, pyfixest; print('OK')"
python -c "from sklearn.ensemble import RandomForestRegressor; print('OK')"
python -c "import pandas; print(pandas.__version__)"   # should be >= 2.2
which make && make --version | head -1
```

If `econml` is not present (the EconML library ships the Athey-Wager honest causal forest), install it into the camp env: `pip install econml==0.15.1`. If your camp container is offline, the fallback is the `grf-python` package (`pip install grf` — a thinner port of the R `grf` library). The lab text uses `econml`'s `CausalForestDML` because its API is closer to scikit-learn and the EconML team maintains the honest-splitting reference implementation. If you ship with `grf`, document the substitution in your `environment.yml` and your appendix footnote — the algorithm is the same.

Create the new folders and stub files:

```bash
cd capstone-2026-<you>
mkdir -p src/robust2 appendix tests/robust2
touch src/robust2/__init__.py src/robust2/romano_wolf.py src/robust2/cate.py
touch src/robust2/mediation.py src/robust2/oster.py src/robust2/transport.py
touch appendix/tab_rw.tex appendix/tab_cate.tex appendix/tab_cde.tex
touch appendix/tab_oster.tex appendix/tab_transport.tex
touch appendix/fig_cate_hist.pdf appendix/fig_oster_curve.pdf
```

The Lab 7/8 rule still binds: **the repository travels freely, the licensed bytes do not.** The pipeline reads from `data/clean/panel.parquet` (built in Lab 7 from CRSP / HMDA / FRED snapshots) and writes to `appendix/`. The `data/raw/` folder containing the licensed bytes is `.gitignore`d; a referee clones the repo, points `DATA_ROOT` at their own WRDS-mounted volume, and the pipeline rebuilds.

---

## Part 1 — The pipeline as a DAG

A robustness suite is a directed acyclic graph: every test reads the same cleaned panel, every test writes its own `.tex` (and possibly `.pdf`) artifact, no test depends on another's output, and the paper's appendix `\input{}`s those artifacts by filename. The benefit of articulating this as a graph is **isolation under failure**: if the CATE forest fails, the Romano-Wolf and Oster targets still build, and you fix the forest without re-running the rest. Lab 8's `make robust` was sequential; Lab 10's `make appendix` is five rules in parallel plus one top rule depending on all five.

### 1.1 The Makefile structure

Here is the target graph, simplified to the five new tests:

```makefile
# Makefile excerpt — robustness battery v2
PANEL    := data/clean/panel.parquet
SEED     := 42
PYTHON   := python -W error::DeprecationWarning

.PHONY: appendix appendix_clean rw cate cde oster transport

appendix: appendix/tab_rw.tex appendix/tab_cate.tex appendix/tab_cde.tex \
          appendix/tab_oster.tex appendix/tab_transport.tex \
          appendix/fig_cate_hist.pdf appendix/fig_oster_curve.pdf \
          appendix/manifest.json

appendix/tab_rw.tex: $(PANEL) src/robust2/romano_wolf.py
	$(PYTHON) -m src.robust2.romano_wolf \
	    --panel $(PANEL) --out $@ --seed $(SEED) --B 999

appendix/tab_cate.tex appendix/fig_cate_hist.pdf: $(PANEL) src/robust2/cate.py \
                                                  appendix/cate_features.json
	$(PYTHON) -m src.robust2.cate \
	    --panel $(PANEL) --features appendix/cate_features.json \
	    --out-tex appendix/tab_cate.tex --out-fig appendix/fig_cate_hist.pdf \
	    --seed $(SEED) --n-trees 4000

appendix/tab_cde.tex: $(PANEL) src/robust2/mediation.py
	$(PYTHON) -m src.robust2.mediation \
	    --panel $(PANEL) --out $@ --seed $(SEED)

appendix/tab_oster.tex appendix/fig_oster_curve.pdf: $(PANEL) src/robust2/oster.py
	$(PYTHON) -m src.robust2.oster \
	    --panel $(PANEL) \
	    --out-tex appendix/tab_oster.tex --out-fig appendix/fig_oster_curve.pdf

appendix/tab_transport.tex: $(PANEL) src/robust2/transport.py appendix/target_pop.csv
	$(PYTHON) -m src.robust2.transport \
	    --panel $(PANEL) --target appendix/target_pop.csv --out $@ --seed $(SEED)

appendix/manifest.json: appendix/tab_rw.tex appendix/tab_cate.tex appendix/tab_cde.tex \
                       appendix/tab_oster.tex appendix/tab_transport.tex \
                       appendix/fig_cate_hist.pdf appendix/fig_oster_curve.pdf
	$(PYTHON) tools/manifest.py appendix/ > $@

appendix_clean:
	rm -f appendix/tab_*.tex appendix/fig_*.pdf appendix/manifest.json
```

Three things to notice. **First**, every target lists its inputs explicitly: the panel, the script, and (for CATE) the pre-registered feature list. Change `panel.parquet` and every test rebuilds; change only `cate.py` and only CATE rebuilds. **Second**, the seed is a CLI flag, not hard-coded — a referee can rerun with a different seed. **Third**, `manifest.json` runs *last*, so its SHA-256 hashes always match the shipped artifacts.

`make -j5 appendix` cuts wall-clock from ~25 minutes serial to ~7 minutes parallel. Verify parallel reproduces before committing: `make appendix_clean && make -j1 appendix`, save the manifest, then `make appendix_clean && make -j5 appendix`, and diff. Any differing SHA-256 is a race or unsealed randomness — fix it.

### 1.2 Why `\input{}` is non-negotiable

The Week 8 paper's tables were already built by code. Lab 10 doubles down: **every number in the appendix is read from a file written by code, never typed into LaTeX.** Maya's appendix has

```latex
\begin{table}[t]\centering
\caption{Romano-Wolf step-down adjusted p-values across heterogeneity cuts.}
\input{appendix/tab_rw.tex}
\end{table}
```

and `appendix/tab_rw.tex` is a `\begin{tabular}...\end{tabular}` block produced by `pandas.DataFrame.to_latex`. The PDF is the same either way, but the **invariant a referee tests** differs: with `\input{}`, `make appendix && pdflatex` produces a paper whose appendix numbers match the manifest's hashes; with typed numbers, that test silently fails. Sam learned this in Lab 8 when his Oster $\delta$ table said 0.42 but the manifest CSV said 0.38 — a twelve-second referee catch, a polite-but-final email.

---

## Part 2 — Romano-Wolf step-down across the heterogeneity family

Chapter 10.2 §5 introduced the Romano-Wolf step-down. The intuition: when you test $m$ hypotheses on the same dataset, the test statistics are *correlated* — two heterogeneity cuts on the same panel share noise — and Bonferroni (which assumes the worst-case correlation, i.e., independence) is unnecessarily conservative. Romano-Wolf bootstraps the joint distribution of the test statistics under the null and walks down from the most extreme one, adjusting in a way that respects the empirical correlation. The result is **FWER control with substantially more power than Bonferroni when tests are correlated.** Lab 10 wires it into the heterogeneity appendix.

### 2.1 The estimator interface

The module `src/robust2/romano_wolf.py` exposes one function:

```python
# src/robust2/romano_wolf.py
"""
Romano-Wolf step-down FWER adjustment via residual bootstrap.

Reference: Romano, J. P., & Wolf, M. (2005). Stepwise multiple testing as
formalized data snooping. Econometrica, 73(4), 1237-1282.
"""
from __future__ import annotations
import argparse
import json
from pathlib import Path

import numpy as np
import pandas as pd


def romano_wolf_adjust(
    point_estimates: np.ndarray,
    null_bootstrap_draws: np.ndarray,
    *,
    one_sided: bool = False,
) -> np.ndarray:
    """
    Compute Romano-Wolf step-down adjusted p-values.

    Parameters
    ----------
    point_estimates : (m,) array of original test statistics |t_j|.
    null_bootstrap_draws : (B, m) array of bootstrap statistics under the
        joint null (recentered around 0).
    one_sided : if True, do not take absolute value.

    Returns
    -------
    p_adj : (m,) array of step-down adjusted p-values, aligned with the
        input order.
    """
    if not one_sided:
        point_estimates = np.abs(point_estimates)
        null_bootstrap_draws = np.abs(null_bootstrap_draws)

    m = point_estimates.shape[0]
    order = np.argsort(-point_estimates)  # largest stat first
    sorted_stats = point_estimates[order]

    # max statistic over the still-active hypotheses in each bootstrap draw,
    # walking from the largest stat (hardest to reject the easy way) down.
    p_sorted = np.empty(m)
    active = np.ones(m, dtype=bool)
    for k in range(m):
        # for the k-th ranked stat, the null distribution is the max over the
        # currently-active hypotheses (those not yet rejected).
        active_idx = order[k:]
        null_max = null_bootstrap_draws[:, active_idx].max(axis=1)
        # raw p-value: fraction of bootstrap draws whose max exceeds our stat.
        p_raw_k = (null_max >= sorted_stats[k]).mean()
        # enforce monotonicity: adjusted p must be non-decreasing in rank.
        if k == 0:
            p_sorted[k] = p_raw_k
        else:
            p_sorted[k] = max(p_raw_k, p_sorted[k - 1])

    p_adj = np.empty(m)
    p_adj[order] = p_sorted
    return p_adj
```

The function takes the original test statistics and a matrix of bootstrap draws under the joint null. The caller produces the bootstrap matrix; the module walks down the rank order and enforces monotonicity. This separation is deliberate. **Different designs need different bootstraps**: a panel DiD needs a *cluster bootstrap*; an IV design needs a *residual bootstrap*; an intraday-momentum design needs a *block bootstrap* that preserves serial dependence. Romano-Wolf cares only that the matrix represents the joint null.

The driver reads Maya's panel, runs the heterogeneity regressions, runs $B = 999$ cluster bootstrap replications under the recentered null, calls `romano_wolf_adjust`, and writes the LaTeX table. The full driver is at `src/robust2/romano_wolf.py:_run`; the structure is:

```python
def _run(args):
    rng = np.random.default_rng(args.seed)
    panel = pd.read_parquet(args.panel)

    cuts = [
        ("Examination intensity: high",   panel["exam_intensity"] == "high"),
        ("Examination intensity: medium", panel["exam_intensity"] == "medium"),
        ("Minority share: top tercile",   panel["min_share_tercile"] == 3),
        ("MSA counties",                  panel["msa"] == 1),
        ("CRA overlap",                   panel["cra_overlap"] == 1),
    ]
    point_t, boot_t = _bootstrap_cluster(panel, cuts, B=args.B, rng=rng)
    p_adj = romano_wolf_adjust(point_t, boot_t)
    p_bonf = np.minimum(1.0, _two_sided_p(point_t) * len(cuts))

    out = pd.DataFrame({
        "Cut": [c[0] for c in cuts],
        "Point $|t|$": point_t,
        "Unadj p": _two_sided_p(point_t),
        "Bonferroni p": p_bonf,
        "Romano-Wolf p": p_adj,
    })
    out.to_latex(args.out, index=False, escape=False, float_format="%.4f")
```

Three things make the resulting table publication-grade. First, the **unadjusted column is shown alongside the adjusted columns** — hiding it is the move of someone who has something to hide. Second, **Bonferroni and Romano-Wolf are both reported**, so the gain from respecting correlation is visible. Third, the **bootstrap seed and $B = 999$ are in the caption**, so a referee can re-run.

### 2.2 The wild-cluster bootstrap inside Romano-Wolf

`_bootstrap_cluster` follows Cameron-Gelbach-Miller (2008) with the wild-cluster modification of MacKinnon-Webb (2018): each draw multiplies cluster-level residuals by a Rademacher $\pm 1$, recomputes the statistic, stacks across $B$ draws. Recentering — subtracting the original cluster mean before resampling — makes the bootstrap consistent under the *joint* null.

The trap to call out: if Maya's design has *few treated clusters* (her staggered DiD treats six states), wild-cluster is right but its Rademacher distribution gives only $2^6 = 64$ distinct draws. Adjusted p-values cannot fall below $1/64 \approx 0.016$, and any "$p < 0.01$" claim is an artifact of the procedure's resolution. The fix: report the discreteness floor in the footnote: *"Wild-cluster bootstrap over $G = 6$ treated clusters; adjusted p-values cannot fall below $1/64 \approx 0.016$."* That footnote turns a borderline result into a defensible one.

---

## Part 3 — Causal forest CATE with honest inference, pre-registered features

Chapter 10.3 §4 introduced the causal forest. The estimator is Athey-Wager (2019)'s honest-splitting random forest: each tree splits on one half of the data and estimates leaf-level treatment effects on the other half, the two halves are independent, and the CATE estimator $\hat\tau(\mathbf{x})$ inherits an asymptotic normal distribution from the leaf-level mean structure. The result is **pointwise confidence intervals for the CATE that are valid under the design's identifying assumptions**, not a black-box prediction. Lab 10 fits the forest, plots the CATE histogram, reports the GATE by predicted-CATE quintile, and ships the pre-registration footnote.

### 3.1 The pre-registration footnote

The discipline that makes a CATE result honest is **a feature list committed to a file in the repository before the forest is fit.** Maya's PAP from Week 7 listed four moderators: examination intensity (categorical, 3 levels), county minority share (continuous), MSA status (binary), and CRA-overlap (binary). Lab 10 adds four pre-treatment county characteristics — log population, log median income, share of mortgage applications from first-time buyers, and the county's three-year-pre-treatment denial-gap trend — for a total of eight features. The feature list lives in `appendix/cate_features.json`, committed before any forest is fit:

```json
{
  "version": "1.0",
  "committed_at_commit": "<hash from `git rev-parse HEAD` at the time of commit>",
  "features": [
    "exam_intensity",
    "min_share_continuous",
    "msa",
    "cra_overlap",
    "log_pop",
    "log_median_income",
    "first_time_buyer_share",
    "pre_treatment_gap_trend_3y"
  ],
  "rationale": "All eight pre-specified in PAP § 4 (Week 7). No post-hoc additions; any feature added after this commit is post-hoc and reported as such in the appendix footnote."
}
```

The footnote in the appendix reads: **"The causal-forest CATE estimator uses the eight pre-treatment features listed in `appendix/cate_features.json`, committed at git hash `<...>` before any forest fit. The file is the pre-registration; deviations from it are post-hoc and would be reported as such."** That sentence is the difference between a CATE result a referee believes and a CATE result a referee dismisses.

### 3.2 The estimator

```python
# src/robust2/cate.py — abridged
from econml.dml import CausalForestDML
from sklearn.ensemble import RandomForestRegressor, RandomForestClassifier
import numpy as np
import pandas as pd
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt


def fit_causal_forest(
    panel: pd.DataFrame,
    *,
    outcome: str,
    treatment: str,
    features: list[str],
    n_trees: int = 4000,
    min_samples_leaf: int = 30,
    seed: int = 42,
):
    rng = np.random.default_rng(seed)
    X = panel[features].to_numpy()
    Y = panel[outcome].to_numpy()
    T = panel[treatment].to_numpy()
    # nuisance models for the orthogonalized DML estimator
    model_y = RandomForestRegressor(
        n_estimators=500, min_samples_leaf=10, random_state=seed
    )
    model_t = RandomForestClassifier(
        n_estimators=500, min_samples_leaf=10, random_state=seed
    )
    cf = CausalForestDML(
        model_y=model_y, model_t=model_t,
        n_estimators=n_trees, min_samples_leaf=min_samples_leaf,
        honest=True, inference="blb", random_state=seed,
    )
    cf.fit(Y=Y, T=T, X=X)
    cate_hat = cf.effect(X)
    cate_lo, cate_hi = cf.effect_interval(X, alpha=0.10)  # 90% CI
    return cf, cate_hat, cate_lo, cate_hi


def gate_by_quintile(cate_hat: np.ndarray, T: np.ndarray, Y: np.ndarray) -> pd.DataFrame:
    """Aggregate point estimates to GATE-by-CATE-quintile, with cluster SE."""
    q = pd.qcut(cate_hat, 5, labels=False)
    rows = []
    for k in range(5):
        mask = q == k
        # within-quintile difference in means (a simple GATE estimator)
        gate = Y[mask & (T == 1)].mean() - Y[mask & (T == 0)].mean()
        # rough SE; the production code uses cluster-bootstrap in cate.py
        se = np.sqrt(
            Y[mask & (T == 1)].var() / max((T[mask] == 1).sum(), 1)
            + Y[mask & (T == 0)].var() / max((T[mask] == 0).sum(), 1)
        )
        rows.append({"Quintile": k + 1, "GATE": gate, "SE": se,
                     "$\\hat\\tau$ midpoint": cate_hat[mask].mean()})
    return pd.DataFrame(rows)
```

The shipped figure `appendix/fig_cate_hist.pdf` is two panels: histogram of $\hat\tau(\mathbf{x})$ with ATT overlaid, and GATE-by-CATE-quintile with 90% CIs. Maya's headline: **"The CATE distribution is skewed; the lower quintile (low examination intensity, weak pre-treatment minority shares) shows essentially no effect and the top quintile (high-intensity, high-share counties) shows roughly $2.4\times$ the average. The variation is in directions the design predicted, not in directions the data discovered."** The last clause is the point: the heterogeneity matches the pre-registered moderators, not a post-hoc discovery.

### 3.3 The honest-inference caveat

Athey-Wager inference rests on the design's orthogonality and overlap assumptions. Maya's overlap is fine; a Devon-style crypto-adoption study with treatment concentrated in a thin covariate slice will see CIs explode at the support edges. The diagnostic is the propensity score from the nuisance step: mass near 0 or 1 means the CATE is not trustworthy there, and the appendix should *trim* those observations (the reference implementation trims at 5-95% and reports the trimmed share in the footnote).

---

## Part 4 — Mediation as a controlled direct effect (Acharya-Blackwell-Sen)

Chapter 10.4 hammered home that the Baron-Kenny mediation regression is almost always biased. The fix — when an instrument for the mediator is unavailable — is the **controlled direct effect (CDE)** under sequential ignorability, estimated via the Acharya-Blackwell-Sen (ABS, 2016) sequential-g procedure. Lab 10 wires the estimator into the appendix and ships the comparison to the biased Baron-Kenny estimate, so the appendix table shows the gap.

### 4.1 The two-step ABS sequential-g

The algorithm, in three lines:

1. **Step A.** Regress the mediator $M$ on the treatment $D$ and the pre-treatment covariates $\mathbf{X}$. Form the *demediated* outcome $\tilde Y = Y - \hat\gamma \cdot M$ where $\hat\gamma$ is the coefficient on $M$ when $Y$ is regressed on $D$, $M$, $\mathbf{X}$ (note: this is the *biased* coefficient on $M$, but we use it only as a transformation, not as a causal estimand).
2. **Step B.** Regress $\tilde Y$ on $D$ and $\mathbf{X}$ only (not $M$). The coefficient on $D$ is the **controlled direct effect (CDE)** of $D$ on $Y$ holding $M$ fixed at its value under treatment, under the sequential-ignorability assumption that $M$ is unconfounded given $(\mathbf{X}, D)$.
3. **Bootstrap** the whole two-step procedure $B = 1000$ times to get the CDE's standard error.

```python
# src/robust2/mediation.py — abridged
import numpy as np
import pandas as pd
import statsmodels.api as sm


def cde_seq_g(
    df: pd.DataFrame,
    outcome: str, treatment: str, mediator: str, covariates: list[str],
    *, seed: int = 42, B: int = 1000,
) -> dict:
    rng = np.random.default_rng(seed)
    Y, D, M = df[outcome].to_numpy(), df[treatment].to_numpy(), df[mediator].to_numpy()
    X = df[covariates].to_numpy()
    XdM = np.c_[D, M, X]
    XdX = np.c_[D, X]

    def _one_fit(idx):
        Yi, Di, Mi, Xi = Y[idx], D[idx], M[idx], X[idx]
        # demediation coefficient gamma from the "bad" regression — used only
        # as a transformation, not interpreted causally.
        gamma = sm.OLS(Yi, sm.add_constant(np.c_[Di, Mi, Xi])).fit().params[2]
        Y_tilde = Yi - gamma * Mi
        # CDE: coefficient on D in regression of Y_tilde on D, X.
        cde = sm.OLS(Y_tilde, sm.add_constant(np.c_[Di, Xi])).fit().params[1]
        # naive Baron-Kenny "direct" coefficient, for comparison.
        bk_direct = sm.OLS(Yi, sm.add_constant(np.c_[Di, Mi, Xi])).fit().params[1]
        # total effect, for comparison.
        total = sm.OLS(Yi, sm.add_constant(np.c_[Di, Xi])).fit().params[1]
        return cde, bk_direct, total

    point = _one_fit(np.arange(len(Y)))
    boots = np.empty((B, 3))
    for b in range(B):
        idx = rng.integers(0, len(Y), len(Y))
        boots[b] = _one_fit(idx)
    se = boots.std(axis=0, ddof=1)
    return {
        "CDE": (point[0], se[0]),
        "Baron-Kenny direct": (point[1], se[1]),
        "Total effect": (point[2], se[2]),
        "Indirect (CDE-implied)": (point[2] - point[0],
                                    np.sqrt(se[2]**2 + se[0]**2)),
    }
```

`appendix/tab_cde.tex` has four rows: total, Baron-Kenny "direct," CDE, and implied indirect (total minus CDE). Maya's headline: **"The Baron-Kenny direct effect, conditioning on compliance-training intensity, is $-0.6$ pp; the CDE under sequential ignorability is $-1.1$ pp. Baron-Kenny overstates the through-mediator channel by about 45%; the CDE-implied indirect-effect share is 21%, not the 56% the naive regression would report."** That paragraph is the audit.

### 4.2 Sequential-ignorability stated explicitly

The CDE is only as honest as the assumption: conditional on pre-treatment covariates and treatment status, no unobserved variables simultaneously drive the mediator and the outcome. This is testable only indirectly — an Oster $\delta$ on the mediator regression, a placebo using a pre-treatment outcome, or a **named sensitivity** showing how the CDE moves if an unobserved confounder of $M$ and $Y$ matches the strongest observed confounder. The reference implementation runs that sensitivity and reports the bound in the bottom row.

---

## Part 5 — Oster $\delta$ swept across $R_{\max}$

Chapter 8.2's Oster (2019) sensitivity analysis treated $R_{\max}$ — the hypothetical R-squared if every confounder were observed — as a single number, usually $1.3 \cdot \tilde R^2$ per Oster's default. Lab 10 sweeps it. The reason: **a single $\delta$ at a single $R_{\max}$ is a point estimate of a sensitivity quantity; what the appendix should ship is a *curve* that shows how $\delta$ moves as the analyst's prior about the unobservable's potential explanatory power changes.**

### 5.1 The sweep

```python
# src/robust2/oster.py — abridged
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt


def oster_delta(
    df: pd.DataFrame,
    outcome: str, treatment: str, controls: list[str],
    *, r_max_grid: np.ndarray,
) -> pd.DataFrame:
    Y = df[outcome].to_numpy()
    D = df[treatment].to_numpy()
    X = df[controls].to_numpy()
    # short and full regressions
    r_short = sm.OLS(Y, sm.add_constant(D)).fit()
    r_full = sm.OLS(Y, sm.add_constant(np.c_[D, X])).fit()
    beta_tilde = r_full.params[1]
    beta_naive = r_short.params[1]
    R_tilde = r_full.rsquared
    R_short = r_short.rsquared
    rows = []
    for r_max in r_max_grid:
        # Oster (2019) eq. 3: delta s.t. beta_star = 0 under proportional selection
        num = (beta_tilde - 0) * (R_tilde - R_short)
        den = (beta_naive - beta_tilde) * (r_max - R_tilde)
        delta = num / den if den != 0 else np.nan
        rows.append({"R_max": r_max, "delta": delta, "R_tilde": R_tilde})
    return pd.DataFrame(rows)
```

The driver sweeps `r_max_grid = np.linspace(R_tilde, min(1.0, 2.5 * R_tilde), 25)`, plots $\delta(R_{\max})$, and marks the conventional $R_{\max} = 1.3 \tilde R^2$. Maya's paragraph: **"At Oster's conventional $R_{\max} = 0.41$, $\hat\delta = 1.8$ — an unobservable would need to be 1.8× as explanatory as the full observed set to drive the estimate to zero. Sweeping $R_{\max}$ from $0.32$ to $0.80$, $\hat\delta$ ranges from infinite (at the degenerate endpoint) to $0.4$ (most adversarial). At every $R_{\max} \le 0.55$, $\hat\delta > 1$, the conventional 'robust to unobservables' threshold."**

The figure crosses $\delta = 1$ at $R_{\max} = 0.55$. Maya argues this is a defensible upper bound because her observed controls already explain $0.32$ and the unobservable would need to exceed the full observed set to push past $0.55$. One paragraph, one PDF — robustness reporting a referee respects.

---

## Part 6 — Transportability reweighting toward the target population

The final test in the battery is the one Lab 9's discussant pressed hardest on: **"your sample is the set of counties where the examination program was *adopted*; my agency cares about the *whole country*. Will your estimate transport?"** The honest answer is "not necessarily," but the appendix can do better than that — it can *bound* the transported estimate using inverse-probability-of-sampling reweighting under the assumptions of the transportability literature (Hartman et al. 2015; Pearl & Bareinboim 2014). Lab 10 ships that bound.

### 6.1 The reweighting

The setup: Maya has an in-sample ATT estimated on counties in adopting states. The target population is *all U.S. counties* (the population the discussant cares about). The transportability assumption is that the conditional ATE given a vector of pre-treatment characteristics $\mathbf{x}$ is the same in the target as in the sample (an *effect-modifier exchangeability* assumption). The transported ATE is then a weighted average of the in-sample CATE over the target distribution of $\mathbf{x}$:

$$ \widehat{\text{ATE}}_{\text{target}} = \sum_{i \in \text{sample}} w_i \cdot \hat\tau(\mathbf{x}_i), \quad w_i \propto \frac{f_{\text{target}}(\mathbf{x}_i)}{f_{\text{sample}}(\mathbf{x}_i)}. $$

The weights are the ratio of target to sample densities, estimated by logistic regression of a sample-indicator on $\mathbf{x}$.

```python
# src/robust2/transport.py — abridged
import numpy as np
import pandas as pd
from sklearn.linear_model import LogisticRegression


def transport_ate(
    sample_df: pd.DataFrame, target_df: pd.DataFrame,
    *, cate_hat: np.ndarray, features: list[str], seed: int = 42,
) -> dict:
    rng = np.random.default_rng(seed)
    X_s = sample_df[features].to_numpy()
    X_t = target_df[features].to_numpy()
    # sample indicator: 1 in sample, 0 in target.
    X = np.r_[X_s, X_t]
    S = np.r_[np.ones(len(X_s)), np.zeros(len(X_t))]
    clf = LogisticRegression(max_iter=1000).fit(X, S)
    p_s = clf.predict_proba(X_s)[:, 1]
    # weight: P(target | x) / P(sample | x) = (1 - p_s) / p_s, normalized
    w = (1 - p_s) / np.clip(p_s, 1e-3, 1 - 1e-3)
    w = w / w.sum()
    ate_target = (w * cate_hat).sum()
    # nonparametric bootstrap for SE
    B = 500
    boots = np.empty(B)
    n = len(X_s)
    for b in range(B):
        idx = rng.integers(0, n, n)
        boots[b] = (w[idx] * cate_hat[idx]).sum() / w[idx].sum()
    return {"ATE_target": ate_target, "SE": boots.std(ddof=1),
            "weight_ESS": 1.0 / (w**2).sum() / n}
```

The diagnostic in the footnote is **effective sample size (ESS)**, $1 / \sum_i w_i^2$ normalized by $n$. ESS below 30% means a few extreme weights drive the result and the transported estimate is not trustworthy. Maya's ESS is 71%, acceptable. Her paragraph: **"Reweighting the in-sample CATE to the all-U.S.-county target moves the estimate from $-1.4$pp to $-1.1$pp, the difference driven by lower-density adoption regions where examination intensity was lighter. The estimate transports under the assumption that the CATE function is the same in adopting and non-adopting counties given the eight pre-registered covariates — an assumption the discussant should push back on, and that I cannot test with these data."** That last clause is what makes the test honest.

---

## Part 7 — Verifying the appendix rebuilds

Once all five tests are wired into the Makefile, the final step is to verify the pipeline reproduces. The verification protocol is the same one Lab 8 §2.5 established, extended for the appendix:

```bash
# from a fresh clone
git clone <your-repo> capstone-fresh
cd capstone-fresh
conda env create -f environment.yml -n capstone-fresh
conda activate capstone-fresh
make clean
make appendix              # serial
sha256sum appendix/tab_*.tex appendix/fig_*.pdf appendix/manifest.json > checksums.txt
make appendix_clean
make -j5 appendix          # parallel
sha256sum appendix/tab_*.tex appendix/fig_*.pdf appendix/manifest.json > checksums_par.txt
diff checksums.txt checksums_par.txt   # should be empty
```

A non-empty diff means a race condition or non-seeded call. Common culprits: a `random_state` not threaded into a scikit-learn estimator, or an `np.random` call (not `rng.<method>`) picking up global state. Both are five-minute fixes once located.

The `manifest.json` is the SHA-256 audit trail. A referee runs `make appendix && python tools/manifest.py appendix/` and compares to the JSON at the cloned commit; any hash mismatch and your appendix is not reproducing. The check is the same one every empirical journal's data editor runs post-acceptance; clearing it now makes that step a formality.

---

## Deliverable for the next session

By the end of Lab 10, your capstone repository has:

1. `src/robust2/` with five new modules, each with a docstring citing the method paper.
2. `appendix/` with five new `.tex` tables and two new `.pdf` figures, all built by `make appendix`.
3. `appendix/cate_features.json` committed before the first forest fit, with its commit hash recorded.
4. `appendix/manifest.json` regenerated by the pipeline and listing every output's SHA-256.
5. A `tests/robust2/` folder with at least one unit test per module — a `pytest` that runs the estimator on a fixed-seed toy dataset and asserts a hash on the resulting table, so a future refactor of `src/robust2/` cannot silently change the numbers in the paper.

That bundle is the input to Assessment 10's Robustness & Heterogeneity Memo. The memo's job is to *narrate* the appendix — to walk a grader through each test, name the threat it addresses, quote the headline number with its conditional clauses, and concede where the test is silent. The pipeline is the proof; the memo is the argument; the combination is what a submission looks like.
