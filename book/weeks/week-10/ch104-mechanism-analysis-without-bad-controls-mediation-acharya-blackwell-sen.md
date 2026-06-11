# Ch 10.4 — Mechanism Analysis Without Bad Controls: Mediation Done Right, the Acharya-Blackwell-Sen Critique, and Sequential-Ignorability as a Last Resort

Chapter 10.3 told you who is affected. This chapter asks *why*. The question is the second-most-common one after every empirical talk in the universe, and it usually arrives in a single sentence: **"What is the mechanism?"** Maya has shown that fair-lending examinations reduced minority denial gaps, and the heterogeneity result from Chapter 10.3 suggested intensity is the active dimension. The natural follow-up — the one the discussant pressed and that lives as a "Required" row on her triage memo — is: *how* did examinations work? Did they change lender behavior directly (intimidation), through new compliance practices (training), through portfolio reshuffling (selection)? Each candidate channel is a separate substantive claim, and each has a different policy implication. Answering the channel question well is the single most expensive thing left on Maya's revision list.

The result this chapter turns on, stated in one ugly sentence so the rest is the unpacking: **conditioning on a post-treatment variable to "isolate" a mechanism is the single most common identification mistake in empirical work, and the modern critique — Acharya, Blackwell & Sen (2016) — formalizes why, while a careful framework (controlled direct effects under sequential ignorability) tells you what you *can* honestly do.**[^abs2016] Most mechanism analyses you will read in journals and most mechanism analyses you will be tempted to run yourself are *wrong*, in the specific sense that they introduce post-treatment selection bias and produce coefficients that do not estimate the quantity their authors claim. The mistake is so widespread that an entire generation of corporate-finance papers has been quietly revised under the Acharya–Blackwell–Sen lens, and the empirical-economics community has converged on a much more cautious vocabulary for what mechanism analysis can and cannot deliver.

This chapter teaches that vocabulary. We will (1) state the bad-controls problem and show with a clean simulation that even a "small" post-treatment confounder produces severely biased mediation estimates; (2) lay out the Acharya–Blackwell–Sen sequential-g framework and its key estimand, the **controlled direct effect** (CDE), with the assumption it requires (sequential ignorability) and what it gives you in exchange; (3) discuss the three modes of honest mechanism analysis in empirical finance — heterogeneity-as-mechanism, instrument-for-mediator, design-based mechanism — and when each is appropriate; and (4) show the code that runs CDE via sequential-g on Maya's panel and that simulates the bias if you don't.

---

## 1. The reveal: why a "mediation" regression is usually wrong

Start with the dominant statistical-mediation framework, **Baron–Kenny (1986)**, which dominated empirical psychology and a decade of finance for one reason — it is simple and seductive.[^bk1986] The recipe is: estimate the total effect of $D$ on $Y$, the effect of $D$ on a candidate mediator $M$, and the effect of $D$ on $Y$ *controlling for* $M$; if the third coefficient is smaller than the first, $M$ "explains" some of the effect. Most papers reduce this to a single regression with both $D$ and $M$ on the right-hand side, and interpret the coefficient on $D$ as the "direct effect" and the implied difference as the "indirect effect through $M$."

This recipe is *almost always invalid* in observational empirical finance, and the reason has nothing to do with the regression's algebra. It has to do with what $M$ is, in a real causal world. $M$ is a *post-treatment* variable — caused by $D$ — and almost always shares unobserved determinants with $Y$. **Conditioning on $M$ in a regression of $Y$ on $D$ opens a collider path between $D$ and $Y$ through those unobserved determinants**, producing what Pearl calls an "M-bias" or "collider bias" and what Acharya–Blackwell–Sen call "post-treatment selection bias." The "direct effect" coefficient is now confounded by the very act of conditioning. The arithmetic looks like a clean decomposition; the causal interpretation is wrong.

Let us see this with a simulation, because the algebra is in §2 but the simulation is in everyone's bones.

