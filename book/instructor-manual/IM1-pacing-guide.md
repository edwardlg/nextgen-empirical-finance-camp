# IM-1 — Pacing Guide

> **Companion documents.** This guide governs the *clock*. For how each deliverable is scored,
> see **IM-2 (Grading Rubrics)**; for the errors to watch as the clock runs, see **IM-3 (Common
> Student Pitfalls)**; for slotting outside speakers into the week, see **IM-4 (Guest Lectures &
> Mentor-Session Facilitation)**; for anchor work and answer keys, **IM-5**; for the access,
> compute, and licensing constraints that shape any schedule you build, **IM-6 (Equity/Access)**.
> All cross-references are by name so this manual survives reordering.

This camp has two clocks running at once, and the first job of any instructor is to keep them
straight. The first clock is the **12-week program clock** the textbook was rebuilt around — twelve
weeks running Jun 26–Sep 11 2026, broken into three phases that each have their own metabolism. The
second clock is the **NextGen calendar** the camp feeds (CONVENTIONS §8), whose Phase 1 is only
**seven** weekly Friday meetings 12:00–2:00pm EST, whose Phase 2 is a single symposium week, and
whose Phase 3 is four Fridays of paper refinement. Two hours a week for seven weeks is roughly
fourteen contact hours; the camp's curriculum was built for closer to two hundred. The Friday
schedule is therefore not a trim of the curriculum — it is a re-architecture against an asynchronous
backbone, and §3 below is the concrete mapping that makes it work. Read §1 and §2 first so you know
what you are compressing *from*, and what Phases 2–3 are *for*.

---

## 1. The 12-week clock

The twelve weeks are not twelve parallel modules; they are one load-bearing arc broken into three
phases, and the order is not negotiable. **Phase 1 (Weeks 1–8) is intensive curriculum and project
build**; **Phase 2 (Week 9) is the symposium**; **Phase 3 (Weeks 10–12) is paper refinement under
referee-style feedback**. The book that lives at `book/weeks/week-NN/` reflects this directly: Weeks
1–8 carry the curriculum and the first capstone draft, Week 9 carries the symposium machinery, and
Weeks 10–12 carry the revise-and-resubmit cycle. Each phase has a different metabolism, a different
weekly rhythm, and a different rubric (IM-2), and an instructor who runs Phase 3 as if it were Phase
1 will exhaust the cohort; an instructor who runs Phase 1 as if it were Phase 3 will arrive at the
symposium with nothing to defend.

### Phase 1 — Weeks 1–8, the intensive curriculum and first paper

Weeks 1–4 build the toolkit from the ground up: probability and the logic of inference (W1), the OLS
engine and its standard-error pathologies (W2), causal inference from potential outcomes through
matching and instruments (W3), and the modern quasi-experimental toolkit — DiD, RD, synthetic
control, shift-share — together with the recent literature showing the obvious estimators are often
wrong (W4). Weeks 5–6 turn from *running* estimators to *reading* them: one empirical paper per day
under a fixed Reader's-Guide anatomy (W5), then text-as-data and a full module on using LLMs as a
research co-pilot without fooling yourself (W6). Weeks 7–8 are the build: question to pre-analysis
plan (W7), then execution, robustness, and a frozen first-look draft (W8). Each week earns the next.
You cannot read a weak-instrument disaster in Week 5 if you did not derive 2SLS in Week 3; you cannot
stress-test your own DiD in Week 8 if you did not meet the staggered-adoption crisis in Week 4. When
you compress (see §3), you may *thin* a week but you may not *reorder* the dependencies.

A useful way to hold the Phase-1 arc in mind: Weeks 1–4 answer "what is a defensible number?", Weeks
5–6 answer "how do I judge someone else's number, including a machine's?", and Weeks 7–8 answer "can
I produce a defensible first-look number of my own?" The frozen first-look is what Phase 2 defends
and Phase 3 turns into a publication-bar paper; every Phase-1 week is rehearsal for it.

### Phase 2 — Week 9, the symposium

