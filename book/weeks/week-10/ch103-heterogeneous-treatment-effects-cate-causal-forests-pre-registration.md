# Ch 10.3 — Heterogeneous Treatment Effects and CATE: From Subgroup Regressions to Causal Forests, with the Pre-Registration Discipline That Keeps It Honest

In Chapter 4 you estimated an *average* treatment effect — one number, $\widehat{\text{ATT}}$ — and treated it as the answer. In Chapter 10.2 you learned how to *test* a small family of pre-specified subgroup effects without lying with p-values. This chapter is what happens when the conference room asks the question that connects those two worlds: **"is the effect the same for everyone, or does it vary across units in ways that matter?"** That question — the question of *heterogeneous treatment effects* — is the most-asked question after every empirical talk in the universe, and answering it well is one of the things that separates a paper that lands in a JFE-tier journal from one that lands a tier below. **Done well, heterogeneity analysis turns "the policy reduced denial gaps by 1.4pp on average" into "the policy reduced denial gaps by 3.1pp in counties with high examination intensity and 0.4pp elsewhere — and the difference is where the policy story actually lives."** Done badly, heterogeneity analysis is a fishing expedition that finds whichever subgroup happens to have a small p-value, dressed up as a finding.

The reveal-the-trick spine of this chapter is the same as last chapter, generalized: **the only honest heterogeneity analysis is one that was, in some way, *committed to in advance* — and modern machine-learning methods like causal forests are useful precisely because they make the commitment auditable when subgroup pre-registration is impractical.** We will walk through three families of methods in order of increasing sophistication and decreasing room for fishing: (1) **subgroup regressions** — split the sample by a pre-specified variable and re-estimate, the bread-and-butter heterogeneity analysis; (2) **interaction regressions** — let the treatment coefficient vary by a continuous moderator, the standard generalization; and (3) **causal forests** — let the data tell you where heterogeneity is, *with cross-validated honesty that prevents the fishing*. The thread that unites all three is the **pre-analysis discipline**: every heterogeneity claim is honest only to the extent that the subgroups, moderators, or feature lists were committed before the data spoke.

Maya's required heterogeneity analysis from the Chapter 10.1 triage is the running example. She has a panel of county-year denial gaps, a staggered DiD with state-level treatment timing, and a list of four moderators she pre-specified in her PAP: examination *intensity* (a discrete three-bin variable from the FFIEC examination scope record), county minority *share* (continuous; she will tercile it), MSA *status* (binary), and CRA *evaluation-period overlap* (binary). The chapter walks her — and you — from the most cautious to the most ambitious analysis.

---

## 1. The reveal: what heterogeneity means and what it doesn't

Begin with definitions, because the literature has accumulated enough acronyms that students confuse them.

**Average Treatment Effect (ATE).** The expected effect of treatment over the entire population: $\text{ATE} = \mathbb{E}[Y(1) - Y(0)]$, where $Y(1)$ and $Y(0)$ are the potential outcomes under treatment and control. This is the one-number summary you have been estimating since Chapter 4.

**Average Treatment Effect on the Treated (ATT).** The expected effect among the units who actually received treatment: $\text{ATT} = \mathbb{E}[Y(1) - Y(0) \mid D = 1]$. Maya's Callaway–Sant'Anna estimator from Chapter 4.2 was an ATT.

**Conditional Average Treatment Effect (CATE).** The expected effect *given* a vector of covariates $\mathbf{x}$: $\tau(\mathbf{x}) = \mathbb{E}[Y(1) - Y(0) \mid \mathbf{X} = \mathbf{x}]$. This is *the* object of heterogeneity analysis. The CATE is a function of $\mathbf{x}$; it tells you how the effect varies across units characterized by their covariates. Estimating $\tau(\mathbf{x})$ is harder than estimating the ATE for two reasons: you have less data per subgroup, and you have many subgroups to compare, which brings the multiple-testing problem from Chapter 10.2 back in force.

**Group Average Treatment Effect (GATE).** A coarsening of CATE: $\tau_g = \mathbb{E}[\tau(\mathbf{X}) \mid \mathbf{X} \in \text{group } g]$. The subgroup-regression approach in §2 estimates GATEs. The causal forest in §4 estimates CATE and then aggregates to GATEs for reporting.

