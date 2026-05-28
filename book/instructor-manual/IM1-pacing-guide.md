# IM-1 — Pacing Guide

> **Companion documents.** This guide governs the *clock*. For how each deliverable is scored,
> see **IM-2 (Grading Rubrics)**; for the errors to watch as the clock runs, see **IM-3 (Common
> Student Pitfalls)**; for slotting outside speakers into the week, see **IM-4 (Guest Lectures &
> Mentor-Session Facilitation)**; for anchor work and answer keys, **IM-5**; for the access,
> compute, and licensing constraints that shape any schedule you build, **IM-6 (Equity/Access)**.
> All cross-references are by name so this manual survives reordering.

This camp has two clocks running at once, and the first job of any instructor is to keep them
straight. The first clock is the **8-week residential/intensive clock** the textbook was written
to — eight themed weeks, each a self-contained unit of five chapters, five problem sets, five
notebooks, a lab or reading pack, a 60-minute Lei Gao mentor session, and an end-of-week assessment.
The second clock is the **real NextGen calendar** the camp feeds (CONVENTIONS §8): a 12-week program
running Jun 26–Sep 11 2026, whose Phase 1 is only **seven** weekly Friday meetings, 12:00–2:00pm EST.
Two hours a week for seven weeks is roughly fourteen contact hours; the 8-week book is built for
something closer to two hundred. The compression is therefore not a trim — it is a re-architecture,
and §3 below is the concrete mapping that makes it work. Read §1 and §2 first so you know what you
are compressing *from*.

---

## 1. The 8-week clock

The eight weeks are not eight parallel modules; they are a single load-bearing arc, and the order is
not negotiable. Weeks 1–4 build the toolkit from the ground up: probability and the logic of
inference (W1), the OLS engine and its standard-error pathologies (W2), causal inference from
potential outcomes through matching and instruments (W3), and the modern quasi-experimental toolkit —
DiD, RD, synthetic control, shift-share — together with the recent literature showing the obvious
estimators are often wrong (W4). Weeks 5–6 turn from *running* estimators to *reading* them: one
empirical paper per day under a fixed Reader's-Guide anatomy (W5), then text-as-data and a full
module on using LLMs as a research co-pilot without fooling yourself (W6). Weeks 7–8 are the
capstone: question to pre-analysis plan (W7), then execution, robustness, writing, and defense (W8).
Each week earns the next. You cannot read a weak-instrument disaster in Week 5 if you did not derive
2SLS in Week 3; you cannot stress-test your own DiD in Week 8 if you did not meet the
staggered-adoption crisis in Week 4. When you compress, you may *thin* a week, but you may not
*reorder* the dependencies.

A useful way to hold the whole arc in mind: Weeks 1–4 answer "what is a defensible number?", Weeks
5–6 answer "how do I judge someone else's number, including a machine's?", and Weeks 7–8 answer "can
I produce a defensible number of my own and survive a referee?" The terminal assessment (W8) is the
only thing the camp was ever building toward, and every earlier week is rehearsal for it.

### The within-week rhythm

Within a full week, the book assumes a five-day cycle with a stable **daily block structure**. The
block is the unit of pacing, and it repeats:

1. **Read the chapter** (one of the week's five), which follows the mandated reveal-the-trick
   structure from CONVENTIONS §1: state the result in a plain sentence, show *why* it works
   (intuition → worked numerical example → algebra), show *when it fails* (the assumption that
   breaks and what you see when it does), then show the runnable code. A chapter is roughly a
   60–90 minute read for the target student.
2. **Work the notebook** that mirrors the chapter (nbN.k), which re-derives the chapter's central
   move in code and ends with a "Your Turn" extension. Budget 45–75 minutes; the notebook is where
   the chapter's claim becomes something the student's own hands have produced.
3. **Do the problem set** (psN.k, ~6 problems), which is the day's graded practice. Solutions live
   in Appendix E; students should attempt before consulting. Budget 60–90 minutes.
4. **Lab / mentor as the week's spine.** The lab (Weeks 1–4, 7–8) or reading pack (Weeks 5–6) is the
   integrative artifact that ties the five chapters into one build — a coin-flip universe (Lab 1), a
   Fama–MacBeth replication (Lab 2), a weak-IV pathology (Lab 3), a clean DiD on HMDA (Lab 4), a
   reproducible data repo (Lab 7), a final manuscript + repo + defense (Lab 8). The 60-minute **Lei
   Gao mentor session** sits late in the week as the intellectual capstone of the days' work, tied to
   one of his papers (see IM-4 for facilitation).

A typical full-day rhythm therefore runs: morning chapter + notebook, afternoon problem set, with
the lab threaded across the back half of the week and the mentor session on day four or five. The
end-of-week **assessment** closes the loop on day five, graded against the week's rubric (IM-2).

### Hours per week, roughly

For a student hitting the daily block, a full week costs on the order of 25–35 contact-and-homework
hours: five chapters (≈6 h reading), five notebooks (≈5 h), five problem sets (≈6 h), the lab
(≈4–6 h), the mentor session (1 h + a pre-read), and the assessment (≈3–4 h). Technical weeks (2–4)
sit at the high end; the reading weeks (5–6) are lighter per-chapter but heavier on the daily
replication problem sets. Knowing these magnitudes is what makes the NextGen compression honest: you
cannot move 30 hours of work into a 2-hour Friday and pretend nothing was cut.

---

## 2. How a week's pieces fit together

The seven components of a week are not interchangeable; each does a distinct pedagogical job, and the
compression in §3 works only if you know which jobs are sacrificable and which are not.

- **The opening narrative** (~1,300 w) sets the week's question in a recurring-cast frame (Maya,
  Devon, Priya, Sam, Leah) — Maya's loan-approval puzzle for causal inference, Priya's
  climate-insurance shock for DiD. It is short, motivational, and *cuttable to a paragraph* under
  compression without loss of rigor.
- **The five chapters** carry the conceptual spine and are the least sacrificable content. Under
  compression you assign them as *pre-reading*, not as in-session reading.
- **The five notebooks** are where understanding is verified by production. They are highly
  compressible *in session* (you demo one, assign the rest) but should never be skipped entirely —
  a student who has never run the code has not learned the week.
- **The five problem sets** are graded practice; under compression they collapse to one or two
  "core" problems per week (IM-5 flags which problems are the highest-signal).
- **The lab / reading pack** is the integrative artifact and the natural home of the week's
  deliverable. It is the piece most worth protecting under compression because it is where skills
  combine.
- **The mentor session** is the camp's signature — a working researcher walking students through how
  a real finding gets made and killed. It maps cleanly onto a guest slot or a live Friday segment
  (IM-4).
- **The assessment** is the graded checkpoint. Under compression, several weekly assessments fold
  into fewer, larger deliverables (see §3 and IM-2).

The dependency that most constrains scheduling is **data access**: the labs in Weeks 2, 4, 5, and the
capstone all touch CRSP/Compustat/HMDA, which under CONVENTIONS §5 stay read-only on GMU
infrastructure. WRDS seats and Hopper compute must be provisioned *before* the week that needs them,
not during it — this is an IM-6 concern that nonetheless drives the pacing, because a week whose lab
cannot run is a week half-lost.

---

## 3. Compressing 8 weeks into NextGen's 7 Friday sessions

This is the section instructors will return to most, so it is concrete. The real program
(CONVENTIONS §8) is 12 weeks, Jun 26–Sep 11 2026, structured in three phases:

- **Phase 1 — seven weekly Friday meetings, 12:00–2:00pm EST** (the synchronous core).
- **Phase 2 — the conference presentation, ~Aug 15** (the talk + defense).
- **Phase 3 — four weeks of paper refinement** (revise-and-resubmit toward the Schar Young Scholars
  Journal and the GMU MARS deposit).

