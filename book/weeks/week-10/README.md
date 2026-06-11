# Week 10 — Triage, Robustness at Submission Standard, and Heterogeneity

You walked out of the conference last Saturday with a notebook full of comments
and a paper that almost-but-not-quite holds together. The feedback ledger from
Chapter 9.5 is on your desk; the discussant's central worry is on the back of
your hand; your advisor's "Oster delta?" scrawl is on the program. Phase 3 of
the NextGen 12-week program begins now, and you have four weeks to turn the
conference paper into a *submission*. **Week 10 is the first of those four
weeks**, and it is the most important: by Friday, every Required item from
your triage memo should have an analytic plan, every modern multiple-testing
discipline should be in place across your families of tests, every heterogeneity
claim should be pre-registered and defensible, every mechanism story should
avoid the bad-controls trap, and the external-validity paragraph that will
appear in the manuscript should already be drafted. See
[`../../TOC.md`](../../TOC.md) for where this fits in the full arc.

The reveal-the-trick of this week: **conference feedback is not noise to ignore
or scripture to obey — it is a triage problem.** Every chapter in Week 10 is
the operationalization of one row or cluster of rows from the triage memo you
build in Chapter 10.1. By the end of the week the memo is no longer a list of
forty-seven comments; it is a contract that drives Weeks 11 and 12.

## Chapters

1. [Ch 10.1 — Triaging Conference Feedback: the Cost / Value / Threat-to-Identification 3×3 and the "Required vs. Welcome vs. Decline" Memo](ch101-triaging-conference-feedback-cost-value-threat-identification-3x3.md) (the framework that decides which comments deserve which response)
2. [Ch 10.2 — Multiple-Testing Across Families: Bonferroni, Holm, BH-FDR, and Romano-Wolf Step-Down — When Each Is the Right Tool](ch102-multiple-testing-bonferroni-holm-bh-fdr-romano-wolf.md) (the decision tree for FWER vs. FDR control, with code for each procedure)
3. [Ch 10.3 — Heterogeneous Treatment Effects and CATE: From Subgroup Regressions to Causal Forests, with the Pre-Registration Discipline That Keeps It Honest](ch103-heterogeneous-treatment-effects-cate-causal-forests-pre-registration.md) (subgroup → interaction → causal forest, ranked by power and discipline)
4. [Ch 10.4 — Mechanism Analysis Without Bad Controls: Mediation Done Right, the Acharya-Blackwell-Sen Critique, and Sequential-Ignorability as a Last Resort](ch104-mechanism-analysis-without-bad-controls-mediation-acharya-blackwell-sen.md) (why Baron–Kenny mediation is broken, and what to do instead)
5. [Ch 10.5 — External Validity: Sample-to-Population, the Transportability Diagram, and the "Would This Replicate in 2030?" Stress Test](ch105-external-validity-transportability-would-this-replicate-2030.md) (the diagram, the re-weighting estimator, the honest paragraph)

## Theme

**Phase 3 Week 1 — Triage, Robustness at Submission Standard, and Heterogeneity.**
You are no longer estimating a model; you are *defending* one. The work of
Week 10 is the work of converting the loose, sympathetic feedback from a
conference room into the rigorous, adversarial-grade response a journal
referee will demand. Every chapter is an answer to a class of conference
comments: 10.1 is the meta-tool that decides which comments require an
answer; 10.2 is the inferential discipline you owe the moment your tables
have more than five rows of p-values; 10.3 turns "who is affected?" into a
pre-registered analysis instead of a fishing expedition; 10.4 keeps the
"what is the mechanism?" question from sliding into the bad-controls trap
that has invalidated a generation of mediation papers; 10.5 closes the week
by answering the question every audience asks and most papers duck: "would
this replicate?"

The seam Week 10 protects is the one between *believing your result* and
*being able to make a skeptic believe it*. Chapter 9 was about the live
defense in front of a room; Chapter 10 is about the written defense in front
of a referee — and the referee is colder, more skeptical, and reads
asynchronously without the benefit of your charm. Every move in this week
is designed to survive that audience.

## Notebooks (`../../../notebooks/week-10/`)