```python
# nb10.4 cell 1 — simulate the bad-controls problem.
# True structural model:
#   U is an unobserved confounder of M and Y (NOT of D, by construction).
#   D is randomly assigned (so D->Y has no confounder; the "total effect" is clean).
#   M is caused by D (with some U-effect on M).
#   Y is caused by D, by M, and by U.
# True direct effect of D on Y = beta_DY (we set to 1.0).
# True indirect effect of D on Y through M = beta_DM * beta_MY (we set to 0.5 * 1.0 = 0.5).
# Total effect = 1.5.
import numpy as np
import statsmodels.api as sm

rng = np.random.default_rng(7)
N = 20_000

U = rng.standard_normal(N)
D = rng.binomial(1, 0.5, N)
M = 0.5 * D + 0.8 * U + 0.3 * rng.standard_normal(N)
Y = 1.0 * D + 1.0 * M + 0.8 * U + 0.3 * rng.standard_normal(N)

# Three regressions: total, direct (naive), and Baron-Kenny "mediation".
total  = sm.OLS(Y, sm.add_constant(D)).fit()
direct = sm.OLS(Y, sm.add_constant(np.c_[D, M])).fit()  # the "bad-controls" spec

print(f"Total effect       beta_D            = {total.params[1]:+.3f}  (truth 1.5)")
print(f"Baron-Kenny 'direct' coef on D       = {direct.params[1]:+.3f}  (truth 1.0)")
print(f"Baron-Kenny 'mediator' coef on M     = {direct.params[2]:+.3f}  (truth 1.0)")
```

Run this and you see, reliably across seeds, the total effect comes back as roughly 1.5 (correct — $D$ was randomized, no confounding). The "direct effect" coefficient comes back as roughly 0.66, *not* 1.0, even though the simulation was kind to us (random $D$, decent sample size). The coefficient on $M$ comes back as roughly 1.41, *not* 1.0. **Both coefficients are biased.** The "direct effect" is contaminated by the confounding between $M$ and $Y$ that the regression cannot resolve; the "mediator effect" is amplified by the same confounding. A Baron–Kenny mediation report on this simulated data would conclude that 56% of the total effect "flows through $M$" — but the true mediation share is 33%. Off by nearly a factor of two, in a setting where $D$ is *randomized*.

If you doubt this, change the simulation: make the unobserved confounder $U$ smaller (set its coefficients to 0.2) and the bias shrinks; make it larger and the bias grows. There is no version of the Baron–Kenny regression that is unbiased when $M$ has unobserved confounders with $Y$. **And in observational empirical finance, $M$ always has unobserved confounders with $Y$.** Compliance practices and outcome variables share unobserved determinants. Portfolio choices and outcome variables share unobserved determinants. CSR ratings and outcome variables share unobserved determinants. The list is long and the bias is generic.

---

## 2. Why the regression fails: directed acyclic graphs and the collider open

Draw the structural model from the simulation as a directed acyclic graph (DAG). $D$ is randomized, so it has no parents. $U$ has no parents. $M$ has two parents, $D$ and $U$. $Y$ has three parents, $D$, $M$, and $U$.

```
        U
       / \
      v   v
D --> M --> Y
 \           ^
  -----------|
```

The total effect of $D$ on $Y$ in this DAG is the sum of two open paths: $D \to Y$ (direct) and $D \to M \to Y$ (indirect). $U$ is *not* on any open path because there is no edge $D \to U$ or $U \to D$ — $D$ is randomized.

Now condition on $M$ (i.e., include $M$ as a regressor). Conditioning on $M$ does two things. First, it correctly blocks the indirect path $D \to M \to Y$, so the indirect contribution is now removed from the $D$ coefficient. *Good.* Second, **it opens a new path** through the collider $M$: the path $D \to M \leftarrow U \to Y$. This path was previously blocked because $M$ was a collider; conditioning on a collider opens it. Now there is a non-causal path from $D$ to $Y$ through $U$, and it biases the $D$ coefficient. *Bad.* The Baron–Kenny "direct effect" is the true direct effect minus the bias from the opened collider, which is what the simulation showed.