The distinction that matters: **CATE is a function; GATE is a number.** Reporting a *function* is harder than reporting a number, and the visual report (a CATE histogram or a CATE-vs-feature plot) is what makes the heterogeneity argument legible to a reader.

The threat: **heterogeneity findings are uniquely vulnerable to p-hacking** because the number of possible subgroup definitions on a moderately-sized dataset is enormous. Twenty covariates and two split points each gives forty subgroups, and at $\alpha = 0.05$ you expect two false positives per dataset under the global null. That is exactly the multiple-testing problem from Chapter 10.2, and the heterogeneity analysis is where it hits hardest because the discovery freedom is largest. **Pre-registration is the antidote.** Causal forests are the machine-learning antidote when pre-registration is impractical.

---

## 2. The cautious tool: subgroup regressions on pre-specified bins

The simplest heterogeneity analysis is the one a referee will look at first: **split your sample by a pre-specified categorical moderator, re-estimate your headline regression on each subsample, and report the per-subgroup ATT.** This is the GATE estimator at its bluntest. Its virtues are that it is transparent (every reader can replicate it), it is method-agnostic (it works for any baseline estimator — DiD, RDD, IV — by inheritance), and it sidesteps the question of how the treatment interacts with covariates by not trying to model the interaction. Its vices are that it loses statistical power (each subsample is smaller than the full sample, so each per-subgroup ATT has wider standard errors), and it requires the moderator to be discrete or pre-binned.

Maya's intensity moderator is naturally discrete (three bins: light, moderate, intense), so the subgroup-regression approach is direct. She runs the Callaway–Sant'Anna estimator on three subsamples — counties in states with light-intensity examination programs, with moderate, and with intense — and reports three ATT estimates with their state-clustered standard errors. The report:

| Subgroup | $N$ counties | $\widehat{\text{ATT}}$ (pp) | SE | $p_{\text{raw}}$ | $p^{RW}$ (adj across 3 cuts) |
|---|---|---|---|---|---|
| Light intensity | 2,114 | $-0.4$ | 0.62 | 0.52 | 0.74 |
| Moderate intensity | 1,873 | $-1.5$ | 0.51 | 0.003 | 0.011 |
| Intense | 1,302 | $-3.1$ | 0.81 | 0.0001 | 0.0006 |

Read this and you see the heterogeneity argument crystal-clear. The overall ATT of $-1.4$pp from her Week 8 spec was the average of three meaningfully-different numbers: light-intensity states show essentially no effect, moderate-intensity states show the average, and intense states show more than twice the average effect. The headline number was hiding a *substantive policy finding*: examination intensity matters, and the intensity of the program — not its mere existence — is the active ingredient. The Romano–Wolf adjustment across the three cuts confirms the moderate and intense rows survive multiple-testing control at the 5% FWER level.

### The dose-response interpretation

The pattern in Maya's table — effect monotonically increasing in intensity — is what economists call a **dose-response relationship**, and it has a special evidentiary role. A monotone dose-response is much harder to explain by confounding than a single-point estimate is, because a confounder would have to vary in lock-step with the treatment intensity to produce the pattern. This is the same logic that underlies Hill's criteria in epidemiology and that motivates the *gradient* in many quasi-experimental papers. When you find a dose-response, *say so explicitly*. It is not a robustness check; it is a positive piece of identification evidence.

### Code: subgroup ATTs with Callaway–Sant'Anna

```python
# nb10.3 cell 1 — per-subgroup ATTs from a staggered DiD, with Romano-Wolf
# adjustment across subgroups. Assumes Callaway-Sant'Anna available via
# `differences` package (or your preferred implementation).
import numpy as np
import pandas as pd
from differences import ATTgt          # pip install differences

def subgroup_atts(
    df: pd.DataFrame,
    id_col: str, time_col: str, treat_col: str, y_col: str,
    moderator_col: str,
    cluster_col: str,
) -> pd.DataFrame:
    """Estimate one ATT per level of `moderator_col`, with clustered SEs."""
    rows = []
    for g, sub in df.groupby(moderator_col):
        att = ATTgt(
            data=sub,
            cohort_name=treat_col,
            base_period="varying",
            strata=None,
        ).fit(formula=f"{y_col}", n_jobs=1, cluster_var=cluster_col)
        # Aggregated overall ATT and its SE on this subgroup.
        agg = att.aggregate("simple")
        rows.append({
            "subgroup": g,
            "n_counties": sub[id_col].nunique(),
            "att": agg["att"],
            "se":  agg["se"],
            "p_raw": agg["pvalue"],
        })
    return pd.DataFrame(rows)
```