- **nb10.1** Triage CSV → Required/Welcome/Decline memo generator (the script from Ch 10.1 §5, applied to the conference feedback ledger from Ch 9.5)
- **nb10.2** Multiple-testing toolkit (Bonferroni, Holm, BH-FDR, Romano–Wolf step-down with cluster bootstrap; the decision tree of Ch 10.2 §7 in code form)
- **nb10.3** Heterogeneity estimation (subgroup ATTs, interaction regression with CI band, causal-forest CATE histogram + BLP test + feature-importance plot)
- **nb10.4** Sequential-g controlled-direct-effect estimator with cluster bootstrap (Ch 10.4 §4), and the bad-controls simulation (§1)
- **nb10.5** Transport re-weighting from source to target sub-population (Ch 10.5 §4), with positivity diagnostic and external-validity-paragraph template

All notebooks pinned to the Week 1 environment (python 3.11, pandas 2.2+,
statsmodels, pyfixest, scikit-learn, econml). All seeded with
`rng = np.random.default_rng(42)` for reproducibility. All run headless under
`matplotlib.use("Agg")`. No deprecated pandas. No hard-coded secrets.

## Problem sets (model exemplars in [Appendix E](../../appendices/E-solutions-manual/))

- **PS 10.1** Triage on your own conference ledger: produce a versioned triage-memo-YYYY-MM-DD.md with at least three Required, three Welcome, and three Decline items; defend each cell assignment in a one-sentence comment.
- **PS 10.2** Multiple-testing audit of your draft paper: count every test with a p-value, group into families, compute Bonferroni / Holm / BH-FDR / Romano–Wolf adjusted p-values for each family, and rewrite the headline sentences that change verdict under adjustment.
- **PS 10.3** Heterogeneity analysis on your paper's pre-registered moderator family: subgroup regression headline + causal-forest exploration + BLP test + a 200-word interpretation paragraph that respects the multiple-testing discipline.
- **PS 10.4** Mechanism plan for your paper: pre-register the candidate channels; choose heterogeneity-as-mechanism vs. sequential-g vs. "no mechanism analysis" with a one-paragraph defense of the choice for each candidate.
- **PS 10.5** External-validity paragraph for your paper: draft the four-move paragraph of Ch 10.5 §5, with the transport re-weighting estimate, the positivity diagnostic, and the mechanism-grounded extrapolation predictions.

## Lab, mentor, assessment

- **Lab 10 — Revision Week One** *(four-half-day sprints, one per chapter)*: convert at least three Required triage items into committed pull-requests against your manuscript repo, each with a reproducible notebook output, an updated table or figure, and a one-paragraph diff in the response-letter draft.
- **Mentor Session 10 — "How I revise a paper between conference and submission"** *(Prof. Gao, drawing on the revision arcs of Gao, Han, Kim & Pan 2024 JCF and Elnahas, Gao, Hossain & Kim 2024 JFQA — both of which went through multiple R&Rs with substantial heterogeneity and mechanism revisions)*
- **Week 10 Assessment + Rubric** — graded on: (a) the triage memo (clarity, defensibility, version control), (b) the multiple-testing audit (completeness, correctness), (c) the heterogeneity analysis (pre-registration evidence, multiple-testing discipline, BLP test if causal forest used), (d) the mechanism plan (avoidance of bad-controls, defense of sequential-ignorability if invoked), and (e) the external-validity paragraph (transport re-weighting, positivity diagnostic, institutional-drift acknowledgment).

## Cross-references

Built on Week 7 (Ch 7.3 pre-analysis plan, Ch 7.5 identification memo), Week 8
(Ch 8.1 specification curve as the disclosure-of-forks tool, Ch 8.2 robustness
battery that the Required items extend, Ch 8.3 paper structure that the
revisions integrate into), and Week 9 (Ch 9.5 feedback ledger that is the raw
input to triage).

Feeds Week 11 (the manuscript-integration week: Ch 11.1 introduction revision,
Ch 11.2 response letter that summarizes Week 10's deliverables, Ch 11.3 cover
letter, Ch 11.4 final replication packet, Ch 11.5 submission) and Week 12 (the
capstone defense, in which the triage discipline of Week 10 is tested against
a new audience).

## Where this leads

Week 10's outputs are *artifacts*: a triage memo, a multiple-testing-adjusted
table, a pre-registered heterogeneity analysis, a mechanism plan, an
external-validity paragraph. Week 11 turns those artifacts into *manuscript
sections*. Week 12 defends the integrated manuscript to a real or simulated
review committee. By the end of Phase 3, you have a paper your future self —
in 2030, reading it again — will not be embarrassed to have written.

The triage memo from Chapter 10.1 is the contract for all of this. Re-render
it at the start of each week, commit the version, and let the memo's table of
contents dictate the manuscript's table of contents. That is what professional
revision looks like.
