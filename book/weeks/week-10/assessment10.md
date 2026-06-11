# Week 10 Assessment — Robustness & Heterogeneity Memo

Week 9 graded whether your *result* survived a room. Week 10 grades whether your *appendix* survives a referee — whether the five-test pipeline you built in Lab 10 produces an appendix a careful reader trusts, and whether the six-page memo *about* the appendix shows you can see the difference between a claim your design supports and one it does not. This is the first of three Phase-3 graded artifacts, weighted **60 points**.

The standard from Mentor 10: **a heterogeneity-and-robustness section that scores well on the four referee signals — pre-registration, monotone pattern, adjusted inference shown alongside unadjusted, and mechanism consistent with the introduction — outscores one that runs more tests but defends none.** A memo that names a moderator as post-hoc and hedges its abstract earns more than one that pretends every moderator was theory-driven. Hold yourself to CONVENTIONS §4 and §5 — these are the floor.

Before submitting, read one finished example in the **capstone gallery** (`book/capstones/` — `[CHECK]` whether a Phase-3 example exists; if not, read the Week 8 fair-lending capstone's Appendix B and imagine it expanded with Lab-10's five tests). Read for the *seams*: the footnote naming a post-hoc moderator, the table showing unadjusted and adjusted p-values side by side, the paragraph conceding a limitation the design cannot resolve.

---

## How you submit

The memo is *one* deliverable from three sides: the prose argument, the appendix it cites, and the pipeline that rebuilds the appendix. You submit them as the `revision/` folder in the capstone repository plus the `appendix/` folder Lab 10 populated. The grader clones, types `make clean && make appendix`, verifies every SHA-256 against `appendix/manifest.json`, then opens `revision/memo10.pdf`. The repository *is* the submission; the appendix tables in the memo are rendered from the same `.tex` files the paper's appendix uses — never typed.

---

## The deliverable spec

### A six-page memo, PDF, AEA single-column

**Six pages including all tables and figures, single-column AEA LaTeX format**, written *about* your Lab-10 appendix. Six pages is a hard cap; padding to reach it is graded down, as is cramming a real argument into four. The skeleton is fixed, because the rubric reads it section by section.

**§1 — Triage carry-over (~½ page).** A compressed restatement of the Chapter 10.1 triage matrix. Three to five rows, one per test, each naming the conference comment (or threats-table row) that motivated it, the cost/value/threat assignment, and the verdict. The reader should see at a glance why each test is in the appendix.

**§2 — Romano-Wolf adjusted heterogeneity (~1 page).** One paragraph plus one table. The paragraph names the family of cuts, states which were pre-registered vs. post-hoc, and names the bootstrap with $B$ and seed. The table (`\input{appendix/tab_rw.tex}`) shows point estimate, raw p, Bonferroni-adjusted p, and Romano-Wolf-adjusted p. The headline reports the *adjusted* significance, with the discreteness-floor caveat if few treated clusters.

**§3 — Pre-registered CATE with honest inference (~1½ pages).** One paragraph naming the pre-registered features and citing `appendix/cate_features.json` by git hash; one paragraph on the Athey-Wager forest with trees, leaf size, and propensity-trim diagnostic; the histogram (`fig_cate_hist.pdf`); the GATE-by-CATE-quintile table (`tab_cate.tex`); one interpretive paragraph naming the direction of variation and tying it to the moderators the introduction named. This is where the *causal-language discipline* row lives: "the policy reduced the gap by 3.1pp in the top quintile" is design-matched; "the policy *caused* a 3.1pp larger reduction *for* high-intensity counties" overclaims.

**§4 — Mechanism audit via CDE (~1 page).** One paragraph stating the candidate mediator, the sequential-ignorability assumption, and the named confounder that would have to be present for the CDE to be biased (named by name, not abstract). The table (`tab_cde.tex`) shows total effect, biased Baron-Kenny "direct" coefficient, CDE, and implied indirect-effect share. The headline reports the CDE and the *gap* to the BK estimate, explaining the gap (post-treatment collider bias from Ch 10.4) in one sentence.