The lesson, in one sentence: **conditioning on a post-treatment mediator that shares unobserved determinants with the outcome opens a collider and biases the implied direct effect.** This is the core insight Acharya, Blackwell & Sen formalized in 2016 (drawing on a much older literature in epidemiology and statistics — Robins 1986, Pearl 2001) and that the empirical-economics community has internalized since.[^abs2016]

---

## 3. What the Acharya–Blackwell–Sen framework offers

ABS (2016) was a methodological article in the *American Political Science Review* targeted at political scientists, but its methodological contribution applies anywhere mediation appears. The contribution is twofold: it explains what the bad-controls problem is (the collider story above), and it offers a procedure for **estimating the controlled direct effect (CDE)** of $D$ on $Y$ holding $M$ fixed at a chosen value — under an assumption (sequential ignorability) that is strong but at least *namable and testable in part*.

### 3.1 The controlled direct effect

The CDE is the average effect of $D$ on $Y$ if the mediator were *held fixed* at $m$ for everyone in the population, regardless of what $D$ does to $M$. In counterfactual notation: $\text{CDE}(m) = \mathbb{E}[Y(d=1, m) - Y(d=0, m)]$, where the second slot is the mediator value being held fixed. The CDE is a *policy-relevant* quantity in many settings: if we could regulate the mediator, what would the effect of treatment be? In Maya's case, $\text{CDE}(m)$ asks: if we held *compliance training intensity* fixed at value $m$ for all lenders, what would be the effect of fair-lending examinations on denial gaps? The answer separates the "examinations cause changes in training, training causes changes in denial gaps" channel from the "examinations cause changes in something other than training" residual.

The CDE is *different from* the indirect effect of mediation analysis (which is the part of the total effect that "flows through" $M$); it is *also* different from the natural direct effect (which is the effect of $D$ on $Y$ if $M$ took its natural-under-$D=0$ value). The ABS framework deliberately focuses on the CDE because it requires the *weakest* assumptions of the three, and because the CDE is what most policy questions actually want.

### 3.2 The sequential-g estimator

The estimator ABS recommend, the **sequential-g** estimator (Robins 1986; ABS 2016), is a two-step procedure that avoids the bad-controls problem by *de-mediating* the outcome before regressing on $D$. The two steps:

**Step 1 — Mediator equation.** Estimate the effect of $M$ on $Y$ holding $D$ fixed:

$$ Y_i = \alpha + \gamma D_i + \delta M_i + \boldsymbol{x}_i'\boldsymbol{\theta} + \boldsymbol{z}_i'\boldsymbol{\phi} + u_i, $$

where $\boldsymbol{x}$ is the set of pre-treatment controls and $\boldsymbol{z}$ is the set of post-treatment intermediate variables you *condition on* to make $M$'s relationship with $Y$ exogenous (more on this in §3.3). Recover $\hat{\delta}$.

**Step 2 — De-mediated outcome regression.** Construct the de-mediated outcome $\tilde{Y}_i = Y_i - \hat{\delta} (M_i - m^*)$, where $m^*$ is the chosen reference value of the mediator (often $m^* = 0$, the no-mediator counterfactual). Regress $\tilde{Y}$ on $D$ and pre-treatment controls only:

$$ \tilde{Y}_i = \alpha + \tau D_i + \boldsymbol{x}_i'\boldsymbol{\theta} + e_i, $$

and read $\hat{\tau}$ as the controlled direct effect of $D$ on $Y$ holding $M$ at $m^*$.

The key thing this does not do: it never *includes* $M$ as a regressor in the outcome equation for $D$'s coefficient. The de-mediation happens in step 1; the $D$-effect is estimated in step 2 *without* $M$ on the right-hand side. The collider is never opened in the $\hat{\tau}$ equation.

Inference is by bootstrap (cluster-bootstrap if your design clusters), because the two-step structure complicates analytic standard errors. ABS provide a derivation under exchangeability assumptions; in practice, 1,000-replication cluster-bootstrap is the default.

### 3.3 Sequential ignorability: the assumption you have to swallow

