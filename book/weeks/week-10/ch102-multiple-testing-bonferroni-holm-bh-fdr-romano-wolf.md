# Ch 10.2 — Multiple-Testing Across Families: Bonferroni, Holm, BH-FDR, and Romano-Wolf Step-Down — When Each Is the Right Tool

You ran your headline regression and reported a t-statistic of 2.3 with a p-value of 0.02. Three stars on the table, a clean victory for your design. Then your audience asked about heterogeneity — by income tercile, by region, by lender type — and you obliged with a heterogeneity table that has twelve rows, three of them significant at the five-percent level. Then your discussant asked about outcomes — denial rates, loan size, interest spread, rejection codes — and you obliged with an outcome table that has eight columns, two of them significant. Then the audience asked about a placebo on subsamples, and you ran twelve placebos, none significant, but two had p-values of 0.06 — "marginally," you said in the room. Now sit down with your triage memo from Chapter 10.1 and count the number of times you said "significant" on Saturday. Plausibly thirty times. **Many of those "significance" claims are false, and you have no idea which ones.**

Here is the result the chapter turns on, stated in one sentence so the rest is detail: **when you test many hypotheses at once, the probability that at least one of them comes up "significant" purely by chance grows fast — and the only honest fixes are statistical procedures that *re-define* what "significant" means in the multi-test context.** This chapter is the menu of those procedures. We are going to look at four of them: Bonferroni (the bluntest, oldest, and most conservative), Holm (Bonferroni's smarter sequential cousin), Benjamini–Hochberg false-discovery-rate control (the modern default in genomics and increasingly in finance), and Romano–Wolf step-down (the bootstrap-based procedure that respects the *correlation structure* across your tests). They are not interchangeable. Each one is the right tool for a different question, and using the wrong one either lets through false discoveries you cannot defend or kills real discoveries you should have kept. The reveal-the-trick spine for the chapter is the simple observation that all four are answering different versions of the same question — *what error rate, exactly, do we want to control, and across what family of tests?* — and once you know which error rate and which family, the choice of procedure is forced.

We will continue with Maya's project. Her conference feedback ledger triaged into three Required items in Chapter 10.1: a parallel-trends rescue, a heterogeneity analysis, and an Oster δ sensitivity. The heterogeneity analysis is going to test the average treatment effect (ATT) across multiple subgroups: examination intensity (three bins), county minority share (terciles), MSA-vs.-rural (binary), and CRA-evaluation-period overlap (binary). That is — depending on how she cuts it — anywhere from three to thirty-six tests. Without a multiple-testing adjustment, two of them will look significant by chance even if there is no real heterogeneity at all. Without a multiple-testing adjustment, she has no way to defend the table at a referee. This chapter is the toolkit for that defense.

---

## 1. The reveal: why "p < 0.05" lies when you run many tests

Start with the simplest demonstration. Suppose every null hypothesis in a family of $m$ tests is true (no real effect anywhere), and you test each one at the conventional level $\alpha = 0.05$, *independently*. The probability that a *single* test rejects falsely is $\alpha = 0.05$, by construction. The probability that *at least one of the* $m$ tests rejects falsely is

$$ \Pr(\text{at least one false rejection}) = 1 - (1-\alpha)^m. $$

For $m = 1$, this is 0.05. For $m = 5$, it is 0.226. For $m = 10$, it is 0.401. For $m = 20$, it is 0.642. For $m = 100$ (a not-uncommon number once you count every cell of every heterogeneity table), it is 0.994. **At one hundred tests, you are essentially guaranteed to find at least one "significant" result purely by chance.** The phrase "significant at the five-percent level" was always shorthand for "significant under the assumption that this is the *only* test"; the moment you violate that assumption the shorthand misleads.

The number $1 - (1-\alpha)^m$ has a name in the literature: the **family-wise error rate** (FWER) — the probability that *any* test in your family of $m$ tests is a false positive. Bonferroni and Holm control FWER. Benjamini–Hochberg controls something different — the **false-discovery rate** (FDR), which we will define in §3. Romano–Wolf controls FWER like Bonferroni, but more efficiently when tests are correlated. Which one you want depends on whether you are scared of *any* false positive (FWER) or only of *most* of your claimed positives being false (FDR), and how much your tests look like each other.

The diagnostic figure that makes the math visceral is below. Run this once, look at the curve, and you will never again present a twelve-row heterogeneity table without an adjusted p-value column.

```python
# nb10.2 cell 1 — the FWER curve under independent tests, alpha=0.05.
import numpy as np
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt

rng = np.random.default_rng(42)
alpha = 0.05
m_grid = np.arange(1, 101)
fwer = 1 - (1 - alpha) ** m_grid

fig, ax = plt.subplots(figsize=(6.5, 4))
ax.plot(m_grid, fwer, lw=2)
ax.axhline(0.05, color="0.4", lw=1, ls="--")
ax.axhline(0.50, color="0.6", lw=1, ls=":")
ax.set_xlabel("Number of independent tests (m)")
ax.set_ylabel("Pr(at least one false rejection)")
ax.set_title("Family-wise error rate vs. number of tests (alpha = 0.05)")
fig.tight_layout()
fig.savefig("fwer_curve.png", dpi=150)
```

Three takeaways from staring at that curve. **First**, the curve crosses 0.50 at $m \approx 14$. At fourteen independent tests, a coin-flip's worth of your discoveries is fake. **Second**, the curve flattens slowly toward 1 — even at $m = 50$, FWER is still about 0.92, not yet 1.00 — so the "obvious" question of "how many tests is too many" does not have a clean threshold; *every* additional test bleeds FWER. **Third**, the assumption of independence is what makes the curve so steep; when tests are *correlated* (because they share subjects, regressors, or noise), the curve flattens, which is exactly the property Romano–Wolf exploits in §5. Memorize the curve. It is the reason this chapter exists.

---

## 2. Bonferroni: the blunt instrument that always works

The simplest fix is also the oldest and the most conservative. **Bonferroni** says: if you want a family-wise error rate of $\alpha$ across $m$ tests, declare each individual test significant only if its p-value is less than $\alpha / m$. Equivalently, multiply each raw p-value by $m$ to get a Bonferroni-adjusted p-value, and compare to the unadjusted $\alpha$.

The proof is one line, and it is the line that makes Bonferroni honest. By the union bound,

$$ \Pr\left( \bigcup_{j=1}^{m} \{p_j < \alpha/m\} \mid \text{all } H_0 \text{ true} \right) \le \sum_{j=1}^{m} \Pr(p_j < \alpha/m) = m \cdot \frac{\alpha}{m} = \alpha. $$

That is the FWER guarantee, no assumptions required about dependence among the tests. **This is Bonferroni's superpower and also its weakness.** It works no matter how your tests are correlated — total independence, total dependence, anything in between — which means it has to assume the worst case (perfect independence at the union-bound stage) and adjust as if every test is contributing fresh information. When tests are highly correlated (you ran the same regression on six closely-related outcomes that move together), Bonferroni is throwing away that correlation and being unnecessarily conservative.

The Maya example. Suppose she runs four heterogeneity cuts (intensity-three, minority-tercile, MSA-vs-rural, CRA-overlap) and reports the per-cut ATT and p-value:

| Cut | ATT | Unadjusted p | Bonferroni-adjusted p |
|---|---|---|---|
| High intensity | $-2.6$ | 0.008 | 0.032 |
| Mid intensity | $-1.3$ | 0.042 | 0.168 |
| High minority share | $-1.9$ | 0.018 | 0.072 |
| MSA | $-1.4$ | 0.035 | 0.140 |

With $m = 4$, the Bonferroni adjustment multiplies each raw p by 4. The "high intensity" cell survives at 0.032 (still less than 0.05); everything else is no longer significant. **The honest report** is "after Bonferroni correction across the four heterogeneity dimensions, only the high-intensity subgroup shows a statistically distinguishable ATT." The headline survives in spirit; three of the four marginal findings do not.

### When Bonferroni is the right tool

Use Bonferroni when (a) the number of tests is small (say, $m \le 5$), (b) you cannot characterize the correlation among your tests, and (c) you want a guarantee that holds for the worst-case correlation structure. Bonferroni is the tool for the conservative claim — "even if my tests were perfectly independent and adversarially designed against me, this discovery survives." For Maya's four-cut heterogeneity table, Bonferroni is defensible.

### When Bonferroni is the wrong tool

When you have many tests (say, $m \ge 20$) or when your tests are obviously correlated (six closely-related outcomes, twenty subgroup cuts on a shared sample), Bonferroni's conservatism becomes painful — you reject far fewer hypotheses than you would under a procedure that respects either the sequential structure (Holm) or the correlation (Romano–Wolf), and your power to detect real effects collapses. We will see this collapse quantitatively in §5.

---

## 3. Holm: Bonferroni's smarter sequential cousin

Bonferroni divides $\alpha$ equally across all $m$ tests. Holm (1979) noticed that this is wasteful: once you have *rejected* a few hypotheses, the remaining tests are no longer a family of $m$, they are a family of $m - k$. So you should be able to use a less stringent threshold for the un-rejected ones, while still controlling FWER overall.

The Holm procedure is sequential. Sort your $m$ p-values from smallest to largest, $p_{(1)} \le p_{(2)} \le \cdots \le p_{(m)}$. Compare:

- $p_{(1)}$ to $\alpha / m$;
- if rejected, $p_{(2)}$ to $\alpha / (m-1)$;
- if rejected, $p_{(3)}$ to $\alpha / (m-2)$;
- and so on.

You **stop** at the first non-rejection and do *not* reject any subsequent hypothesis, even if its p-value is small enough to cross its own threshold. That's the "step-down" structure: you start at the smallest p-value (the easiest to reject) and walk up, and once the chain breaks the rest stays unrejected.

The proof that Holm controls FWER is more involved than Bonferroni's, but the intuition is simple: at every step you are protecting against the *worst case* among the un-rejected hypotheses, and the worst case shrinks as you reject more, so the dividend goes back into a less stringent threshold. Mathematically, Holm strictly dominates Bonferroni — it rejects every hypothesis Bonferroni does, *and sometimes more*, with the same FWER guarantee.

Applied to Maya's four-row table:

| Rank | Cut | Raw p | Holm threshold | Reject? |
|---|---|---|---|---|
| 1 | High intensity | 0.008 | 0.05/4 = 0.0125 | Yes |
| 2 | High minority share | 0.018 | 0.05/3 = 0.0167 | No (0.018 > 0.0167) |
| 3 | MSA | 0.035 | 0.05/2 = 0.0250 | No (step-down stops) |
| 4 | Mid intensity | 0.042 | 0.05/1 = 0.0500 | No (step-down stops) |

Holm rejects the same one hypothesis Bonferroni did. In this example, the gain is zero — but that is the worst case for Holm. In larger families, Holm's sequential structure routinely gains one or two extra rejections over Bonferroni. The cost is essentially zero: same FWER guarantee, no assumption changes. **Holm is therefore the strict upgrade to Bonferroni; you should never use Bonferroni when you could use Holm.** The only reason to mention Bonferroni at all is that students and referees still recognize it, and the explanation is the cleanest.

```python
# nb10.2 cell 2 — Holm step-down on a vector of raw p-values.
import numpy as np

def holm_adjust(pvals: np.ndarray, alpha: float = 0.05) -> tuple[np.ndarray, np.ndarray]:
    """Return (holm-adjusted p-values, reject-indicator) in the original order."""
    pvals = np.asarray(pvals, dtype=float)
    m = pvals.size
    order = np.argsort(pvals)                 # ascending
    sorted_p = pvals[order]
    adj_sorted = np.empty(m)
    # Adjusted p at rank k = min over j>=k of (m - j + 1) * p_(j), capped at 1.
    running = 0.0
    for k in range(m):
        running = max(running, (m - k) * sorted_p[k])
        adj_sorted[k] = min(running, 1.0)
    adj = np.empty(m)
    adj[order] = adj_sorted
    reject = adj < alpha
    return adj, reject

# Maya's four heterogeneity cuts.
raw = np.array([0.008, 0.042, 0.018, 0.035])
adj, rej = holm_adjust(raw, alpha=0.05)
for r, a, x in zip(raw, adj, rej):
    print(f"raw={r:.3f}   holm-adj={a:.3f}   reject={x}")
```

---

## 4. Benjamini–Hochberg: when you can tolerate some false discoveries

Now we change the question. FWER asks: "what is the probability that I make *any* false positive?" That is the right question if a single false positive would be catastrophic — say, in clinical drug trials, or in fair-lending litigation where a single false discrimination claim would be ruinous. But it is the wrong question if your goal is to identify a *set* of promising findings for further study, and you can tolerate a small fraction of that set being false positives.

The **false-discovery rate** (FDR) is the expected proportion of false positives *among the rejected hypotheses*: $\text{FDR} = \mathbb{E}\left[V / \max(R, 1)\right]$ where $R$ is the number of rejections and $V$ is the number of false rejections among them. Controlling FDR at $\alpha$ means: of every batch of "discoveries" you announce, on average no more than a fraction $\alpha$ are false. This is a much weaker guarantee than FWER (which insists no false discoveries at all), and as a result it allows you to reject many more hypotheses for the same nominal $\alpha$.

The **Benjamini–Hochberg** (BH) procedure (1995) controls FDR. Sort your p-values ascending as before. Find the largest $k$ such that

$$ p_{(k)} \le \frac{k}{m} \cdot \alpha. $$

Reject all hypotheses with $p_{(j)} \le p_{(k)}$, i.e., the smallest $k$ p-values. Note the asymmetry with Holm: Holm steps *down* and stops at the first failure, BH steps *up* (or, equivalently, finds the largest passing index) and rejects everything *at or below* that index, even if intermediate indices have "failed" the BH criterion.

Applied to Maya's four cuts at $\alpha = 0.10$ (a common FDR threshold; with FDR you can afford to be more permissive than with FWER):

| Rank $k$ | Cut | Raw p | BH threshold $k\alpha/m$ | Pass? |
|---|---|---|---|---|
| 1 | High intensity | 0.008 | 0.025 | Yes |
| 2 | High minority share | 0.018 | 0.050 | Yes |
| 3 | MSA | 0.035 | 0.075 | Yes |
| 4 | Mid intensity | 0.042 | 0.100 | Yes |

All four pass under BH at the 10% FDR level. The interpretation: of these four claimed heterogeneity effects, the *expected* fraction that are false is at most 10%. That allows Maya to report all four — but with a different label than "significant at the 5% level." The honest label is "discovered with FDR control at 10%." A reader who wants the stricter guarantee can look at the Holm column; a reader who wants the looser FDR claim can look at the BH column. **Reporting both is good practice when the choice of error-control framework is itself contestable.**

### When BH is the right tool

BH is the right tool when you are *screening* a large family of hypotheses and the cost of missing a true effect (a false negative) is high relative to the cost of including a false positive in the rejection set. This is the genomics use case (testing thousands of genes for association with a phenotype, with the understanding that downstream validation experiments will weed out false positives). In empirical finance, BH is appropriate when you are reporting many heterogeneity cuts in an exploratory section — explicitly labeled exploratory — and you want a defensible procedure for which cuts to highlight. **What BH is not appropriate for is the headline claim of the paper.** The headline lives or dies under FWER. BH belongs in the heterogeneity section and the appendix.

### When BH is the wrong tool

When the tests are *highly negatively correlated*, BH's theoretical guarantees weaken (the original theorem assumed positive regression dependence or independence; Benjamini & Yekutieli (2001) gives a modified procedure for arbitrary dependence). For most empirical settings — heterogeneity cuts on the same sample, multiple outcomes on the same regression — positive correlation is the norm and BH is fine. But if you are doing something exotic (testing a difference and its negation, for example), check the dependence structure.

```python
# nb10.2 cell 3 — Benjamini-Hochberg FDR control.
def bh_fdr(pvals: np.ndarray, alpha: float = 0.10) -> tuple[np.ndarray, np.ndarray]:
    """Return (BH-adjusted p-values, reject-indicator). Adjustment is the
    standard BH q-value: q_(k) = min over j>=k of m/j * p_(j), capped at 1."""
    pvals = np.asarray(pvals, dtype=float)
    m = pvals.size
    order = np.argsort(pvals)
    sorted_p = pvals[order]
    adj_sorted = np.empty(m)
    running = 1.0
    # Walk from largest to smallest, taking running minimum.
    for k in range(m - 1, -1, -1):
        running = min(running, m / (k + 1) * sorted_p[k])
        adj_sorted[k] = running
    adj = np.empty(m)
    adj[order] = adj_sorted
    reject = adj < alpha
    return adj, reject

adj, rej = bh_fdr(raw, alpha=0.10)
for r, a, x in zip(raw, adj, rej):
    print(f"raw={r:.3f}   bh-adj={a:.3f}   reject@10%={x}")
```

---

## 5. Romano–Wolf step-down: when your tests are correlated

The fourth tool is the one your discussant will ask about if they are sharp. **Romano–Wolf** (2005, 2016) is a bootstrap-based step-down procedure that controls FWER and is *substantially more powerful* than Holm or Bonferroni when your tests are correlated.[^rw2016] The intuition is the one we noticed in §1: Bonferroni assumes the worst-case correlation among tests (treating each as a fresh union-bound contribution to the FWER); when your tests are actually correlated, the *effective* number of independent tests is smaller than $m$, and you should be able to use a less stringent threshold. Romano–Wolf operationalizes this by *bootstrapping the joint distribution* of your test statistics and reading the appropriate quantile from the bootstrap, rather than using a Bonferroni-style $\alpha/m$ approximation.

Here is the procedure in pseudo-code; the package implementation is in §6.

**Step 0.** Compute your $m$ test statistics $T_1, \ldots, T_m$ on the real data. Let them be (signed) t-statistics, and the null hypothesis for each be that the corresponding parameter is zero.

**Step 1.** Bootstrap. Re-sample the data $B$ times (with the resampling unit being the cluster, if you cluster). For each bootstrap sample, re-estimate all $m$ test statistics, *centered at the original-data estimates* so the null is imposed. Call them $T_1^{*(b)}, \ldots, T_m^{*(b)}$ for $b = 1, \ldots, B$. The centering step is the critical innovation: it ensures the bootstrap distribution approximates the joint distribution of the t-statistics *under the global null*.

**Step 2.** Step-down. Sort your real test statistics by magnitude, largest first. Compute the bootstrap p-value for the largest:

$$ p^{RW}_{(1)} = \frac{1}{B} \sum_{b=1}^{B} \mathbb{1}\!\left[ \max_j |T_j^{*(b)}| \ge |T_{(1)}| \right]. $$

If $p^{RW}_{(1)} < \alpha$, reject the first hypothesis, *remove its bootstrap column from the max*, and repeat for the second-largest statistic:

$$ p^{RW}_{(2)} = \frac{1}{B} \sum_{b=1}^{B} \mathbb{1}\!\left[ \max_{j \ne (1)} |T_j^{*(b)}| \ge |T_{(2)}| \right]. $$

Continue until a hypothesis fails or all are rejected. The "max" inside the bootstrap is what captures the correlation: if the test statistics co-move strongly, the max is not much larger than any individual statistic, and the procedure is permissive; if they are nearly independent, the max is much larger, and the procedure is conservative (recovering Bonferroni-like behavior).

The Maya example, expanded to a richer set of tests. Suppose she now runs *twelve* heterogeneity cuts — three intensity bins × two minority-share bins × two MSA-vs-rural bins — and the twelve p-values (positively correlated across cuts because they share the same underlying ATT panel) come out:

| Cut | Raw p | Holm | BH (10%) | Romano–Wolf |
|---|---|---|---|---|
| 1 | 0.005 | reject | reject | reject |
| 2 | 0.012 | reject | reject | reject |
| 3 | 0.018 | reject | reject | reject |
| 4 | 0.022 | no | reject | reject |
| 5 | 0.031 | no | reject | reject |
| 6 | 0.044 | no | reject | no |
| 7 | 0.058 | no | no | no |
| ... | ... | ... | ... | ... |

Holm rejects 3, BH (at 10%) rejects 6, Romano–Wolf (FWER 5%) rejects 5. The ordering is informative: Holm < Romano–Wolf < BH, when tests are correlated. **Romano–Wolf gives you FWER control with more rejections than Bonferroni/Holm because it credits the correlation; BH gives you yet more rejections than RW because it controls a weaker error rate (FDR rather than FWER).**

### When Romano–Wolf is the right tool

Use Romano–Wolf when (a) your family of tests is large (say, $m \ge 10$), (b) the tests are correlated (the usual case in empirical work with shared samples), and (c) you want to claim FWER control rather than only FDR control. Romano–Wolf is the modern default for the *primary* heterogeneity table or the *primary* multi-outcome table in a paper where you want to make claims about specific individual rows. Anderson (2008) popularized it in development economics for multi-outcome tests; the procedure has become standard in serious empirical work since.[^anderson2008]

### When Romano–Wolf is the wrong tool

Two cases. First, when you have *very few* tests ($m \le 3$); the bootstrap machinery is overkill and Holm gives essentially the same answer. Second, when you cannot characterize the *re-sampling unit* — Romano–Wolf requires you to bootstrap, and the bootstrap is only valid if you know how to re-sample (clusters? observations? blocks?). If your design has unusual dependence (network effects, spillovers across treated units), the bootstrap may itself be invalid and Romano–Wolf inherits that problem.

---

## 6. Code: a Romano–Wolf implementation you can read

The educational implementation below shows the bootstrap-and-step-down logic on a panel regression. For production use, the R package `RomanoWolfTest` or the Stata package `rwolf2` (Clarke 2021) is standard;[^clarke2021] in Python, `multipletests` from `statsmodels` covers Bonferroni / Holm / BH but not Romano–Wolf, so you write the loop yourself or call out to R.

```python
# nb10.2 cell 4 — Romano-Wolf step-down for a vector of t-statistics from
# m parallel regressions, with a cluster-bootstrap that re-samples states.
# Pedagogical: O(B * m) regression refits; for production, vectorize or
# replace inner refit with a Frisch-Waugh-Lovell residualization.
import numpy as np
import pandas as pd
import statsmodels.formula.api as smf

def romano_wolf(
    df: pd.DataFrame,
    formulas: list[str],         # m regression formulas, each yielding ONE coefficient of interest
    param: str,                  # the coefficient name (same across formulas)
    cluster_col: str,            # cluster bootstrap unit
    B: int = 999,
    seed: int = 7,
) -> pd.DataFrame:
    """Romano-Wolf step-down on m hypothesis tests. Returns a table with
    raw p-values, adjusted p-values, and the step-down decision at alpha=0.05."""
    rng = np.random.default_rng(seed)
    m = len(formulas)

    # Step 0: real-data t-statistics.
    t_obs = np.empty(m)
    for j, f in enumerate(formulas):
        fit = smf.ols(f, data=df).fit(
            cov_type="cluster", cov_kwds={"groups": df[cluster_col]}
        )
        t_obs[j] = fit.params[param] / fit.bse[param]

    # Step 1: cluster bootstrap, recentering each t* at the observed coefficient.
    clusters = df[cluster_col].unique()
    n_clusters = clusters.size
    T_boot = np.empty((B, m))
    for b in range(B):
        sampled = rng.choice(clusters, size=n_clusters, replace=True)
        db = pd.concat([df[df[cluster_col] == c] for c in sampled], ignore_index=True)
        for j, f in enumerate(formulas):
            fb = smf.ols(f, data=db).fit(
                cov_type="cluster", cov_kwds={"groups": db[cluster_col]}
            )
            # Center at the original estimate so the null is imposed.
            T_boot[b, j] = (fb.params[param] - fit_orig_params[j]) / fb.bse[param] \
                if False else (fb.params[param] / fb.bse[param]) - t_obs[j]

    # Step 2: step-down.
    order = np.argsort(-np.abs(t_obs))    # largest |t| first
    p_rw = np.empty(m)
    active = set(range(m))
    for k, j in enumerate(order):
        max_abs = np.max(np.abs(T_boot[:, list(active)]), axis=1)
        p_rw_k = (max_abs >= np.abs(t_obs[j])).mean()
        # Monotonicity: enforce p_(k) >= p_(k-1).
        if k > 0:
            p_rw_k = max(p_rw_k, p_rw[order[k-1]])
        p_rw[j] = p_rw_k
        active.discard(j)
    return pd.DataFrame({
        "formula": formulas,
        "t_obs": t_obs,
        "p_raw": 2 * (1 - 0.5 * (1 + np.abs(t_obs)/np.abs(t_obs).max())),  # placeholder; use real p
        "p_rw":  p_rw,
        "reject_rw_5pct": p_rw < 0.05,
    })
```

A note on the code's pedagogical fidelity. The function above re-runs every regression on every bootstrap, which is honest about what the procedure does but slow for $B = 1000$ and $m = 12$. In practice, a careful implementation uses Frisch–Waugh–Lovell to residualize once and then bootstrap only the residuals × treatment products; the running time drops by orders of magnitude. We keep the slow version here because it makes the *what* of Romano–Wolf transparent. When you actually run this on a real paper, use `rwolf2` in Stata or the R package.

The line that reads `T_boot[b, j] = (fb.params[param] / fb.bse[param]) - t_obs[j]` is the centering step. Without it, the bootstrap distribution of the t-statistic is centered at the observed t, not at zero, and the step-down procedure does not control FWER under the null. The bug is subtle and easy to miss; lecturing on this single line is half of why this chapter exists.

---

## 7. The decision tree: which procedure for which question

Here is the decision tree, distilled. Tape it to the inside of your laptop.

**Q1: Is this a single headline test, or a family?** Single test → no adjustment needed (you are not in this chapter's territory). Family → continue.

**Q2: What error rate do you want to control?** *Any false positive in the family would be a problem* → FWER → Q3. *Some false positives are tolerable if most of my claims are real* → FDR → BH (skip to §4 to confirm the assumption fits your dependence structure).

**Q3: Are the tests correlated, and is $m$ moderate-to-large?** *Yes (both)* → Romano–Wolf. *No* (small $m$ or unknown correlation) → Holm. (We do not recommend Bonferroni except as a known-conservative sanity check; Holm dominates it.)

The tree is small because the choices are small. The trap is in Q2 — students reach for BH because it gives them more rejections, when the right framework for their question is FWER. **The rule:** if the rejection is going into the *headline* of the paper, control FWER (Holm or RW). If the rejection is going into an *exploratory* section explicitly labeled as such, FDR (BH) is acceptable. **Mixing the two in the same table without labeling is dishonest**, even if it would not be caught by a referee.

---

## 8. Five places multiple-testing problems hide that you do not notice

Multiple-testing problems are insidious. The obvious form — a heterogeneity table with twelve rows — students adjust for. The non-obvious forms below are the ones that bite in revision.

**1. Multiple outcomes.** You run the same regression on six closely-related outcomes (denial rate, denial rate for purchase mortgages, denial rate for refi, denial rate by ethnicity, denial rate by loan size, ...) and report whichever has the smallest p-value. This is a multiple-testing problem with $m = 6$ even though you only report one row. The discipline is: **pre-register the outcome family in your PAP (Chapter 7.3), and report an adjusted p-value across the family even when you also report a single "primary outcome."** Anderson (2008) is the canonical reference for this case.

**2. Specification searching.** You ran the spec curve from Chapter 8.1 and reported the headline using one of the 96 forks. Even if you pre-registered the headline fork, the *act of having considered* the other forks is a form of multiple-testing in spirit, though not in the formal FWER sense; the spec-curve plot is the honest disclosure that addresses this. Some recent work (Simonsohn, Simmons, Nelson 2020) proposes formal multiple-testing corrections on the spec-curve median; we mention it as a research frontier.[^ssn2020]

**3. Lookup-and-test in placebos.** You ran twelve placebos and one was "marginal" at p = 0.06. Under FWER control, the *probability* that twelve placebos return at least one p < 0.06 under the null is roughly $1 - (1 - 0.06)^{12} \approx 0.52$. The marginal placebo is *expected by chance*, not a danger sign. The right report: "twelve placebos, all p > 0.05 after Bonferroni; the smallest unadjusted p is 0.06."

**4. Subgroup discovery.** You discovered a heterogeneity result by *looking at the data*, then ran the test on the same data, then declared it significant. This is the garden-of-forking-paths problem (Gelman & Loken 2014), and no after-the-fact multiple-testing correction can fully fix it.[^gl2014] The discipline is to either pre-register the heterogeneity, or split the sample into discovery and confirmation halves (lose half your power, gain credibility), or report the result explicitly as exploratory with FDR control rather than FWER.

**5. Sequential analyses across drafts.** Between conference and submission, you re-estimated your headline twice and updated the spec twice. Each re-estimation is, in spirit, another test against the same null. Under any formal multiple-testing framework, this would require an adjustment; in practice, no one does it, but the *meta-discipline* of locking the headline at the pre-registration stage and *committing all spec changes to git* is your protection. The spec curve is the visible artifact of the alternative-specs population; your pre-registration is the protection against the temporal-search version of the problem.

---

## 9. Reporting: the table and the sentence

When you report multiple-testing-adjusted results, the table and the sentence both need to be explicit.

**Table.** Add a column for the unadjusted p-value *and* a column for the adjusted p-value, with a footnote naming the procedure. Example:

> *Table 7.* Heterogeneity of fair-lending examination effect by examination intensity, county minority share, MSA status, and CRA overlap. Reported p-values are unadjusted (column 4) and Romano–Wolf step-down adjusted across the 12-test family (column 5, B = 999 cluster-bootstrap replications). Stars in column 6 indicate Romano–Wolf-adjusted significance at the 5% (FWER) level.

**Sentence.** In the text, write what you found *after* the adjustment, not before. Bad: "We find significant heterogeneity in three of the twelve cuts (p < 0.05)." Good: "After Romano–Wolf adjustment for the family of twelve heterogeneity tests, two cuts remain significant at the 5% FWER level: high-intensity examinations (p^{RW} = 0.014) and high-minority-share counties (p^{RW} = 0.028)."

The phrase **"after adjustment"** is the load-bearing two-word phrase of this chapter. If you find yourself reporting a result without it, you are claiming a p-value that no longer means what it says.

---

## 10. Common student mistakes and the audit you should run

Four mistakes are nearly universal in first drafts:

1. **Counting tests inconsistently.** Students adjust within the heterogeneity table but not across heterogeneity + outcomes + placebos. The right count is *across every test in the paper that contributes to a discovery claim*. Be liberal; the cost of over-counting is a slightly conservative adjustment, the cost of under-counting is a false discovery.

2. **Using Bonferroni when Holm or Romano–Wolf would dominate.** No reason for this except inertia. Use Holm at minimum; use Romano–Wolf when $m \ge 10$ and tests are correlated.

3. **Reporting BH-adjusted p-values as if they were FWER-controlled.** They are not. A BH q-value of 0.05 means "of the rejections at this threshold, at most 5% are expected to be false," *not* "the probability that this single rejection is false is at most 5%."

4. **Forgetting to adjust the headline.** If the headline test is one of a family — and it usually is — the adjustment applies to the headline too. The headline is not exempt because it is the headline.

The audit you should run before submission: open your paper, list every test that has a p-value attached, count them, and decide which families they belong to. (Pre-registration helps here, because the families were named in advance.) For each family, compute the adjusted p-values. For each "significant" claim in the paper, check whether it is still significant under adjustment. Fix the text wherever it is not.

---

## 11. Where this chapter sits in Week 10

The triage memo from Chapter 10.1 told you which conference comments were Required. Many of those Required items are heterogeneity comments, and heterogeneity is where multiple testing bites hardest. **Chapter 10.2 (this chapter) gives you the tools; Chapter 10.3 gives you the modern methodology (causal forests, CATE) that uses those tools properly; Chapter 10.4 warns you about mediation-style multiple-testing problems that look like mechanism but are really fishing; Chapter 10.5 closes the week by tying the multiple-testing discipline to external validity, where the question "would this replicate?" is itself a form of out-of-sample multiple testing.**

The next chapter assumes you can compute a Romano–Wolf-adjusted p-value on a vector of subgroup estimates. If you cannot — if the code in §6 did not yet make sense — re-read this chapter and run the worked example before continuing.

---

[^anderson2008]: Anderson, M. L. (2008). "Multiple Inference and Gender Differences in the Effects of Early Intervention: A Reevaluation of the Abecedarian, Perry Preschool, and Early Training Projects." *Journal of the American Statistical Association* 103(484):1481–1495.

[^rw2016]: Romano, J. P. and Wolf, M. (2016). "Efficient computation of adjusted p-values for resampling-based stepdown multiple testing." *Statistics and Probability Letters* 113:38–40.

[^clarke2021]: Clarke, D., Romano, J. P., and Wolf, M. (2020). "The Romano–Wolf Multiple Hypothesis Correction in Stata." *Stata Journal* 20(4):812–843.

[^ssn2020]: Simonsohn, U., Simmons, J. P., and Nelson, L. D. (2020). "Specification curve analysis." *Nature Human Behaviour* 4:1208–1214.

[^gl2014]: Gelman, A. and Loken, E. (2014). "The Statistical Crisis in Science." *American Scientist* 102(6):460.

---

**Chapter cross-references.** Built on Ch 2.4 (the language of significance and standard errors), Ch 7.3 (pre-registration of the outcome family), Ch 7.5 (the threats table where each test connects to a threat), Ch 8.1 (the specification curve as the multi-test disclosure), Ch 8.2 (the wild cluster bootstrap as a sibling resampling technique), and Ch 10.1 (the triage memo that pointed at multiple-testing problems in the conference comments). Feeds Ch 10.3 (heterogeneity testing under the discipline of pre-registration and FWER control) and Ch 10.4 (mediation as a multi-step inference where multiple-testing problems multiply).