A note: the `differences` package API is one of several Python ports of Callaway–Sant'Anna; the code above is illustrative. In a real paper, you would also pull pre-treatment event-study leads per subgroup to check that parallel trends holds *within* each subgroup, not just on average — because heterogeneous parallel-trends violations are a real and underappreciated threat in subgroup analysis.

### When subgroup regressions are right

When (a) the moderator is naturally discrete with a small number of levels, (b) you have enough observations in each level to estimate the per-subgroup ATT with adequate precision, and (c) you can argue for the parallel-trends or identification assumption *within* each subgroup separately. Maya's intensity-by-three is a clean case. So is the MSA-vs-rural binary cut. The minority-share tercile is borderline — terciles are pre-binned to make the analysis tractable, but the choice of tercile boundaries is itself a fork that a referee can attack. We will see in §3 how the interaction regression handles continuous moderators more honestly.

### When subgroup regressions are wrong

When the moderator is continuous and the choice of binning is a researcher degree of freedom; when subsamples are too small to support the estimator; when within-subgroup parallel-trends assumptions fail in a subgroup but hold on average; when there are many moderators and the joint heterogeneity surface is the object of interest (then a causal forest, §4, is the right tool).

---

## 3. Interaction regressions: heterogeneity in one model

The interaction regression keeps the entire sample together and lets the treatment effect vary with a continuous moderator. The structural form is

$$ Y_{it} = \alpha_i + \gamma_t + \beta_0 \cdot D_{it} + \beta_1 \cdot D_{it} \cdot M_i + \boldsymbol{x}_{it}'\boldsymbol{\delta} + \varepsilon_{it}, $$

where $D_{it}$ is the treatment indicator, $M_i$ is the (centered) moderator, and the **interaction coefficient $\beta_1$ is the heterogeneity-of-interest parameter**. The implied treatment effect at moderator value $M$ is $\beta_0 + \beta_1 \cdot M$, so the *function* $\tau(M)$ is a line through the data. Most papers report $\beta_0$ (the effect at the mean moderator value, if $M$ is centered), $\beta_1$ (the slope of the effect in $M$), and a plot of $\tau(M)$ over the range of observed $M$ with a confidence band.

For Maya's minority-share moderator, the spec is:

$$ \text{Gap}_{it} = \alpha_i + \gamma_t + \beta_0 \cdot \text{Exam}_{it} + \beta_1 \cdot \text{Exam}_{it} \cdot (\text{MinShare}_i - \bar{\text{MinShare}}) + \varepsilon_{it}, $$

clustered by state. She reports $\hat{\beta}_0 = -1.4$ pp (the effect at average minority share, matching the headline), $\hat{\beta}_1 = -3.7$ pp per unit of (de-meaned) minority share. The implied $\tau(M)$ at the 25th percentile of minority share is about $-0.8$ pp; at the 75th, about $-2.2$ pp. Counties with more minority residents see larger denial-gap reductions from examinations — the policy is, in effect, *targeted by where it matters most*, even though the law itself was uniform.

### The functional-form catch

The interaction regression is only as good as its functional form. Writing $\tau(M) = \beta_0 + \beta_1 M$ assumes the treatment effect is *linear* in the moderator. This is rarely literally true. In many policy applications the effect is nonlinear (an S-curve, a threshold, a U-shape) and a linear interaction will hide that structure. The standard moves are:

1. **Pre-bin the moderator** (§2 above) — robust to functional form but loses information.
2. **Add quadratic interactions** $\beta_1 M + \beta_2 M^2$ — captures U-shapes and curvature.
3. **Use a fully nonparametric kernel regression** of $\tau(M)$ on $M$ — captures any shape but requires more data and obscures the parametric uncertainty.
4. **Use a causal forest** (§4) — captures any shape automatically and provides honest inference.