Week 9 is the symposium itself. The chapters (`book/weeks/week-09/ch91-..ch95-...md`) cover talk
craft, slide architecture, the threats-table-as-question-bank discipline, the dry-run protocol, and
the post-talk Q&A turn. The mentor session is Mentor 9 (the presentation rubric and how a working
researcher answers the question they wish you'd asked). The deliverables are the talk, the slide
deck, and the live defense; the grading rubric for the week is the **presentation rubric from Mentor
8** combined with Week-9's defense rubric (IM-2 §9). Phase 2 is short and high-stakes, and its
weekly rhythm is unlike Phase 1's: there is no new technical content, the daily block dissolves into
rehearsal, and the synchronous time becomes coaching, not teaching.

### Phase 3 — Weeks 10–12, paper refinement

Phase 3 is where the camp's terminal standard — a paper that survives a first-round referee at the
Schar Young Scholars Journal and deposits cleanly into GMU MARS — is actually met. Weeks 10–12 cover
the three movements of a real revise-and-resubmit: **W10 — reading and triaging the referee report**,
producing a point-by-point response memo and a revised plan of action; **W11 — executing the
revision**, with new robustness, rewritten exposition, and publication-quality tables; **W12 — the
final reproducibility check and submission**, with the `make clean && make all` rebuild, the
responsible-AI disclosure, and the MARS deposit. The mentors for these weeks are Mentor 10
("How a referee actually reads"), Mentor 11 ("Revising without overfitting to the referee"), and
Mentor 12 ("What submission day looks like"). The rubric is the **paper-refinement rubric** in IM-2
§10–§12, which weights the response memo, the revision quality, and the reproducibility of the final
artifact — *not* the cleverness of new analyses.

### The within-week rhythm — Phase 1

Within a full Phase-1 week, the book assumes a five-day cycle with a stable **daily block
structure**. The block is the unit of pacing, and it repeats:

1. **Read the chapter** (one of the week's five), which follows the mandated reveal-the-trick
   structure from CONVENTIONS §1: state the result in a plain sentence, show *why* it works
   (intuition → worked numerical example → algebra), show *when it fails* (the assumption that
   breaks and what you see when it does), then show the runnable code. A chapter is roughly a
   60–90 minute read for the target student.
2. **Work the notebook** that mirrors the chapter (nbN.k), which re-derives the chapter's central
   move in code and ends with a "Your Turn" extension. Budget 45–75 minutes.
3. **Do the problem set** (psN.k, ~6 problems). Solutions live in Appendix E; students should
   attempt before consulting. Budget 60–90 minutes.
4. **Lab / mentor as the week's spine.** The lab (Weeks 1–4, 7–8) or reading pack (Weeks 5–6) is the
   integrative artifact that ties the five chapters into one build. The 60-minute **Lei Gao mentor
   session** sits late in the week as the intellectual capstone, tied to one of his papers (see
   IM-4 for facilitation).

A typical Phase-1 day runs: morning chapter + notebook, afternoon problem set, with the lab threaded
across the back half of the week and the mentor session on day four or five. The end-of-week
**assessment** closes the loop on day five, graded against the week's rubric (IM-2). For a student
hitting the daily block, a Phase-1 week costs on the order of 25–35 contact-and-homework hours —
five chapters (≈6 h reading), five notebooks (≈5 h), five problem sets (≈6 h), the lab (≈4–6 h), the
mentor session (1 h + a pre-read), and the assessment (≈3–4 h). This is **full-time effective load**;
the residential cohort treats it as a workday.

### The within-week rhythm — Phase 2

Week 9 dissolves the chapter-a-day rhythm. The week's five "chapters" (ch91–ch95) are short — talk
craft, the slide architecture, the threats table as a question bank, the dry-run protocol, and the
post-talk turn — and they are best read in two evenings, not five mornings. The week then runs as
**three rehearsal cycles**: a private dry-run (Mon), a peer dry-run with the threats-table question
bank (Wed), and a final dry-run with at least one faculty critic (Thu). The **conference dry-run
itself is scheduled Mon Aug 10** (the symposium week); the **symposium is Fri Aug 14, Week 9**. The
mentor segment (Mentor 9) sits Tuesday, between the private and peer dry-runs, when students have
just enough self-awareness about their own talk to learn from a professional's. Total load drops to
about 15–20 hours, weighted toward rehearsal and slide iteration rather than reading or coding.

### The within-week rhythm — Phase 3

Weeks 10–12 invert Phase 1. There is no chapter-a-day; instead, the week has a **referee-report
metabolism**. W10 begins with the referee report (peer plus instructor) on the Phase-1 first-look,
delivered Monday; the cohort spends Tuesday in close reading, Wednesday drafting the response memo,
Thursday in a peer-critique circle on the memo, and Friday (the synchronous Friday) defending the
revision plan with Mentor 10. W11 is execution: re-running specifications, building new robustness,
rewriting the exposition, retiring weak figures, and stress-testing tables — the daily block becomes
"one referee point per day", graded against IM-2 §11. W12 is closeout: the `make clean && make all`
rebuild on a fresh machine, the responsible-AI disclosure, the MARS deposit checklist, and the
submission. Load is uneven — W10 is light (15–20 h), W11 is heavy (30+ h), W12 returns to ~20 h with
a hard stop at the submission deadline.

---

## 2. How a week's pieces fit together

The seven components of a Phase-1 week are not interchangeable; each does a distinct pedagogical
job, and the compression in §3 works only if you know which jobs are sacrificable and which are
not. The opening narrative (~1,300 w) sets the week's question in a recurring-cast frame (Maya,
Devon, Priya, Sam, Leah) — Maya's loan-approval puzzle for causal inference, Priya's
climate-insurance shock for DiD; it is motivational and *cuttable to a paragraph* under compression.
The **five chapters** carry the conceptual spine and are the least sacrificable content; under
compression you assign them as *pre-reading*, not as in-session reading. The **five notebooks** are
where understanding is verified by production — highly compressible in session (demo one, assign the
rest) but never skippable entirely. The **five problem sets** are graded practice; under compression
they collapse to one or two core problems per week (IM-5 flags which). The **lab / reading pack** is
the integrative artifact and the natural home of the week's deliverable, the piece most worth
protecting. The **mentor session** is the camp's signature, mapping cleanly onto a guest slot or a
live Friday segment (IM-4). The **assessment** is the graded checkpoint.

Phase 2's pieces are different: five short chapters, one mentor (Mentor 9), three rehearsal cycles,
and one live defense. Phase 3's pieces are different again: the referee report (an artifact, not a
chapter), the response memo, the revision artifact, three mentor sessions (10, 11, 12), and the
submission packet. The dependency that most constrains scheduling across all three phases is **data
access**: the labs in Weeks 2, 4, 5, and the capstone all touch CRSP/Compustat/HMDA, which under
CONVENTIONS §5 stay read-only on GMU infrastructure. WRDS seats and Hopper compute must be
provisioned *before* the week that needs them, not during it — an IM-6 concern that drives pacing,
because a week whose lab cannot run is a week half-lost, and a Phase-3 revision whose data pipeline
breaks is a submission missed.