The CDE is identified by sequential-g *only if* a specific assumption holds, and the assumption is the load-bearing piece of this entire chapter. **Sequential ignorability**: conditional on pre-treatment controls $\boldsymbol{x}$ and on the intermediate post-treatment variables $\boldsymbol{z}$, the mediator $M$ is as good as randomly assigned with respect to the outcome's residual.

That is the same as saying: there is no unobserved confounder of $M$ and $Y$ once you condition on $(\boldsymbol{x}, \boldsymbol{z})$. The set $\boldsymbol{z}$ is allowed to include post-treatment variables that lie on other channels between $D$ and $Y$ — that is the *sequential* part — but it must close every back-door path between $M$ and $Y$ that does not pass through $D$.

This assumption is **very strong** in observational empirical finance. It is the analog of the unconfoundedness assumption from Chapter 4 (the strongest assumption in causal inference), now applied to the mediator step. In Maya's setting, sequential ignorability would require that, conditional on county-year covariates and on every other channel (portfolio composition, lender entry, compliance staffing), there is no unobserved variable that causes both training intensity and denial gaps. That is hard to believe. Lenders that adopt training likely also adopt other unobserved practices (managerial culture, monitoring intensity) that affect denial gaps directly.

**The honest report**, when you run sequential-g, says exactly that: "Sequential-g delivers the controlled direct effect under sequential ignorability; this assumption is strong, and we provide sensitivity analyses [Oster δ in Chapter 8.2, Cinelli–Hazlett sensitivity contours] showing how the CDE estimate moves under plausible violations." The CDE result is reported with explicit dependence on the assumption, not as a stand-alone causal claim.

---

## 4. Code: sequential-g estimation of the CDE

The code below implements the two-step procedure on Maya's panel, with a cluster-bootstrap for inference.

```python
# nb10.4 cell 2 — sequential-g estimator of the CDE, with cluster bootstrap.
import numpy as np
import pandas as pd
import statsmodels.formula.api as smf

rng = np.random.default_rng(8)

def sequential_g(
    df: pd.DataFrame,
    y_col: str,                 # outcome
    d_col: str,                 # treatment
    m_col: str,                 # mediator (post-treatment, the channel we're isolating)
    x_cols: list[str],          # pre-treatment controls
    z_cols: list[str],          # other post-treatment intermediates to condition on in step 1
    cluster_col: str,
    m_star: float = 0.0,        # value to hold mediator at; default 0 (no-mediator counterfactual)
    B: int = 999,
) -> dict:
    """Estimate the controlled direct effect of D on Y holding M at m_star.

    Step 1: regress Y on D, M, X, Z; recover delta_hat = coef on M.
    Step 2: form Y_tilde = Y - delta_hat * (M - m_star); regress on D, X.
    Bootstrap by cluster for inference.
    """
    def estimate(d_sample):
        # Step 1.
        rhs1 = " + ".join([d_col, m_col] + x_cols + z_cols)
        fit1 = smf.ols(f"{y_col} ~ {rhs1}", data=d_sample).fit()
        delta_hat = fit1.params[m_col]
        # Step 2.
        d_sample = d_sample.copy()
        d_sample["_y_tilde"] = d_sample[y_col] - delta_hat * (d_sample[m_col] - m_star)
        rhs2 = " + ".join([d_col] + x_cols)
        fit2 = smf.ols(f"_y_tilde ~ {rhs2}", data=d_sample).fit()
        tau_hat = fit2.params[d_col]
        return tau_hat, delta_hat

    # Point estimate.
    tau_hat, delta_hat = estimate(df)

    # Cluster bootstrap.
    clusters = df[cluster_col].unique()
    tau_boot = np.empty(B)
    for b in range(B):
        sampled = rng.choice(clusters, size=clusters.size, replace=True)
        df_b = pd.concat([df[df[cluster_col] == c] for c in sampled], ignore_index=True)
        tau_boot[b], _ = estimate(df_b)
    se = tau_boot.std(ddof=1)
    ci = np.quantile(tau_boot, [0.025, 0.975])
    return {
        "tau_hat": tau_hat,
        "delta_hat": delta_hat,
        "se_boot": se,
        "ci_boot": ci,
        "B": B,
    }

# Maya's call: Y=gap, D=exam, M=training_intensity, X=pre-treatment county controls,
# Z=other post-treatment intermediates (portfolio composition, lender entry).
result = sequential_g(
    df=maya_panel,
    y_col="gap",
    d_col="exam",
    m_col="training_intensity",
    x_cols=["log_pop", "median_inc", "pre_minority_share"],
    z_cols=["lender_entry", "portfolio_concentration"],
    cluster_col="state",
    m_star=0.0,
    B=999,
)
print(f"CDE (training=0)     = {result['tau_hat']:+.3f} pp")
print(f"Bootstrap SE         = {result['se_boot']:.3f}")
print(f"95% CI               = [{result['ci_boot'][0]:+.3f}, {result['ci_boot'][1]:+.3f}]")
```