A useful diagnostic before committing to a parametric form: fit the regression with three binned interactions (low, mid, high tercile of $M$) and see whether the three coefficients line up linearly or not. If they do, the linear interaction is fine; if they don't, you have evidence of nonlinearity and need a richer form.

### The "interaction with a fixed effect" trap

A subtle mistake: when you include unit fixed effects $\alpha_i$, you cannot identify the *main effect* of a time-invariant moderator $M_i$, only its *interaction with treatment*. Maya's minority share is (approximately) time-invariant per county, so the spec above cannot include a main effect on $M_i$ — it would be absorbed by $\alpha_i$. The interaction $D \cdot M$ is still identified, but be careful: students often try to add the main effect and either get a singular regression or, in some pyfixest implementations, silently get an absorbed coefficient that the package does not report. **Always double-check the rank condition and the printed coefficient list when you interact a covariate with a fixed effect.**

### Code: interaction with a continuous moderator

```python
# nb10.3 cell 2 — interaction regression with a continuous moderator,
# clustered SEs, and a plot of tau(M).
import numpy as np
import pandas as pd
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt
import pyfixest as pf

df = ...  # county-year panel with cols: gap, exam, min_share, fips, year, state

# Center the moderator so beta_0 = effect at the mean moderator value.
df = df.copy()
df["min_share_c"] = df["min_share"] - df["min_share"].mean()
df["exam_x_share"] = df["exam"] * df["min_share_c"]

fit = pf.feols(
    "gap ~ exam + exam_x_share | fips + year",
    data=df,
    vcov={"CRV1": "state"},
)
print(fit.tidy())

# Plot tau(M) = beta_0 + beta_1 * (M - mean), with a delta-method CI.
b0, b1 = fit.coef()["exam"], fit.coef()["exam_x_share"]
V = fit.vcov().loc[["exam", "exam_x_share"], ["exam", "exam_x_share"]].to_numpy()
m_grid = np.linspace(df["min_share"].quantile(0.05),
                     df["min_share"].quantile(0.95), 100)
delta = m_grid - df["min_share"].mean()
tau = b0 + b1 * delta
se_tau = np.sqrt(V[0,0] + 2 * delta * V[0,1] + delta**2 * V[1,1])
ci_lo = tau - 1.96 * se_tau
ci_hi = tau + 1.96 * se_tau

fig, ax = plt.subplots(figsize=(6.5, 4))
ax.plot(m_grid, tau, lw=2, label=r"$\hat\tau(M)$")
ax.fill_between(m_grid, ci_lo, ci_hi, alpha=0.25)
ax.axhline(0, color="0.4", lw=1, ls="--")
ax.set_xlabel("County minority share")
ax.set_ylabel(r"Implied ATT $\hat\tau(M)$ (percentage points)")
ax.set_title("Heterogeneous treatment effect by minority share")
ax.legend()
fig.tight_layout()
fig.savefig("cate_min_share.png", dpi=150)
```

The delta-method confidence interval is what most papers report; for nonlinear specifications, a bootstrap CI on $\tau(M)$ is more honest.

---

## 4. Causal forests: machine learning, but honestly

Now the modern tool. **Causal forests** (Wager & Athey 2018; Athey, Tibshirani & Wager 2019) estimate $\tau(\mathbf{x})$ as a function of a high-dimensional covariate vector $\mathbf{x}$, using a random-forest architecture adapted for causal inference.[^wa2018][^atw2019] The key ideas are: (a) at each split of each tree, the splitting criterion is the *heterogeneity in treatment effect*, not the heterogeneity in $Y$ itself; (b) the data used to *select* the splits is disjoint from the data used to *estimate* the effects at the leaves — this is **honesty**, and it is what saves you from the fishing problem; (c) the method gives you not just a point estimate $\hat{\tau}(\mathbf{x})$ but *asymptotically valid pointwise confidence intervals*, courtesy of the trees-as-kernel construction.

Conceptually, you can think of a causal forest as a clever way of automatically discovering the subgroup definitions that would be most heterogeneous in treatment effect — and then estimating effects on those subgroups using fresh data so the discovery does not bias the estimate. The honesty rule, formalized, is: **split the training sample into two halves; use one half to grow the trees, use the other half to fill in the leaf estimates.** This is the same idea as cross-validation but applied to the discovery step, and it is what makes causal forests legitimate inference (rather than a flexible exploratory tool with no honest p-values).