**§5 — Transportability bound (~½ page).** One paragraph naming the in-sample population, the target population, and the effect-modifier-exchangeability assumption. The table (`tab_transport.tex`) shows in-sample ATT, transported ATE, and the ESS diagnostic. The headline hedges: "under the assumption that the CATE function is the same...given the eight pre-registered covariates, the estimate transports to..."

**§6 — The honest sentence (~½ page).** The closer. ~200 words naming the *one* limitation the full battery does not address — the assumption that, if violated, would invalidate the entire story. Maya's: "the entire battery rests on the staggered-DiD parallel-trends assumption; if adopting states were on a steeper pre-treatment trend, every test in this appendix would still report the same numbers and the headline would still be wrong." That paragraph is what separates a memo that defends the work from a memo that flatters it.

### Three rules that apply to the whole memo

1. **Every number is `\input`ed from the appendix `.tex` files. No number is typed.** A grader running `make clean && make appendix && pdflatex revision/memo10.tex` sees numbers matching the manifest. Typed-vs-manifest mismatches cap the reproducibility row at Missing.

2. **Causal-language discipline applies to every verb.** Headline sentences in §§2-5 use design-matched verbs: *estimates / reports / is associated with / predicts* for observational, *identifies / measures / causes* only where the design supports it. Three or more verb-design mismatches cap the causal-language row at Developing.

3. **The 4-signal audit is visible in the memo's structure.** §2 covers signal 3 (adjusted inference visible); §3 covers signals 1 and 2 (pre-registration; monotone pattern); §4 covers signal 4 (mechanism consistency). A grader running the checklist should find each one addressed.

---

## The analytic rubric (100 points, scaled to 60 for the gradebook)

The rubric is scored out of 100 points across seven rows, then **multiplied by 0.60** to produce the gradebook score. The 100-point scale is what the grader uses on the rubric sheet; the 60-point scale is what appears on the transcript. The rows are weighted by what the Mentor 10 deck named as the four signals plus the reproducibility floor plus the causal-language discipline that runs through every row.

