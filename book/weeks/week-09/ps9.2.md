# PS 9.2 — Anticipated-Questions Matrix for Your Paper

**Course:** 8-Week Empirical Finance Camp · Week 9 · Problem Set 9.2
**Covers:** Ch 9.2 (Reading the Room: Anticipating Questions), building on Ch 7.5 (the identification memo and its threats-and-responses table), Ch 8.4 (peer review and revision), and PS 8.5 Part 3 (defending identification under questions). Uses no notebook: this is a written matrix you build by sitting in the chair of a hostile-but-fair reader of your paper and writing down what they would ask.
**Type:** Project deliverable, not a numeric problem set. You produce a single Markdown file — `qa-matrix.md` — containing a minimum of **twelve** anticipated questions about your capstone, each mapped (i) to the slide where it will most likely land, (ii) to the backup slide that holds the answer's evidence, and (iii) to the four-part prepared response (threat → plausible → what you did → residual concern). There is no single right answer because the answer is *your* paper's question landscape, not a number — and what is graded is whether the matrix is *complete* (covers the five canonical question categories), *honest* (includes the questions you fear, not just the ones flattering to your design), and *mapped* (each row points to a specific slide and a specific backup slide that *exist* in your deck).

**Total: 100 points.** Point values are stated per part. A model deliverable — a 14-question matrix for one cast project (Sam's intraday-momentum event study), with instructor grading notes keyed to the rubric — is in Appendix E (`E-w9-ps9.2-solutions.md`). Read it *after* you draft your own, the way Ch 9.2 walked through Sam's matrix: not to copy, but to calibrate.

A boundary to hold throughout. The matrix is not a substitute for *answering* the question well in the moment; it is the *preparation* that makes the in-the-moment answer possible. A talk you have rehearsed against 12 questions will not be derailed by a 13th — because you will have *practiced the shape* of an honest answer, and the 13th will fit one of the same five categories. Conversely, a talk that has prepared answers to zero questions in writing will be derailed by the first one, because you will be inventing the shape in real time, on stage, with a stranger watching. The whole apparatus is a defense against the moment of panic that converts a defensible result into a flailing one.

---

## What you submit

A single Markdown file, `qa-matrix.md`, committed to your capstone repository alongside `paper/slides-vfinal.pdf` and `paper/slides-notes.md`. The file has exactly five sections, in this order:

1. **The five categories and your taxonomy** — the framework you used to ensure coverage (Part 1).
2. **The matrix itself** — at least **12 questions**, in table form, each with the five required columns (Part 2).
3. **The slide-and-backup map** — a small diagram or table that shows which slides hold which backup material (Part 3).
4. **The two hardest questions, expanded** — the two from the matrix you expect to get and find hardest, written as full prose answers (Part 4).
5. **The honest gaps** — questions you cannot fully answer and what you will say (Part 5).

The whole file is three to four pages plus the matrix table. The matrix is the heart of the deliverable; the prose around it is the *justification* for the matrix's design and the *practice text* for the two hardest answers.

---

## Part 1 — The five categories of conference question (15 points)

Ch 9.2 §1 named the five canonical categories that every empirical-finance Q&A draws from. Your matrix must demonstrate coverage of all five, with at least two questions in each of categories 1–3 (identification, robustness, data) and at least one in categories 4–5 (interpretation, mechanism). The categories, restated:

1. **Identification questions** — *"Isn't your estimate just picking up [confounder]?"* The structural attack on the comparison; the rows of your Ch 7.5 threats table become the rows here. Every identification design has its archetypal version: parallel trends for DiD, exclusion-restriction violation for IV, manipulation around the cutoff for RD, donor-pool selection for synthetic control. You **must** include at least one question of the archetypal form for *your* design.
2. **Robustness questions** — *"Does the result survive [alternative analytic choice]?"* Different clustering, alternative outcome scaling, dropped years, alternative samples. These are *survivable* questions (PS 8.5 Part 3c): a re-clustered SE that moves the t-statistic from 3.2 to 2.8 does not kill your claim. They are pre-empted by your spec curve (PS 8.1).
3. **Data questions** — *"How did you construct [variable X]?"* and *"Why this sample window?"* The audience asking these does not yet trust the dataset; the answer is operational and short, and the backup is usually a data-card snapshot.
4. **Interpretation questions** — *"Is the magnitude economically meaningful?"* and *"How should we read 1.8 percentage points?"* The audience asking does trust the number but wants help sizing it. The answer is in human units; the backup is usually a baseline comparison.
5. **Mechanism questions** — *"By what channel does X cause Y?"* The most ambitious category, and often the trap: a strong reduced-form result is not a mechanism, and pretending otherwise overclaims. The honest answer often names a plausible channel *and* says what would be needed to identify it separately.

**(a) Coverage statement (8 pts):** at the top of `qa-matrix.md`, list the five categories and, beneath each, the count of questions in your matrix that belong to it. The minimum thresholds (2-2-2-1-1, summing to 8 of your 12) are floors, not targets. If you have only one robustness question, you have not anticipated enough of the survivable attacks; go back and add. Coverage is what makes the matrix *complete*; without it, the matrix is a list of questions you happen to have thought of, not a defense.

**(b) Why these five (4 pts):** in two or three sentences, state why these five (and not three, not seven) are the right taxonomy for *your* paper. A pure machine-learning prediction paper might compress mechanism into interpretation; a structural model might split identification into "is the model identified" and "are the moments hit." Most empirical-finance capstones use the five as stated.

**(c) The category you fear most (3 pts):** name the one category where you feel your defense is weakest, and write one sentence stating *why*. Most papers fear *identification*; some — text-heavy projects, for example — fear *data*; few honestly fear mechanism enough. Naming the fear is not weakness; it is the act that makes the matrix's coverage in that category *more*, not less, careful.

---

## Part 2 — The matrix itself: minimum 12 questions (40 points)

The heart of the deliverable. Build a table with exactly these columns:

| # | Category | Question (as a stranger would ask it) | Slide it lands on | Backup slide | Four-part answer (threat → plausible → what you did → residual) |
|---|---|---|---|---|---|

The five columns each carry a discipline:

- **Question** — phrase it *as a stranger would ask it*, not as you would charitably restate it. *"Isn't your effect just picking up the trend in algorithmic underwriting?"* — six seconds, the way it would be said standing at a microphone — not "I considered whether the underlying technological trend in lender automation could confound my treatment indicator." The bluntness is the point: rehearse the version you will actually hear.
- **Slide it lands on** — slide *number*, not a vague "results section." Identification questions usually land on the design/identification slide (slide 3); robustness on slide 5; data on slide 1 or 2; interpretation on slide 4; mechanism on slide 6. If a question lands "on no slide because the talk does not cover it," that is the row that tells you to add a sentence to the talk or to add a backup slide.
- **Backup slide** — the slide you will *navigate to* in answer (or "verbal only" if the answer is short enough that no slide is needed). Every identification and robustness row should point to a backup slide that actually exists; if it does not, build it now.
- **Four-part answer** — the PS 8.5 Part 3 template, in compressed form. Each cell holds:
  - **Threat:** what the questioner is worried about (their fear, charitably restated).
  - **Plausible:** the one phrase acknowledging *why* their worry is reasonable — *"yes, that's the central worry"* — never dismissed.
  - **What you did:** the test, the design choice, the spec curve fork, the placebo — the column-3 of your Ch 7.5 table.
  - **Residual:** the column-4 honest concession of what you still cannot fully rule out.

**(a) The minimum twelve, by category (24 pts).** At least 12 rows total, hitting the floor counts in Part 1(a). Score: 2 pts per honestly written, category-correct row up to 12. A row that misclassifies its category (a "robustness" question that is actually a mechanism question) loses half its points; a row whose question is sanitized — phrased as you wish it were asked, not as it will be — loses points for honesty.

**(b) The archetypal-for-your-design row (8 pts).** One row must be the archetypal identification question for *your* design, exactly as the chair of a session would ask it:

| Design | The archetypal question |
|---|---|
| Difference-in-differences | "Are pre-trends really parallel? Your treated states look like they were diverging before the policy." |
| Instrumental variables | "Why is [the instrument] excludable from the outcome equation other than through [the treatment]?" |
| Regression discontinuity | "What stops actors from manipulating their position around the cutoff?" |
| Event study (market) | "Was the event actually a surprise on that date — and how do you know?" |
| Synthetic control | "Why is your donor pool a credible counterfactual for [the treated unit]?" |
| Cross-sectional with controls | "What's the experiment? Why should this be causal rather than correlational?" |

Your row uses *this exact phrasing* (or a faithful variant) for *your* design; the four-part cell is your prepared answer. This is the question most likely to land; it is the one you must rehearse most.

**(c) The hardest-to-answer row, marked (4 pts).** Among your 12, mark the **one** row you find hardest to answer. The mark is a single ⚑ or [HARDEST] tag in the # column. This row gets its full prose expansion in Part 4. Marking it is the act that prevents you from drifting toward easier questions in rehearsal — the conference will not let you choose which questions you get.

**(d) No padding (4 pts).** A matrix padded with *easy* questions (the ones you can answer in your sleep) is graded *harder*, not easier, because it conceals the work the matrix exists to do. If three of your 12 rows are versions of "how is mortgage denial defined" with three different phrasings, the rubric collapses them to one and you have only 10. Each row must be *substantively distinct*: a different worry, a different evidence base, a different cell-3 answer.

---

## Part 3 — The slide-and-backup map (15 points)

A small diagram or table that makes the *physical layout* of your defense legible at a glance.

**(a) Slide-to-questions map (8 pts).** A table with one row per slide (slides 0–6 plus backups) and a column listing which question numbers from your matrix land on that slide:

| Slide | Title (full-sentence claim) | Anticipated questions (matrix #) |
|---|---|---|
| 3 (design) | "Our estimate is credible if…" | Q1 (parallel trends), Q4 (selection on treatment timing), Q7 (clean-control choice) |
| 5 (robustness) | "The result is stable across…" | Q3 (clustering), Q9 (window), Q11 (placebo) |

Reading this table downward tells you *where the heat will be*. If a slide has zero questions mapped to it, ask yourself: is the slide pulling its weight? If it has six, ask yourself: have I budgeted enough verbal time for that slide?

**(b) Backup-slide inventory (5 pts).** A short list of every backup slide your deck contains, with one sentence on what each backup answers:

- **Backup A — regression table (Appendix D format).** Answers data-pedantic and "what's the standard error" questions.
- **Backup B — Goodman-Bacon decomposition.** Answers "is your staggered DiD's negative weights doing the work" questions.
- **Backup C — placebo distribution.** Answers "is the result an artifact of the estimator" questions.
- **Backup D — pre-trends with confidence bands.** Answers parallel-trends questions in numerical form.

Every identification and robustness row in your matrix must point to a backup that *exists* in this list. If a row points to a backup not in the list, you must *build the backup*, not edit the matrix. The matrix drives the deck, not the other way around.

**(c) Cut-line awareness (2 pts).** State, in one sentence, which backup slides you can navigate to *during* the talk (with a slide-number keystroke or a hyperlink) versus which you would only show in Q&A. The headline figure backup (the full regression table) is usually Q&A only; the pre-trends panel might be reachable mid-talk if the design slide invites the question. Knowing which is which prevents the seven-second panic of fumbling for backup C while the room watches.

---

## Part 4 — The two hardest questions, expanded (20 points)

Take the one row you marked ⚑ in Part 2(c) plus *one more* — your second-hardest. Write each as a full prose answer, the way you will deliver it aloud. About 100–150 words each.

**(a) Hardest question, full prose answer (10 pts).** Begin with the *acknowledgment* — *"Yes, that's the central worry"* — never with "But." Then walk the four parts in order: name the threat, concede why it is plausible, describe the design choice or test that addresses it, and *name the residual concern* honestly. End with one sentence pointing at the backup slide that holds the supporting evidence: *"backup slide C shows the placebo distribution and the real estimate sitting in the tail."* The whole answer fits in 45 seconds spoken.

The grading focuses on the *acknowledgment-first* discipline and the *residual* honesty. An answer that opens with "But actually…" loses points; an answer that pretends the residual is zero loses *more* points, because the audience will recognize the pretense and the credibility damage compounds. The model deliverable in Appendix E shows the form.

**(b) Second-hardest question, full prose answer (10 pts).** Same template. The repetition is deliberate: rehearsing two answers in the same shape makes the shape automatic, so when the *third* hardest question comes — the one you did not anticipate — your mouth produces the four-part shape before your brain catches up.

---

## Part 5 — The honest gaps (10 points)

The matrix's most-revealing entries are the questions you *cannot* fully answer. Ch 9.2 §4 named the discipline: an honest *located* "I don't know" is more credible than a manufactured answer.

**(a) Two located "I don't know" rows (6 pts).** Add to the matrix (or call out from it) **two** questions whose four-part cell, in the "what you did" column, honestly reads *"my design cannot speak to this; here is what I can say and what I cannot."* The form is the PS 8.5 Part 3(b) template:

> *"I don't know — that's outside what my design can speak to, because [reason]; my guess is [direction], but I'd want to [specific check] before claiming it."*

The two rows are not weaknesses; they are *credibility moves*. A reviewer who sees a researcher locate the edge of their evidence trusts the researcher's claims *inside* the edge more, not less.

**(b) The retreat position (4 pts).** State, in a single sentence at the bottom of the matrix, the retreat position you will use if a fatal critique lands — the concession-and-survives sentence from PS 8.5 Part 3(c). *"If parallel trends fail at the magnitude the critic claims, we cannot claim causal; what we have shown is a stable empirical regularity that future work with [the better design] should test causally."* This sentence is *not* in the matrix as a question; it is the safety net under the matrix, written once, ready when needed.

---

## Submission checklist

Before you commit, confirm:

- [ ] `qa-matrix.md` has all five sections (categories · matrix · map · two hardest · gaps), in order.
- [ ] The matrix has **at least 12 questions** with the floor coverage (≥2 identification, ≥2 robustness, ≥2 data, ≥1 interpretation, ≥1 mechanism).
- [ ] Each row has all five columns filled, and the questions are phrased *as a stranger would ask them*, not as you wish they were asked.
- [ ] The **archetypal-for-your-design** question is present and uses the exact (or faithful-variant) phrasing for your identification strategy.
- [ ] The **hardest-to-answer row** is marked ⚑ and gets its prose expansion in Part 4.
- [ ] Every identification and robustness row points to a backup slide that *exists* in your deck; missing backups have been *built*, not deleted from the matrix.
- [ ] The slide-to-questions map shows which slides hold which questions; the backup inventory names what each backup answers.
- [ ] Both prose answers in Part 4 begin with *acknowledgment*, walk the four parts in order, name a *residual* honestly, and end pointing at the backup slide.
- [ ] Two **located "I don't know"** rows exist, with the *"outside what my design can speak to"* form.
- [ ] The retreat position is one sentence at the bottom of the matrix.

---

## How this is graded

Part 1 (coverage and taxonomy, 15) on whether the five categories are present at the floor counts. Part 2 (the matrix, 40 — the heaviest part) on whether the 12+ questions are honest, category-correctly classified, mapped to slides, and use the four-part template. Part 3 (slide-and-backup map, 15) on whether the physical defense plan exists and the backups it points to exist in the deck. Part 4 (two hardest expanded, 20) on whether the prose answers use the acknowledgment-first / residual-honest discipline. Part 5 (honest gaps, 10) on whether two located "I don't know"s and the retreat-position sentence are present. The highest-signal single check: **does the archetypal-for-your-design question appear in the matrix with a prepared four-part answer and a backup slide?** A `Y` says you have anticipated the question that will most likely land; a `N` says you have not, and the rubric weights it accordingly.

---

## The bridge to PS 9.3

PS 9.2 gives you twelve questions and the backups that answer them; PS 9.3 collapses the *whole* defense onto a single object — the *one figure* that, if every other slide were lost, would still carry the identification argument. The matrix you built here is the *menu* of attacks; the one-figure defense in PS 9.3 is the *single* piece of evidence that survives every attack at once. Building it forces you to ask which piece of your design is so load-bearing that, without it, the talk is not the talk.

*End of PS 9.2. The model deliverable is in `book/appendices/E-solutions-manual/E-w9-ps9.2-solutions.md`. Write your own matrix first; read the exemplar to calibrate, not to copy. The questions you write down before the conference are the questions you can answer; the ones you don't write down are the ones that will surprise you — this assignment is you converting the second set into the first.*