For Maya, the causal-forest pipeline is:

1. **Define $\mathbf{X}$.** The vector of moderators she pre-specified in the PAP: intensity, minority share, MSA, CRA overlap, plus any other county-level covariates she wants to allow into the forest. Crucially, **the *list* of features is pre-registered even though the forest decides which features matter.**
2. **Fit the forest.** Using a causal-forest package (in Python, `econml.dml.CausalForestDML` or `econml.grf.CausalForest`; in R, `grf::causal_forest`).
3. **Aggregate to GATEs.** For reporting, compute the average $\hat{\tau}(\mathbf{x})$ within each pre-specified subgroup; these are the same GATEs as in §2, but estimated from the forest and inheriting its honesty.
4. **Test for heterogeneity.** The causal-forest community has converged on a specific test — the **Best Linear Predictor (BLP) of CATE on its own out-of-sample fitted values** — that asks whether the forest has actually found heterogeneity beyond chance (Chernozhukov, Demirer, Duflo & Fernández-Val 2018).[^cddfv2018]
5. **Report.** A histogram of $\hat{\tau}(\mathbf{x})$ across the sample; the BLP test statistic and p-value; the per-subgroup GATEs with confidence intervals; a feature-importance plot showing which covariates drive heterogeneity.

### Code: a causal forest with EconML

```python
# nb10.3 cell 3 — causal forest CATE on Maya's panel. Pedagogical version
# treating each county-year as i.i.d.; for a real DiD panel, residualize
# the outcome and treatment on (county, year) fixed effects FIRST using
# pyfixest, then feed the residuals into the forest. This is the
# Robinson (1988) / DML decomposition used by econml.DML.
import numpy as np
import pandas as pd
from econml.grf import CausalForest

rng = np.random.default_rng(42)

df = ...  # as above; assume already FE-residualized
X = df[["intensity_bin", "min_share", "msa", "cra_overlap",
        "lender_concentration", "pop", "median_inc"]].to_numpy()
T = df["exam_resid"].to_numpy()   # FE-residualized treatment
Y = df["gap_resid"].to_numpy()    # FE-residualized outcome

# Honest causal forest: half-sample splitting per tree.
forest = CausalForest(
    n_estimators=2000,
    honest=True,
    min_samples_leaf=50,
    max_depth=None,
    random_state=42,
)
forest.fit(X=X, T=T, y=Y)

# Per-observation CATE and pointwise SE (from the forest's kernel weights).
tau_hat = forest.predict(X)
se_hat  = forest.predict_var(X) ** 0.5

# Group-average treatment effects on pre-specified subgroups.
def gate(df, mask):
    return tau_hat[mask].mean(), se_hat[mask].mean() / np.sqrt(mask.sum())

for label, mask in [
    ("intensity=light",    df["intensity_bin"].eq(0).to_numpy()),
    ("intensity=moderate", df["intensity_bin"].eq(1).to_numpy()),
    ("intensity=intense",  df["intensity_bin"].eq(2).to_numpy()),
    ("min_share top tercile", (df["min_share"] >= df["min_share"].quantile(0.67)).to_numpy()),
]:
    g, sg = gate(df, mask)
    print(f"{label:25s}  GATE={g:+.3f}pp   SE={sg:.3f}")

# Best Linear Predictor heterogeneity test.
# Regress observed (residualized) outcome on forest-predicted CATE x treatment,
# using held-out folds (econml does this internally with `cate_interpreter`).
from econml.cate_interpreter import BLPInterpreter
blp = BLPInterpreter().interpret(forest, X)
print(blp.summary())          # reports coefficient on tau_hat * T; p-value < 0.05 => real heterogeneity
```

The two outputs to read carefully: the **GATE table** is the heterogeneity argument in human-legible form, and the **BLP test** is the formal hypothesis test ("is there *any* heterogeneity in this forest beyond what chance would produce?"). The BLP coefficient on $\hat{\tau}(\mathbf{x}) \cdot T$ should be near 1 if the forest's predictions are calibrated; a coefficient significantly less than 1 means the forest is over-fitting heterogeneity (the predictions are too extreme), and a coefficient near 0 with a small SE means there is no real heterogeneity in the sample.

### How to read a causal-forest output honestly