---

## 3. The 12 weeks against NextGen's Friday-only calendar

NextGen Phase 1 is **seven** weekly Fridays, 12:00–2:00pm EST, Jun 26–Aug 7. The book's Phase 1 is
**eight** weeks of curriculum, so something has to give — but the give is on the *Friday* side, not
the curriculum side. The governing principle: **the seven Phase-1 Fridays cover eight weeks of
material by merging the two reading weeks (W5+W6) into one Friday and pushing all chapter reading
and most notebook execution to async between-Friday self-study**. The synchronous two hours buy what
recordings cannot: the mentor's live reasoning, a critique that responds to *this* student's error,
and the experience of watching a result break in real time.

### The seven Phase-1 Fridays

Each Friday is two hours. A reliable internal shape is: **0:00–0:20** debrief on the week's pre-work
and prior deliverable; **0:20–1:10** the mentor/teaching segment; **1:10–1:50** live work — a
critique circle, pair-coding clinic, or design workshop; **1:50–2:00** assign the coming week's
pre-work and deliverable. The seven Fridays map to the eight book-weeks like this:

| Friday | Date (2026) | Book content | Synchronous focus | Async between Fridays | Deliverable due |
|---|---|---|---|---|---|
| **F1** | Jun 26 | W1 — Probability & Inference | Mentor 1, *"What is a finding?"*; live size/power demo (Lab 1 core) | W1 chapters + notebooks | W1 mini-sim (size of a t-test) |
| **F2** | Jul 3 | W2 — OLS Engine | Mentor 2, *"Why your SE is the whole ballgame"*; FWL + clustered-SE clinic | W2 chapters + notebooks | W2 SE-choice mini-replication |
| **F3** | Jul 10 | W3 — Causal I (PO, matching, IV) | Mentor 3, *"Natural experiments"* (Deng, Gao & Kim 2020); weak-IV demo | W3 chapters + notebooks; Lab 3 | W3 weak-IV / AR-coverage task |
| **F4** | Jul 17 | W4 — Causal II (DiD/RD/SC) | Mentor 4, *"Detecting discrimination with a clean design"* (Gao & Sun 2019) | W4 chapters + notebooks; Lab 4 (HMDA DiD) | W4 staggered-DiD task; **first capstone idea memo** |
| **F5** | Jul 24 | W5 + W6 merged | Mentor 5 *"Anatomy of a JF paper"* + Mentor 6 *"AI without fooling yourself"*; Reader's-Guide walk | W5 reading pack + W6 Ch 6.5 + nb6.5 | Reader's Guide on unseen paper + one classifier OOS-validation report |
| **F6** | Jul 31 | W7 — Question → PAP | Mentor 7, *"How I pick a project — and kill one"*; identification-memo workshop | W7 chapters + notebooks; Lab 7 (stand up repo) | **PAP filed end of Week 5 of the program — a `pap-filed` tagged commit** |
| **F7** | Aug 7 | W8 — Execution & frozen first-look | Mentor 8, *"Defending a result"*; robustness clinic; **presentation-rubric introduced** | W8 chapters + notebooks; run pre-registered spec once | **First-look frozen Week 5 of program (tagged commit)** + robustness battery + draft talk |