When Maya runs this, she might get a CDE of, say, $-0.7$ pp with a 95% CI of $[-1.2, -0.2]$. Compare to her total ATT of $-1.4$ pp. **The interpretation: holding training intensity at zero, the examination effect would be reduced to about half of its observed magnitude. The other half (the "indirect" portion) flows through training intensity.** This is a meaningful mechanism finding — but the meaningfulness rests on the sequential-ignorability assumption, which Maya must defend.

### How to read the output

Three quantities to interpret carefully:

1. **The CDE point estimate $\hat{\tau}$.** This is the effect of examinations on denial gaps if training were prevented from responding. It is the *non-training* channel.
2. **The implied mediation share**, $(\widehat{\text{ATT}} - \hat{\tau}) / \widehat{\text{ATT}}$. In Maya's example, $(-1.4 - (-0.7)) / -1.4 = 0.5$, so half of the effect is mediated through training. *Do not over-interpret this number*: it is a function of two estimates, each with its own error, and it depends on the sequential-ignorability assumption.
3. **The bootstrap CI on $\hat{\tau}$.** This is your honest uncertainty about the CDE. If the CI is wide, you cannot pin down the channel; if it is narrow, you have evidence.

---

## 5. The other modes of honest mechanism analysis

Sequential-g with sequential ignorability is one tool in the kit; it is the most ambitious one because it tries to give you a *quantitative* decomposition. Three other modes are often more defensible because they require weaker assumptions, at the cost of weaker conclusions.

### 5.1 Heterogeneity-as-mechanism

This is the move you started in Chapter 10.3 — and it is the cleanest "mechanism" argument when you can pull it off. The logic: if a *pre-treatment* moderator predicts which units show the largest treatment effects, and that moderator has a substantive interpretation as a *proxy for the mechanism*, then the heterogeneity *is* the mechanism evidence. Maya's intensity-by-three dose-response is exactly this: examinations *are more intense* in some states; *more intense examinations* generate larger effects; therefore the active ingredient is *intensity*. We never had to estimate a mediator coefficient because we did not need to.

The advantage of heterogeneity-as-mechanism is that it is identified under the *same* assumption as the headline (parallel trends within each subgroup) — no extra sequential-ignorability machinery, no bad-controls trap, no Baron–Kenny regression to defend. The disadvantage is that it is only available when you have a pre-treatment proxy for the mechanism. If you cannot operationalize "training intensity" as a pre-treatment variable (because all training is post-treatment by construction), heterogeneity-as-mechanism cannot reach this channel.

**The discipline**: name your candidate mechanisms before estimation, identify which can be operationalized as pre-treatment moderators, and use heterogeneity-as-mechanism for those. For the rest, you need sequential-g or one of the modes below.

### 5.2 Instrument-for-mediator

If you have an instrument $Z$ that affects $M$ but not $Y$ directly (i.e., $Z$ is excluded from the structural outcome equation), you can identify the effect of $M$ on $Y$ via 2SLS, and back out the indirect effect of $D$ through $M$ as the product of $D$'s effect on $M$ and $M$'s effect on $Y$ (now both causally estimated). This is the IV-mediator approach (Imai et al. 2010 derive identification conditions in detail).[^iktv2010]