When you report a causal forest, three pieces are essential.

**The histogram of $\hat{\tau}(\mathbf{x})$.** This is the most direct visualization of heterogeneity: how spread out are the per-unit CATEs? If they are tightly clustered around the ATT, there is no real heterogeneity — the forest has not found anything the average effect missed. If they are widely spread, the forest has found something, and the next step is to figure out *which features drive the spread.*

**The feature-importance plot.** Random forests have a natural notion of which features drove the splits the most; for causal forests, the relevant version is the *heterogeneity-importance*, which counts each feature by how much its splits reduced heterogeneity in treatment effects (not in $Y$). The top features are the ones the paper should discuss; the bottom features are noise.

**The BLP test.** The formal "is there any heterogeneity" test. A p-value of < 0.05 is the green light to discuss the causal forest's findings; a p-value of > 0.10 is the red flag — the forest may be over-fitting, and you should *not* lean on its disaggregated predictions.

### When causal forests are right

When (a) you have many candidate moderators ($\mathbf{x}$ is high-dimensional), (b) you cannot pre-specify which ones matter, (c) you want a function $\tau(\mathbf{x})$ rather than a finite list of GATEs, and (d) you have enough data ($N$ in the low thousands, at least, for stable forests) to support a forest with two thousand honest trees. Maya's panel has tens of thousands of county-years; a causal forest is appropriate.

### When causal forests are wrong

When the sample is small (forests need data; $N < 500$ is borderline), when the design's identifying assumption breaks if the residualization step is wrong (Robinson 1988 residualization assumes a partially-linear model that may not match your DiD or RDD exactly), or when interpretability matters more than predictive accuracy (a senior referee in a finance journal may simply not accept a causal-forest as the headline result, no matter how appropriate; in that case use the forest as the *exploratory* tool and the subgroup regression as the *headline*).

---

## 5. The pre-registration discipline that keeps it all honest

The methods above are *technologies* for estimating heterogeneous effects. **The discipline that turns them into honest inference is pre-registration**, and the connection between the two is the load-bearing idea of this chapter. Let us be explicit about three levels of pre-registration discipline, in decreasing order of stringency.

**Level 1 — Full pre-registration of subgroups.** Before you saw the data, your pre-analysis plan (Chapter 7.3) named exactly which subgroups you would estimate and which moderators you would use. The analysis in §2 above runs and reports those subgroups in the order specified, with Romano–Wolf adjustment across the pre-specified family. This is the gold standard, used in clinical trials and increasingly in randomized policy experiments. It is rare in observational empirical finance because the PAP step is often only a partial commitment.

**Level 2 — Pre-registration of the moderator list, with the analysis fully data-driven.** You committed *which features* could enter the heterogeneity analysis, but you let a causal forest decide *which features actually matter and how*. This is the modern compromise: it preserves the discipline of disclosure (the feature list is in the PAP and version-controlled) while accommodating the reality that you usually do not know in advance which moderator is going to be the one that lights up. The honesty rule of the causal forest (sample-splitting between split-selection and leaf-estimation) is what makes Level 2 legitimate.

**Level 3 — Sample splitting for discovery and confirmation.** When no pre-registration is available, you can manufacture one ex-post by splitting your sample into two halves: use the *discovery half* to run any heterogeneity exploration you like, find the most promising subgroup or feature; then *re-run the analysis on the confirmation half* and report the confirmation-sample result as your headline. The discovery-sample results are explicitly exploratory and not used for inference. This is roughly half as powerful as the full-sample analysis would be, but it is uncontaminated by the discovery process. For Maya, with tens of thousands of county-years, a 50-50 split is feasible and credible; for a smaller-sample paper, the precision loss is painful.

**The wrong move** is to claim Level 1 discipline when you had only Level 3 (or no) commitment. A first-draft revision under pressure often slides into this — students remember that *something* about the moderator was in the PAP and dress up an exploratory finding as confirmatory. The audit trail (the dated PAP, the version-controlled feature list, the timestamped commit of the forest code) is what protects you from this slide. If you are unsure whether a finding meets Level 1, downgrade it to Level 2 and report accordingly.

---

## 6. The threats to a heterogeneity story

