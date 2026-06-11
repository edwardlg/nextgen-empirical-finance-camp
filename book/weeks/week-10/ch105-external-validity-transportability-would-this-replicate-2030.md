# Ch 10.5 — External Validity: Sample-to-Population, the Transportability Diagram, and the "Would This Replicate in 2030?" Stress Test

You have an internally-valid estimate. The Callaway–Sant'Anna ATT survived the wild-cluster bootstrap, the placebo battery, the multiple-testing adjustment, the heterogeneity analysis, and at least one defensible mechanism story. The number is real *in the data you have*. The conference comment that has been hovering over every revision week since Chapter 10.1, and that the discussant in Maya's session phrased with characteristic bluntness — *"Would this replicate in 2030?"* — is not a comment about internal validity. It is a comment about **external validity**: whether the effect you measured in *this* sample, in *this* time period, in *this* institutional setting, would persist in a different population, different period, or different setting. **A paper that ducks the external-validity question gets a referee report that asks it.** A paper that confronts the question — even to argue it has *limited* external validity — earns the trust that lets the headline travel.

The result this chapter turns on, stated in one sentence so the rest is the work: **external validity is identification all over again — different threats, different remedies, same discipline of stating an assumption and then writing what you would see if it broke.** The internal-validity question of Chapters 4–8 was "given my data, did the treatment cause the outcome in my sample?"; the external-validity question is "would the same treatment cause the same outcome in a *different* sample?", and answering it requires a structural argument about which features of *your* setting carry the causal effect and which were incidental. The vocabulary for that argument is the **transportability diagram** (Pearl & Bareinboim 2014; Bareinboim & Pearl 2016) — a DAG-like diagram that names which variables differ between your sample and the target population and asks whether the effect estimand survives the difference.[^pb2014][^bp2016] We will build that diagram in §3, learn to read it in §4, and use it to interrogate Maya's headline against the 2030 question in §5.

Before that, two preliminaries. §1 unpacks why external validity is logically separate from internal validity (and why "my N is huge" is not an answer). §2 lays out the four canonical threats to external validity — sample-population mismatch, period non-stationarity, institutional drift, and treatment-effect heterogeneity that does not transport — and how each maps to a node on the diagram. Then we are ready for the diagram itself.

---

## 1. Why external validity is *not* solved by a large sample

A common student instinct, when asked the external-validity question, is to point at the sample size: "$N = 47{,}000$ county-years across all fifty states from 2008–2024; this *is* the population." The instinct is wrong, and it is wrong in a precise way worth naming. **External validity is not about *sampling* error; it is about *transport* error.** With $N = 47{,}000$, sampling error around the average effect for *this* population is small (the standard error of the ATT is, say, 0.55 percentage points). With $N$ a billion, sampling error would be smaller still. But the *target population* about which a policy reader cares — the population of county-years in 2030, in a future political-economic regime, with future racial demographics, future technology, future regulatory equilibrium — is not the population from which Maya sampled. **No amount of sampling-error reduction in the source population can address the gap between the source and target populations.** That gap is the external-validity problem, and it is structural, not statistical.

This is sometimes called the "Lalonde gap" after Lalonde (1986), who famously showed that experimental and observational evaluations of the same training program gave very different answers — and the source of the gap was not sample size but population differences.[^lalonde1986] Manski (1990) formalized the partial-identification version of the problem, asking what we can learn about average effects in target populations when only source-population data is available; the answer is that we can bound them, sometimes tightly, sometimes very loosely, depending on what we assume about the differences.[^manski1990]

So when the conference room asks "would this replicate in 2030?", the wrong answer is "yes, my standard error is small." The right answer is some version of "*conditional on the assumption that [specific features of the 2026 setting] also hold in 2030, yes; if those features change in the following ways, the effect would be expected to change as follows.*" The next sections show you how to fill in those bracketed clauses.

---

## 2. The four threats to external validity

Just as internal validity has four canonical threats (omitted variable, reverse causality, measurement error, selection — Chapter 7.5), external validity has four canonical threats. They look superficially like the internal threats but operate differently: they are not threats to the *estimate* in the source sample; they are threats to the *transport* of the estimate to a target population.