The hard part is finding $Z$. In Maya's setting, an instrument for training intensity might be a state-level legal requirement (some states mandate annual fair-lending training, others do not, in ways that vary independently of the examination program). If she can argue exclusion (the training mandate affects denial gaps only through training), she can run a 2SLS where examinations are exogenous (by the parallel-trends assumption of the headline) and training intensity is endogenized by the mandate instrument. This gives an honest causal effect of training on denial gaps.

The advantage is that the IV-mediator approach can give a *causal* mechanism estimate without sequential ignorability. The disadvantage is that the instrument is rarely credible. Excludability is a strong assumption; in practice, IV-mediator papers in finance are rare and most reviewers are skeptical.

### 5.3 Design-based mechanism: separate experiments for different channels

The cleanest mechanism analysis is the *separate experiment*. If you can find a quasi-experimental variation that affects only one candidate channel (say, a policy that changes training requirements but nothing else about examinations), and you can estimate its effect on denial gaps, you have a direct measurement of that channel — no mediation regression needed. The total examination effect can then be apportioned: the part of the examination effect "consistent with" the training-only-experiment effect is the training channel; the residual is "other channels."

Design-based mechanism is the gold standard. It rarely exists. When it does, it is typically the result of years of institutional knowledge about which policy changes affect which channels — exactly the institutional knowledge that emerges in the mentor session (Lab 10) and that you build over a research career.

---

## 6. Gao et al. (2024) on overlapping ownership: a worked mechanism story

A real example from the empirical-finance literature. **Gao, Han, Kim & Pan (2024)** in *Journal of Corporate Finance* estimate the effect of overlapping institutional ownership on firm outcomes.[^ghkp2024] The headline result is that firms whose top institutional owners also hold large stakes in competing firms make different strategic choices (price coordination, capital expenditure timing) than firms without overlapping ownership. The natural mechanism question is: *how* does overlapping ownership cause coordination? Through board-level pressure? Through information channels? Through compensation contract design?

The paper's mechanism analysis (§5 of the paper) uses *heterogeneity-as-mechanism*: it shows that the coordination effect is stronger when (a) the overlapping owner has a board seat at both firms (suggesting board channel) and (b) when the overlapping owner is an active investor rather than a passive index fund (suggesting active-monitoring channel). The paper *does not* attempt a sequential-g decomposition of overlapping ownership's effect on, say, executive compensation; it uses heterogeneity-as-mechanism precisely because the candidate mechanisms have pre-treatment proxies (board seats, fund-type designations) that the data can support.

This is the modern template for honest mechanism analysis in empirical finance: lean on heterogeneity-as-mechanism wherever possible, use sequential-g sparingly and with explicit sensitivity analysis, and avoid the Baron–Kenny mediation regression entirely. Reviewers in top finance journals now recognize the Baron–Kenny spec as a red flag in observational papers; do not put one in yours.

---

## 7. The mediation-report sentence, and what *not* to say

The honest mediation-report sentence has three parts: (a) what mechanism you tested, (b) what method you used (with the assumption named), and (c) what you found, *with explicit uncertainty about the assumption*.

**Good**: "We tested the *training-intensity* channel using sequential-g (Acharya, Blackwell & Sen 2016), conditioning on lender-entry and portfolio-composition intermediates. The controlled direct effect of examinations on denial gaps holding training at zero is $-0.7$ pp (95% bootstrap CI: $[-1.2, -0.2]$), implying that approximately half of the total $-1.4$ pp ATT operates through changes in training intensity. This decomposition relies on sequential ignorability: we provide sensitivity analyses (Appendix D.3) showing the implied mediation share remains in the $40$–$60$% range across plausible violations."

**Bad** (Baron–Kenny mediation): "Controlling for training intensity, the examination effect drops from $-1.4$ pp to $-0.7$ pp, showing that half the effect flows through training." (No mention of the bad-controls problem, no sensitivity, no assumption.)