Suppose Maya runs the analysis above and finds the dose-response in intensity she reported in §2. A sharp referee will not stop at "is the heterogeneity real?"; they will ask the deeper question: **"is the heterogeneity *causally* real, or is it confounded?"** This is identification in subgroups, and it has three distinct forms.

**Threat A — Different identification quality in different subgroups.** Maya's identifying assumption is per-cohort parallel trends. It might hold strongly in intense-examination states (which adopted earlier, with cleaner pre-periods) and weakly in light-examination states (which adopted later, with more contemporaneous policy noise). The dose-response could then partly reflect *better identification* in the intense subgroup, not a real intensity effect. The check: run the event-study leads test (Chapter 4.2) *within each subgroup* and report the joint test of zero leads for each.

**Threat B — Composition effects in subgroups.** If intense-examination states differ systematically from light-examination states in some other relevant dimension (population, banking concentration, racial composition of the lending sector), then the "intensity effect" might be a confounded label for that other dimension. The check: include the candidate confounder as a moderator alongside intensity in the interaction regression or the causal forest. If the intensity coefficient survives, the threat is bounded; if it does not, the heterogeneity belongs to the confounder.

**Threat C — Subgroup-specific reverse causality.** In some subgroups, the moderator may itself be a downstream consequence of the treatment. This is the bad-controls problem from Chapter 10.4 (next chapter), applied to subgroups. The example: if intense-examination programs *attract* fair-lending NGOs to a state, and NGO presence is a moderator, then the heterogeneity-by-NGO-presence finding is confounded by post-treatment selection into the moderator. The check: use only *pre-treatment* values of the moderator — and document that you did so.

**The general principle:** every heterogeneity claim is a separate causal claim, and inherits the identifying assumption of the headline only when the moderator is pre-treatment, balanced across subgroups, and the parallel-trends-or-equivalent assumption holds within each subgroup. **Heterogeneity does not get a free pass.**

---

## 7. Reporting: the table, the figure, the sentence

The honest report of a heterogeneity analysis has four elements.

**The pre-specified subgroup table** (§2 above). Per-subgroup ATTs, standard errors, raw and adjusted p-values, with a footnote naming the moderator and the source of its bin definitions.

**The interaction-regression line plot** (§3 above). $\hat{\tau}(M)$ over the observed range of the continuous moderator, with a confidence band, and a vertical mark at the sample-mean $M$ where the plotted slope equals $\hat{\beta}_0$.

**The causal-forest output** (§4 above). The CATE histogram, the BLP test, and the feature-importance plot, all in an appendix figure with a sentence-long caption per panel.

**The interpretation sentence**, which is the hardest of the four. It should explicitly do three things: (a) characterize the heterogeneity in plain English ("the effect is concentrated in counties with high examination intensity and substantial minority population"), (b) cite the multiple-testing adjustment ("survives Romano–Wolf control across the family of pre-specified moderators"), and (c) link to the policy interpretation ("suggesting that program intensity, not mere program existence, is the active ingredient — consistent with the implementation literature of FAIR-housing oversight").

The interpretation sentence is what most students under-write, because they want the reader to do the inferential work. Don't. The audience after the conference is now the referee, and the referee will read your sentence as your commitment to a substantive claim.

---

## 8. The four classmates' heterogeneity sketches

A brief tour of how the methods of this chapter look in the other four students' projects, so you can see the pattern across different designs.

**Sam (intraday momentum).** Heterogeneity by *liquidity* (Amihud-ratio terciles) is the standard cut in the asset-pricing literature; Sam pre-registered three terciles and runs subgroup regressions. His "treatment" is the high-momentum strategy and his "moderator" is liquidity; the question is whether momentum returns are larger or smaller in less-liquid stocks. A causal forest on liquidity, market-cap, book-to-market, idiosyncratic volatility, etc. would let the data find which features matter most — but Sam's PAP committed to liquidity-only, so his Level 1 analysis sticks to the tercile.

**Devon (DeFi adoption).** Heterogeneity by *chain* is unavoidable in cross-chain studies; Devon pre-registered five chains as subgroups. A causal forest on chain, TVL-tier, smart-contract-language, validator-count, etc. would discover that chain-language interacts strongly with regulatory-event effects — but Devon's PAP committed to chain-only as the moderator family, so the forest result is Level 2 exploratory.