### 2.1 Sample-population mismatch

The source sample is not representative of the target population. Maya's HMDA panel covers all U.S. counties from 2008–2024; her *target* (the policy question) might be "would this work in a new state that has not yet adopted, in 2030?". The relevant comparison population is "U.S. county-years circa 2030 in the not-yet-treated cohort"; the relevant source population is "U.S. county-years 2008–2024 in the treated cohort." These two populations differ in pre-treatment characteristics (demographics, lending market structure, regulatory baseline), and any effect heterogeneity along those characteristics implies the average effect in the target differs from the average effect in the source.

Diagnostic: compare the *distribution* of pre-treatment covariates in the source-treated sample to the distribution in the target population. If they look similar, sample-population mismatch is mild. If they differ markedly — say, the source-treated counties are urban and Southern while the target population is national — mismatch is severe.

### 2.2 Period non-stationarity

The treatment effect itself is a function of the *period*, not just of the population. Fair-lending examinations in 2010, in the wake of the financial crisis, might have had different effects than fair-lending examinations in 2025 (different baseline credit conditions) or 2030 (different demographic mix, different technology of lending decisions — automated systems, AI underwriting). The "2030" question is partly a period question: even if the population is identical, the treatment effect might differ because the world has moved.

Diagnostic: check whether the within-source treatment effect varies *across* the years your data covers. If the per-year ATT is stable from 2010 to 2024, period non-stationarity is mild. If the per-year ATT trends or shifts (say, it is large in 2010–2015 and shrinks toward zero in 2020–2024), period non-stationarity is severe and extrapolation to 2030 is reckless.

### 2.3 Institutional drift

The institutions that *mediate* the treatment effect change over time, in ways that may dampen or amplify the effect. Maya's examinations work through compliance practices, banker behavior, and the broader regulatory ecosystem (CRA evaluations, NGO monitoring, media attention). If by 2030 the regulatory ecosystem has shifted — for example, if a federal pre-emption decision has weakened state examination authority, or if automated underwriting has displaced loan-officer discretion as the locus of bias — the mediating institutions on which the examination effect operates may no longer exist in their current form, and the effect would not transport even if the population and period otherwise matched.

Diagnostic: list the institutions that are *load-bearing* for your mechanism story (from Chapter 10.4). For each, ask: is this institution likely to exist in 2030 in roughly its current form? If yes, drift is mild for that channel; if no, drift is severe.

### 2.4 Effect-heterogeneity that does not transport

This is the deepest threat, and the one that combines with the previous three. Even if the *average* effect in your source happens to equal the *average* effect in the target by coincidence, the *distribution* of effects across subgroups may not transport. If the source-target populations differ on the heterogeneity dimension you identified in Chapter 10.3 (say, the source is mostly moderate-intensity examinations and the target is mostly intense), the average effect in the target might differ from the source-average in a way that aligns with the heterogeneity.

Diagnostic: combine 2.1 and the Chapter 10.3 heterogeneity table. If the target-population distribution along your moderators differs from the source-population distribution, *and* if your moderators predict heterogeneity in effects, then the transported ATE will differ from the source ATT in a quantifiable way. We will see in §6 how to do this quantification.

---

## 3. The transportability diagram

The transportability diagram is the formal tool that organizes these threats. It is a DAG with one critical addition: a *selection node* $S$ that takes value $S = 1$ in the source population and $S = 0$ in the target population. Variables that are *invariant* across source and target appear in the diagram with no edge to $S$; variables that *differ* across source and target have a directed edge from $S$ (or are flagged as "selection-dependent"). The transportability question — whether the causal effect identified in the source transports to the target — reduces to a question about which paths from $D$ to $Y$ are *cut* by the selection-dependent variables. **A causal effect is transportable if every path from $D$ to $Y$ avoids selection-dependent variables; it is non-transportable otherwise.** (Pearl & Bareinboim 2014 formalize this with the s-do calculus; we will not need the full machinery.)

Maya's transportability diagram, in plain English:

- **Nodes:** $D$ = examination treatment; $Y$ = denial gap; $X$ = pre-treatment county-level covariates (population, income, demographics); $I$ = institutional ecosystem (CRA, NGO, federal pre-emption); $T$ = period (year); $S$ = source/target selector.
- **Edges within the causal model**: $X \to D$ (treatment selection responds to county characteristics); $X \to Y$ (county characteristics affect outcomes directly); $D \to Y$ (the causal effect of interest); $D \to I$ — *no*, $I$ is exogenous to $D$ in this design — let's correct: $I \to D$ (institutional context shapes examination adoption) and $I \to Y$ (institutional context affects outcomes through pathways other than examinations).
- **Selection edges:** $S \to X$? Probably — the source-2008–2024 population's demographics differ from the target-2030 population's. $S \to I$? Likely — the institutional ecosystem in 2030 may differ. $S \to T$? Yes — period is part of the source/target distinction.

```
   X <-- S
   /\    /\
  /  \  /
 v    vv
 D --> Y
  ^    ^
  |    |
  I <-- S
  ^
  |
  T
```

(Apologies for the ASCII; in the textbook this is rendered as a proper graph. The key features: $S$ has edges into $X$ and $I$, meaning these variables differ across source and target; $D \to Y$ is the effect we want to transport; and $X, I$ both have edges into $Y$ (direct effects) and into $D$ (treatment-selection effects).)

### What the diagram tells us

The effect of $D$ on $Y$ is *transportable* from source to target if the path $S \to X \to Y$ and $S \to I \to Y$ can be closed by conditioning on $X$ and $I$ — i.e., if we can re-weight or stratify the source data so that the $X$ and $I$ distributions match the target. **This is the principle behind post-stratification, sample re-weighting, and the synthetic-control logic of transport.** If we can match the target's distribution of $X$ and $I$ in the source, the causal effect transports. If we cannot — for example, if the target population has $I$ values that are *outside the support* of the source — transport fails and the effect cannot be honestly extrapolated.

The "outside the support" problem is the most common reason transportation fails. If by 2030 the institutional ecosystem includes features (say, AI underwriting at scale) that were absent in the 2008–2024 source, the source data has no observations at those $I$ values, and no amount of re-weighting can produce an estimate for them. The honest report is: "*the source data does not support extrapolation to settings where AI underwriting dominates*; if the target population has substantial AI-underwriting share, our estimate does not apply." This is a *strength* of the analysis, not a weakness: it tells the reader exactly where you cannot speak.

---

## 4. Operationalizing the diagram: re-weighting

The most common formal tool for transport is **inverse-probability re-weighting**. The idea is straightforward: if you can estimate, for each source observation, the probability that it would have come from the target population (given its covariates), you can re-weight the source by the inverse of that probability and compute the target-population ATE.

Concretely: stack the source and target on common covariates $\mathbf{X}$ and estimate a logistic regression of $S$ (= 1 if source, 0 if target) on $\mathbf{X}$. The fitted probability $\hat{\pi}(\mathbf{X}_i) = \Pr(S=1 \mid \mathbf{X}_i)$ is the source-membership probability. The transport weight for source observation $i$ is

$$ w_i = \frac{1 - \hat{\pi}(\mathbf{X}_i)}{\hat{\pi}(\mathbf{X}_i)}, $$

which up-weights source observations whose covariates resemble the target. The re-weighted ATT estimator is

$$ \widehat{\text{ATT}}_{\text{target}} = \frac{\sum_{i \in \text{source-treated}} w_i \cdot \hat{\tau}_i}{\sum_{i \in \text{source-treated}} w_i}, $$

where $\hat{\tau}_i$ is the per-unit treatment effect (from a causal forest, Chapter 10.3, or from a heterogeneity-by-strata estimator).

The catch: you need *target data on $\mathbf{X}$* to estimate the source-membership probability. If the target is "U.S. county-years in 2030" and 2030 has not yet happened, you need a *projected* distribution of $\mathbf{X}$ in 2030 — Census Bureau projections, BLS labor-force projections, your own demographic forecast. The transport-weighting estimate is only as good as the projection.

In practice, the move most papers make is more modest: instead of transporting to a hypothetical 2030 target, they transport to a *known but different* target — say, "states that have not yet adopted examination programs as of 2024." That target's $\mathbf{X}$ distribution is directly observable, so the re-weighting is clean, and the resulting estimate ("what would the effect be if these never-adopted states had adopted?") is policy-relevant and identifiable.

