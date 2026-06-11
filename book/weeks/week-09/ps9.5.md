# PS 9.5 — Post-Conference Feedback Ledger and 48-Hour Triage Memo

**Course:** 8-Week Empirical Finance Camp · Week 9 · Problem Set 9.5
**Covers:** Ch 9.5 (After the Conference: Feedback as Data), building on Ch 8.4 (peer review and revision), Ch 7.5 (the identification memo and its threats-and-responses table), and PS 9.2 (the anticipated-questions matrix). Uses no notebook: the deliverable is a written ledger and a triage memo that turn the conference into the input for Weeks 10–12's paper refinement.
**Type:** Project deliverable, not a numeric problem set. You produce two artifacts — a comprehensive `feedback-ledger.md` recording *every* comment, question, and suggestion you received at the conference, and a 48-hour `triage-memo.md` that classifies each ledger entry into act-now / act-by-Week-11 / do-not-act, with reasons. There is no single right answer because the answer is *what the conference actually said to you* and *how honestly you sorted it* — and what is graded is whether the ledger is *complete* (you wrote down what you heard, including the comments that stung), *attributed* (you noted who said what, where reasonable), and *triaged with discipline* (the do-not-act bucket has reasons, not dismissals).

**Total: 100 points.** Point values are stated per part. A model deliverable — a complete post-conference ledger and 48-hour triage memo for one cast project (Devon's spot-Bitcoin-ETF event study), with instructor grading notes keyed to the rubric — is in Appendix E (`E-w9-ps9.5-solutions.md`). Read it *after* you draft your own, the way Ch 9.5 walked through Devon's ledger: not to copy, but to calibrate.

A boundary to hold throughout. A feedback ledger is *not* a place to argue back with the conference; nothing in the ledger is rebutted, defended, or rationalized in-line — every entry is recorded *as said*, in the speaker's words as best you can reconstruct them, even when (especially when) the comment was unkind or wrong. The argument-back happens in the triage memo, with 48 hours of distance and the audit trail of the ledger to keep you honest. The discipline is the same one a careful trial lawyer uses with a deposition: write down what the witness said, *then* decide what to do with it — never both at once. Conversely, the triage memo is not a place to record the conference *neutrally*; that is the ledger's job. The memo is *your* judgment, written 48 hours later, with reasons, on what each comment merits in terms of revision effort. The two artifacts are deliberately separate so you cannot blur "what was said" with "how I'm going to handle it."

---

## What you submit

Two Markdown files, both committed to your capstone repository under `paper/feedback/`:

1. `feedback-ledger.md` — the comprehensive, attributed record of every comment, question, and suggestion received at the conference (Parts 1–2).
2. `triage-memo.md` — the 48-hour triage decision document, classifying every ledger entry into one of three action buckets with reasons (Parts 3–4).

The ledger is written within 24 hours of the conference, while memory is fresh; the triage memo is written 48 hours after the conference, *deliberately later than the ledger*, with the gap providing the cooling-off period that converts emotional reactions into engineering decisions.

Together, the two artifacts are about three pages plus the tables. The triage memo's action items feed directly into the Week 10–12 revision plan; PS 10.1 will reference the triage memo by line number.

---

## Part 1 — Build the feedback ledger (`feedback-ledger.md`) (35 points)

The ledger is a table with one row per comment, question, or suggestion. The format is unforgiving in the same way a court reporter's transcript is — every row records *what was said*, *who said it*, *when and where*, *what slide / poster panel / part of the paper it was about*, and *whether you have a response in the room*. Argumentation is forbidden in this artifact.

**(a) Ledger format and completeness (15 pts).** Use this exact column set:

| # | Source venue | Speaker (name + affiliation, or anonymous descriptor) | Comment / question (verbatim or close paraphrase) | Topic (slide # / poster panel / paper section) | Category (per PS 9.2 §1) | In-room response given | Tone (constructive / mixed / hostile) |
|---|---|---|---|---|---|---|---|

The columns each carry a discipline:

- **Source venue:** which event — your talk's Q&A, your poster session, a hallway conversation, a coffee-break exchange, an email follow-up the day after. Different venues produce different signal qualities.
- **Speaker:** name and affiliation when you got them. *"David Bergstresser, Brandeis"* is a usable row; *"a senior person on the front row"* is also usable when you did not catch the name; *"anonymous referee-style commenter"* is the residual category. Honesty about the attribution is what makes the ledger trustworthy. **Do not invent names you didn't catch** — anonymous-with-descriptor is always better than a guess.
- **Comment / question:** the verbatim or close-paraphrase text of what was said. Use quotation marks when you are quoting; use indirect speech when paraphrasing. If a comment was a full paragraph, capture the gist in two sentences but include the *exact phrasing of the central claim* in quotes. Do *not* rebut, restate-charitably, or sanitize — the comment goes in as-said, even when as-said is uncomfortable.
- **Topic:** the most specific pointer you can — *"slide 3, the parallel-trends defense"* or *"poster middle-right, the spec curve"* or *"paper §4.2, the clustering choice"* — so a future-you reading the ledger can map the comment to the artifact it addressed.
- **Category:** the PS 9.2 five-category taxonomy (identification / robustness / data / interpretation / mechanism). Categorizing forces you to recognize that a vague-sounding comment is, in shape, the same as one of the anticipated-question categories.
- **In-room response given:** what you said back in the moment, summarized in one phrase. Even *"no response, took the question and moved on"* is a row entry. The point is to record what *you* said, so the triage memo can audit whether your in-room response was the right one or whether you wish, in retrospect, you had answered differently.
- **Tone:** a single word — *constructive*, *mixed*, *hostile*. The tone is real information for the triage, because hostile-tone comments are *not* automatically wrong (some of the sharpest feedback is delivered uncharitably) and constructive-tone comments are *not* automatically right (some kind suggestions are off-target). The tone column lets the triage memo separate the *content* of the comment from the *emotional register* it arrived in.

Grading on completeness:

- **Minimum row count (5 pts):** at least **15 rows** for a conference talk + poster session combination. (A pure-poster session at a smaller venue might produce 8–10; a major talk with active Q&A and a poster session might produce 25–30. Use 15 as the floor; if you have 8, your ledger is under-built and you have likely forgotten comments — go back and reconstruct.)
- **Coverage (5 pts):** the rows hit at least 3 of the 5 PS 9.2 categories. A ledger with 15 identification-only rows is unrealistic and suggests you only recorded the comments you felt good about handling; reconstruct the rest.
- **Verbatim discipline (5 pts):** at least 5 rows include direct-quote phrasing (in quotation marks) of the comment, not just paraphrase. The verbatim phrase is what lets the triage memo respond to *what was actually said*, not your charitable restatement of it.

**(b) The "sharpest comment" annotation (10 pts).** Among your ledger rows, mark **one** row as the *sharpest single comment* — the one that, on its own, would most damage your paper if it landed and you could not answer it. The mark is a ⚑ in the # column. Write, immediately under the ledger, a 3-sentence note on:

1. Why this comment was the sharpest (what part of your design or claim it attacked).
2. Whether your in-room response handled it or not.
3. Whether the comment is, on reflection 24 hours later, *correct*. This is hard: a sharp comment can be wrong; a kindly-delivered comment can be right. The annotation forces you to assess content separately from tone.

This is the single highest-value entry in the ledger. The triage memo will revisit it.

**(c) The praise rows (5 pts).** Include at least 2 rows of *praise* the conference offered — a comment of the form *"this is a clean identification strategy"* or *"the poster is the best I've seen at this session"*. Capture them honestly because they will *also* be triaged: positive feedback that points at a specific design choice is signal about what *not* to abandon under pressure from other comments. A common revision failure is to weaken a strong feature of the paper because one critic disliked it, while losing sight of three other reviewers who praised that exact feature. The praise rows are the audit trail against that drift.

**(d) The cold-start rule (5 pts).** Write the ledger *within 24 hours of the conference*. Memory of conference comments decays sharply after one day; what felt like "the obvious central comment" on Monday morning will be a vague impression by Thursday. Note in the ledger header the exact timestamp you started writing it and the timestamp you finished — *"started 2026-08-17 18:30 EDT, four hours after the talk; finished 2026-08-17 21:15 EDT."* The cooler the start time, the better the recall.

---

## Part 2 — Source-venue audit and reconstruction quality (10 points)

Different conference venues produce different feedback densities and qualities, and the ledger is only as good as the venues it covers.

**(a) Venue checklist (5 pts).** Confirm in `feedback-ledger.md` that you have at least one row from *each* of:

- Your talk's Q&A.
- Your poster session.
- At least one hallway / coffee-break / lunch conversation.
- At least one email or message follow-up the day after the conference, if any arrived.

If a venue produced *zero* comments — a poster session where nobody stopped, an empty Q&A — say so, with one sentence on why ("session was scheduled in parallel with the keynote; foot traffic at posters was minimal"). A zero with a reason is honest data; a missing venue without a reason is a gap.

**(b) Reconstruction notes (5 pts).** For each row whose phrasing you reconstructed from memory rather than transcribed in real time (most rows, realistically), note whether the reconstruction is high-confidence (you can almost hear the speaker's voice) or low-confidence (you remember a question was asked but only the gist). A column or footnote suffices. Low-confidence rows are still useful in the ledger — they remind you a comment existed — but the triage memo will weight high-confidence rows more heavily.

---

## Part 3 — The 48-hour triage memo (`triage-memo.md`) (35 points)

The triage memo is written **48 hours after** the conference, not sooner. The 48-hour gap is a feature: it converts the emotional reactions of the conference itself (defensiveness about hostile comments, gratitude about kind ones) into engineering judgments. Note the exact timestamp at the top of the memo.

The memo classifies every row in the ledger into one of three action buckets, with reasons. The format is again a table:

| Ledger # | Comment (one-line restatement) | Bucket (act-now / act-by-W11 / do-not-act) | Reason | Effort estimate | Owner |
|---|---|---|---|---|---|

**(a) The three buckets and what each means (12 pts):**

1. **Act-now (week of the conference).** A *correctable error* the conference caught: a typo on slide 4 that misstated the headline number, a citation that is wrong, a poster panel with an off-by-one footnote. You fix it within the week — not because the conference embarrassed you (it did, slightly, and that's fine) but because the fix is cheap, the error is real, and Week 10's revision should start from a corrected baseline. Typical effort: minutes to hours.
2. **Act-by-Week-11 (revision-window action).** A *substantive change* the conference correctly flagged: a robustness check that should be added (a different clustering, a placebo on never-treated units, a sample window the questioner suggested), a piece of the paper that needs to be rewritten to acknowledge a residual concern more honestly, a citation to a paper you missed. The fix requires a code change, a regression, a new figure, or a section rewrite — work scoped for the Weeks 10–11 refinement window. Typical effort: half a day to two days.
3. **Do-not-act (with reasons).** A comment you have *considered* and decided not to act on, with the reason recorded. Three legitimate reasons:
   - *Out of scope:* the comment asks for an analysis a different paper would do ("have you tried extending this to corporate bonds?"). Out-of-scope is not a dismissal — the comment is real and the paper acknowledging it as future work is the right response, in the contribution slide and the paper's conclusion.
   - *Already addressed:* the comment asks for a check that *is* in your spec curve or robustness, and the in-room response was insufficient. The action is to *cite* the existing check more visibly in the revised paper, not to redo it.
   - *Substantively wrong:* the comment is mistaken about your design or about a fact (a confused recollection of how Callaway-Sant'Anna handles never-treated units, a misreading of your data card). You write down the reason in two sentences. *"Substantively wrong"* is the hardest verdict to deliver honestly — humans are wired to defer to senior commenters — and the rubric rewards naming it when it is right.

The bucket distribution matters. A memo with 100% act-by-Week-11 ratings is overpromising; a memo with 100% do-not-act ratings is defensive; a healthy distribution is roughly 10–20% act-now, 50–70% act-by-Week-11, 20–30% do-not-act-with-reasons. Your distribution may differ; state and justify it.

**(b) Effort estimates and ownership (8 pts).** Every act-now and act-by-Week-11 row has:

- **Effort estimate:** in hours or half-days, your best honest guess. *"4 hours: add not-yet-treated control comparison, regenerate event-study, update slide 5"* is a usable estimate; *"some work"* is not. Estimates are graded on whether they exist, not on whether they prove accurate (the estimating skill itself is a real one; you will revisit and learn from your over-/under-estimates in Week 10).
- **Owner:** who does the work. For solo capstones, this is you on every row, and the column is trivial — but state it. For team projects, the owner column distributes the load.

**(c) The sharpest-comment treatment (10 pts).** The row marked ⚑ in the ledger gets a *dedicated section* in the triage memo — three paragraphs:

1. **Restate the comment in its sharpest, most-charitable form** — not the form the speaker delivered (which may have been uncharitable), but the strongest version of the *underlying critique*. The discipline is reading-as-a-skeptic from Ch 5: convert the comment to the question it should have been.
2. **State your honest 48-hour assessment.** Was the comment right, partly right, or wrong? If right, what does that mean for the paper? If partly right, which part? If wrong, what specifically is the error and how do you know? The 48-hour gap is what lets this assessment be calmer than the in-room response.
3. **State the action.** Almost always *act-now* (if the sharpest comment caught a real error) or *act-by-Week-11* (if the sharpest comment requires a substantive revision). The rare *do-not-act* on the sharpest comment must be justified at length — three sentences minimum — and is itself a high-stakes call: a sharp criticism dismissed without acting *can* be the right move, but it is the move most likely to be wrong, so the rubric weights its justification heavily.

**(d) The praise-row triage (5 pts).** The praise rows from Part 1(c) get their own short treatment: a one-sentence note per praise row stating *which design choice or feature was praised* and *flagging it as a do-not-weaken commitment* for Weeks 10–11. *"The poster's center panel — the headline event-study — was praised by two questioners as 'clean'; do not crowd this figure or replace it during revision."* The praise rows protect the strong features of the paper against well-meaning over-revision.

---

## Part 4 — Feed-forward to PS 10.1 (10 points)

The triage memo is *not* the revision plan — PS 10.1 (Week 10) will produce the actual revision plan with milestones, branches, and figure-by-figure changes. But the triage memo is the *input* to PS 10.1, and the handoff must be clean.

**(a) The act-by-Week-11 list, ordered (6 pts).** At the bottom of `triage-memo.md`, list the act-by-Week-11 rows in *priority order* — most important first, with one sentence on why that ordering. The ordering is your engineering judgment: typically (i) revisions that strengthen identification > (ii) revisions that strengthen robustness > (iii) revisions that strengthen interpretation > (iv) revisions that add citations or polish prose. State your ordering and the principle behind it; PS 10.1 will start from this list.

**(b) The repo handoff (4 pts).** Commit `triage-memo.md` with a message of the form `feedback: triage memo, conference 2026-08-17, N act-now, M act-by-W11, K do-not-act`. The commit is the named, dated, hashable handoff. PS 10.1's revision plan will reference this commit by its short SHA and by the action-row numbers, so revision in Week 10 can audit-trail back to "the comment from Senior Person X at the 2026-08-17 session that prompted this change."

---

## Part 5 — The honest reflection (10 points)

A final short section at the bottom of the triage memo: 250 words on what the conference *taught you about your paper*, separate from any specific action item. The reflection answers three questions, briefly:

1. **What surprised you?** Which comment or question came from a direction you had not anticipated in your PS 9.2 matrix?
2. **What did the conference confirm?** Which part of your design or finding did multiple independent commenters identify as strong (the praise rows are signal)?
3. **What changed in your understanding of the result?** Has the conference shifted, even slightly, how you interpret the headline — not the headline itself (you do not move that under social pressure) but the *meaning* you assign to it?

The reflection is graded on honesty, not depth. A reflection that says *"the conference confirmed what I already knew"* is graded harshly because it is rarely true; a reflection that says *"a comment from a junior PhD student in the poster session made me realize the contribution clause was vaguer than I thought"* is graded well because it identifies a real updating event.

---

## Submission checklist

Before you commit, confirm:

- [ ] `feedback-ledger.md` and `triage-memo.md` are both committed under `paper/feedback/`.
- [ ] The ledger has at least **15 rows** with all 8 columns (#, venue, speaker, comment, topic, category, in-room response, tone).
- [ ] Coverage hits at least 3 of the 5 PS 9.2 categories; at least 5 rows include direct-quote phrasing.
- [ ] The sharpest comment is marked ⚑ with the 3-sentence annotation.
- [ ] At least 2 praise rows are recorded.
- [ ] The ledger header records start and finish timestamps within 24 hours of the conference.
- [ ] Each of the four venues (talk Q&A, poster, hallway, follow-up) has at least one row, or a one-sentence reason for zero.
- [ ] Low-confidence reconstructions are flagged as such.
- [ ] The triage memo is timestamped 48 hours after the conference and classifies every ledger row into act-now / act-by-Week-11 / do-not-act with reasons.
- [ ] Every act-now and act-by-Week-11 row has an effort estimate and an owner.
- [ ] The sharpest-comment row has a dedicated three-paragraph treatment.
- [ ] Praise rows are flagged as do-not-weaken commitments.
- [ ] The act-by-Week-11 list is ordered with a stated principle.
- [ ] The commit message records the conference date and the bucket counts; the 250-word reflection answers the three required questions.

---

## How this is graded

Part 1 (the ledger, 35 — the heaviest part) on completeness, verbatim discipline, and the sharpest-comment annotation. Part 2 (venue coverage, 10) on whether all four venue types are represented or explained. Part 3 (the triage memo, 35) on whether every row is triaged with reasons and the sharpest-comment treatment is honest. Part 4 (handoff to PS 10.1, 10) on whether the priority-ordered list and the named commit exist. Part 5 (reflection, 10) on whether the 250-word reflection identifies a real updating event. The highest-signal single check: **was the sharpest comment recorded verbatim, marked, and either acted on or honestly justified as do-not-act?** A `Y` says you processed the conference as data; a `N` says you let it bounce off you.

---

## The close of Week 9, and the bridge to Weeks 10–12

This problem set closes the conference week. Look back at the arc Week 9 walked: PS 9.1 froze your deck and hashed your packet, so the file you uploaded matched the file you rehearsed; PS 9.2 wrote down the twelve questions you expected; PS 9.3 compressed your identification argument to one figure that would survive projector failure; PS 9.4 explodes the paper onto a 48×36 poster that a hallway viewer reads in 60 seconds; and now PS 9.5 captures what the conference said back and triages it into the revision plan.

Weeks 10–12 are the *paper-refinement* phase of the camp's NextGen calendar — four weeks during which the triage memo's act-by-Week-11 rows become committed code, regenerated figures, and revised prose, and the do-not-act rows become explicit "future work" sentences in the conclusion. The conference is not the finish line; it is the input the camp deliberately delivers to your revision process at the moment your paper has been external-tested for the first time. Most papers are *more honest* after that test — the residual concerns named in your PS 9.5 reflection become the explicit limitations of the Week 12 final paper, and the praise becomes the contribution you defend without hedging. That is the work of Weeks 10–12. PS 9.5 is the input it needs.

*End of PS 9.5. The model deliverable is in `book/appendices/E-solutions-manual/E-w9-ps9.5-solutions.md`. Write your own ledger and triage memo first; read the exemplar to calibrate, not to copy. The conference is data, and the ledger-plus-triage is how you turn data into the next four weeks of work — this assignment is you doing that processing on purpose, with the cooling-off period the discipline requires.*