The 8-week book maps onto these three phases as follows. The governing principle: **move chapters
and notebooks to asynchronous pre-work, reserve the two synchronous Friday hours for the mentor
session and live design/critique that cannot happen alone, and let Phases 2–3 absorb Weeks 7–8.**

### The seven Friday sessions (Phase 1)

Each Friday is two hours. A reliable internal shape is: **0:00–0:20** debrief on the week's pre-work
and the prior deliverable; **0:20–1:10** the mentor/teaching segment (a live or recorded Lei Gao
mentor session, or the instructor walking one notebook); **1:10–1:50** live work — a critique
circle, a pair-coding clinic, or a design workshop; **1:50–2:00** assign the coming week's pre-work
and deliverable. The seven sessions map to the eight book-weeks like this:

| Friday | Book content folded in | Synchronous focus (the 2 hours) | Async pre-work assigned | Deliverable due |
|---|---|---|---|---|
| **F1** | W1 (Probability & Inference) | Mentor Session 1, *"What is a finding?"*; live coin-flip/size-power demo (Lab 1 core) | W1 Ch 1.3–1.5 + nb1.3–1.5 | W1 mini-sim (size of a t-test) — core of Assessment W1 |
| **F2** | W2 (OLS Engine) | Mentor Session 2, *"Why your SE is the whole ballgame"*; FWL + clustered-SE clinic | W2 Ch 2.1, 2.3, 2.4 + nb2.4 | W2 SE-choice mini-replication |
| **F3** | W3 (Causal I: PO, matching, IV) | Mentor Session 3, *"Natural experiments"* (Deng, Gao & Kim 2020); weak-IV live demo (Lab 3 core) | W3 Ch 3.1, 3.4, 3.5 + nb3.4–3.5 | W3 weak-IV / AR-coverage task |
| **F4** | W4 (Causal II: DiD/RD/SC/shift-share) | Mentor Session 4, *"Detecting discrimination with a clean design"* (Gao & Sun 2019); staggered-DiD clinic | W4 Ch 4.1–4.3 + nb4.1–4.2; Lab 4 (HMDA DiD) as take-home | W4 staggered-DiD task; **first capstone idea memo** |
| **F5** | W5 + W6 (Reading the Frontier I & II) **merged** | Mentor 5 *"Anatomy of a JF paper"* + Mentor 6 *"Text as data, AI without fooling yourself"* (paired); one live Reader's-Guide walk-through; the responsible-AI checklist | W5 Reader's-Guide pack + one classic; W6 Ch 6.5 (AI co-pilot) + nb6.5 | A single Reader's Guide on an unseen paper **+** a one-classifier OOS-validation report (merged W5/W6 assessment) |
| **F6** | W7 (Question → PAP) | Mentor Session 7, *"How I pick a project — and kill one"*; live idea-generation + identification-memo workshop | W7 Ch 7.1–7.5 + nb7.2, nb7.4; Lab 7 (stand up the repo) | **PAP + identification memo, filed as a `pap-filed` tagged commit** (the W7 deliverable) |
| **F7** | W8 (Execution & robustness, kickoff) | Mentor Session 8, *"Defending a result"*; robustness-battery clinic; talk-craft + peer-review setup | W8 Ch 8.1–8.5 + nb8.1–8.4; run the pre-registered spec once | **Confirmatory results + robustness battery + draft paper**; talk scheduled into Phase 2 |