### Code: transport re-weighting

```python
# nb10.5 cell 1 — transport ATT re-weighting from source to a target sub-population.
# Source: states that adopted examinations 2010-2020. Target: states that
# have not yet adopted as of 2024 (the policy-relevant target).
import numpy as np
import pandas as pd
import statsmodels.api as sm
from econml.grf import CausalForest

# Build the source (treated states) and target (never-treated states) panels.
source = panel[panel["state"].isin(ADOPTING_STATES)].copy()
target = panel[panel["state"].isin(NEVER_ADOPTED_STATES)].copy()

# 1. Per-unit CATE in the source from a causal forest (Chapter 10.3).
X = ["log_pop", "median_inc", "pre_minority_share", "msa_share",
     "lender_concentration", "cra_density"]
forest = CausalForest(n_estimators=2000, honest=True, random_state=42)
forest.fit(X=source[X].to_numpy(),
           T=source["exam_resid"].to_numpy(),
           y=source["gap_resid"].to_numpy())
source["tau_hat"] = forest.predict(source[X].to_numpy())

# 2. Source-membership propensity using the stacked source + target.
stacked = pd.concat([source.assign(S=1), target.assign(S=0)], ignore_index=True)
prop = sm.Logit(stacked["S"], sm.add_constant(stacked[X])).fit(disp=0)
source["pi_hat"] = prop.predict(sm.add_constant(source[X]))

# 3. Transport weight.
source["w_transport"] = (1 - source["pi_hat"]) / source["pi_hat"]

# 4. Re-weighted ATT.
src_treated = source[source["exam"] == 1]
att_source = src_treated["tau_hat"].mean()
att_target = np.average(src_treated["tau_hat"], weights=src_treated["w_transport"])
print(f"Source-population ATT      = {att_source:+.3f} pp")
print(f"Transported-to-target ATT  = {att_target:+.3f} pp")
print(f"Implied delta              = {att_target - att_source:+.3f} pp")
```

The output to interpret: if `att_target` is materially different from `att_source`, the transport reveals that the effect we measured in the source is not the effect we would expect to see in the target — even before accounting for period effects or institutional drift. If the two are similar, the source's heterogeneity has been pulled into a target with similar covariate distribution and the average is preserved.

### When re-weighting fails: positivity violation

Re-weighting requires that every $\mathbf{X}$-value in the target also appears in the source — formally, that $\hat{\pi}(\mathbf{X})$ is bounded away from 1 for every target observation. If the target has support outside the source (the AI-underwriting example from §3), some $\hat{\pi}$ values approach 1 and the corresponding transport weights blow up: the re-weighted estimator is dominated by a handful of source observations and has enormous variance. The diagnostic is the **distribution of transport weights**: if a small number of weights exceed, say, 10 (meaning a single source observation is being asked to represent 10× its own weight in the target), you have a positivity problem and the transport estimate is not reliable.

The honest response to a positivity violation: *truncate*. Trim the source to observations within the target's covariate support (or trim the target to the source's), report the trimmed transport estimate, and explicitly note the region of the target population for which no estimate is available. This is the same discipline as the trimming in Chapter 4 propensity-score matching — and it is honest.

---

## 5. The "would this replicate in 2030?" stress test

We can now formally answer the discussant's question. The stress test has four steps, each with a deliverable.

**Step 1 — Specify the target.** Be precise. "2030" is not a target; "the distribution of U.S. county-years in 2030 under Census Bureau medium-fertility projection, with the institutional ecosystem assumed to be the 2024 status quo" is a target. Specifying the target forces you to confront which features you are assuming away.

**Step 2 — Diagnose the gap.** Compare the source covariate distribution to the target projection. For each covariate $X_k$, report the source mean, the target mean, and the standardized mean difference. Covariates with large differences are the candidate transport-breakers.

**Step 3 — Re-weight.** Run the transport-weighting from §4 to the projected target. Report `att_target` alongside `att_source` and the difference. Be honest about the propensity-model assumption (logistic with covariates $\mathbf{X}$) and the positivity diagnostic.

