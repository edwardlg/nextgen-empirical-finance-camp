# Week 12 — Submission, the Public Record, and What Comes Next

Phase 3 of the NextGen 12-week program is in its fourth and final week.
Last week (Week 11) you turned the analytic content of Week 10 into a
manuscript at publication standard — abstract, headline table, three
publication-grade figures, five-paragraph introduction, three-strand
literature review. The manuscript is sitting in your repository, the
response letter to the conference referees is drafted, and the work of
*producing* the paper is complete. **This week is about putting the paper
into the public record and beginning the long life of the research it
contains.** See [`../../TOC.md`](../../TOC.md) for where this fits in the
full arc.

The reveal-the-trick of this week: **a submission is not a single event
but the beginning of a multi-year sequence — preprint, conference,
referee report, revise-and-resubmit, journal acceptance, citation — and
the discipline of building a research career is the discipline of
sustaining the practice through the silences and the rejections that
mark every step.** Week 12's five chapters teach the mechanics of the
sequence chapter by chapter, with Maya's fair-lending paper carrying the
worked example through the Schar Young Scholars Journal submission, the
SSRN preprint, the conference circuit, the R&R cycle, and the five-year
research identity. By Friday the paper is submitted, the preprint is
live, the MARS deposit is approved, the FMA Undergraduate Poster
abstract is in, the eighteen-month conference plan is committed to the
calendar, and you have a written articulation of what the next five
years of your research life can look like. The camp ends here; the work
does not.

## Chapters

1. [Ch 12.1 — Submitting to the Schar Young Scholars Journal and the MARS Repository: the Submission Packet, the Cover Letter, and the Author-Statement Mechanics](ch121-submitting-to-schar-young-scholars-journal-and-mars-repository.md) (the five-component submission packet — manuscript, cover letter, CRediT author statement, data-and-code availability statement, conflicts-of-interest declaration — engineered for three audiences: the editor, the archivist, and the future-you of 2030)
2. [Ch 12.2 — The SSRN Pre-Print: Posting Decisions, Versioning, the DOI Question, and Why Pre-Prints Matter for High-School Authors](ch122-the-ssrn-preprint-posting-decisions-versioning-doi-question.md) (the preprint is the time-stamped priority claim, the dissemination channel, and the resume credential that the journal article cannot yet provide; the versioning discipline prevents the "which version did you read?" problem; the DOI question has a layered answer)
3. [Ch 12.3 — From Poster to Journal of Finance: the Decade-Long Arc of a Paper, with One Honest Case Study](ch123-from-poster-to-journal-of-finance-the-decade-long-arc-of-a-paper.md) (the seven-phase trajectory of an empirical-finance paper from idea to top-journal publication, illustrated honestly through the Rainbow of Credits municipal-borrowing paper still in flight)
4. [Ch 12.4 — The Conference Circuit Next: FMA Undergraduate Poster, AEA Pipeline, SFS Cavalcade — what each is, who attends, and what they reward](ch124-the-conference-circuit-fma-undergraduate-poster-aea-pipeline-sfs-cavalcade.md) (the six-tier conference ecosystem and the canonical climbing path for camp graduates: FMA Undergraduate Poster Session → regional FMA → Carroll Round Conference → SFS Cavalcade Undergraduate Symposium → AEA Pipeline → graduate-school venues)
5. [Ch 12.5 — What Comes After Submission: the Reviewer Wait, the Desk-Reject, the R&R, and How to Build the Five-Year Research Identity That Survives Both](ch125-what-comes-after-submission-the-reviewer-wait-the-desk-reject-the-rr.md) (the four outcomes of the first-decision letter, the response-letter discipline for the R&R cycle, the journal-ladder strategy across desk-rejects, and the six practices — reading, writing, presenting, portfolio-building, relationship-investing, journaling — that build the five-year research identity)

## Theme

**Phase 3 Week 4 — Submission, the Public Record, and What Comes Next.**
Week 11 was about turning analytic content into a publishable
manuscript; Week 12 is about putting the manuscript into the *public
record* and starting the multi-year life of the work it contains. The
distinction between the two weeks is the distinction between *producing*
a paper and *publishing* a paper — between having a manuscript that is
ready and having a paper that is in the conversation. The mechanics of
the publication move have multiple components, multiple audiences, and
multiple time scales; each of the five chapters takes one component, one
audience, or one time scale and walks it through with care.

