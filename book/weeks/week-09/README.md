# Week 9 — The Conference: Presenting Empirical Research as a Real Deliverable

You have a paper. It compiles from raw bytes to PDF with one command, the
specification curve from Chapter 8.1 is tight enough that none of your
robustness siblings flip sign, the identification memo from Chapter 7.5 names
every threat the threats-and-responses table can hold. None of that matters on
Saturday. On Saturday you stand up, you have eight minutes, and a room of
people who have *never read your paper* decides whether your work is real.
This week is about that day — the seventy-two hours before it, the eight
minutes of it, the question period that follows, the poster session the next
afternoon, and the twenty-four hours after, when you turn what just happened
into the agenda for Weeks 10–12. See [`../../TOC.md`](../../TOC.md) for the full plan.

## Chapters
1. [Ch 9.1 — Before the Conference: The 72-Hour Pre-Flight](ch91-before-the-conference-72-hour-pre-flight.md) (slide-freeze; replication packet final; anticipated-questions matrix)
2. [Ch 9.2 — The 8-Minute Talk, Decomposed](ch92-the-8-minute-talk-decomposed.md) (Hook · Design · Identification Punchline · One Picture · Threats · Ask)
3. [Ch 9.3 — During the Conference: Reading the Room and the Three Honest Answers](ch93-during-the-conference-three-honest-answers.md) ("I don't know," "In the paper," "Good point" — and the hostile-question taxonomy)
4. [Ch 9.4 — The Poster and the Hallway Conversation](ch94-poster-and-hallway-conversation.md) (a different medium, a different argument structure, a different success metric)
5. [Ch 9.5 — After the Conference: Capturing Feedback in 24 Hours](ch95-after-the-conference-feedback-ledger-triage.md) (the feedback ledger; the triage rubric; the bridge into Weeks 10–12)

## Notebooks (`../../../notebooks/week-09/`)
- nb9.1 Pre-flight checklist runner (slide-freeze hash; packet `make clean && make all` honesty test; anticipated-Q matrix scaffold) · nb9.2 Talk timer + arc-budget tool (per-slide rehearsal stopwatch, cut-line marker) · nb9.3 Question-taxonomy classifier (survivable vs. fatal, with the Ch 7.5 threats table joined on threat-id) · nb9.4 Poster layout helper (matplotlib figure-grid + headline-band export) · nb9.5 Feedback ledger + triage emitter (CSV → R&R-style task board for Weeks 10–12)
- All verified to run headless; no hard-coded secrets.

## Problem sets (capstone-defense deliverables; model exemplars in [Appendix E](../../appendices/E-solutions-manual/))
- [PS 9.1](ps9.1.md) Pre-flight packet (frozen deck SHA, packet rebuild log, anticipated-Q matrix) · [PS 9.2](ps9.2.md) Six-slide arc + timed dry-run video · [PS 9.3](ps9.3.md) Hostile-question simulation: ten prepared answers · [PS 9.4](ps9.4.md) Poster + 90-second elevator pitch · [PS 9.5](ps9.5.md) Post-conference feedback ledger + 4-week revision plan

## Lab, mentor, assessment
- [Lab 9 — Conference Day, End-to-End](lab9-conference-day-end-to-end.md) (full dress rehearsal: 72-hour pre-flight checklist → timed 8-minute talk → adversarial Q&A → poster session → 24-hour feedback ledger; recorded and reviewed)
- [Mentor Session 9 — "What I tell my students the night before they present"](mentor9-night-before-you-present.md) (Gao & Sun 2019 *PNAS*; the HUD/Fed/Congress testimony arc — what changes when the room is policy, not academic)
- [Week 9 Assessment + Rubric — Conference Defense](assessment9.md) — graded on the live talk, the question period, the poster, and the feedback ledger (the first checkpoint of the revision phase)

## Theme

**The conference is the credibility-transfer event.** The seam you built — the
pre-analysis-plan tag, the threats table, the one-click packet — is *invisible*
in a PDF; the talk is where it becomes visible to other humans. Reveal the
trick: the talk does not deliver the result, it delivers the *argument*, and
the question period does not test what you know, it tests whether you can
locate what you don't. Every move in this week is about widening the gap
between *believing your number is right* and *being able to make a skeptic
believe it is right*.

## Where this leads

Week 9 closes Phase 2 of the NextGen 12-week program (the conference-presentation
week) and opens Phase 3 (paper-refinement Weeks 10–12). The feedback ledger you
build in Ch 9.5 is the *input* to Week 10: every "good point" from Saturday
becomes a row on the triage board on Monday. Do not let it leak.