**Step 4 — Add institutional drift.** This is the step that requires substantive judgment, not statistics. List the load-bearing mediating institutions (from Chapter 10.4). For each, write a one-sentence prediction: "By 2030, this institution is expected to be [stable / weakened / strengthened] because [reason]. If weakened, we expect the effect to [shrink / sign-flip]; if strengthened, we expect the effect to [grow]." Aggregate these institutional predictions into a single sentence-level qualifier on the transport estimate.

The result of the stress test is a *paragraph* in the paper's external-validity section, not a number. Something like:

> *External validity.* Our estimates are most credible for the populations and periods directly sampled (U.S. county-years 2008–2024 in states that adopted fair-lending examinations during this window). Re-weighting to states that have not yet adopted as of 2024 produces an ATT of $-1.1$ pp (95% bootstrap CI $[-1.7, -0.5]$), modestly smaller than the source-sample ATT of $-1.4$ pp — consistent with the lower examination-intensity propensity of the never-adopted states. Extrapolation to 2030 requires assuming that (i) the institutional ecosystem of CRA evaluation and NGO monitoring is preserved in form, and (ii) the locus of lending discretion remains the loan officer rather than fully-automated underwriting. We do not attempt a numerical 2030 estimate because the second of these assumptions is in active flux; should the locus shift, our mechanism analysis (Section 5.3) suggests the magnitude of the examination effect would decline, with the sign preserved.

That paragraph is what an external-validity section looks like. Notice the four moves: (a) honest naming of the source population, (b) a *quantified* near-target transport estimate, (c) explicit non-extrapolation to a far-target with reasons, and (d) a sign-and-magnitude prediction grounded in the mechanism analysis. **This is the external-validity equivalent of the threats-and-responses table from Chapter 7.5.**

---

## 6. Sub-population effects and target-specific transports

A subtler form of the transport question is *not* "what is the effect in the average 2030 county?" but "what is the effect in *this specific* 2030 county?" — a policy-maker asking whether to adopt the program in, say, a specific not-yet-adopted state. The answer combines transport (re-weighting to the state's covariate distribution) and prediction (the causal-forest CATE at that state's covariate vector).

The pipeline is the same as §4 with one addition: instead of computing the mean of re-weighted CATEs across the target, you compute the *target-specific* mean for the state of interest. The output is a per-state predicted ATT with a bootstrap CI. For a policy-maker, this is the answer they want: "If your state adopts a fair-lending examination program of the intensity our heterogeneity analysis identified as effective, we project an effect of $-1.7$ pp (95% bootstrap CI $[-2.5, -0.9]$), based on transporting from comparable adopting states in the source sample."