Two structural moves make this fit. First, **W5 and W6 merge into one Friday (F5)**: both are
"reading the frontier," both replace a lab with a reading/AI pack, and both end-of-week assessments
are "produce one artifact and validate it." Second, **W7 and W8 are not in self-contained Fridays**:
F6 freezes the design (PAP tag) and F7 freezes the first-look (results tag), with the actual paper,
talk craft, and defense deliberately spilling into Phases 2 and 3.

Two critical milestones live inside this table and are worth restating, because everything
downstream depends on them holding. The **PAP is filed end of Week 5 of the program (F6, Jul 31)**
as a `pap-filed` tagged commit; this is non-negotiable, because breaking the pre-registration freeze
voids the meaning of every Week-8 p-value. The **first-look results are frozen Week 5 of the program
as well — at F7 (Aug 7)** with a `first-look-frozen` tag; everything after Phase 1 is revision under
review, not exploration.

### The NextGen Phase-2 Friday (Week 8 of NextGen = Week 9 of the book)

Phase 2 in the NextGen calendar is a single week, Aug 10–14, and book Week 9 covers it. The
**conference dry-run is Mon Aug 10**, the peer dry-run is Wed Aug 12, the final dry-run with a
faculty critic is Thu Aug 13, and the **symposium itself is Fri Aug 14**. The synchronous Friday
*is* the symposium — there is no separate mentor segment; Mentor 9 was delivered Tuesday Aug 11
asynchronously or in a 30-minute live drop-in. Grading uses the **presentation rubric from Mentor
8** (introduced at F7) plus the Week-9 defense rubric in IM-2 §9; weights are **40% talk craft, 30%
defense, 20% slide architecture, 10% reproducibility of the demo result**. Phase 1's content-mastery
rubric is **paused** during this week — the cohort is not learning new methods, they are defending
the ones they have.

### The four Phase-3 Fridays (Weeks 9–12 of NextGen = Weeks 10–12 of the book)

NextGen Phase 3 runs Aug 21–Sep 11, four Fridays. Book Weeks 10–12 cover three of them; the fourth
Friday is the submission day itself. Each Phase-3 Friday is two hours with the same internal shape
as Phase 1, but the content shifts entirely to revision craft:

| Friday | Date | Book week | Synchronous focus | Async between Fridays | Deliverable due |
|---|---|---|---|---|---|
| **F8** | Aug 21 | W10 — Reading the referee | Mentor 10, *"How a referee actually reads"*; live walk through a real referee report on a published paper | Read your own referee report (peer + instructor); draft response memo | **First revision draft + response memo (Week 10)** |
| **F9** | Aug 28 | W11 — Executing the revision | Mentor 11, *"Revising without overfitting to the referee"*; specification-curve clinic; figure/table refactoring | Execute the revision: new robustness, rewritten exposition, publication-quality tables | **Final manuscript (Week 11)** |
| **F10** | Sep 4 | W12 — Closeout | Mentor 12, *"What submission day looks like"*; reproducibility audit on a peer's repo | `make clean && make all` on a fresh machine; responsible-AI disclosure; MARS deposit dry-run | Reproducibility certificate; submission packet assembled |
| **F11** | Sep 11 | — | **Submission Friday**: live submission to Schar Young Scholars Journal + MARS deposit; cohort retrospective | — | **Submission Week 12** |