Two structural moves make this fit. First, **Weeks 5 and 6 merge into one Friday (F5)**: both are
"reading the frontier," both replace a lab with a reading/AI pack, and both end-of-week assessments
are "produce one artifact and validate it" (a Reader's Guide; a classifier with an OOS report). They
combine into a single deliverable without losing the load-bearing skill of either — critical reading
and validated measurement. Second, **Weeks 7 and 8 stop being self-contained weeks and become the
spine of the whole program**: F6 produces the design (PAP + memo), F7 kicks off execution, and the
actual paper, robustness, talk, and defense spill deliberately into Phases 2 and 3.

### A worked Friday, end to end (F3 as the example)

To make the two-hour shape concrete, here is F3 (the causal-inference-I / weak-IV session) at the
minute level. The cohort arrives having read W3 Ch 3.1, 3.4, 3.5 and worked nb3.4–3.5 as async
pre-work, and having submitted the prior week's deliverable (the W2 SE-choice mini-replication).

- **12:00–12:20 — Debrief.** Walk three submitted W2 deliverables (one strong, one with the classic
  SE-flavor-by-reflex error, one in between), so the debrief teaches from the cohort's own work, not
  a generic example. This is also where you surface the highest-signal Week-2 pitfall (IM-3) before
  it migrates into Week-3 thinking.
- **12:20–1:10 — Mentor segment.** Run (live or recorded) Mentor Session 3, *"Natural experiments:
  finding the lever nature pulled,"* tied to Deng, Gao & Kim (2020). The three Socratic warm-ups and
  three stretch questions in the mentor packet are the spine; IM-4 gives the facilitation protocol.
- **1:10–1:50 — Live weak-IV demo.** The core of Lab 3: build a DGP where 2SLS is badly biased toward
  OLS, show the first-stage F flag it, and contrast with a strong instrument. Do this as a
  pair-coding clinic, not a lecture — students should *watch their own 2SLS estimate blow up* as the
  instrument weakens. This is the durable cure for Pitfall 3.2 (IM-3).
- **1:50–2:00 — Assign.** Hand out the W3 weak-IV / Anderson–Rubin coverage deliverable with its
  rubric attached (IM-2 §3), and the async pre-work for F4 (W4 Ch 4.1–4.3, nb4.1–4.2).

Every Friday follows this skeleton; only the mentor topic, the live clinic, and the deliverable
change. The discipline that makes it work is that **nothing solvable alone happens in the room** —
the reading and most of the coding are async, and the two synchronous hours buy what a recording
cannot: the mentor's live reasoning, a critique that responds to *this* student's error, and the
experience of watching a result break in real time.

### An alternative shape: the two-week aggregation

Some instructors will prefer a coarser mapping that keeps each Friday tied to a single coherent block
rather than splitting and merging. The two-week aggregation pairs the book-weeks and is a clean
fallback when the cohort is large or underprepared:

| Friday | Paired book-weeks | Synchronous focus |
|---|---|---|
| F1 | W1 | Inference foundations + Mentor 1 |
| F2 | W2 | OLS + SEs + Mentor 2 |
| F3 | W3 | Causal I (IV) + Mentor 3 |
| F4 | W4 | Causal II (DiD) + Mentor 4 |
| F5 | W5 + W6 | Reading + AI co-pilot (Mentors 5 & 6) |
| F6 | W7 | PAP + memo (Mentor 7) |
| F7 | W8 kickoff | Execution + defense setup (Mentor 8) |

This is the shape the table in the preceding subsection uses, and it is the recommended default: it
preserves one mentor session per Friday, keeps the dependency order intact, and folds the two reading
weeks into the single Friday they naturally share. The only weeks that *must* combine to fit seven
slots are W5 and W6; everything else maps one-to-one, with Weeks 7–8 deliberately spilling into Phases
2–3. If your cohort can sustain more than two contact hours a week, do not compress at all beyond the
W5/W6 merge — give Weeks 7 and 8 their own Fridays and run an eighth or ninth session inside Phase 2.

### Phase 2 — the conference presentation (~Aug 15)

This is Week 8's deliverables D3 (the 8-minute presentation + defense) and a near-final D1 (the
paper). Between F7 and the conference, students are executing the W8 chapters asynchronously — the
specification curve (Ch 8.1), the robustness battery and Oster δ (Ch 8.2), publication-quality tables
(Ch 8.3, Appendix D), peer review (Ch 8.4), and the talk + replication packet (Ch 8.5). The
conference *is* the defense the W8 assessment grades; the threats-table-as-question-bank discipline
(W8 D3) is what students rehearse here. Schedule at least one **dry-run defense** in the week before
the conference — the mentor-session facilitation notes in IM-4 give the question protocol.