**Worse** (causal language overreach): "Training is the mechanism through which examinations reduce denial gaps." (The decomposition does not identify *the* mechanism; it identifies the share *consistent with* the training channel under a strong assumption.)

The word *mechanism* should be used with the same discipline as the word *causal*: only when the design supports the claim, and only with the assumption made explicit.

---

## 8. The pre-registration of mediators

The mediator family — the list of candidate channels you will examine — should be pre-registered in the same way the moderator family for heterogeneity was (Chapter 10.3). This serves two purposes: it constrains the multiple-testing problem (each candidate channel is an additional test, contributing to the FWER across the mechanism family), and it forces you to think about the channel structure before the data tells you what looks promising.

Maya's PAP listed three candidate mechanisms:
1. Training intensity (compliance practices).
2. Portfolio reshuffling (lenders changing which neighborhoods they target).
3. Lender entry (new lenders attracted to examined states).

Her sequential-g analysis estimates the CDE for each, with Romano–Wolf adjustment across the three-test family. The Required item from her triage memo is satisfied by reporting all three, with the explicit caveat about sequential ignorability for each. If, post hoc, she identifies a fourth candidate channel (say, branch-network restructuring), she labels its analysis as exploratory and *does not* include it in the FWER family.

---

## 9. When mechanism analysis is the wrong question

A frank piece of advice. Many papers in empirical finance — and many of your future papers — will be stronger if they do *not* attempt a mechanism analysis at all. There are two reasons.

**Reason 1: the headline is the contribution.** If your paper's central contribution is showing *that* examinations reduce denial gaps, with a clean identification design that no other paper has shown, the *mechanism* question is a follow-up paper. Trying to estimate the mechanism in the same paper dilutes the focus, weakens the average rigor of each claim, and gives reviewers more things to attack. The discipline is: be willing to leave the mechanism question for another paper.

**Reason 2: the mechanism cannot be honestly identified.** If sequential-ignorability is implausible for every candidate channel, if no IV-for-mediator exists, if no design-based mechanism is available, and if heterogeneity-as-mechanism does not have a pre-treatment proxy — then any mechanism analysis you run will be statistical theater. **It is better to say "we cannot identify the mechanism with this design; we leave the channel question to future work" than to run a Baron–Kenny regression and pretend.**

The mature judgment is to know when to do neither. Many of the finance papers you most admire — by Gao and his coauthors, by your favorite empirical economists — make a strong identification claim about the *headline* and refuse to overreach on the *channel*. That refusal is not a limitation; it is a credibility marker.

---

## 10. The four classmates' mechanism sketches

A brief tour of how mechanism analysis looks in the other four projects.

**Sam (intraday momentum).** Sam's "mechanism" question is: why does momentum exist at all? The candidate channels are *underreaction to news* (limits to attention), *autocorrelated liquidity provision* (market-maker inventory), and *gradual information diffusion* (analyst slow-walk). He pre-registers all three and uses heterogeneity-as-mechanism: he shows momentum is stronger on news days (consistent with underreaction), stronger in low-liquidity periods (consistent with inventory), and stronger when analyst coverage is sparse (consistent with information diffusion). Each is a heterogeneity result whose interpretation is *the* mechanism evidence. He does not attempt sequential-g.

**Devon (DeFi adoption).** Devon's mechanism question is: why does a regulatory event in one jurisdiction affect adoption on a chain that is technically global? The candidate channels are *user-base relocation* (US users moving to non-US chains), *liquidity reshuffling* (TVL flowing between chains), and *developer migration* (smart-contract deployment patterns). Heterogeneity-as-mechanism here would use pre-event chain characteristics (US-user share, developer concentration). Sequential-g would require post-treatment intermediates that are themselves problematic.

