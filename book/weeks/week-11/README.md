# Week 11 — Manuscript Polish to Publication Standard

Phase 3 of the NextGen 12-week program is in week two. Last week (Week 10)
you converted forty-seven rows of conference feedback into a triage memo,
ran the multiple-testing audit, completed the pre-registered heterogeneity
analysis, drafted the mechanism plan, and wrote the external-validity
paragraph. The artifacts are sitting on your desk. **This week is about
turning those artifacts into a manuscript that survives a referee.**
See [`../../TOC.md`](../../TOC.md) for where this fits in the full arc.

The reveal-the-trick of this week: **every artifact in a publication-grade
manuscript — abstract, table, figure, introduction, literature review — is
engineered to credibilize the same contribution at a different level of
detail.** Week 11's five chapters teach the engineering, artifact by
artifact, with Maya's fair-lending paper carrying the worked example. By
Friday the abstract is 248 words, the headline table answers the
one-glance test, three publication-grade figures sit alongside the tables,
the introduction fits the five-paragraph structure in about 1,200 words,
and the literature review's three-strand braid earns the contribution
sentence. The manuscript is ready for the cover-letter and submission
stage of Week 12.

## Chapters

1. [Ch 11.1 — The 250-Word Abstract: the Five-Sentence Skeleton (Question, Setting, Design, Finding, Why-It-Matters) and the Common Failure Modes](ch111-the-250-word-abstract-the-five-sentence-skeleton.md) (the abstract is a contract with three different readers — the editor, the referee, and the future citer — and the five-sentence skeleton is how the contract takes shape)
2. [Ch 11.2 — Publication-Grade Tables: pyfixest etable to LaTeX, Stars Discipline, Panel Structure, and the One-Glance Test](ch112-publication-grade-tables-pyfixest-etable-stars-discipline-panel-structure.md) (the headline table is engineered for the one-glance test — coefficient, precision, sample, controls — and `pyfixest`'s `etable()` to LaTeX is the workhorse)
3. [Ch 11.3 — Publication-Grade Figures: the Event-Study Plot, the Specification-Curve Plot, the Heterogeneity Forest — and the Tufte Rules That Apply](ch113-publication-grade-figures-event-study-specification-curve-heterogeneity-forest.md) (the three figures every empirical-finance paper needs, with the Tufte data-ink discipline applied to each)
4. [Ch 11.4 — The Introduction Rewrite: the Five-Paragraph Structure (Hook / Question / What-We-Do / Findings / Contribution) and How to Diagnose a Sick Intro](ch114-the-introduction-rewrite-five-paragraph-structure-and-how-to-diagnose-a-sick-intro.md) (five paragraphs, one job each — and the six diagnostic pathologies that name what is wrong with the intro you have)
5. [Ch 11.5 — The Expanded Literature Review: from a Bullet List to a Three-Strand Argument that Earns Your Contribution Sentence](ch115-the-expanded-literature-review-from-bullet-list-to-three-strand-argument.md) (the three-strand braid: each strand traces one literature into the gap your paper fills, and the three strands together make your paper inevitable)

## Theme

**Phase 3 Weeks 2–3 — Manuscript Polish to Publication Standard.** Week 10
was about the analytic content of the response to conference feedback;
Week 11 is about the *presentation* of that content in the manuscript
itself. The discipline of presentation is not decorative; it is the
machinery through which the analytic content reaches the referee. A clean
table is the difference between a finding that gets read and a finding
that gets skimmed past. A five-sentence abstract is the difference between
desk-rejection and assignment for review. A three-strand literature
review is the difference between a contribution claim that is asserted
and one that is earned.

The seam Week 11 protects is the one between *having a defensible result*
and *being able to present a defensible result to an asynchronous referee*.
Every move in this week is designed to remove friction from the referee's
reading experience: tables that pass the one-glance test, figures whose
captions are redundancy checks rather than load-bearing prose,
introductions that funnel from broad context to specific contribution and
back to broader literature, literature reviews that argue rather than
enumerate. The work is prose engineering. It is the part of writing
empirical economics that the methods classes do not teach but that
determines whether the empirical work is published.

## Notebooks (`../../../notebooks/week-11/`)

- **nb11.1** `abstract_audit()` script — auto-flags the four abstract failure modes (Disappearing Finding, Method-Heavy, Literature-Review Opening, Diffuse Conclusion), with Maya's February-draft and revised-draft as test cases
- **nb11.2** Publication-grade table production with `pyfixest`'s `etable()` to LaTeX — including the panel-table stitching helper, the balance-table function, and the five-item commit checklist as a script
- **nb11.3** Three publication-grade figures (event-study, specification-curve, heterogeneity-forest) for Maya's project, with the styling block adapted for the Tufte data-ink discipline; vector-PDF output at the correct display size
- **nb11.4** `intro_audit()` script — auto-flags the six introduction pathologies (Wandering Funnel, Methodological Detour, Diffuse Hook, Findings-Free Findings, Question Paragraph Conscripted, Contribution Inflation), with worked examples
- **nb11.5** Literature-spreadsheet-to-section workflow — CSV template, the strand-and-move grouping function, the prose-conversion checklist; runs the §11 commit checklist programmatically

All notebooks pinned to the Week 1 environment (python 3.11, pandas 2.2+,
`pyfixest`, `matplotlib`, statsmodels). All seeded with
`rng = np.random.default_rng(42)`. All run headless under
`matplotlib.use("Agg")`. Each notebook produces output that is committable
directly to a manuscript repository.

## Problem sets (model exemplars in [Appendix E](../../appendices/E-solutions-manual/))

- **PS 11.1** Rewrite your own abstract using the five-sentence skeleton. Run `abstract_audit()` on your February draft and on your revised version; produce both, with a one-paragraph diagnostic comparing them.
- **PS 11.2** Produce your manuscript's headline Table 2 to publication standard using `pyfixest`'s `etable()` to LaTeX. Run the five-item commit checklist. Include the FE indicator block, the cluster count, and the notes block.
- **PS 11.3** Produce three publication-grade figures for your paper: the event-study (or analogue), the specification curve, the heterogeneity forest (or analogue). Each figure must pass the six-item commit checklist of Ch 11.3 §13.
- **PS 11.4** Rewrite your introduction using the five-paragraph structure. Run `intro_audit()` on your February draft and your revised version; produce both, with a one-paragraph diagnostic comparing them.
- **PS 11.5** Convert your literature-review draft into a three-strand braid. Produce the literature spreadsheet (CSV), the strand-and-move outline, and the prose version. Run the six-item commit checklist of Ch 11.5 §11.

## Lab, mentor, assessment

- **Lab 11 — Revision Week Two** *(five half-day sprints, one per chapter)*: convert your Week 10 analytic artifacts (triage memo, multiple-testing audit, heterogeneity analysis, mechanism plan, external-validity paragraph) into publication-grade manuscript sections. By Friday: abstract committed, three tables committed, three figures committed, introduction committed, literature review committed, response-letter draft updated.
- **Mentor Session 11 — "How an abstract gets rewritten between submission and acceptance"** *(Prof. Gao, drawing on the abstract-revision trajectories of Gao, Han, Kim, and Pan (2024) JCF, Elnahas, Gao, Hossain, and Kim (2024) JFQA, and the Rainbow-of-Credits municipal-borrowing paper targeting JF — each of which went through three to five abstract revisions across the review process)*
- **Week 11 Assessment + Rubric** — graded on: (a) the abstract (five-sentence skeleton, word count, no failure modes), (b) the headline table (one-glance test, stars discipline, FE block, cluster count, caption length), (c) the figures (Tufte discipline, axis labels with units, reference lines, file format), (d) the introduction (five-paragraph structure, word count target, no superlatives, contribution-paragraph alignment with literature review's three strands), (e) the literature review (three-strand braid, intellectual moves within each strand, synthesis closer, cross-references to Sections 3 and 6 of the manuscript)

## Cross-references

Built on Week 7 (Ch 7.3 pre-analysis plan, Ch 7.5 identification memo —
the assumption named in the abstract's Sentence 3 is the assumption from
the Ch 7.5 memo), Week 8 (Ch 8.1 specification curve — the disclosure
tool that becomes the figure of Ch 11.3 §4; Ch 8.2 robustness battery
— the source of the robustness columns in the headline table of Ch 11.2;
Ch 8.3 writing the empirical paper — the foundation for the introduction
discipline of Ch 11.4), Week 9 (Ch 9.2 the 8-minute talk decomposed —
the same five-job structure as the introduction's five paragraphs;
Ch 9.5 feedback ledger — the raw input that Week 10 triaged), and
Week 10 (Ch 10.1 triage memo, Ch 10.2 multiple-testing audit, Ch 10.3
heterogeneity analysis, Ch 10.4 mechanism plan, Ch 10.5 external-validity
paragraph — the analytic content that Week 11 presents).

Feeds Week 12 (the capstone defense and submission package — the
manuscript polished this week is the manuscript submitted next week, and
the response-letter draft from this week's lab is the response letter
that accompanies submission).

## Where this leads

Week 10's outputs were *artifacts*: triage memo, adjusted-p-value table,
heterogeneity analysis, mechanism plan, external-validity paragraph.
Week 11 turns those artifacts into *manuscript sections*: the abstract,
the publication-grade tables and figures, the introduction, the
literature review. **By the end of Week 11, you have a manuscript that
a referee at the journal you are targeting would read carefully and that
your future self — in 2030, opening the published version — will not be
embarrassed to have written.**

The discipline that Week 11 enforces is the one that, more than any
other, separates students who get published from students who do not.
Most students at this stage have the empirical content; few of them have
the prose engineering. The five chapters here — abstract, table, figure,
introduction, literature review — are the engineering toolkit. The
diagnostic scripts (`abstract_audit()`, `intro_audit()`, the table and
figure checklists) catch the obvious failures; the prose discipline of
"five sentences in the abstract, one job per paragraph in the intro,
three strands in the literature review" catches the structural
failures; the cross-referencing between the artifacts catches the
coherence failures.

Apply the discipline. Commit the artifacts. The submission package of
Week 12 builds on what you commit this week.