**Priya (climate-shock insurance).** Heterogeneity by *region* and by *peril type* (wildfire vs. flood vs. hurricane) is the standard cut. Priya's PAP committed to a 2×3 region-by-peril grid (six subgroups); she reports the 2x3 GATE table with Romano–Wolf adjustment.

**Leah (patent-language innovation).** Heterogeneity by *technology class* (CPC section) is the standard cut. Leah's panel of patent-text-derived novelty scores can be sliced by 8 CPC sections, giving 8 GATEs that she reports with Holm adjustment (small $m$, so Holm is fine and Romano–Wolf is overkill).

Across all five students, the pattern is the same: **pre-specify the moderator family, run a subgroup-regression headline, use a causal forest as exploratory enrichment, and adjust p-values across the family.** That is the template.

---

## 9. What to do when the heterogeneity *vanishes*

A real possibility that students rarely prepare for: you run the heterogeneity analysis and find *no significant heterogeneity*. The CATE histogram is tightly clustered around the ATT; the BLP test fails; the per-subgroup ATTs are all within sampling noise of each other. What do you report?

**You report exactly that, and you make it a feature, not a bug.** Null heterogeneity is *information*. It tells the policy reader: "the effect is uniform across the populations we measured; the policy is not differentially helpful or harmful to subgroups in a way our data can detect." That is a substantive finding. The phrasing matters:

- Bad: "We do not find significant heterogeneity, but ..." (followed by post-hoc fishing).
- Good: "We do not detect heterogeneity across the pre-specified moderator family at conventional significance levels. The point estimates and confidence intervals (Table 7) are consistent with a uniform treatment effect across intensity, minority-share, and MSA-vs-rural subgroups, with a precision that rules out per-subgroup effects more than 1pp away from the average."

The "rules out" phrase is the load-bearing one. *Quantify the null*: state what the confidence intervals can and cannot detect. A null with wide CIs is uninformative; a null with tight CIs is a substantive finding ("we can rule out heterogeneity larger than X pp").

---

## 10. The seam to Chapters 10.4 and 10.5

Heterogeneity is *one* answer to the deeper question "why does the headline effect happen?" The other major answer — the **mechanism** answer — is the topic of Chapter 10.4. Heterogeneity says *for whom*; mechanism says *through what channel*. They are complementary, and a paper that gets both right is a much stronger paper than one with only the average effect.

Chapter 10.5 then asks whether the heterogeneity you found in your sample would persist in a different population (the external-validity question). The transportability diagram of Chapter 10.5 is, in part, an honest account of which subgroups your heterogeneity analysis identified well and which it identified poorly — and that account inherits directly from the per-subgroup parallel-trends evidence of this chapter.

The next chapter (10.4) starts where this one ends: with a paper that has an average effect and a story about heterogeneity, asking "what is the *channel*?"

---

[^wa2018]: Wager, S. and Athey, S. (2018). "Estimation and Inference of Heterogeneous Treatment Effects Using Random Forests." *Journal of the American Statistical Association* 113(523):1228–1242.

[^atw2019]: Athey, S., Tibshirani, J., and Wager, S. (2019). "Generalized Random Forests." *Annals of Statistics* 47(2):1148–1178.

[^cddfv2018]: Chernozhukov, V., Demirer, M., Duflo, E., and Fernández-Val, I. (2018). "Generic Machine Learning Inference on Heterogeneous Treatment Effects in Randomized Experiments." *NBER Working Paper* 24678.

---

**Chapter cross-references.** Built on Ch 4.2 (Callaway–Sant'Anna staggered DiD whose ATT is the headline), Ch 5 (the residualization / Robinson decomposition that lets causal forests handle panel data), Ch 7.3 (pre-analysis-plan discipline that commits the moderator family), Ch 7.5 (the threats table where heterogeneity-specific identification threats live), Ch 8.1 (the specification curve and its disclosure logic, sibling to Level 2 pre-registration here), Ch 10.1 (the triage that made the heterogeneity comment Required), and Ch 10.2 (Romano–Wolf adjustment across the subgroup family). Feeds Ch 10.4 (mechanism analysis, which complements heterogeneity), Ch 10.5 (external validity, which builds on the per-subgroup evidence), and Ch 11.2 (the response-letter section on heterogeneity).