This is the move that turns an academic finding into a usable policy tool. **It is also the move that requires the most assumption-tracking discipline.** Every step (the source ATT, the forest's CATE, the transport propensity, the institutional-drift assumption) compounds; the final state-specific estimate has wide effective confidence intervals once all assumptions are honest. Report the wide intervals.

---

## 7. Three classes of external-validity claims, ranked by strength

You now have the tools to make external-validity claims of three different strengths. Ordered from weakest-but-defensible to strongest-but-rare:

**Class 1 — Local internal validity.** "We estimate the effect for the population sampled. We do not claim transport." This is the modest claim. It is *always* defensible if your identification is good. It is also unsatisfying to policy readers, who want to know whether the result helps their decision.

**Class 2 — Bounded transport.** "We transport to a near-target with explicit re-weighting and report the transported estimate alongside the source estimate. We do not transport to far-targets where the institutional ecosystem is not stable." This is the modal modern claim, and it is what Maya's paragraph in §5 does. It is rigorous, it is honest about its boundaries, and it gives the reader a quantified near-target estimate.

**Class 3 — Structural transport.** "We estimate a structural model of the mechanism (e.g., a parameter-recoverable model of how examinations interact with lending behavior) and report counterfactual predictions for any target population whose primitives we can specify." This is the strongest claim and the rarest, because it requires a credible structural model that most reduced-form papers cannot offer. Industrial-organization and macro papers do this routinely; corporate-finance papers usually do not. It is a goal for an ambitious sequel paper, not the current revision.

The decision: aim for Class 2 in the current paper. Naming Class 1 in your external-validity section is *too modest* and looks like flinching; naming Class 3 is *too ambitious* and looks like overreach. Class 2, done with the rigor of §3–§5, is the right altitude.

---

## 8. External validity and the four classmates

A brief tour of how external-validity arguments differ across the five students' projects, showing how the same framework adapts to different designs.

**Sam (intraday momentum).** Sam's external-validity question is the hardest: "would this strategy persist out-of-sample?" The answer is essentially "no" for strategies that have been published (the arbitrage gets traded away); the transport question for Sam is therefore *backwards-looking* — "would this strategy have worked in earlier periods?" His source is 2015–2024 intraday data; his target is 2005–2014 intraday data; the transport re-weighting accounts for differences in market microstructure (HFT penetration, decimal-tick adoption). The mature answer: "the strategy works in our sample, the period-stationarity is moderate, and we expect post-publication decay; we report a five-year-rolling out-of-sample test in Appendix C."

**Devon (DeFi adoption).** Devon's external-validity question is "would this hold for a future chain not in our sample?" Transport here is *cross-chain*: re-weight from the chains he has to the characteristics of a hypothetical new chain. His honest paragraph would acknowledge that the institutional ecosystem of DeFi is itself unstable (the regulatory landscape is in active flux), making Class 2 transport credible only for chains and periods with regulatory characteristics similar to the source.

**Priya (climate-shock insurance).** Priya's external-validity question is sharp: "would the wildfire-premium relationship hold under future climate?" This is the *period-non-stationarity* threat at its most direct. Her source is 2010–2024 wildfire seasons; her target is 2030+ wildfire seasons, with frequencies projected to be substantially higher. She must make a Class 2 transport with explicit acknowledgement that the *frequency of wildfire shocks* in the target is outside the support of the source. The honest claim: "We estimate the conditional response *given* a wildfire shock; we do not estimate the increase in average premiums driven by the increased frequency of such shocks under 2030 climate projections."

**Leah (patent-language innovation).** Leah's external-validity question is "would this hold under AI-augmented patent examination?" Her source is human-examiner-period patents (pre-2025); her target is AI-augmented period (post-2025). Class 2 transport here is dangerous because the *mediating institution* (the human examiner) is in the process of being replaced. Her honest paragraph: "We estimate the human-examiner-period elasticity; the post-AI-period elasticity is, in our view, an open question that this paper does not attempt to answer."

The pattern: **each student names their target precisely, transports to the nearest credible target, and explicitly declines to extrapolate beyond the institutional support.**

---

## 9. The replication-in-2030 prediction registry (optional but powerful)

A final move that increasingly distinguishes the most rigorous papers from the merely careful ones: **pre-register your replication prediction.** When you submit the paper, lodge with the paper (in an appendix, or in a public predictions registry like the AEA Pre-Registry) a specific numerical prediction for what the effect would be in a future, identifiable population — say, the average ATT in the "not-yet-adopted" states if they adopt in 2026–2030. The prediction is testable: in 2030, someone can re-run your code on the new data and check whether your prediction was accurate.

This is a high-cost, high-credibility move. Most papers do not do it. The papers that do — and the increasing community of empirical economists who treat replication-prediction as a marker of intellectual integrity (Camerer et al. 2018 on social-science replication; Open Science Foundation projects) — are the ones whose external-validity sections carry the most weight.[^camerer2018] If you are confident in the transport, register the prediction. If you are not confident, *say so explicitly* — confidence is itself information for the reader. We do not require the registry move for Maya's paper, but we mention it because the discipline of imagining the registry sharpens the external-validity argument even when you do not submit it.

---

## 10. Where this week ends, where Week 11 begins

Week 10 has been the application of the conference-feedback triage from Chapter 10.1 to the four most-asked classes of comments: heterogeneity (Chapter 10.3), mechanism (10.4), multiple-testing across families (10.2), and external validity (this chapter). The Required items in your triage memo should now correspond, one-to-one, to sections of the revised paper that you have either added or substantially strengthened. The Welcome items should be addressed if time permits; the Decline items should be on record with a one-sentence reason.

The work of Week 11 is to *integrate* these revisions into the manuscript: the prose changes in the introduction (Chapter 11.1), the response-to-referee-style letter that summarizes the revisions (Chapter 11.2), the polished tables and figures (Chapter 11.3), the final replication packet (Chapter 11.4), and the cover letter for journal submission (Chapter 11.5). Each of these depends on the deliverables you produced in Week 10. You do not need to revisit the methods of Chapters 10.2–10.5; you do need to make sure their outputs appear in the manuscript with the right framing.

A final discipline note. The triage memo from Chapter 10.1 is the *living document* that has been driving Week 10. Update it once before closing the week: each Required item should be checked-off with a pointer to the paper-section where the response now lives; each Welcome item should be checked-off-or-deferred-with-reason; each Decline item should remain in its section with the reason intact. This is the artifact you will hand to your advisor, your co-author, and (in spirit) the editor of the journal you are about to submit to. *The paper is now what it should be at submission;* Week 11 makes it a manuscript.

---

## 11. The honest sentence about external validity, one more time

Before you leave this chapter, write the external-validity sentence for *your* paper. It should have the form: "*Our estimates apply directly to [precisely specified source population]. Re-weighting to [near target] yields [transported estimate]. We do not extrapolate to [far target] because [specific institutional or covariate-support reason]. Our mechanism analysis (§X) suggests that, conditional on [stability of mechanism], the sign of the effect would be preserved under [class of changes].*"

If you can write that sentence in two minutes, you understand external validity. If you cannot, you should re-read the chapter — specifically, the diagram in §3 and the paragraph template in §5 — until you can.

---

## 12. Connection back to the threats table

We close where Week 7 began. The identification memo from Chapter 7.5 had a four-column threats-and-responses table for internal validity. Week 10 has, in effect, built the *external-validity* counterpart: a table whose columns are the threat (population mismatch, period non-stationarity, institutional drift, non-transporting heterogeneity), the diagnostic (covariate-balance table, per-period ATT, mechanism-list, target-X-distribution), the response (re-weighting, period-restricted estimate, mechanism-conditional extrapolation, target-specific CATE), and the residual uncertainty (the institutional drift you cannot address, the support-violation you must trim around). This four-column external-validity table belongs in the appendix of your revised manuscript, parallel to the Chapter 7.5 internal-validity table. Together, they constitute the *complete* identification argument for the paper.

You now have everything Week 10 promised. The four chapters of Week 11 are about turning the work of Week 10 into a manuscript a journal will accept. Onwards.

---

[^pb2014]: Pearl, J. and Bareinboim, E. (2014). "External Validity: From Do-Calculus to Transportability Across Populations." *Statistical Science* 29(4):579–595.

[^bp2016]: Bareinboim, E. and Pearl, J. (2016). "Causal inference and the data-fusion problem." *Proceedings of the National Academy of Sciences* 113(27):7345–7352.

[^lalonde1986]: LaLonde, R. J. (1986). "Evaluating the Econometric Evaluations of Training Programs with Experimental Data." *American Economic Review* 76(4):604–620.

[^manski1990]: Manski, C. F. (1990). "Nonparametric Bounds on Treatment Effects." *American Economic Review* 80(2):319–323.

[^camerer2018]: Camerer, C. F. et al. (2018). "Evaluating the replicability of social science experiments in Nature and Science between 2010 and 2015." *Nature Human Behaviour* 2:637–644.

---

**Chapter cross-references.** Built on Ch 4 (the internal-validity foundation of causal-effect estimation), Ch 7.3 (pre-registration discipline transferred here to the prediction registry), Ch 7.5 (the threats-and-responses table whose external-validity counterpart this chapter builds), Ch 10.1 (the triage memo whose external-validity comments became Required items), Ch 10.3 (the per-unit CATE that feeds transport re-weighting), and Ch 10.4 (the mechanism story that informs institutional-drift predictions). Feeds Ch 11.1 (the introduction revision, which incorporates the external-validity paragraph), Ch 11.2 (the response letter that summarizes the external-validity work), and the Week 12 capstone defense.