The seam Week 12 protects is the one between *finishing the manuscript*
and *starting the research career*. Most students at the precollege
stage finish the manuscript and stop; the camp's premise is that the
manuscript is not the end of the project but the beginning. The
mechanics of submission, of preprint posting, of conference
presentation, and of the R&R cycle are the *infrastructure* of a
research life; the camp's job is to teach the infrastructure carefully
enough that a graduating senior in 2026 can keep building on it through
2031 without needing to learn the basics over again.

## Notebooks (`../../../notebooks/week-12/`)

- **nb12.1** `credit_audit()` — checks CRediT author-statement completeness against the NISO taxonomy (all fourteen roles assigned, intensity descriptors valid, corresponding author named); ships with the Maya/Devon/Priya/Sam/Leah variant test cases from Ch 12.1
- **nb12.2** `ssrn_metadata_builder()` — produces a structured CSV of SSRN posting metadata (title, abstract, JEL codes, networks, keywords, MARS handle, ORCID linkages) ready to paste into SSRN's submission form; runs the versioning-footnote insertion for the manuscript title page
- **nb12.3** `arc_simulator()` — Monte Carlo simulation of the decade-long publication arc for an empirical-finance paper, given parameters (starting tier, identification quality, topical heat), producing distributional projections of acceptance probability by year (used to build Ch 12.3's honest projections for the Rainbow of Credits paper)
- **nb12.4** `conference_planner()` — produces an eighteen-month conference calendar from a paper's current version, the student's available travel budget, and a tier-preference vector; outputs venue list, submission deadlines, expected decision dates, travel-cost estimates
- **nb12.5** `response_letter_template()` — generates a structured response-letter scaffold from a referee report (parsed into numbered points), with the §6 principles enforced (verbatim quotes, section/page anchoring, disagreement-template flags); ships with the Ch 12.5 example referee report on Maya's paper

All notebooks pinned to the Week 1 environment (python 3.11, pandas
2.2+, statsmodels, matplotlib). All seeded with
`rng = np.random.default_rng(42)`. All run headless under
`matplotlib.use("Agg")`. Each notebook produces output that is committable
directly to a research-process repository (an analog of the manuscript
repository, used by active researchers to track submission histories and
correspondence).

## Problem sets (model exemplars in [Appendix E](../../appendices/E-solutions-manual/))

- **PS 12.1** Assemble the full submission packet for your camp paper to the Schar Young Scholars Journal and the MARS repository. Produce all five components: manuscript, cover letter, CRediT author statement, data-and-code availability statement, conflicts-of-interest declaration. Run the eight-item Friday-night verification of Ch 12.1 §9. Submit.
- **PS 12.2** Post your paper to SSRN with primary and secondary networks chosen, JEL codes, ORCID linked, and the MARS handle named in the abstract. Run `ssrn_metadata_builder()` to produce the metadata CSV. Document the version footnote on the title page.
- **PS 12.3** Write a five-page "arc projection" for your paper. Following Ch 12.3, name the substantive question, the methodological identity, the venue identity, the target first-submission venue, the journal-ladder, and the realistic outcome distribution. Use `arc_simulator()` to produce the probability projections; defend the parameter choices in writing.
- **PS 12.4** Produce your eighteen-month conference plan. Following Ch 12.4, name five venues with submission deadlines, decision dates, travel-cost estimates, and the function-mix each venue serves. Apply the tier-climbing logic. Submit one conference abstract before Friday of Week 12.
- **PS 12.5** Write your "five-year research identity" statement. Following Ch 12.5 §10, articulate your substantive area, your methodological identity, your venue identity, your one-year plan, your three-year plan, and your five-year plan. The statement is private (it does not get shared with the journal or the conference); it is for you, kept in your research journal.

## Lab, mentor, assessment

- **Lab 12 — Submission Week** *(five sessions, one per chapter)*: by Friday the submission to the Schar Young Scholars Journal is complete and confirmed, the SSRN preprint is live, the MARS deposit is approved, the FMA Undergraduate Poster abstract is submitted, the eighteen-month conference plan is on the shared calendar, the five-year research-identity statement is written and committed to the student's private research journal, and the cohort gathers Friday afternoon for a closing reflection.
- **Mentor Session 12 — "What the decade-long arc actually feels like, year by year"** *(Prof. Gao, drawing on the trajectories of Gao and Sun (2019) — from initial JFE submission in 2015 to PNAS publication in 2019 with Congressional testimony in between; of Gao, Han, Li, and Zhou (2018) — from intraday-momentum working paper in 2014 to JFE publication in 2018; of Elnahas, Gao, Hossain, and Kim (2024) — from political-ideology working paper in 2018 to JFQA in 2024; of the Rainbow of Credits paper still in flight in 2026 with JF as the target — each tells a different chapter of the arc, with the honest emotional and time-cost details students rarely hear from textbooks)*
- **Week 12 Assessment + Rubric** — graded on: (a) the submission packet (all five components, no procedural failures, eight-item verification documented), (b) the SSRN posting (live, metadata complete, versioning footnote present, MARS handle cross-linked), (c) the arc projection (five pages, realistic, defending the parameter choices, naming the journal ladder), (d) the conference plan (five venues with submission deadlines and travel budgets, tier-climbing logic explicit), (e) the five-year research-identity statement (substantive area, methodological identity, venue identity, one/three/five-year plans, in the student's voice, honest about uncertainty).

## Cross-references

Built on Week 7 (Ch 7.5 identification memo — the assumption named in
the cover letter's contribution paragraph and the assumption that any
referee will probe; the foundation of every R&R defense the paper will
ever face), Week 8 (Ch 8.1 specification curve — the disclosure tool
that protects against the "robustness" critique; Ch 8.2 robustness
battery — the source of the robustness tables in the submitted
manuscript and the new tables added in R&R revisions; Ch 8.3 writing the
empirical paper — the foundation for the manuscript that the submission
packet wraps), Week 9 (Ch 9.2 the 8-minute talk decomposed — the
foundation for the longer paper-presentation format at regional FMAs and
the SFS Cavalcade; Ch 9.5 feedback ledger — the structural memory that
becomes the basis for the response letter), Week 10 (Ch 10.1 triage
memo — the discipline applied at full scale to referee comments in the
R&R cycle; Ch 10.2 multiple-testing audit — the second-order defense
referees in empirical finance now expect; Ch 10.5 external-validity
paragraph — embedded in the discussion section of the submitted
manuscript), and Week 11 (Ch 11.1–11.5 — the manuscript that the
submission packet wraps and that the R&R revises).

Feeds beyond the camp: the eighteen-month conference plan from Ch 12.4
sets the calendar for fall 2026 through spring 2028; the five-year
research-identity statement from Ch 12.5 sets the trajectory for 2026
through 2031. The book has no Week 13 because the next week of work is
private to each student — the FMA poster preparation, the AEA in
January, the Carroll Round application in February, the second paper
beginning to take shape in the back of the notebook. Each student's
Week 13 looks different. The discipline is to commit to it.

## Where this leads

Week 11's outputs were a manuscript at publication standard — the
visible artifact of the camp. Week 12 puts the manuscript into the
public record (the submission, the preprint, the archival deposit) and
sets the multi-year trajectory (the conference plan, the journal
ladder, the five-year research identity). **By the end of Week 12 the
paper has begun its public life and the student has begun the research
career that the paper started.**

The discipline that Week 12 enforces — the procedural care of the
submission packet, the priority discipline of the preprint, the patient
climbing of the conference tiers, the durable practices of the research
identity — is what separates students who treat the camp as a one-off
project from students for whom the camp is the start of something
longer. Most camp graduates do not become academic researchers. The
students who do are the students who keep doing the work of §9's six
practices — reading, writing, presenting, portfolio-building,
relationship-investing, journaling — past the week the camp ends.

The book ends with Week 12. The work continues. The Schar Young Scholars
Journal acceptance email arrives in 14 weeks. The FMA Undergraduate
Poster Session is in 18 weeks. The SSRN download count crosses 200 by
the end of the month. The first response from a senior faculty member
who read the paper arrives in 23 weeks. Each is a small event; the
sequence is the career. Maya, Devon, Priya, Sam, Leah, and you have all
begun it. The camp's job is done. The rest is yours.