| Criterion | Excellent | Proficient (~75%) | Developing (~50%) | Missing (0-25%) | Pts |
|---|---|---|---|---|---|
| **Triage carry-over** (§1; Ch 10.1). Compressed table; each test traceable to a conference comment or threats-table row; cost/value/threat verdicts visible; ≤ ½ page. | Table present, one slip: one verdict not obviously tied to a comment, or the threat axis missing from one row. | Two or more verdicts feel post-hoc-justified, or §1 runs to 1+ page. | No triage table, OR no traceability to comments or threats. | **10** |
| **Romano-Wolf adjusted heterogeneity** (§2; Ch 10.2; Lab 10 §2). Unadjusted and Romano-Wolf adjusted columns side-by-side; Bonferroni column also shown; bootstrap named with $B$ and seed; discreteness-floor footnote if few treated clusters; headline reports adjusted, not raw. | All columns present; one slip: Bonferroni column omitted (headline still adjusted), or discreteness-floor footnote missing for a 3-6 cluster bootstrap. | Adjusted p-values present but headline reports raw, OR bootstrap procedure unnamed, OR seed missing from caption. | No multiple-testing adjustment, OR adjusted column shown but interpreted as raw. | **15** |
| **Pre-registered CATE with honest inference** (§3; Ch 10.3; Lab 10 §3; Mentor 10 signals 1 & 2). Feature list committed to `cate_features.json` *before* the forest fit with git hash quoted; histogram and GATE-by-quintile both shown; propensity-trim diagnostic reported; interpretive paragraph names the direction and ties it to the introduction's moderators; pattern monotone (or non-monotone honestly flagged). | Feature list committed and quoted; one slip: propensity-trim diagnostic omitted, or GATE shown without monotonicity comment. | Forest fit but feature list not committed before the fit (no git hash), OR pattern non-monotone and memo claims monotone without acknowledging it. | No causal forest, OR feature list assembled post-hoc (commit timestamp after first fit), OR interpretation ignores the actual pattern. | **20** |
| **Controlled direct effect mediation audit** (§4; Ch 10.4; Lab 10 §4; Mentor 10 signal 4). CDE and Baron-Kenny shown side-by-side; sequential-ignorability stated explicitly; candidate omitted confounder named (specific variable, not "potential confounders"); BK-CDE gap explained in one sentence; mechanism matches introduction's story (or mismatch named). | CDE and BK shown; sequential-ignorability stated; one slip: confounder generic ("economic conditions") rather than specific, or BK-CDE gap reported without source explanation. | CDE shown but BK comparison missing, OR sequential-ignorability not stated. | Baron-Kenny run as if clean mediation (no CDE), OR mediator on RHS without acknowledging post-treatment selection bias. | **15** |
| **Transportability bound** (§5; Lab 10 §6). In-sample and target populations both named; effect-modifier-exchangeability assumption stated; transported ATE and in-sample ATT both reported; ESS visible; headline hedges with the assumption; §6 references which feature of the target population the assumption is most likely to fail on. | Transported estimate present; one slip: ESS not in table footnote, or headline drops the conditional clause. | Reweighting computed but assumption not stated, OR ESS below 30% and transported estimate treated as trustworthy. | No transportability analysis, OR a generalization claim made without any reweighting. | **10** |
| **Causal-language discipline** (Mentor 10; CONVENTIONS §4). Every headline sentence in §§2-5 uses a design-matched verb: *estimates / reports / is associated with / predicts* for observational, *identifies / measures / causes* only where supported; §6 names a real limitation, not generic future-work. | Mostly disciplined; one or two soft slips conceded elsewhere; §6 names a real limitation. | Three or more verb-design mismatches in headlines, OR §6 generic. | Headline sentences claim causation from observational variation without acknowledgment, OR no §6. | **15** |
| **Reproducibility — `make clean && make appendix`** (Lab 10 §7; CONVENTIONS §5). On a fresh clone, appendix rebuilds byte-for-byte; `manifest.json` matches; every memo number `\input`ed; SEED fixed/named/threaded; env pinned via `environment.yml` + `environment.lock.yml`; no secret anywhere. | Rebuilds and pins; one slip: one number typed in a textual aside (not a table), OR SEED not threaded through one stochastic step. | A re-run fails without a hand-tweak: `make appendix` errors on a `[CHECK]` step, OR one appendix `.tex` is stale. | `make clean && make appendix` does not reproduce, OR a hardcoded API key (this alone caps at Missing). | **15** |

**Total: 100 points, scaled to 60.** Row weights (10 + 15 + 20 + 15 + 10 + 15 + 15 = 100) reflect the Mentor 10 priorities. The CATE row is heaviest (20) because pre-registered CATE with honest inference covers two of the four heterogeneity signals at once. The four 15-point rows are the pillars of the submission-grade memo: adjusted inference, mechanism audited, verbs matched to design, pipeline rebuilds. Triage and transportability (10 each) are weighted by length, not importance.

---

## Instructor answer key / model-answer sketch

This section is the grader's reference, not part of the student submission. It uses Maya's fair-lending capstone as the worked case; students on other designs (Devon's crypto, Priya's climate, Sam's momentum, Leah's patents) map the structure across.

**§1 (model).** Five-row table whose verdict column reads *Required · Required · Required · Welcome · Decline*. Each Required row points to a Lab-9 panelist question (logged in `bundle/ledger.csv`) or a threats-table row. The Welcome row gets one sentence on why it was completed (marginal-value-per-hour high). The Decline row gets one sentence on why declined. The Excellent version closes by mapping the Required column one-to-one to §§2-5.