The grading rubric used during Phase 3 is the **paper-refinement rubric** in IM-2 §10–§12, not the
Phase-1 content rubric and not the Phase-2 presentation rubric. Its weights are: **35% response-memo
quality (does the student show they read what the referee actually said?), 30% revision quality (is
the new draft actually better?), 20% reproducibility (does the rebuilt artifact pass `make clean &&
make all` on a fresh env?), 15% responsible-AI disclosure and MARS metadata.** Notice what this
rubric does *not* reward: novelty, additional analyses, scope creep. A Phase-3 paper that adds three
new robustness checks at the referee's request and otherwise leaves the design alone scores higher
than one that pivots to a new identification strategy in the third week. This is deliberate; the
camp is teaching revision discipline, not a second project.

### Grading rubric weights shift across phases

The rubric is not constant across the twelve weeks, and instructors should make this shift explicit
to the cohort *before* it happens, not after a student is surprised by their Phase-2 score. **Phase
1 weights methods mastery (≈40%), the PAP (≈25%), and the frozen first-look (≈35%)** — the things a
student can demonstrate through executed empirical work. **Phase 2 weights the presentation rubric
from Mentor 8** as above. **Phase 3 weights the paper-refinement rubric from Mentors 10–12** as
above. The terminal grade is a weighted blend: 50% Phase 1, 20% Phase 2, 30% Phase 3 — the heaviest
weight on the longest phase, but enough Phase-3 weight that a strong revision can rescue a
mid-pack first-look.

### What gets cut, and what never does

Be explicit with yourself about the trade. Under the seven-Friday Phase-1 compression you will
**cut**: most in-session chapter reading (async), three of every five problem sets per week (keep
the highest-signal two — IM-5 flags them), and most in-session notebook execution (demo one, assign
the rest). You will **protect, without exception**: the dependency order of Weeks 1→4; at least one
mentor session per Friday; the W7 PAP-and-tag discipline (the pre-registration freeze is
non-negotiable); the W8 first-look freeze; and the W12 reproducibility standard (`make clean && make
all`). A compression that sacrifices any of these has not compressed the camp — it has cancelled it.

---

## 4. A pacing checklist for the instructor

Before the program starts: provision WRDS seats and Hopper/A100 compute for the weeks that need
them (W2 Fama–MacBeth, W4 HMDA DiD, W5 portfolio sorts, W6 AI module, W7–W8 capstone, and again for
Phase-3 revisions); run FM-4 (Prerequisite Self-Test) and triage; pin the environment
(`python=3.11` + the CONVENTIONS §5 stack) and confirm every notebook runs on a fresh env; stand up
GitHub Classroom and the repo template so the `pap-filed` and `first-look-frozen` tag workflows are
ready by F6 and F7.

Each Phase-1 Friday: confirm the prior deliverable arrived and was graded against its rubric (IM-2)
before the session, so the debrief is specific; keep the synchronous two hours for what cannot
happen alone; assign the next deliverable explicitly with its rubric attached.

Phase 2 week (Aug 10–14): schedule the **Mon Aug 10 dry-run** as a hard calendar event; confirm the
threats-table question bank is built before the peer dry-run on Aug 12; book the symposium logistics
(room, A/V, faculty critics) by F6 at the latest.

Each Phase-3 Friday: confirm the referee report was delivered Monday so the cohort has four days
with it before the synchronous critique; protect the W12 reproducibility check (it is the single
most objective row in the terminal rubric, and it is the MARS deposit standard); reserve the final
Friday (Sep 11) for the actual submission, not for more revision.

The clock is unforgiving precisely because the deliverable is real: these papers are headed for an
actual journal and an actual repository. Pace the camp so that the freezes hold (Week 5 PAP, Week 5
first-look), the symposium gets a real defense (Aug 14), the revision is disciplined rather than
sprawling, the code rebuilds on submission day (Sep 11), and every student can say the sentence the
whole program exists to let them say truthfully — *here is what I found, here is why you should
believe it, and here is the command that lets you check me.*