**Priya (climate-shock insurance).** Priya's mechanism question is: why does a wildfire raise the next-year premium in a county? The candidate channels are *risk-revision* (insurers update their loss model), *reinsurance pass-through* (reinsurance prices rise, retail premia follow), and *capacity withdrawal* (some insurers exit, raising the average premium). She uses heterogeneity-as-mechanism by reinsurance-concentration and by insurer-stay-vs-exit. She also has a quasi-experimental moment: a 2025 reinsurance-rate change driven by an exogenous Bermuda tax policy that affected reinsurance prices but not local risk; this is an IV-for-mediator for the reinsurance channel.

**Leah (patent-language innovation).** Leah's mechanism question is: when an examiner's caseload increases, do they (a) reject more good patents, (b) accept more bad patents, or (c) both? She uses heterogeneity-as-mechanism by patent-quality-as-measured-by-citations: if caseload effects are concentrated among low-quality patents, the (b) channel dominates; if among high-quality, the (a) channel dominates.

The pattern: **heterogeneity-as-mechanism, with pre-treatment proxies for candidate channels, is the default. Sequential-g is the second-best. Baron–Kenny mediation regression is not in any of the five toolkits.**

---

## 11. The seam to Chapter 10.5

You have now answered, at the conference-feedback level, every form of the "what is the channel?" question. The next chapter — Chapter 10.5 — closes Week 10 by asking the other big external question: not "what is the channel?" but "would this replicate in a different setting?" External validity is a sibling concept to mechanism: a paper with a strong mechanism story can argue that the mechanism *transports* to other settings where the mechanism is present, even if the average effect varies. Without a mechanism story, external validity is much harder to argue.

Chapter 10.5 builds the transportability diagram that formalizes the external-validity argument, and ties it back to the heterogeneity (10.3) and mechanism (this chapter) analyses you have done.

---

## 12. Worked checklist before you leave this chapter

Before you start Chapter 10.5, you should have on disk:

1. A `revision/mediation-analysis.md` file listing your pre-registered candidate channels.
2. For each channel: (a) the heterogeneity-as-mechanism analysis (if a pre-treatment proxy exists), (b) the sequential-g analysis (if sequential ignorability is plausible), or (c) an explicit statement that the channel cannot be identified with this design.
3. A sensitivity analysis on the strongest mechanism claim (Oster δ; Cinelli–Hazlett).
4. A version of the manuscript that has either (i) a mechanism section with the language of §7, or (ii) an explicit statement that mechanism is left to future work — no Baron–Kenny mediation regression anywhere.
5. An update to the Chapter 10.1 triage memo showing each mediation-related Required item has been resolved.

You are now ready for the last chapter of Week 10.

---

[^abs2016]: Acharya, A., Blackwell, M., and Sen, M. (2016). "Explaining Causal Findings Without Bias: Detecting and Assessing Direct Effects." *American Political Science Review* 110(3):512–529.

[^bk1986]: Baron, R. M. and Kenny, D. A. (1986). "The moderator-mediator variable distinction in social psychological research: Conceptual, strategic, and statistical considerations." *Journal of Personality and Social Psychology* 51(6):1173–1182.

[^iktv2010]: Imai, K., Keele, L., Tingley, D., and Yamamoto, T. (2011). "Unpacking the black box of causality: Learning about causal mechanisms from experimental and observational studies." *American Political Science Review* 105(4):765–789.

[^ghkp2024]: Gao, L., Han, M., Kim, S. T., and Pan, X. (2024). "Overlapping institutional ownership, common ownership, and corporate strategy." *Journal of Corporate Finance* 84:102520.

---

**Chapter cross-references.** Built on Ch 2.3 (the bad-controls warning in the first regression chapter), Ch 7.5 (the threats-table where post-treatment selection threats live), Ch 8.2 (Oster δ sensitivity analysis used here for mediation robustness), Ch 10.1 (the triage memo whose "channel" comments became Required items), Ch 10.2 (Romano–Wolf adjustment across the mediator family), and Ch 10.3 (heterogeneity-as-mechanism, which is the first-line mechanism tool). Feeds Ch 10.5 (external validity, which depends on the mechanism story for transportability arguments) and Ch 11.2 (the response-letter section on mechanism).