**§2 (model).** Five-cut family: examination-intensity-high, examination-intensity-medium, minority-share-top-tercile, MSA, CRA-overlap. Headline (magnitudes hedged): **"After Romano-Wolf adjustment ($B = 999$ wild-cluster bootstrap, seed 42, six treated state clusters), the high-intensity and minority-share-top-tercile cuts survive FWER control at the 5% level; the other three do not. The discreteness floor is $1/64 \approx 0.016$, which the surviving adjusted p-values respect."** Four cuts are in the PAP; CRA-overlap is footnoted as post-hoc (added in response to Lab-9 panelist). The Excellent version shows Bonferroni alongside Romano-Wolf and notes Romano-Wolf rejects one more hypothesis.

**§3 (model).** Opening paragraph quotes the git hash of `cate_features.json` from before the first forest fit and lists the eight pre-registered features. Methods paragraph names EconML `CausalForestDML` (4000 trees, leaf size 30, honest splitting, BLB inference), propensity-trim share 3.4%. Histogram shows right-skewed $\hat\tau(\mathbf{x})$ with ATT marked. GATE-by-quintile table shows monotone gradient; interpretive paragraph names the direction ("steepest in counties with high pre-registered examination intensity and high minority share, matching the mechanism in §1.3 of the main paper") and monotonicity test ($p < 0.01$ one-sided). The Excellent version ties signal 2 (monotone) to signal 4 (mechanism consistent).

**§4 (model).** Candidate channel: *compliance-training intensity*. Sequential-ignorability stated. Named confounder: *changes in county-level FHA-loan share post-2015* (specific). Table: total $-1.5$pp; BK "direct" $-0.6$pp; CDE $-1.1$pp; implied indirect share 27% (CDE) vs. 60% (BK). Headline: **"Baron-Kenny would overstate the through-mediator channel by more than a factor of two; the CDE implies compliance-training accounts for about 27% of the total effect."** Excellent version names what the residual 73% might be — examination intimidation, portfolio reshuffling, regulator attention.

**§5 (model).** In-sample: counties in six adopting states, 2015-2022. Target: all U.S. counties. Effect-modifier-exchangeability stated. Reweighted ATE moves from $-1.4$pp to $-1.0$pp; ESS 71%. Headline: **"Under effect-modifier-exchangeability, the in-sample ATT of $-1.4$pp reweights to $-1.0$pp at the all-U.S.-county target; the ~30% attenuation is driven by lower-density adoption regions where examination intensity is lighter."** §6 notes the most likely failure mode: unobserved political-economy variation between adopting and non-adopting states.

**§6 (model).** Maya's: **"Every test in this appendix takes parallel trends as given. If adopting states were on a steeper pre-treatment trend toward narrowing denial gaps — because they were politically primed to address fair lending — then Romano-Wolf, the CATE, the CDE, and the transported ATE would all report the same numbers and the headline would still be wrong. The pre-test rejects no pre-trend at conventional significance, but a low-power pre-test cannot rule out a moderate violation. This is the single threat no test in the appendix addresses, and a referee who pressed it would press the most important point left in the paper."**

### Common failure modes

- **Post-hoc CATE feature list.** Student fits the forest first, then writes `cate_features.json`. Git log shows the commit is after the first `cate.py` run. Caught at the CATE row.
- **Baron-Kenny without naming the bias.** Coefficient on $D$ in $Y \sim D + M$ interpreted as a direct effect. Caps the mediation row at Missing — Ch 10.4's textbook error.
- **Transportability claim without reweighting.** "Likely generalizes" written without computation. Caps the transportability row at Missing.
- **Causal-language verb creep.** "Reduced" (defensible) → "drove" (overclaims) → "caused differential effects." Three or more = Developing; six or more = Missing.
- **§6 says "future work would help."** Generic future-work caps the causal-language row at Developing. The rubric reads §6 looking for a *named* limitation.

The grader's last instruction: read §6 *first*. The honest sentence is the cleanest signal of whether the student has understood the discipline.
