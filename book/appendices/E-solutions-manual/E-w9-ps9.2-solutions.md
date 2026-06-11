# Model Deliverable — PS 9.2 (Anticipated-Questions Matrix for Your Paper)

**Problem set:** `book/weeks/week-09/ps9.2.md` (PS 9.2, Week 9).
**Chapter:** Ch 9.2 — Reading the Room: Anticipating Questions.

PS 9.2 has no numeric answer key: it is a project deliverable, and what is graded is whether the matrix is complete (covers the five categories), honest (includes the questions you fear, not just the flattering ones), and mapped (each row points at a specific slide and backup slide that *exist*). So this appendix entry is not a worked solution but a **model deliverable**: a complete 14-question matrix for one cast project (Sam's intraday-momentum event study, designed to mirror the Gao-Han-Li-Zhou 2018 *JFE* result on first-half-hour returns predicting last-half-hour returns), with full prose answers for the two hardest questions and instructor grading notes keyed to the rubric.

The project is **Sam's intraday-momentum event study** — a refresher-style replication-and-extension of Gao, Han, Li & Zhou (2018), *Journal of Financial Economics* 129:394–414. Sam's question: *does the first half-hour return on SPY predict the last half-hour return, and does the predictability survive accounting for trading costs and recent regime breaks?* Primary estimate is a Newey-West-adjusted predictive regression coefficient on 15-minute SPY data, sample 2014–2024. Every magnitude below is **illustrative**, presented as a worked *matrix* example to show what A-grade row entries and prose answers look like, not as a claimed empirical finding (the published numbers belong to Gao, Han, Li & Zhou 2018, and Sam's replication recovers them up to sampling); a student running `make all` on the real pinned data gets the real numbers.

---

## THE MODEL DELIVERABLE — `qa-matrix.md`

### 1. The five categories and Sam's taxonomy

Coverage statement (PS 9.2 Part 1(a)):

- **Identification:** 4 questions (Q1, Q4, Q5, Q9) — floor is 2 ✓
- **Robustness:** 3 questions (Q2, Q7, Q11) — floor is 2 ✓
- **Data:** 2 questions (Q3, Q6) — floor is 2 ✓
- **Interpretation:** 2 questions (Q8, Q12) — floor is 1 ✓
- **Mechanism:** 3 questions (Q10, Q13, Q14) — floor is 1 ✓

Total: **14 questions** (PS 9.2 minimum is 12).

Why these five for this paper: Sam's intraday-momentum design is a *predictive* exercise resting on a time-series identification (the first half-hour's information being predictive of the last half-hour's, conditional on a market-microstructure mechanism). The five categories all apply directly — there is no compression of mechanism into interpretation because the *mechanism* (who is trading in the last 30 minutes, and why their flow correlates with the open) is itself the most-discussed feature of the published paper.

The category Sam fears most: **mechanism**. The reduced-form predictability is robust; the story about *why* (late-day institutional rebalancing) is harder to identify cleanly, and the most senior potential audience member at the camp's symposium (the published paper's author is *the camp instructor*) will ask exactly this. The matrix's three mechanism rows are accordingly the longest-prepared.

### 2. The matrix itself

| # | Category | Question (as a stranger would ask it) | Slide # | Backup slide | Four-part answer (threat → plausible → what you did → residual) |
|---|---|---|---|---|---|
| 1 | identification | **"Is this just a coding error? Are you sure the first half-hour return doesn't leak into the last half-hour through your timestamps?"** | 3 | Backup A (data dictionary) | T: timestamp leakage would mechanically produce predictability. P: it's the first thing anyone would suspect. W: I use exchange-stamped TAQ minute bars; the first-half-hour return ends at 10:00:00 ET, the last-half-hour starts at 15:30:00 ET, with 5h 30m of separation. R: I cannot fully rule out that some aggregator's reporting lag could blur boundaries on holiday-shortened days; I drop holiday-shortened days as a robustness, no change. |
| 2 | robustness | **"What happens if you use 5-minute or 1-minute bars instead of 30-minute?"** | 5 | Backup B (spec curve) | T: the predictability could be an artifact of the 30-min aggregation. P: yes, that's a defensible robustness check. W: I ran 1-min, 5-min, 15-min, and 30-min; the predictive coefficient is positive and significant at all four; the spec curve clusters at the 30-min headline. R: at 1-min, microstructure noise widens the CI, but the sign and significance hold; this is the bottom-right corner of the spec curve. |
| 3 | data | **"Why SPY and not /ES or SPX? The futures market is open longer and has fewer microstructure issues."** | 2 | (verbal) | T: futures would be a cleaner instrument. P: yes, /ES has tighter spreads. W: I use SPY because retail-accessible products are the policy-relevant unit, and TAQ data is reproducible in the packet; I re-ran on /ES futures as a robustness in backup, same sign. R: SPY tracking error vs. /ES is non-trivial intraday on volatile days; this widens my CI by ~10% relative to /ES. |
| 4 | identification ⚑ | **"Aren't you just rediscovering known calendar effects — Fed days, OPEX Fridays, holiday-shortened sessions — that have nothing to do with intraday momentum?"** | 3 | Backup C (Fed/OPEX dummy regressions) | T: known calendar anomalies could drive predictability. P: this is the central confound; it's why intraday momentum is hard to publish. W: I include Fed-day, OPEX-Friday, and holiday-shortened indicators interacted with the open-period return; the headline coefficient on the open-return survives at 80% of its baseline magnitude after the interactions. R: I cannot fully eliminate anomalies I have not named; my magnitude under all known calendar controls is a lower bound. |
| 5 | identification | **"What's your overlapping-period correction? With 15-minute bars over 10 years you have a serial-correlation nightmare in your residuals."** | 3 | Backup D (Newey-West vs. Bartlett kernels) | T: classical SEs would massively overstate t-statistics. P: this is correct and standard. W: I use Newey-West with bandwidth = 4 (Andrews 1991 plug-in selection on the residuals); the t-statistic on the open-return coefficient is 4.2 under Newey-West, vs. 12.8 under classical (which is wrong). R: bandwidth choice is a fork; the spec curve in Q2 varies bandwidth 2–8 and the t-statistic stays above 3. |
| 6 | data | **"How do you handle the 2020 COVID volatility shock? That period could be doing all the work."** | 5 | (verbal, point at Backup B) | T: 2020 could be an outlier driving the result. P: it was the most volatile year in the sample. W: I dropped 2020 entirely as a robustness; the headline coefficient moves from 0.082 to 0.075, the same sign and significance. The spec curve in Q2 includes drop-2020 as one of the forks; it sits in the cluster. R: dropping any single year reduces statistical power slightly; results are not as tight without 2020 but are not driven by it. |
| 7 | robustness | **"What about transaction costs? Once you account for the bid-ask spread, does the strategy actually make money?"** | 6 | Backup E (net-of-cost Sharpe) | T: a strategy with positive gross alpha can have zero net alpha. P: this is the standard practical critique. W: I compute net-of-cost returns assuming 1 bp round-trip on SPY (conservative for retail); the net Sharpe is 0.41, down from gross 0.68. The strategy survives a 3-bp assumption; it dies at 5 bp. R: a retail trader paying spread-plus-commission on Robinhood pays ~2 bp; an institution pays <0.5 bp; this is implementable for institutions but marginal for retail. |
| 8 | interpretation | **"Is 8.2 basis points per day actually economically meaningful? Sounds tiny."** | 4 | (verbal, with the Sharpe quote from Q7) | T: small-coefficient effects can be statistically real but economically negligible. P: 8.2 bps does sound small in isolation. W: 8.2 bps per day, when realized in the last 30 minutes of trading on a strategy that is in the market only 30 minutes a day, annualizes to a Sharpe of 0.68 — well above SPY buy-and-hold (0.45 in-sample). The right unit is Sharpe, not basis-points-per-day. R: realized Sharpe in out-of-sample 2020–2024 is 0.51; the in-sample Sharpe is an upper bound. |
| 9 | identification | **"How do you know your sample isn't contaminated by look-ahead bias from index reconstitutions or dividend timing?"** | 3 | Backup F (reconstitution check) | T: index events could mechanically create open-to-close patterns. P: this is a real concern in long-horizon strategies. W: reconstitutions affect SPY by a tiny weight rebalancing on quarterly Fridays; I include a reconstitution-Friday indicator, no change in coefficient. Dividends are ex-distribution dates; I exclude the 4 quarterly ex-div days, no change. R: corporate-action timing is the threat I am least certain about; I do not have a clean instrument for it. |
| 10 | mechanism | **"What's the mechanism? Why would the first half-hour predict the last half-hour?"** | 6 | (verbal, then point at Backup G) | T: a reduced-form result without a mechanism is descriptive, not causal. P: this is the question Gao Han Li Zhou (2018) is most known for. W: the leading mechanism in the literature is late-day institutional rebalancing — closing auctions and market-on-close orders flow in a direction correlated with the morning's information. I show that the predictability is stronger on days with above-median closing-auction volume, consistent with this. R: I cannot identify the mechanism cleanly with intraday returns alone; my evidence is consistent with the rebalancing story but does not pin it down against alternatives like inventory-management by market makers. |
| 11 | robustness | **"What's your clustering? Standard errors clustered by day are different from clustered by week, and predictive regressions are notorious for overstated SEs."** | 5 | Backup B (spec curve), Backup D | T: clustering choice can move the t-statistic substantially. P: the predictive-regression SE literature is exactly about this. W: my primary is Newey-West with bandwidth 4. I also computed (i) cluster-by-day, (ii) cluster-by-week, (iii) Hodrick (1992) overlapping-data correction; the t-statistic ranges 3.8 to 4.5 across the four; all reject zero at 5%. R: under more aggressive bandwidth choices (NW bw=20), the t-statistic falls to 2.9; this is the edge case I cite as my robustness boundary. |
| 12 | interpretation | **"If this works, why doesn't everyone do it? Why hasn't it been arbitraged away?"** | 6 | (verbal) | T: a profitable, persistent predictability should attract capital and disappear. P: the efficient-markets prior says it should. W: trade is costly (Q7); the strategy is in the market only 30 minutes a day so capacity is limited; institutional rebalancing flow is exogenous to a predictor's strategy. The published paper's coefficient (Gao Han Li Zhou 2018) is positive on out-of-sample data through 2014; my 2014–2024 sample is also out-of-sample relative to their data and recovers the effect. R: if institutional rebalancing changes (e.g., closing-auction rules shift), the predictability could fade; I see no decay trend in my sub-period estimates. |
| 13 | mechanism | **"Could this be a behavioral story — retail investors trading on the open, sophisticated investors trading on the close?"** | 6 | (verbal) | T: a behavioral story would be a non-rational alternative mechanism. P: the retail-vs.-institutional flow distinction is well documented. W: the rebalancing-flow mechanism in Q10 is itself partly behavioral (anchoring on the morning's information). I cannot separate "rational rebalancing on news arrival" from "behavioral momentum-chasing" with my data. R: distinguishing the two would require order-level data linking trader IDs to flow direction — outside my packet. |
| 14 | mechanism | **"Does this work in international markets — does the FTSE-100 first half-hour predict its own close?"** | 6 | (verbal) | T: a mechanism-claim should generalize if the mechanism is real. P: yes, this is the standard cross-market test for a mechanism. W: out-of-scope for this paper; the published paper (Gao Han Li Zhou 2018) does test cross-market and finds similar effects in some indices and not others, with cross-sectional variation that lines up with closing-auction structure. R: I do not extend cross-market; this is the most reasonable "future work" extension I would name. |

**(c) The hardest-to-answer row — Q4** (⚑). The calendar-effects-confound question is the one that, on its own, would most damage the paper: if the predictability comes entirely from Fed days and OPEX Fridays, the open-period coefficient is an artifact, and the published-paper replication claim does not hold. Sam's defense (controls + lower-bound framing) is real but the residual is meaningful.

**(d) No padding.** Each row is substantively distinct: a different worry (timestamp leakage, bar-frequency, ticker choice, calendar effects, serial correlation in SEs, COVID outlier, transaction costs, economic magnitude, look-ahead, mechanism, clustering, why-not-arbitraged, behavioral alternative, cross-market). No two rows can be collapsed.

### 3. The slide-and-backup map

**(a) Slide-to-questions map:**

| Slide | Title (full-sentence claim) | Anticipated questions (matrix #) |
|---|---|---|
| 0 (title) | *Does the First Half-Hour Predict the Last Half-Hour? Replicating Gao Han Li Zhou (2018)* | — |
| 1 (question) | *Does the first half-hour return on SPY predict the last half-hour return?* | — |
| 2 (why) | *If yes, intraday momentum is a free lunch that markets keep missing — or a story about who trades when.* | Q3 (why SPY) |
| 3 (design) | *Our predictive coefficient is causal-of-late-day-return if the open-period return is not contaminated by leakage or known calendar effects.* | Q1, Q4 ⚑, Q5, Q9 |
| 4 (headline) | *The first half-hour return predicts the last half-hour return with coefficient 0.082 (NW t = 4.2), out-of-sample 2014–2024.* | Q8 |
| 5 (robustness) | *The result is stable across bar frequency, sample sub-periods, and clustering choices.* | Q2, Q6, Q11 |
| 6 (contribution) | *Intraday momentum is a robust empirical regularity consistent with late-day rebalancing flow; we do not identify the mechanism cleanly against behavioral alternatives.* | Q7, Q10, Q12, Q13, Q14 |
| Backup A | data dictionary + timestamp diagram | Q1 |
| Backup B | spec curve (4 bar frequencies × 4 clustering × 3 sample windows) | Q2, Q11 |
| Backup C | Fed/OPEX/holiday dummy regressions | Q4 |
| Backup D | NW vs. Hodrick vs. cluster-by-day | Q5, Q11 |
| Backup E | net-of-cost Sharpe under 1, 3, 5 bp | Q7 |
| Backup F | reconstitution + ex-div day robustness | Q9 |
| Backup G | closing-auction volume sort | Q10 |

**(b) Backup-slide inventory:** seven backup slides exist in the deck, each named above. Every identification and robustness row in the matrix points at a backup that exists. Cross-check: Q1→A ✓, Q2→B ✓, Q4→C ✓, Q5→D ✓, Q7→E ✓, Q9→F ✓, Q10→G ✓, Q11→B+D ✓.

**(c) Cut-line awareness:** Backups A, C, F are navigation targets *during* the talk (slide-number hyperlinks set up in Beamer). Backups B, D, E, G are Q&A-only. The headline regression table (a hypothetical Backup H showing the coefficient with four decimals) is *not* in the deck — Sam decided the spec curve in B and the figure on slide 4 are the visual answer; the four-decimal table lives in the paper, not on a slide.

### 4. The two hardest questions, expanded

**4(a) Hardest question — Q4 (calendar effects):**

> *"Yes, that's the central worry — Fed days and OPEX Fridays are exactly the kind of calendar anomaly that can mechanically produce predictability between morning and afternoon, and the intraday-momentum literature has spent twenty years separating real predictability from calendar artifacts. Here's what I did: I included interactions of the open-period return with three calendar indicators — Fed-announcement day, OPEX-Friday, and holiday-shortened session — running the predictive regression jointly. The coefficient on the open-return survives at 0.066 — about 80% of its baseline magnitude of 0.082 — and remains significant with a Newey-West t-statistic of 3.4. So the calendar anomalies absorb some of the predictability, as they should, but they do not eliminate it. What I cannot fully rule out is calendar anomalies I have not named — earnings-announcement clusters, monthly fund-flow timing, anything I did not think to include. My defense there is that my robustness magnitude is the lower bound on the true effect, not the upper bound. Backup slide C has the full table."*

(150 words; reads aloud in ~45 seconds. Opens with the acknowledgment, walks the four parts in order, names the residual honestly, ends pointing at the backup slide.)

**4(b) Second-hardest — Q10 (mechanism):**

> *"This is the question the published paper (Gao Han Li Zhou 2018) is most defined by, and the honest answer is that I have a reduced-form result and a *consistent* mechanism, not an identified one. The leading story in the literature is late-day institutional rebalancing — market-on-close orders and closing-auction flow line up in the direction of the morning's information, because institutional traders who saw the news at 9:30 are deciding by 15:30 how to reposition. I test this by sorting days on closing-auction volume from NYSE: on above-median-volume days the predictive coefficient is 0.106; on below-median days it is 0.061. The relative magnitude is consistent with the rebalancing story. What I cannot do is rule out alternative mechanisms — market-maker inventory management, or a purely behavioral momentum-chasing story — without order-level data linking trader IDs to direction. That data is licensed at order-level and not in my packet, so I scope the contribution to the reduced form. Backup G has the volume-sort regression."*

(180 words; reads aloud in ~55 seconds. Same template; the residual concern is sharper because mechanism is genuinely harder.)

### 5. The honest gaps

**5(a) Two located "I don't know" rows:**

- **Q14 — cross-market generalization.** *"I don't know — my design can't speak to that. I have only U.S. SPY data; the published paper finds intraday momentum in some international indices and not others, with cross-sectional variation that correlates with closing-auction structure. My guess is that the effect is present in markets with concentrated closing-auction flow (UK, Germany) and weaker in markets without (some Asian markets). I'd want to re-run on each index's local data with its own bar timestamps before claiming any of that."*
- **Q13 — behavioral vs. rational mechanism.** *"I don't know — distinguishing 'rational rebalancing on news arrival' from 'behavioral momentum-chasing' would require order-level data linking trader IDs to flow direction. That data is licensed at order-level and not in my packet. My guess is that the truth is some weighted average of both, but I cannot put numbers on the weights. I'd want either signed-trade data or a trader-ID identifier before claiming one over the other."*

**5(b) The retreat position (one sentence):**

> *"If the calendar-anomaly critique is right that all of my predictability comes from named-or-unnamed anomalies, then I cannot claim intraday momentum in the SPY index; what I have shown — at minimum — is that the morning-to-afternoon correlation in SPY returns is robust to bar-frequency, sample, and clustering choices, and future work with a clean exogenous-news instrument can test whether the residual after all anomalies is genuinely a momentum effect or a refined calendar one."*

---

## INSTRUCTOR GRADING NOTES

### Where this deliverable earns full marks

- **Part 1 (categories and taxonomy, 15/15).** All five categories hit the floor counts (4-3-2-2-3, sum 14). The fear-statement — mechanism — is specific to *this* paper's design, not a generic worry. The why-these-five sentence is paper-specific.
- **Part 2 (the matrix, 40/40 — the heaviest part).** Fourteen rows, each with all five columns, each substantively distinct. Questions are phrased as a stranger would ask them (Q4's *"aren't you just rediscovering known calendar effects"* has the bluntness of an in-room delivery; the four-part answers compress the threats-and-responses table from Sam's Ch 7.5 identification memo). The archetypal-for-design row is present (Q4 — the standard predictive-regression confound for intraday-momentum work). The ⚑ mark on Q4 is justified by the in-room damage potential.
- **Part 3 (map, 15/15).** Every backup slide referenced by the matrix exists in the deck inventory; the cross-check confirms it. The cut-line awareness (which backups are mid-talk vs. Q&A-only) is concrete, not vague.
- **Part 4 (two hardest expanded, 20/20).** Both prose answers open with acknowledgment, walk the four parts in order, name a residual honestly, and end pointing at the backup slide. The Q10 mechanism answer carries the additional difficulty of conceding "consistent with, not identified," which is exactly the calibration the contribution slide requires.
- **Part 5 (honest gaps, 10/10).** Two located *"I don't know"s* in the *"outside what my design can speak to, because [reason]; my guess is [direction], but I'd want to [check]"* form. The retreat position is one sentence that concedes the fatal critique and names what survives.

### What loses points (illustrative)

- A matrix with 12 rows where three are restatements of "how do you define your outcome variable" with cosmetic variations. The rubric collapses them to one row; you have 10 substantively distinct questions and lose Part 2(d) points.
- A row whose four-part cell omits the residual concern column — "...so this completely addresses the worry." The rubric calls this dishonest closure: every real threat has a residual, and pretending otherwise loses honesty points.
- An archetypal-for-design question phrased softly. *"To what extent do you consider potential calendar-effect confounds?"* loses points; *"Aren't you just rediscovering known calendar effects?"* earns them. The bluntness is the point.
- A backup slide referenced by the matrix that does not exist in the deck. The rubric requires you to *build the backup*, not edit the matrix; missing backups are graded as a failure to map.
- A prose answer that opens with "But actually…" instead of "Yes, that's the central worry." The acknowledgment-first discipline is what keeps the room with you; opening with rebuttal loses both the room and the points.

### The highest-signal single check

**Does the archetypal-for-your-design question appear in the matrix with a prepared four-part answer and a backup slide?** Sam's deliverable: Q4 ✓, with the four-part answer and Backup C. A `Y` says he has anticipated the question that will most likely land; he has rehearsed it; the supporting evidence is in the deck. A `N` would have flagged the single largest gap in the defense.

*End of model deliverable. The 14-question matrix above is one shape PS 9.2 can take; the structure (five sections, five-category floor coverage, four-part answers, archetypal question, two-hardest-expanded, located I-don't-knows, retreat position) is required of any submission, but the questions themselves are paper-specific. The point of reading the exemplar is to calibrate the standard of phrasing-honesty and four-part discipline, not to copy any specific row.*