### Phase 3 — four weeks of paper refinement

This is Week 8's D1 (final paper), D2 (the `make clean && make all` replication packet), and D4 (the
responsible-AI disclosure) brought to the publication bar. Phase 3 is where the camp's terminal
standard — a paper that survives a first-round referee at the Schar Young Scholars Journal and
deposits cleanly into GMU MARS (W8 assessment, "How the rubric maps to the publication standard") —
is actually met. The four weeks correspond to a revise-and-resubmit cycle: referee report (peer +
instructor), R&R memo, revision, and the final reproducibility check. Grade D1/D2/D4 against the
**200-point terminal rubric** at the end of Phase 3 (IM-2), not at the conference.

### What gets cut, and what never does

Be explicit with yourself about the trade. Under the 7-Friday compression you will **cut**: most
in-session chapter reading (moved to async), three of every five problem sets (keep the highest-signal
two per week — IM-5 flags them), and most in-session notebook execution (demo one, assign the rest).
You will **protect, without exception**: the dependency order of Weeks 1→4; at least one mentor
session per Friday; the W7 PAP-and-tag discipline (the pre-registration freeze is non-negotiable —
breaking it voids the meaning of every Week-8 p-value); and the W8 reproducibility standard
(`make clean && make all`). A compression that sacrifices the freeze or the rebuild has not
compressed the camp — it has cancelled it.

### A note on cohort size and pacing variance

The Friday shape above assumes a cohort small enough for a live critique circle (roughly 8–16). With
a larger cohort, push critique into asynchronous peer-review pairs (Ch 8.4 machinery) and reserve the
Friday live block for the mentor segment and a single worked example. With a cohort that arrives
underprepared on the prerequisites, run the **Prerequisite Self-Test** (Front Matter FM-4) *before*
F1 and route weak students to Appendices A (math) and B (Python/LaTeX) as async remediation during
F1–F2 — do not let prerequisite gaps surface for the first time during the OLS week, when they
compound. IM-6 covers the access side of this (compute, seats, accommodations); the pacing side is
simply: diagnose early, remediate async, and never let the synchronous Friday become a lecture you
could have recorded.

---

## 4. A pacing checklist for the instructor

Before the program starts:

- Provision WRDS seats and Hopper/A100 compute for the weeks that need them (W2 Fama–MacBeth, W4
  HMDA DiD, W5 portfolio sorts, W6 AI module, W7–W8 capstone). Lead time is the binding constraint;
  see IM-6.
- Run FM-4 (Prerequisite Self-Test) and triage. Assign Appendix A/B remediation to anyone who misses
  the calculus/probability/Python anchors.
- Pin the environment (`python=3.11` + the CONVENTIONS §5 stack) and confirm every notebook runs on
  a fresh env. A week whose code does not run is a week lost.
- Stand up GitHub Classroom and the repo template (Lab 7 / Appendix B.2) so the `pap-filed` tag
  workflow is ready by F6.

Each Friday:

- Confirm the prior deliverable arrived and was graded against its rubric (IM-2) before the session,
  so the debrief is specific.
- Keep the synchronous two hours for what cannot happen alone — the mentor's reasoning, live
  critique, pair debugging — and push everything solvable individually to async pre-work.
- Assign the next deliverable explicitly, with its rubric attached.

Across Phases 2–3:

- Schedule a dry-run defense before the ~Aug 15 conference.
- Reserve the final Phase-3 week for the `make clean && make all` check on every student's repo —
  it is the single most objective row in the terminal rubric, and it is the MARS deposit standard.

The clock is unforgiving precisely because the deliverable is real: these papers are headed for an
actual journal and an actual repository. Pace the camp so that the freeze holds, the code rebuilds,
and every student can say the sentence the whole program exists to let them say truthfully — *here is
what I found, here is why you should believe it, and here is the command that lets you check me.*
