# Model Deliverable — PS 9.5 (Post-Conference Feedback Ledger and 48-Hour Triage Memo)

**Problem set:** `book/weeks/week-09/ps9.5.md` (PS 9.5, Week 9).
**Chapter:** Ch 9.5 — After the Conference: Feedback as Data.

PS 9.5 has no numeric answer key: it is a project deliverable, and what is graded is whether the ledger is complete, attributed, and verbatim where possible, and whether the 48-hour triage memo classifies every ledger entry into act-now / act-by-Week-11 / do-not-act with reasons. So this appendix entry is not a worked solution but a **model deliverable**: a complete, A-grade `feedback-ledger.md` and `triage-memo.md` pair for one cast project (Devon's spot-Bitcoin-ETF event study, the same project used as the running example in PS 9.1), with instructor grading notes keyed to the rubric.

The project is **Devon's spot-Bitcoin-ETF event study** — the daily-frequency cumulative-abnormal-return-on-volatility design. The conference is the GMU Camp 2026 symposium on 2026-08-17. Every comment below is **illustrative** — phrased as a plausible question or critique a real conference Q&A would produce, mapped onto Devon's specific paper. The point of the exemplar is the *form* of the ledger and the *discipline* of the triage, not the literal content; a student running the assignment after their own symposium produces their own rows.

---

## THE MODEL DELIVERABLE

### Part A — `feedback-ledger.md`

```
# Feedback Ledger — Devon R., spot-Bitcoin-ETF event study
# Conference: GMU Camp 2026 Symposium, 2026-08-17
# Ledger writing window: started 2026-08-17 18:30 EDT (4h after talk);
#                        finished 2026-08-17 21:15 EDT (2h 45m of writing).
```

| # | Source venue | Speaker | Comment / question (verbatim or paraphrase) | Topic (slide / panel) | Category | In-room response | Tone |
|---|---|---|---|---|---|---|---|
| 1 | talk Q&A | senior faculty, front row (name caught: Prof. K. Bergstresser, Brandeis) | *"Was the SEC approval really a surprise? Prediction markets had it at 90% for weeks."* | slide 3 (design) | identification | answered with the placebo on the 3 prior false-rumor dates from `qa-script.md` Q1; backup A shown | constructive |
| 2 | talk Q&A | PhD student, back row (name not caught, descriptor: "tall, white shirt, asked first follow-up") | *"What's your event-window? You said 20 days but the placebo windows were shorter."* | slide 4 (headline) | data | clarified that the placebo windows are *fake event dates*, not different windows; the 20-day window is the same in all robustness specs | constructive |
| 3 | talk Q&A | mid-career researcher, middle row (name caught: Dr. L. Chen, GMU finance) | *"How does your daily-frequency CAR compare to an intraday approach? The Gao Han Li Zhou 2018 paper would say intraday is much cleaner here."* | slide 6 (contribution) | mechanism | acknowledged the trade-off; pointed at the Backup C intraday-version slide with -10.2% vs. -9.1% daily; said the daily version is reported because intraday data is licensed and not in the packet | mixed |
| 4 | talk Q&A | senior academic, middle row (name caught: Prof. M. Robinson, GMU finance) ⚑ | *"I'm not convinced your placebo is the right placebo. The prior false-rumor dates already had elevated implied volatility — your placebo can't reject the null because the null itself was contaminated."* | slide 5 (robustness) | identification | gave a 2-sentence answer; suggested it was a fair concern; promised to think about a better placebo set | mixed |
| 5 | talk Q&A | early-career, side aisle (name not caught) | *"Beautiful talk. The contract-form sentence on slide 3 was the clearest framing I've seen at this symposium."* | slide 3 (design) | praise | thanked, moved on | constructive |
| 6 | talk Q&A | senior, front row, second question (Prof. K. Bergstresser) | *"What's your robustness to the choice of return-model? Fama-French market-model vs. a constant-mean adjustment?"* | slide 5 (robustness) | robustness | said "yes, ran both; backup B has the spec curve including the choice; sign is identical" — pointed at spec curve | constructive |
| 7 | poster session | small-bank-research analyst, briefly | *"How do you handle the futures-vs.-spot basis on event days? On the SEC release day the basis blew out."* | poster middle-right (robustness) | data | did not have a prepared answer; said it was a fair point and would look at it | mixed |
| 8 | poster session | grad student, longer conversation (name caught: Aisha N., U Chicago Booth) | *"Have you tried this for the Ether spot ETF launches in 2024? Same mechanism should apply."* | poster bottom-center (contribution) | mechanism | gave the located-I-don't-know answer from `qa-script.md`; pointed at the FUTURE-WORK note | constructive |
| 9 | poster session | senior, "looks like a chairperson, didn't introduce himself" (anonymous descriptor) | *"Your strategy assumes 1bp transaction cost. That's institutional; retail pays 5-10 bp on bitcoin spreads. Your effect dies for retail."* | poster top-right (headline) | interpretation | low-confidence reconstruction: agreed in the moment that retail costs are higher; did not push back | hostile |
| 10 | poster session | junior faculty, name caught (Dr. R. Patel, NYU Stern, but visiting) | *"The fact that the spec curve has all 16 specs significant is suspicious — that's too tight. Are you sure you're not over-clustering?"* | poster middle-right (robustness) | robustness | defended the cluster-by-event-date choice; said the unclustered version is in the spec curve and is *also* significant; offered to show backup D | mixed |
| 11 | poster session | early-career, brief stop, name not caught | *"Really clean poster — the headline figure with the CI band is the best example of that style I've seen today."* | poster middle-center (headline figure) | praise | thanked | constructive |
| 12 | hallway, coffee break | senior, side conversation (Prof. K. Bergstresser, follow-up to Q1) | *"Just to follow up — the prediction-market data is publicly available from Kalshi. Worth including as a covariate for the surprise component of the announcement."* | (not on any slide; new methodological idea) | identification | thanked for the suggestion; said it would go on the revision list | constructive |
| 13 | hallway, lunch | peer student (Sam, fellow camper) | *"The spec curve panel is amazing. Don't let the Q4 critic talk you out of it."* | poster middle-right | praise | thanked; noted in head | constructive |
| 14 | email follow-up | Prof. M. Robinson (the Q4 critic) | *"I want to follow up on my comment — I realize the placebo dates I pushed on aren't all the same in IV terms; some had elevated IV, some did not. Could you sort the placebo dates by IV-on-the-day and report the placebo CAR conditional on that sort?"* | follows-up on slide 5 / Q4 | identification | acknowledged the email; said I would add the analysis to the Week-11 revision | constructive |
| 15 | email follow-up | Aisha N. (the Ether-ETF questioner from Q8) | *"Here's the Ether spot ETF approval date file if you decide to extend. github.com/aishan/ether-etf-events"* | extension/future work | mechanism | thanked, bookmarked, said it might be Week-11 if time permits | constructive |

**Total rows: 15** (PS 9.5 floor is 15). **Verbatim rows: 8** (rows 1, 2, 3, 4, 7, 8, 10, 12, 14 — 9 actually). **Categories covered:** identification (5), data (2), robustness (2), interpretation (1), mechanism (3), praise (3) — all 5 PS 9.2 categories plus a praise bucket. ✓

**The sharpest comment annotation (Part 1(b)):** Row 4 (⚑) is marked as the sharpest. The note:

> *"Prof. Robinson's comment is the sharpest because it targets the validity of the placebo itself — the central robustness check on slide 5 and the line of defense on identification slide 3. If the placebo dates are contaminated (already had elevated IV), the placebo cannot reject the null, and my 'placebos don't fire' defense from PS 9.2 Q1 is undermined.*
> *In-room I gave a weak 2-sentence answer and conceded too quickly — should have asked 'what would convince you the placebo is valid?', which would have located the critique. The follow-up email (Row 14) is the more constructive version of the same comment and provides a specific fix.*
> *On reflection 24 hours later: the comment is **correct**. The placebo set should be sorted by IV-on-the-day and reported conditionally. This is an act-by-Week-11 item; the headline survives but the robustness section needs strengthening."*

**Praise rows (Part 1(c)):** Rows 5, 11, 13. Three praise comments — about the contract-form sentence on slide 3, the headline-figure CI-band design, and the spec curve. All three are signal about *what not to weaken under pressure from the critical comments*.

### Part B — `triage-memo.md`

```
# Triage Memo — Devon R., spot-Bitcoin-ETF event study
# Drafted: 2026-08-19 14:00 EDT (48h after talk)
# Reading the ledger 48 hours later, with calmer head.
```

| Ledger # | Comment (one-line restatement) | Bucket | Reason | Effort | Owner |
|---|---|---|---|---|---|
| 1 | "Was the SEC approval a surprise?" | act-by-W11 | strengthen by adding Kalshi prediction-market series as a covariate (per Row 12) | 6h | Devon |
| 2 | "What's your event-window?" | do-not-act | already addressed in slide 4 caption and paper §3.2; re-read slide caption to ensure clarity | 0.5h | Devon |
| 3 | "Daily vs. intraday cleanliness" | act-by-W11 | add explicit paragraph in paper §2 explaining the daily-choice rationale (data availability, replication packet); cite Gao Han Li Zhou 2018 | 2h | Devon |
| 4 ⚑ | "Placebo dates were contaminated" | act-by-W11 | sort placebo dates by IV-on-the-day; report placebo CAR conditional on the IV-sort (per Row 14 email) | 8h | Devon |
| 5 | praise on contract-form sentence | do-not-act | DO NOT WEAKEN: contract-form sentence on slide 3 is reinforced by multiple praises | — | — |
| 6 | "Return-model choice (FF vs constant-mean)" | do-not-act | already in spec curve (backup B); add visible cite in paper §3.3 | 0.5h | Devon |
| 7 | "Futures-spot basis on event days" | act-by-W11 | compute basis-adjusted CAR for the 5 SEC event days; add as Backup H slide | 4h | Devon |
| 8 | "Try for Ether ETF launches" | do-not-act | OUT OF SCOPE for this paper; add as explicit future-work sentence in conclusion; thank Aisha N. by name in acknowledgments | 0.5h | Devon |
| 9 | "Retail transaction costs higher than 1bp" | act-now | re-check the 1bp assumption: the paper text reads "1bp institutional"; the slide says "1bp" without qualification; FIX SLIDE on the conference packet to read "1-3bp depending on counterparty" | 1h | Devon |
| 10 | "Spec curve too tight, over-clustering?" | do-not-act | SUBSTANTIVELY WRONG: the cluster-by-event-date choice is correct because treatment turns on at the event-date level; the unclustered version is *also* significant (in the spec curve); this critic confused tight CIs with mis-clustered ones. Note: do not change clustering. | — | — |
| 11 | praise on headline-figure CI band | do-not-act | DO NOT WEAKEN: keep the CI-band visual on slide 4 and on the poster middle-center | — | — |
| 12 | "Add Kalshi prediction-market data" | act-by-W11 | merged with row 1; same action | (in row 1) | Devon |
| 13 | praise on spec curve | do-not-act | DO NOT WEAKEN: keep the spec curve as the slide 5 / poster middle-right | — | — |
| 14 | follow-up email from Row 4 critic | act-by-W11 | merged with row 4; same action | (in row 4) | Devon |
| 15 | Ether ETF event-date file from Aisha N. | do-not-act | OUT OF SCOPE for the immediate paper; bookmark for a possible Week-11 stretch extension if time; thank Aisha in acknowledgments | 0.5h | Devon |

**Bucket distribution:**

- act-now: 1 (Row 9)
- act-by-W11: 6 (Rows 1, 3, 4, 7, 12, 14 — though 12 and 14 merge into 1 and 4, so 4 distinct actions)
- do-not-act: 8 (Rows 2, 5, 6, 8, 10, 11, 13, 15)

That distribution is roughly 7% / 40% / 53% by row count, but counting *distinct actions*, the act-by-W11 bucket is 4 actions (rows 1+12, 3, 4+14, 7). Devon's distribution is leaner on act-now than the PS 9.5 suggested range (10-20%) because the conference caught only one correctable error (the slide qualification on 1bp) — which is honest data, not a mis-triage. The act-by-W11 share is at the low end of the suggested range (50-70%), reflecting that Devon's paper was already well-vetted via the spec curve and the PS 9.2 anticipated-questions matrix.

### The sharpest-comment treatment (Part 3(c)):

**Restatement in the sharpest, most-charitable form.** Prof. Robinson's critique, at its sharpest: "Your placebo test claims the headline result is not an artifact of the estimator, because placebo dates do not produce the same magnitude. But your placebo dates are *not chosen at random* — they are the prior false-rumor dates, which were exactly the dates on which the implied-volatility surface was elevated and the market was 'priced' for a possible approval. A placebo that has the same selection mechanism as the true event is no placebo at all; it is a contaminated null distribution, and your test fails to reject for the same reason a sandbagged audit fails to find fraud."

**Honest 48-hour assessment.** The comment is **correct**. The placebo dates were chosen because they were rumor-dates with elevated IV, which is what makes them rumor-dates. The placebo therefore does not test "would a random non-event date produce the same CAR?" — it tests "would a rumor-date produce the same CAR as the true approval date?", which is a different question. The original placebo is still informative (it tests against a *harder* null than a random date), but it is not what the slide claimed it was. Devon's in-room answer conceded too quickly without locating the critique; the follow-up email (Row 14) is the more constructive version and points at the fix.

**Action.** Act-by-Week-11. The fix has two parts: (i) add a *random-date* placebo set (truly non-event dates, sampled with replacement from the trading-day calendar), to test the "random non-event" null; (ii) sort the existing rumor-date placebo by IV-on-the-day, reporting the placebo CAR conditional on the IV-sort, per the email suggestion. Both extensions strengthen rather than weaken the paper. Effort estimate: 8 hours. The headline result survives in either case; what changes is the framing of what the placebo establishes.

### The praise-row treatment (Part 3(d)):

- Row 5 (contract-form sentence on slide 3): **do-not-weaken commitment.** The PS 9.2 archetypal-question defense rested on this sentence; keep it.
- Row 11 (headline-figure CI band on slide 4): **do-not-weaken commitment.** Keep the CI-band visualization on the paper's headline figure and on the poster.
- Row 13 (spec curve as slide 5 / poster middle-right): **do-not-weaken commitment.** Keep the spec curve; do not collapse it to a single robustness table.

### Part C — Feed-forward to PS 10.1 (Part 4)

The act-by-Week-11 list, ordered by priority for the Week 10 revision plan:

1. **Row 4+14 — IV-sorted placebo and random-date placebo.** Highest priority: strengthens identification, addresses the sharpest comment. ~8h.
2. **Row 1+12 — Add Kalshi prediction-market data as surprise covariate.** Second priority: strengthens identification on the same axis (whether the announcement was a surprise). ~6h.
3. **Row 7 — Futures-spot basis adjustment.** Third priority: strengthens robustness on the event days; clean win. ~4h.
4. **Row 3 — Daily vs. intraday rationale paragraph.** Fourth priority: interpretation/exposition fix; cite Gao Han Li Zhou 2018 explicitly. ~2h.

Total estimated act-by-W11 effort: ~20 hours over 4 weeks. The principle of the ordering: (i) revisions that strengthen identification (Rows 4, 1) > (ii) revisions that strengthen robustness (Row 7) > (iii) revisions that strengthen interpretation (Row 3). Within (i), the sharpest-comment fix comes first.

The repo handoff commit message:

```
feedback: triage memo, conference 2026-08-17;
1 act-now, 4 act-by-W11 (distinct), 8 do-not-act-with-reasons.
Sharpest comment (Row 4, Prof. Robinson) → act-by-W11 with IV-sorted
placebo + random-date placebo set. PS 10.1 revision plan starts here.

Co-Authored-By: Claude Opus 4.7 <noreply@anthropic.com>
```

### Part D — The 250-word honest reflection (Part 5)

> The conference surprised me twice. First, the **placebo critique from Prof. Robinson (Row 4)** came from a direction my PS 9.2 matrix had under-prepared for. I had anticipated *"was the announcement a surprise?"* (Q1 in my matrix), but I had not anticipated the meta-question *"is your placebo set itself a valid null distribution?"* — a critique aimed not at the announcement's surprise content but at the choice of placebo dates. That is a more sophisticated version of the same identification concern, and it produced the largest single update to my paper: the random-date placebo set I will add in Week 10 makes the robustness claim more honest than it was on stage.
>
> Second, the conference *confirmed* two things I had been uncertain about. Multiple independent commenters praised the contract-form identifying-assumption sentence on slide 3 (Rows 5, 13). I had been worried that the sentence read as too cautious; the conference's response was the opposite — caution read as credibility. I will not weaken the sentence during revision. The headline-figure CI band (Row 11) was praised by a hallway viewer as the best of the session, which is signal that the *figure choice* (a CI band, not a point estimate alone) is the right one for this paper and worth carrying into other presentations.
>
> What changed in my understanding: the *meaning* of the headline shifted slightly. I went in thinking the result was "ETF launches reduce spot-volatility, period." I leave thinking the result is "ETF launches reduce spot-volatility *under a placebo that is harder to defend than I claimed on stage*, and the right framing acknowledges both the headline magnitude and the placebo's limitations." That is a sharper, less-confidently-stated, more-defensible version of the same result. Word count: 297. *(Adjusted to 250 in the committed version; this draft is left verbose to show the structure.)*

The reflection is 297 words in this draft, slightly above the 250 cap; the committed version is trimmed to 252 words. The substance — naming the surprise (Robinson's meta-placebo critique), the confirmation (the contract-form sentence praise), and the meaning-shift (more-defensible-but-less-bold framing) — is what the rubric rewards.

---

## INSTRUCTOR GRADING NOTES

### Where this deliverable earns full marks

- **Part 1 (ledger, 35/35 — the heaviest part).** Fifteen rows, all eight columns, verbatim phrasing on at least nine rows including the sharpest comment. The ⚑ on Row 4 with the three-sentence annotation that honestly says "the comment is correct and my in-room answer was weak." Three praise rows (5, 11, 13). The ledger header records the start and finish timestamps within 24 hours of the conference.
- **Part 2 (venue audit, 10/10).** All four venues represented (talk Q&A: 6 rows; poster: 5 rows; hallway: 2 rows; email follow-up: 2 rows). One row (Row 9) flagged as low-confidence reconstruction.
- **Part 3 (triage memo, 35/35).** Every ledger row triaged with a reason. Bucket distribution honest (1/4/8 — leaner on act-now than the typical range, but the conference caught only one correctable error). The sharpest-comment treatment is three paragraphs: charitable restatement, 48-hour assessment ("correct"), action. The praise rows are explicitly flagged as do-not-weaken commitments — protecting against revision-pressure drift in Weeks 10–12.
- **Part 4 (handoff, 10/10).** The act-by-Week-11 list is ordered with a stated principle (identification > robustness > interpretation), effort estimated, and the commit message names the date and bucket counts.
- **Part 5 (reflection, 10/10).** Identifies a real updating event (the meta-placebo critique that wasn't anticipated), names what the conference confirmed (the contract-form sentence and the CI-band figure), and names a meaning-shift in the result's framing.

### What loses points (illustrative)

- A ledger that includes only the comments the student felt good about handling. The rubric catches this in the "tone" column distribution — a ledger with zero "hostile" or "mixed" rows is unrealistic for a real conference Q&A and suggests selective recording.
- A ledger written four days later. Memory has decayed; the rows read like impressions rather than quotes; the verbatim count is low. The cold-start rule is the discipline that produces a usable ledger.
- A triage memo with 80% act-by-Week-11 ratings. This is overpromising; the student will not deliver. The rubric rewards an honest distribution that includes substantive do-not-act rows with reasons.
- A do-not-act row that says "this is wrong" without explaining why. *"Substantively wrong"* is the hardest verdict to deliver honestly, and the rubric requires it to be *explained*, not asserted. Row 10 in Devon's memo does this correctly: the explanation names the confusion (the critic mistook tight CIs for mis-clustered ones) and the evidence (the unclustered version is also significant).
- The sharpest-comment treatment that says "the critic was wrong because…" The rubric weights this against the deliverable: the sharpest comment is *by definition* the one most likely to be right, and dismissing it requires a much higher bar of justification than acting on it. If the student's sharpest-comment row is do-not-act, the three paragraphs must reach the same standard of rigor that a methods section reaches.

### The highest-signal single check

**Was the sharpest comment recorded verbatim, marked, and either acted on or honestly justified as do-not-act?** Devon's deliverable: Row 4 is verbatim, marked ⚑, and triaged as act-by-Week-11 with a specific 8-hour action and an honest acknowledgment that the in-room response was weak. A `Y` says he processed the conference as data; a `N` says he let the sharpest comment bounce off him and the revision plan is starting from a defended-position rather than from an honest-update position.

*End of model deliverable. The ledger and triage memo above are one shape PS 9.5 can take; the structure (15+ ledger rows with 8 columns, ⚑-marked sharpest comment, 48-hour triage with reasons, sharpest-comment treatment, praise-row commitments, ordered act-by-W11 list, 250-word reflection) is required of any submission, but the specific comments and decisions are conference- and paper-specific. The point of reading the exemplar is to calibrate the standard of verbatim discipline and triage honesty, not to copy any specific row into a project that had a different conference.*
