# Table of Contents — *Empirical Finance from the Ground Up*
### A Textbook, Lab Manual, and Problem-Set Bank for the GMU 12-Week Empirical-Finance Research Camp

**Host:** Prof. Lei Gao, Associate Professor of Finance, Costello College of Business, George Mason University
**Feeds:** NextGen FinTech Scholars / Data Science Young Scholars Research Program (Schar School)
**Audience:** mathematically gifted U.S. high-school students (AP Calc BC + AP Stats; some Python)

> **How to read this TOC.** Every line item carries a word-count estimate `[~N w]`. Prose chapters
> count finished prose only (worked examples included; code listings counted as their explanatory
> prose). Problem sets count problem statements **plus** the fully worked solutions that live in
> Appendix E. Notebooks count their markdown narration + code comments + "Your Turn" prose (cell
> counts shown separately, e.g. `~22 cells`). Per-week subtotals and a grand total appear at the end.
> Citations follow `CONVENTIONS.md §6`; anything unverified is tagged **[CHECK]**.

---

## FRONT MATTER

| # | Item | Description | Est. words |
|---|------|-------------|-----------|
| FM-0 | **Title page, copyright, dedication** | GMU / Costello / Schar branding; CC-BY-NC license note | 300 |
| FM-1 | **Preface** (by Prof. Gao) | Why empirical finance, why high-schoolers can do real research, what the camp feeds into; grounded in verified CV facts | 1,700 |
| FM-2 | **Articulation Matrix** (Camp ↔ NextGen) | 2-page matrix: 12-week camp aligned to the real NextGen program (12 wks, Fri 12–2 EST, Jun 26–Sep 11 2026; CRSP/Compustat/EDGAR/Bloomberg; Claude/ChatGPT; Schar Young Scholars Journal + GMU MARS; awards ≤ $2,000). Phase 1 (Weeks 1–7) ↔ instructional core; Phase 2 (Week 8 of NextGen) ↔ Week 9 symposium; Phase 3 (NextGen Weeks 9–12) ↔ Weeks 10–12 paper refinement | 1,800 |
| FM-3 | **How to Use This Book** | Daily rhythm; how chapters/problems/notebooks/labs/mentor sessions interlock; the reveal-the-trick structure; the recurring student cast (Maya, Devon, Priya, Sam, Leah) | 1,800 |
| FM-4 | **Prerequisite Self-Test** | 20 questions (calculus, probability/stats, light Python) + full solutions + routing table ("missed these → read Appendix A/B first") | 4,500 |
| FM-5 | **Notation & Conventions quick-card** | One-page reproduction of the `CONVENTIONS.md` notation table + spec-discipline checklist | 700 |
| FM-6 | **Roadmap diagram + dependency graph (prose)** | Narrative walkthrough of the 12-week arc — Weeks 1–8 instructional core, Week 9 symposium, Weeks 10–12 paper refinement — and how skills compound | 1,100 |

**Front Matter subtotal: ~11,900 words**

---

# THE 12-WEEK ARC

> Each week contains: (1) a week-opening narrative, (2) **five** chapters, (3) **five** daily problem
> sets (~6 problems each; solutions in Appendix E), (4) a **notebook per chapter** with a "Your Turn"
> extension, (5) a lab manual (Weeks 1–4, 7–12) or reading guides (Weeks 5–6), (6) a 60-minute **Lei
> Gao mentor session**, and (7) an **end-of-week assessment with rubric**. Weeks 1–8 are the
> **instructional core** (NextGen Phase 1 + symposium transition); **Week 9** is the **symposium
> week** (NextGen Phase 2, ~Aug 14); **Weeks 10–12** are the **paper-refinement arc**
> (NextGen Phase 3, Aug 21 – Sep 11).

---

## WEEK 1 — Probability, Sampling, and the Logic of Inference
**Theme:** Rebuild probability and frequentist inference from the ground up, using simulation as the
microscope, so OLS in Week 2 rests on solid foundations.

- **W1 Opening narrative** — From "the average return was 8%" to "what could we have seen instead?": randomness as the object of study. `[~1,300 w]`

**Chapters**
- **Ch 1.1 — Joint, Conditional, and the Two Laws That Run Everything.** Joint/marginal/conditional distributions; independence; the Law of Iterated Expectations and Law of Total Variance, with a portfolio-decomposition worked example (Sam). `[~5,200 w]`
- **Ch 1.2 — Expectations, Variance, Covariance as Geometry.** Linearity of expectation, variance/covariance algebra, correlation as a cosine; covariance matrices previewed. Maya's two-asset budget. `[~4,800 w]`
- **Ch 1.3 — Estimators and Their Sampling Distributions.** Estimator vs. estimate; bias, variance, MSE, consistency; the sampling distribution of the mean by simulation. `[~5,000 w]`
- **Ch 1.4 — The LLN and the CLT, Shown Not Asserted.** Weak LLN; CLT; Monte Carlo convergence plots; when the CLT is slow (heavy tails, crypto returns — Devon). `[~5,400 w]`
- **Ch 1.5 — Hypothesis Testing Done Right.** Null/alternative, size, power, the t-test derived; confidence intervals as inverted tests; one- vs. two-sided; effect sizes. `[~5,600 w]`

**Daily Problem Sets** (≈6 problems each; solutions → Appendix E)
- **PS 1.1** Conditional probability & LIE/LTV drills `[~2,200 w]`
- **PS 1.2** Expectation/variance algebra + correlation geometry `[~2,000 w]`
- **PS 1.3** Bias/variance/MSE of estimators (analytic + simulated) `[~2,300 w]`
- **PS 1.4** CLT/LLN simulation experiments `[~2,400 w]`
- **PS 1.5** Power & size calculations, CI construction `[~2,300 w]`

**Notebooks** (one per chapter; markdown + code + "Your Turn")
- **nb1.1** LIE/LTV by simulation `[~1,400 w / ~20 cells]`
- **nb1.2** Covariance matrices & correlation heatmaps `[~1,300 w / ~18 cells]`
- **nb1.3** Sampling-distribution explorer `[~1,500 w / ~22 cells]`
- **nb1.4** CLT/LLN convergence animations `[~1,600 w / ~24 cells]`
- **nb1.5** Power curves & the t-test from scratch `[~1,500 w / ~22 cells]`

- **Lab 1 (Lab Manual): "Build a Coin-Flip Universe."** Simulate sampling distributions, verify CLT, measure empirical size/power of a test you wrote yourself. `[~3,400 w]`
- **Mentor Session 1 (Lei Gao):** *"What is a finding?"* — pre-read packet (a 1-page excerpt framing), 3 Socratic warm-ups, 5-slide deck, 3 stretch questions tied to Intraday Momentum (Gao, Han, Li & Zhou 2018), post-session reflection prompt. `[~2,200 w]`
- **Assessment W1 + rubric** — short-answer + a mini-simulation task; analytic rubric. `[~1,800 w]`

**Week 1 subtotal: ~62,000 words** *(chapters 26,000 · problems 11,200 · notebooks 7,300 · lab 3,400 · mentor 2,200 · assessment 1,800 · narrative 1,300 · overhead/figures prose ~8,800)*

---

## WEEK 2 — The OLS Engine
**Theme:** Ordinary least squares in matrix form, its guarantees (Gauss–Markov, FWL), and the three
ways the textbook story breaks (heteroskedasticity, clustering, misspecification).

- **W2 Opening narrative** — A regression is a machine with knobs; this week we open the case. `[~1,300 w]`

**Chapters** (technical week — longer)
- **Ch 2.1 — OLS in Matrix Form.** $\mathbf{y}=\mathbf{X}\boldsymbol\beta+\boldsymbol\varepsilon$; the normal equations; $\hat{\boldsymbol\beta}=(\mathbf{X}'\mathbf{X})^{-1}\mathbf{X}'\mathbf{y}$ as projection; geometry of the hat matrix. `[~6,200 w]`
- **Ch 2.2 — Gauss–Markov and the Meaning of "Best."** The five assumptions stated as testable claims; BLUE; what "efficient" buys you; unbiasedness vs. consistency. `[~6,000 w]`
- **Ch 2.3 — The Frisch–Waugh–Lovell Theorem.** Partialling-out; controls as residualization; why FWL is the key to reading every multivariate coefficient; demeaning = fixed effects preview. `[~6,400 w]`
- **Ch 2.4 — When the Errors Misbehave: Heteroskedasticity, Clustering, HC/HAC.** Robust SEs (HC1/HC2/HC3), clustered SEs, Newey–West (HAC); Petersen (2009) panel-SE taxonomy; why your t-stat lies. `[~6,800 w]`
- **Ch 2.5 — Misspecification: OVB, Measurement Error, Functional Form.** Omitted-variable-bias sign analysis; attenuation from classical measurement error; RESET & functional-form diagnostics; the bias–consistency ledger. `[~6,600 w]`

**Daily Problem Sets**
- **PS 2.1** Matrix-OLS derivations + numerical inversion `[~2,400 w]`
- **PS 2.2** Gauss–Markov assumption-breaking diagnostics `[~2,300 w]`
- **PS 2.3** FWL by-hand partialling-out exercises `[~2,400 w]`
- **PS 2.4** Robust/clustered/HAC SE computation + comparison `[~2,500 w]`
- **PS 2.5** OVB sign predictions + measurement-error simulation `[~2,400 w]`

**Notebooks**
- **nb2.1** OLS from scratch with NumPy vs. statsmodels `[~1,600 w / ~24 cells]`
- **nb2.2** Gauss–Markov Monte Carlo (efficiency demo) `[~1,500 w / ~22 cells]`
- **nb2.3** FWL residualization, visualized `[~1,500 w / ~22 cells]`
- **nb2.4** SE flavors on a clustered panel `[~1,700 w / ~24 cells]`
- **nb2.5** Biased-estimator lab (simulate OVB & attenuation) `[~1,700 w / ~24 cells]`

- **Lab 2 (Lab Manual): "Replicate a Textbook Fama–MacBeth on CRSP."** Two-pass cross-sectional regressions; rolling betas; FM standard errors; pin CRSP snapshot date; licensed-data-on-GMU-infra note. `[~4,200 w]`
- **Mentor Session 2 (Lei Gao):** *"Why your standard error is the whole ballgame."* Pre-read packet, 3 warm-ups, 5-slide deck, 3 stretch questions tied to Petersen (2009) and Gao's panel work, reflection. `[~2,200 w]`
- **Assessment W2 + rubric** — derive-and-interpret + a small replication; rubric. `[~2,000 w]`

**Week 2 subtotal: ~68,000 words** *(chapters 32,000 · problems 12,000 · notebooks 8,000 · lab 4,200 · mentor 2,200 · assessment 2,000 · narrative 1,300 · overhead/figures prose ~6,300)*

---

## WEEK 3 — Causal Inference I: Potential Outcomes, Selection-on-Observables, and Instruments
**Theme:** Correlation is cheap; the Rubin causal model makes "effect" precise, and we earn causal
claims through design, not control variables.

- **W3 Opening narrative** — Maya's loan-approval puzzle: why "controlling for income" isn't enough. `[~1,400 w]`

**Chapters** (technical week — longer)
- **Ch 3.1 — Potential Outcomes, SUTVA, and the Fundamental Problem.** Treatment effects (ATE/ATT/LATE); the missing counterfactual; SUTVA; selection bias decomposed. `[~6,400 w]`
- **Ch 3.2 — Selection on Observables I: Matching & Propensity Scores.** Conditional independence; nearest-neighbor & caliper matching; PSM; common support; balance diagnostics. `[~6,400 w]`
- **Ch 3.3 — Selection on Observables II: Entropy Balancing & Doubly-Robust Estimation.** Entropy balancing (Hainmueller); IPW; AIPW/doubly-robust estimators; why "doubly" robust. `[~6,600 w]`
- **Ch 3.4 — Instrumental Variables.** Relevance & exclusion; 2SLS as FWL-with-an-instrument; LATE interpretation; weak instruments — first-stage F, Stock–Yogo critical values, Olea–Pflueger effective F. `[~7,000 w]`
- **Ch 3.5 — Reading IV in the Wild + The Weak-IV Pathology.** Anderson–Rubin inference; many-instruments bias; a guided reproduction of a weak-instrument disaster. `[~6,400 w]`

**Daily Problem Sets**
- **PS 3.1** Potential-outcomes algebra; selection-bias decomposition `[~2,400 w]`
- **PS 3.2** Hand-matching + propensity-score estimation `[~2,500 w]`
- **PS 3.3** Entropy-balancing weights + AIPW by hand `[~2,500 w]`
- **PS 3.4** 2SLS derivation + weak-IV F diagnostics `[~2,600 w]`
- **PS 3.5** Anderson–Rubin CIs; instrument-validity critique `[~2,400 w]`

**Notebooks**
- **nb3.1** Simulating potential outcomes & selection bias `[~1,600 w / ~22 cells]`
- **nb3.2** PSM with balance diagnostics `[~1,700 w / ~24 cells]`
- **nb3.3** Entropy balancing vs. IPW vs. AIPW `[~1,700 w / ~24 cells]`
- **nb3.4** 2SLS with `linearmodels`; first-stage F `[~1,700 w / ~24 cells]`
- **nb3.5** Weak-IV pathology reproduction `[~1,800 w / ~26 cells]`

- **Lab 3 (Lab Manual): "Reproduce a Weak-IV Pathology."** Build a DGP where 2SLS is badly biased toward OLS; show Olea–Pflueger effective-F flags it; contrast with a strong instrument. `[~4,200 w]`
- **Mentor Session 3 (Lei Gao):** *"Natural experiments: finding the lever nature pulled."* Tied to Deng, Gao & Kim (2020) short-sale natural experiment. Pre-read, 3 warm-ups, 5-slide deck, 3 stretch questions, reflection. `[~2,200 w]`
- **Assessment W3 + rubric.** `[~2,000 w]`

**Week 3 subtotal: ~70,000 words** *(chapters 32,800 · problems 12,400 · notebooks 8,500 · lab 4,200 · mentor 2,200 · assessment 2,000 · narrative 1,400 · overhead/figures prose ~6,500)*

---

## WEEK 4 — Causal Inference II: DiD, RD, Synthetic Control, and Shift-Share
**Theme:** The modern panel/quasi-experimental toolkit — and the recent literature showing the
"obvious" estimators are often wrong.

- **W4 Opening narrative** — A state changes a law; did it change behavior? Priya's climate-insurance shock. `[~1,400 w]`

**Chapters** (technical week — longer)
- **Ch 4.1 — Difference-in-Differences & Event Studies.** 2×2 DiD; parallel-trends assumption (and how to interrogate it); event-study/leads-and-lags specification; pre-trend tests. `[~6,600 w]`
- **Ch 4.2 — The Staggered-Adoption Crisis.** Why TWFE is biased under heterogeneous timing: Goodman-Bacon decomposition; the negative-weights problem (de Chaisemartin–D'Haultfœuille); Sun–Abraham, Callaway–Sant'Anna, and Borusyak–Jaravel–Spiess estimators. `[~7,200 w]`
- **Ch 4.3 — Regression Discontinuity.** Sharp & fuzzy RD; local polynomial estimation; bandwidth choice (Imbens–Kalyanaraman, Calonico–Cattaneo–Titiunik robust bias-corrected); McCrary density test; RD validity threats. `[~7,000 w]`
- **Ch 4.4 — Synthetic Control & Synthetic DiD.** Abadie's synthetic control; donor pools & placebo inference; Arkhangelsky et al. synthetic DiD; when one treated unit is all you have. `[~6,400 w]`
- **Ch 4.5 — Bartik / Shift-Share Designs.** Shift-share instruments; the Borusyak–Hull–Jaravel exposure-weights view; Goldsmith-Pinkham–Sorkin–Swift identification; where the variation really comes from. `[~6,400 w]`

**Daily Problem Sets**
- **PS 4.1** 2×2 DiD + event-study construction `[~2,400 w]`
- **PS 4.2** Goodman-Bacon decomposition by hand; negative-weights demo `[~2,600 w]`
- **PS 4.3** RD local-polynomial fitting + bandwidth experiments `[~2,500 w]`
- **PS 4.4** Synthetic control weights + placebo inference `[~2,500 w]`
- **PS 4.5** Shift-share exposure weights + identification critique `[~2,400 w]`

**Notebooks**
- **nb4.1** Event-study plots & parallel-trends tests `[~1,700 w / ~24 cells]`
- **nb4.2** Staggered DiD: TWFE vs. Callaway–Sant'Anna (`pyfixest`/`differences`) `[~1,900 w / ~28 cells]`
- **nb4.3** RD with `rdrobust` (CCT bandwidths) `[~1,800 w / ~26 cells]`
- **nb4.4** Synthetic control & synthetic DiD `[~1,800 w / ~26 cells]`
- **nb4.5** Bartik instrument decomposition `[~1,700 w / ~24 cells]`

- **Lab 4 (Lab Manual): "A Clean DiD on HMDA + a State Policy Shock."** Build a panel from HMDA, define treatment by a state regulatory change, run event-study + Callaway–Sant'Anna, stress parallel trends; ties to the fair-lending thread. `[~4,600 w]`
- **Mentor Session 4 (Lei Gao):** *"Detecting discrimination with a clean design."* Tied to Gao & Sun (2019, *PNAS*) fair-lending. Pre-read, 3 warm-ups, 5-slide deck, 3 stretch questions, reflection. `[~2,200 w]`
- **Assessment W4 + rubric.** `[~2,000 w]`

**Week 4 subtotal: ~73,000 words** *(chapters 33,600 · problems 12,400 · notebooks 8,900 · lab 4,600 · mentor 2,200 · assessment 2,000 · narrative 1,400 · overhead/figures prose ~7,900)*

---

## WEEK 5 — Reading the Frontier I: Decoding Empirical Papers
**Theme:** One paper per day. For each, a 4-page **Reader's Guide** with a fixed anatomy: research
question · identification strategy · data · table-by-table reading order · what's clever · what's
vulnerable · three replication exercises.

- **W5 Opening narrative** — How a professional reads a paper: not front-to-back, but tables-first. `[~1,400 w]`

**Chapters (Reader's Guides, ~4 pp ≈ 2,800–3,400 w each)**
- **Ch 5.1 — Reader's Guide: Fama & French (1992), "The Cross-Section of Expected Stock Returns," *JF* 47(2):427–465.** Size/value, sorting, the death of CAPM beta. `[~3,200 w]`
- **Ch 5.2 — Reader's Guide: Fama & French (1993), "Common Risk Factors...," *JFE* 33(1):3–56.** The factor-model machinery; time-series vs. cross-section. `[~3,200 w]`
- **Ch 5.3 — Reader's Guide: Jegadeesh & Titman (1993), "Returns to Buying Winners and Selling Losers," *JF* 48(1):65–91.** Momentum portfolios; overlapping holding periods. `[~3,100 w]`
- **Ch 5.4 — Reader's Guide: Petersen (2009), "Estimating Standard Errors in Finance Panel Data Sets," *RFS* 22(1):435–480.** A methods paper read as a paper; clustering choices. `[~3,100 w]`
- **Ch 5.5 — Reader's Guide: Bertrand, Duflo & Mullainathan (2004), "How Much Should We Trust DiD Estimates?" *QJE* 119(1):249–275.** Serial correlation in DiD; the placebo-law method. `[~3,100 w]`

**Daily Problem Sets** (replication-flavored; ~6 tasks each)
- **PS 5.1** FF92 sorting & univariate portfolio replication tasks `[~2,300 w]`
- **PS 5.2** FF93 factor construction & time-series regressions `[~2,300 w]`
- **PS 5.3** Momentum portfolio replication + transaction-cost critique `[~2,300 w]`
- **PS 5.4** Re-run Petersen's clustering comparison on a panel `[~2,200 w]`
- **PS 5.5** Reproduce a BDM placebo-DiD false-positive `[~2,300 w]`

**Notebooks**
- **nb5.1** FF92 portfolio sorts on CRSP/Compustat `[~1,700 w / ~24 cells]`
- **nb5.2** FF93 factor regressions `[~1,700 w / ~24 cells]`
- **nb5.3** Momentum strategy backtest `[~1,800 w / ~26 cells]`
- **nb5.4** Petersen clustering replication `[~1,600 w / ~22 cells]`
- **nb5.5** BDM placebo-law simulation `[~1,700 w / ~24 cells]`

- **Reading Guide Pack 5 (meta-guide):** the fixed Reader's-Guide template, a "reading order" heuristic, a glossary of table conventions, and a self-check rubric students apply to each paper. `[~3,000 w]`
- **Mentor Session 5 (Lei Gao):** *"Anatomy of a JF paper."* Tied to the *Rainbow of Credits* municipal-borrowing working paper (AEA 2025). Pre-read, 3 warm-ups, 5-slide deck, 3 stretch questions, reflection. `[~2,200 w]`
- **Assessment W5 + rubric** — students write their own 4-page Reader's Guide on an unseen paper; rubric. `[~2,200 w]`

**Week 5 subtotal: ~58,000 words** *(guides 15,700 · problems 11,400 · notebooks 8,500 · reading pack 3,000 · mentor 2,200 · assessment 2,200 · narrative 1,400 · overhead/figures prose ~13,600)*

> **[CHECK]** Verify exact page ranges for Fama–French (1992) *JF* 47(2):427–465; FF (1993) *JFE* 33(1):3–56; Jegadeesh–Titman (1993) *JF* 48(1):65–91; Petersen (2009) *RFS* 22(1):435–480; Bertrand–Duflo–Mullainathan (2004) *QJE* 119(1):249–275. Years are confident; precise pages to confirm against the journals before publication.

---

## WEEK 6 — Reading the Frontier II: Text, Modern Empirics, and the AI Co-Pilot
**Theme:** Text-as-data and machine-learning-flavored empirical finance, plus a full module on using
LLMs *responsibly* as a research co-pilot.

- **W6 Opening narrative** — When the data is words: 10-Ks, 8-Ks, and the temptation to let a model do your thinking. `[~1,500 w]`

**Chapters (Reader's Guides + the AI module)**
- **Ch 6.1 — Reader's Guide: Kogan, Papanikolaou, Seru & Stoffman (2017), "Technological Innovation, Resource Allocation, and Growth," *QJE* 132(2):665–712.** Patent-value measure from stock returns. `[~3,200 w]`
- **Ch 6.2 — Reader's Guide: Hoberg & Phillips (2016), "Text-Based Network Industries and Endogenous Product Differentiation," *JPE* 124(5):1423–1465.** TNIC; cosine similarity of 10-K text. `[~3,200 w]`
- **Ch 6.3 — Reader's Guide: Loughran & McDonald (2011), "When Is a Liability Not a Liability? Textual Analysis...," *JF* 66(1):35–65.** Finance-specific sentiment dictionaries; the bag-of-words era. `[~3,200 w]`
- **Ch 6.4 — Reader's Guide (paired): Bartlett, Morse, Stanton & Wallace (2022), "Consumer-Lending Discrimination in the FinTech Era," *JFE* 143(1):30–56; and Bhutta, Hizmo & Ringo, "How Much Does Racial Bias Affect Mortgage Lending?" Federal Reserve FEDS / working paper.** Fair-lending in the algorithmic era; ties to Gao & Sun (2019). `[~3,600 w]`
- **Ch 6.5 — The AI Co-Pilot for Research (LLM-in-the-Loop).** Prompt patterns for empirical work; RAG over 10-Ks; LLM text classification with **out-of-sample validation**; critical limits — hallucinated cites, look-ahead/training-data leakage, prompt-induced p-hacking; reproducibility of stochastic outputs. `[~7,200 w]`

**Daily Problem Sets**
- **PS 6.1** KPSS patent-value measure construction tasks `[~2,300 w]`
- **PS 6.2** 10-K cosine-similarity / TNIC mini-build `[~2,400 w]`
- **PS 6.3** LM dictionary sentiment vs. a naive dictionary `[~2,300 w]`
- **PS 6.4** Fair-lending decomposition + disparate-impact critique `[~2,400 w]`
- **PS 6.5** LLM-classification with held-out validation + leakage audit `[~2,600 w]`

**Notebooks**
- **nb6.1** Building a patent-value panel `[~1,700 w / ~24 cells]`
- **nb6.2** 10-K text vectorization & similarity `[~1,900 w / ~28 cells]`
- **nb6.3** Loughran–McDonald sentiment pipeline `[~1,800 w / ~26 cells]`
- **nb6.4** Mortgage-disparity decomposition on HMDA `[~1,800 w / ~26 cells]`
- **nb6.5** AI co-pilot lab: **Anthropic Messages API**, **GMU Azure OpenAI** deployment (`${AZURE_OPENAI_KEY}`), local **Ollama / Hopper A100** fallback; RAG over 10-Ks; OOS-validated classification `[~2,600 w / ~36 cells]`

- **Reading Guide Pack 6 + AI Lab Manual:** RAG architecture diagram (prose), prompt-pattern catalog, an evaluation harness for LLM labels (precision/recall vs. hand labels), and a "responsible-use & disclosure" checklist for the capstone. `[~4,000 w]`
- **Mentor Session 6 (Lei Gao):** *"Text as data, and AI without fooling yourself."* Tied to Gao, Han, Kim & Pan (2024, *JCF*, 84:102520) overlapping supply-chain institutional ownership and supplier-firm earnings management (as a measured construct), and Gao et al. (forthcoming) AI trading simulation. Pre-read, 3 warm-ups, 5-slide deck, 3 stretch questions, reflection. `[~2,400 w]`
- **Assessment W6 + rubric** — build + validate one LLM text classifier with an OOS report; rubric weights validation & honesty. `[~2,400 w]`

**Week 6 subtotal: ~62,000 words** *(guides+AI chapter 20,400 · problems 12,000 · notebooks 9,800 · reading/AI pack 4,000 · mentor 2,400 · assessment 2,400 · narrative 1,500 · overhead/figures prose ~9,500)*

> **[CHECK]** Confirm exact pages/venues: KPSS (2017) *QJE* 132(2):665–712; Hoberg–Phillips (2016) *JPE* 124(5):1423–1465; Loughran–McDonald (2011) *JF* 66(1):35–65; Bartlett–Morse–Stanton–Wallace (2022) *JFE* 143(1):30–56. **Bhutta–Hizmo–Ringo** publication venue/year (Federal Reserve FEDS working paper vs. journal) to be verified before citing a page range.

---

## WEEK 7 — Independent Research Project I: From Question to Pre-Analysis Plan
**Theme:** Turn a hunch into a falsifiable, pre-registered empirical design with data in hand.

- **W7 Opening narrative** — The scariest blank page in science: choosing your own question. `[~1,500 w]`

**Chapters**
- **Ch 7.1 — Idea-Generation Workshop.** From puzzle to testable hypothesis; the "so what / who cares / what's new" filter; mapping each student's interest (Maya/Devon/Priya/Sam/Leah) to a feasible dataset. `[~5,200 w]`
- **Ch 7.2 — Data Acquisition in Practice.** WRDS Cloud, SEC EDGAR (full-text + XBRL), FRED, HMDA, 13F, USPTO PatentsView, yfinance; rate limits, licensing, and building a reproducible pull. `[~5,600 w]`
- **Ch 7.3 — The Pre-Analysis Plan (short form, Olken 2015).** Hypotheses, primary spec, controls/FEs/clustering, sample, multiple-testing plan (FDR), what would falsify you; registering before you peek. `[~5,200 w]`
- **Ch 7.4 — Building the Analysis Dataset.** Merging keys (PERMNO/GVKEY/CIK crosswalks), survivorship & look-ahead bias, winsorizing, missing-data discipline, a documented data-build script. `[~5,400 w]`
- **Ch 7.5 — Identification Memo.** Writing the one-paragraph identifying-assumption statement and the threats-and-responses table that the whole paper will defend. `[~4,800 w]`

**Daily Problem Sets** (project-scaffolding deliverables)
- **PS 7.1** Three candidate questions scored on the feasibility/novelty rubric `[~2,000 w]`
- **PS 7.2** A working data-pull script + data card for one source `[~2,200 w]`
- **PS 7.3** A complete pre-analysis plan draft `[~2,400 w]`
- **PS 7.4** A reproducible merged analysis dataset + diagnostics `[~2,300 w]`
- **PS 7.5** Identification memo + threats table `[~2,100 w]`

**Notebooks**
- **nb7.1** Idea-to-spec template notebook `[~1,400 w / ~18 cells]`
- **nb7.2** Multi-source data-pull harness `[~1,900 w / ~28 cells]`
- **nb7.3** PAP companion (power calc for your design) `[~1,600 w / ~22 cells]`
- **nb7.4** Dataset-build & validation notebook `[~1,800 w / ~26 cells]`
- **nb7.5** First-look regressions (frozen until PAP filed) `[~1,600 w / ~22 cells]`

- **Lab 7 (Lab Manual): "Your Data, Reproducibly."** Stand up a GitHub repo from the template, wire GitHub Classroom, pin environments, write a README + data card, and file the PAP as a tagged commit. `[~4,200 w]`
- **Mentor Session 7 (Lei Gao):** *"How I pick a project — and kill one."* Tied to Gao, He & Wu (2023, *JFQA*) CSR/price-pressure and the *Rainbow of Credits* pipeline. Pre-read, 3 warm-ups, 5-slide deck, 3 stretch questions, reflection. `[~2,200 w]`
- **Assessment W7 + rubric** — PAP + identification memo graded on the research-design rubric. `[~2,200 w]`

**Week 7 subtotal: ~60,000 words** *(chapters 26,200 · problems 11,000 · notebooks 8,300 · lab 4,200 · mentor 2,200 · assessment 2,200 · narrative 1,500 · overhead/figures prose ~4,400)*

---

## WEEK 8 — Independent Research Project II: Execution, Robustness, Writing, and Defense
**Theme:** Run it, break it on purpose, write it up to publication standard, and present.

- **W8 Opening narrative** — A result is not a finding until it survives your own attempts to kill it. `[~1,500 w]`

**Chapters**
- **Ch 8.1 — Execution & Specification Curve.** Running the pre-registered spec; specification-curve / multiverse analysis; honest deviations log. `[~5,400 w]`
- **Ch 8.2 — Robustness & Inference Stress-Tests.** Alternative SEs, placebo tests, sensitivity to bandwidth/controls/sample, multiple-testing corrections (Bonferroni/BH-FDR), Oster (2019) δ for selection-on-unobservables. `[~5,800 w]`
- **Ch 8.3 — Writing the Empirical Paper.** Structure (intro that promises, lit that positions, data, design, results, robustness, conclusion); table & figure craft per Appendix D; the one-sentence contribution. `[~5,600 w]`
- **Ch 8.4 — Peer Review & Revision.** Refereeing another student's paper; responding to a referee report; the revise-and-resubmit memo. `[~4,800 w]`
- **Ch 8.5 — The 8-Minute Presentation & the Replication Packet.** Slide discipline; defending identification under questions; assembling a one-click replication packet (data, code, README, seed). `[~4,800 w]`

**Daily Problem Sets** (capstone-production deliverables)
- **PS 8.1** Specification curve for your main result `[~2,200 w]`
- **PS 8.2** A full robustness battery + write-up `[~2,400 w]`
- **PS 8.3** Draft intro + results section against the style guide `[~2,300 w]`
- **PS 8.4** A referee report on a peer's paper + your R&R memo `[~2,300 w]`
- **PS 8.5** 8-minute deck + replication-packet checklist `[~2,000 w]`

**Notebooks**
- **nb8.1** Specification-curve generator `[~1,800 w / ~26 cells]`
- **nb8.2** Robustness-battery harness (placebos, Oster δ) `[~1,900 w / ~28 cells]`
- **nb8.3** Publication-quality tables/figures (`pyfixest`/`stargazer`-style → LaTeX) `[~1,800 w / ~26 cells]`
- **nb8.4** Reproducibility-check notebook (fresh-env rerun) `[~1,500 w / ~20 cells]`
- **nb8.5** Final manuscript build (Markdown/LaTeX → PDF) `[~1,500 w / ~20 cells]`

- **Lab 8 (Lab Manual): "Final Manuscript + Repo + Defense."** Compile the LaTeX paper (AEA template variant) on Overleaf, finalize the GitHub repo with replication packet, dry-run the 8-minute talk. `[~4,600 w]`
- **Mentor Session 8 (Lei Gao):** *"Defending a result: what a referee actually asks."* Tied to Elnahas, Gao, Hossain & Kim (2024, *JFQA*) disclosure/CEO-politics. Pre-read, 3 warm-ups, 5-slide deck, 3 stretch questions, reflection. `[~2,200 w]`
- **Assessment W8 + rubric** — the capstone paper + presentation graded on the full research rubric (the program's terminal assessment). `[~2,600 w]`

**Week 8 subtotal: ~61,000 words** *(chapters 26,400 · problems 11,200 · notebooks 8,500 · lab 4,600 · mentor 2,200 · assessment 2,600 · narrative 1,500 · overhead/figures prose ~4,000)*

---

## WEEK 9 — Symposium Week: From Manuscript to Conference Talk
**Theme:** Convert the Week-8 manuscript into a research-symposium talk and poster, dry-run with
mentors and peers, and present at the live event (aligns with NextGen Phase 2, ~Aug 14, 2026).

- **W9 Opening narrative** — Eight weeks of building, one room of strangers, eight minutes to tell them the truth: what changes when the audience is no longer the grader. `[~1,400 w]`

**Chapters**
- **Ch 9.1 — Before the Conference: The 72-Hour Pre-Flight.** Slide-freeze SHA, replication-packet `make clean && make all` honesty test, anticipated-questions matrix; the seventy-two hours that decide what the eight minutes feel like. `[~5,200 w]`
- **Ch 9.2 — The 8-Minute Talk, Decomposed.** The Hook → Design → Identification Punchline → One Picture → Threats → Ask arc; per-slide budgets, cut-lines, table-to-figure conversion; one claim per slide; the contribution that survives compression. `[~5,400 w]`
- **Ch 9.3 — During the Conference: Three Honest Answers and the Hostile-Question Taxonomy.** "I don't know," "It's in the paper," "Good point" — and what each commits you to; the question-class taxonomy (clarifying / methodological / fatal / off-topic) and the rehearsed 30-second responses. `[~5,000 w]`
- **Ch 9.4 — The Poster and the Hallway Conversation.** A different medium, a different argument structure, a different success metric: poster as 60-second standalone read; the 90-second elevator pitch; printing logistics and the QR-to-replication. `[~5,200 w]`
- **Ch 9.5 — After the Conference: The 24-Hour Feedback Ledger and Triage.** Capturing every comment within 24 hours; the cost-value-threat triage rubric; the bridge from Saturday's talk to Monday's revision plan that opens Week 10. `[~4,600 w]`

**Daily Problem Sets** (symposium-prep deliverables; ~6 tasks each)
- **PS 9.1** A 1-sentence + 1-paragraph contribution statement scored on the rubric `[~2,000 w]`
- **PS 9.2** First-draft 8-slide deck against the slide-grammar checklist `[~2,300 w]`
- **PS 9.3** Conference poster (PDF) and the standalone-read self-test `[~2,200 w]`
- **PS 9.4** A peer Q&A drill: write 6 anticipated questions + rehearsed 30-second answers `[~2,200 w]`
- **PS 9.5** A structured post-symposium reflection memo `[~2,000 w]`

**Notebooks**
- **nb9.1** Slide-timing simulator: per-slide rehearsal stopwatch with cut-line markers and a 30-trial timing-variance distribution `[~1,600 w / ~22 cells]`
- **nb9.2** Anticipated-questions matrix builder: join the Ch 7.5 threats table to a survivable/fatal classifier and emit a 20-row Q&A flashcard deck `[~1,700 w / ~24 cells]`
- **nb9.3** One-figure test: turn the paper's Table 1 + Figure 1 into a single talk-grade figure (large fonts, fewer rows, color-blind palette) `[~1,700 w / ~24 cells]`
- **nb9.4** Poster-layout engine: matplotlib figure-grid + headline-band poster export to print-ready PDF `[~1,500 w / ~20 cells]`
- **nb9.5** Feedback ledger + triage emitter: CSV of every comment → R&R-style task board that becomes the Week 10 input `[~1,500 w / ~20 cells]`

- **Lab 9 (Lab Manual): "Conference Day, End-to-End."** Full dress rehearsal: 72-hour pre-flight checklist → timed 8-minute talk → adversarial Q&A → poster session → 24-hour feedback ledger; recorded and reviewed against the rubric. `[~4,400 w]`
- **Mentor Session 9 (Lei Gao):** *"What I tell my students the night before they present."* Tied to Gao & Sun (2019, *PNAS*, 116(19):9293–9302) fair-lending — what changes when the room is policy (HUD / Federal Reserve / Congress) instead of academic. Pre-read, 3 warm-ups, 5-slide deck, 3 stretch questions, reflection. `[~2,200 w]`
- **Assessment W9 + rubric** — the symposium talk + poster, graded on the presentation rubric (contribution clarity, slide discipline, identification defense under Q&A, poster as standalone). `[~2,200 w]`

**Week 9 subtotal: ~56,500 words** *(chapters 25,400 · problems 10,700 · notebooks 8,000 · lab 4,400 · mentor 2,200 · assessment 2,200 · narrative 1,400 · overhead/figures prose ~2,200)*

---

## WEEK 10 — Post-Conference Revision I: From Feedback to a Better Paper
**Theme:** Convert symposium feedback into a structured revision plan and a second-round robustness
battery; rewrite the introduction to position the contribution correctly (aligns with NextGen
Phase 3 Week 1, Aug 21, 2026).

- **W10 Opening narrative** — A finding that survived a hostile room is not yet a finding that will survive a referee: the next four weeks are when the paper grows up. `[~1,500 w]`

**Chapters**
- **Ch 10.1 — Triaging Conference Feedback with the Cost–Value–Threat-to-Identification 3×3.** Sorting every Saturday comment on three axes (cost to address, value if addressed, threat-to-identification if ignored); the kill-list vs. the defer-list; when feedback says "redesign" and when it says "rewrite a paragraph." `[~5,400 w]`
- **Ch 10.2 — Multiple Testing Done Right: Bonferroni, Holm, BH-FDR, Romano–Wolf.** Why "we ran 14 robustness checks" is itself a multiple-testing problem; family-wise error rate vs. false-discovery rate; the Romano–Wolf step-down procedure; what to pre-specify and what to disclose. `[~5,800 w]`
- **Ch 10.3 — Heterogeneous Treatment Effects: CATE, Causal Forests, and Pre-Registration.** From ATE to CATE; honest causal forests (Athey–Wager); the danger of *p*-hacking via subgroups; how a Week-7 PAP constrains what you can claim post-conference. `[~6,200 w]`
- **Ch 10.4 — Mechanism Analysis Without Bad Controls: Acharya–Blackwell–Sen Mediation.** Why "include the mechanism as a control" is wrong; the Acharya–Blackwell–Sen sequential-*g* approach; when you can credibly decompose a total effect into direct + mediated. `[~5,400 w]`
- **Ch 10.5 — External Validity and Transportability: Would This Replicate in 2030?** The Pearl–Bareinboim transportability framework; the "out-of-sample by design" mindset; the honest external-validity paragraph that should close every paper. `[~4,800 w]`

**Daily Problem Sets** (revision-production deliverables)
- **PS 10.1** Feedback triage matrix: every comment scored on cost × value × threat-to-identification, with a defended kill-list and defer-list `[~2,200 w]`
- **PS 10.2** Romano–Wolf step-down on your robustness battery + a multiple-testing disclosure paragraph `[~2,300 w]`
- **PS 10.3** A pre-registered CATE / heterogeneous-effects analysis on your data, with the honest subgroup-found-after-the-fact disclosure `[~2,500 w]`
- **PS 10.4** Mediation analysis with the Acharya–Blackwell–Sen sequential-*g* approach + a "bad-controls" critique of a naive alternative `[~2,300 w]`
- **PS 10.5** A one-page external-validity / transportability paragraph for your paper `[~2,000 w]`

**Notebooks**
- **nb10.1** Romano–Wolf step-down procedure (paired with a Bonferroni / Holm / BH-FDR comparison harness) `[~1,800 w / ~26 cells]`
- **nb10.2** Causal forest on synthetic data: `econml`/`grf`-style honest forest with CATE plots and the over-fitting diagnostic `[~1,800 w / ~26 cells]`
- **nb10.3** Mediation done right: Acharya–Blackwell–Sen sequential-*g* on a worked example, contrasted with the bad-control naive approach `[~1,700 w / ~24 cells]`
- **nb10.4** Oster δ and Altonji–Elder–Taber bounds: selection-on-unobservables that survives a referee `[~1,500 w / ~20 cells]`
- **nb10.5** Transportability audit: a Pearl–Bareinboim diagram + the "would this replicate in 2030?" simulator `[~1,500 w / ~20 cells]`

- **Lab 10 (Lab Manual): "Robustness Battery v2."** End-to-end second-round robustness: run Romano–Wolf, a causal-forest CATE analysis, sequential-*g* mediation, Oster δ, and a transportability audit on the student's own paper; assemble the multiple-testing-honest robustness section and the deviations-from-PAP log. `[~4,400 w]`
- **Mentor Session 10 (Lei Gao):** *"How referees read heterogeneity."* Tied to Deng, Gao & Kim (2020, *JCF*, 60:101498) short-sale natural-experiment paper, with a walk-through of how the heterogeneity section was sharpened during peer review. Pre-read, 3 warm-ups, 5-slide deck, 3 stretch questions, reflection. `[~2,300 w]`
- **Assessment W10 + rubric** — the revision memo + the rewritten introduction, graded on the revision rubric (coverage of comments, honesty, gain-on-paper). `[~2,300 w]`

**Week 10 subtotal: ~58,500 words** *(chapters 26,800 · problems 11,300 · notebooks 7,900 · lab 4,400 · mentor 2,300 · assessment 2,300 · narrative 1,500 · overhead/figures prose ~2,000)*

---

## WEEK 11 — Post-Conference Revision II: Journal-Style Writing and Publication-Quality Craft
**Theme:** Turn the revised draft into a journal-style manuscript: a literature section that
positions, tables and figures to publication standard, and the ethics/data-availability scaffolding
a real journal expects (aligns with NextGen Phase 3 Week 2, Aug 28, 2026).

- **W11 Opening narrative** — There is a moment when a student paper becomes a paper, and it is almost always the moment the lit review stops being a list. `[~1,500 w]`

**Chapters**
- **Ch 11.1 — The 250-Word Abstract and the Five-Sentence Skeleton.** The empirical-finance abstract grammar: (1) what we study, (2) how we identify it, (3) what we find, (4) why it matters, (5) what's new; word-budget enforcement; the abstract as the only paragraph 90% of readers will read. `[~5,000 w]`
- **Ch 11.2 — Publication-Grade Tables: `pyfixest`/`etable`, Stars Discipline, Panel Structure.** From regression output to JF/JFE/RFS house-style tables; stars discipline (no \*\*\* at 10%); panel A / panel B structure; what goes in the table notes; the "every cell defensible at a referee meeting" test. `[~5,600 w]`
- **Ch 11.3 — Publication-Grade Figures: Event-Study, Specification Curve, Heterogeneity Forest.** Three figure types that carry empirical finance papers; CI bands done correctly; color-blind palettes and print-safe choices; captions that read as mini-results-paragraphs. `[~5,400 w]`
- **Ch 11.4 — The Introduction Rewrite: Five-Paragraph Structure and How to Diagnose a Sick Intro.** The puzzle / design / result / contribution / roadmap arc; the diagnostic checklist for an intro that is doing too much, too little, or the wrong job; cutting throat-clearing; the one-sentence contribution restated three ways. `[~5,400 w]`
- **Ch 11.5 — The Expanded Literature Review: From Bullet List to Three-Strand Argument.** The "three conversations" structure — your paper joins which conversation, against which papers, contributing what; how to cite without summarizing; what to do when the closest paper is yours-but-better. `[~5,000 w]`

**Daily Problem Sets** (publication-quality deliverables)
- **PS 11.1** A 250-word abstract built from the five-sentence skeleton + a 50-word "ultra-abstract" `[~2,000 w]`
- **PS 11.2** Two publication-quality `etable` regression tables (LaTeX) with the disclosure footnote `[~2,300 w]`
- **PS 11.3** Three publication-quality figures — event-study, specification curve, heterogeneity forest — with print-safe captions `[~2,400 w]`
- **PS 11.4** Rewritten introduction against the five-paragraph diagnostic + a before/after side-by-side `[~2,400 w]`
- **PS 11.5** Expanded lit section as a three-strand argument with a citation-graph appendix `[~2,300 w]`

**Notebooks**
- **nb11.1** Abstract builder: a structured-prompt harness + a 250-word counter + a five-sentence-skeleton linter `[~1,500 w / ~20 cells]`
- **nb11.2** `etable` camera-ready: `pyfixest` → LaTeX with the JF/JFE house-style template and panel A/B support `[~1,800 w / ~26 cells]`
- **nb11.3** Event-study twelve ways: the same data, twelve plotting choices, the one defensible chart `[~1,800 w / ~26 cells]`
- **nb11.4** Intro diagnostic: a structured prose-linter (throat-clearing, hedge-then-overclaim, verb audit) `[~1,500 w / ~20 cells]`
- **nb11.5** Lit-review network: OpenAlex/Semantic-Scholar citation-graph builder + the three-conversations clusterer `[~1,500 w / ~20 cells]`

- **Lab 11 (Lab Manual): "Manuscript Build."** Compile the full manuscript in the AEA LaTeX template — abstract, rewritten intro, expanded lit, publication-grade tables and figures, disclosure statements; cross-check with a peer on the abstract and intro; produce a press-ready PDF. `[~4,400 w]`
- **Mentor Session 11 (Lei Gao):** *"Earning space in a crowded field."* Tied to Elnahas, Gao, Hossain & Kim (2024, *JFQA*, 59(8):3671–3707) — how a disclosure-quality measure becomes a credible main result and how the intro had to position it against a crowded prior literature. Pre-read, 3 warm-ups, 5-slide deck, 3 stretch questions, reflection. `[~2,300 w]`
- **Assessment W11 + rubric** — the press-ready manuscript + the AEA-style code/data appendix, graded on the publication-craft rubric (lit positioning, table/figure quality, disclosure completeness, prose discipline). `[~2,300 w]`

**Week 11 subtotal: ~58,000 words** *(chapters 25,800 · problems 11,200 · notebooks 8,100 · lab 4,400 · mentor 2,300 · assessment 2,300 · narrative 1,500 · overhead/figures prose ~2,400)*

---

## WEEK 12 — Submission Packet, Self-Referee, and Next Steps
**Theme:** Assemble a one-click replication archive, write a self-referee report, choose a venue,
and submit (aligns with NextGen Phase 3 Weeks 3–4, Sep 4 – Sep 11, 2026).

- **W12 Opening narrative** — The last act of the camp is the one that decides whether any of it survives the year: the click that turns a project into a record. `[~1,500 w]`

**Chapters**
- **Ch 12.1 — Submitting to the Schar Young Scholars Journal and the GMU MARS Repository.** The realistic first venue for a strong high-school empirical-finance paper: Schar Young Scholars Journal submission portal, formatting requirements, the GMU MARS undergraduate-research repository deposit, ORCID and DOI setup. `[~5,000 w]`
- **Ch 12.2 — The SSRN Preprint: Posting Decisions, Versioning, and the DOI Question.** SSRN as the working-paper standard in finance; when to post vs. when to wait; SSRN abstract-ID vs. DOI; versioning policy (v1 / v2 / v3); the SSRN download-count temptation and what it actually measures. `[~4,800 w]`
- **Ch 12.3 — From Poster to *Journal of Finance*: The Decade-Long Arc of a Paper.** The realistic timeline (NBER WP → conference → top-five journal R&R → published) using a real Gao paper as the case study; what high-school work realistically achieves *now* and what it makes possible *later*. `[~5,000 w]`
- **Ch 12.4 — The Conference Circuit: FMA Undergraduate Poster, AEA Pipeline, SFS Cavalcade.** The conferences that matter for emerging finance researchers; the FMA undergraduate poster session as a credible target; the AEA continuing-education pipeline; SFS Cavalcade as a long-term goal; submission deadlines and how to read a call-for-papers. `[~4,800 w]`
- **Ch 12.5 — What Comes After Submission: The Reviewer Wait, the Desk Reject, the R&R.** The post-submission rules of engagement (don't ping the editor); reading a desk-reject letter without taking it personally; the R&R as the actual start of the paper; the "what I would do differently next time" memo. `[~5,000 w]`

**Daily Problem Sets** (submission-packet deliverables)
- **PS 12.1** A Schar Young Scholars Journal submission packet + the MARS repository deposit form `[~2,200 w]`
- **PS 12.2** An SSRN preprint draft (abstract, JEL codes, keywords) + a versioning-policy statement `[~2,100 w]`
- **PS 12.3** A "decade-arc map" applied to your own paper: where it is today, the realistic next two venues, and the long shot `[~2,000 w]`
- **PS 12.4** A populated conference-submission calendar for the next 12 months (FMA / SFS / AEA / regionals) `[~2,000 w]`
- **PS 12.5** A "five-year research identity" memo: which two questions you would still want to answer in 2030 `[~2,200 w]`

**Notebooks**
- **nb12.1** Submission-packet builder: one-click `make all` rebuild on a clean conda env + a MANIFEST mapping every table/figure to its producing script `[~1,800 w / ~26 cells]`
- **nb12.2** SSRN metadata generator: abstract, JEL codes, keywords, suggested-reader emails — packaged for the SSRN portal `[~1,500 w / ~20 cells]`
- **nb12.3** MARS repository schema: a structured-metadata builder that maps the paper's bibliography, datasets, and replication archive to the MARS deposit schema `[~1,500 w / ~20 cells]`
- **nb12.4** Conference calendar engine: a year-ahead deadline-tracker for FMA / SFS / AEA / regional finance conferences with submission-cost and acceptance-rate priors `[~1,500 w / ~20 cells]`
- **nb12.5** Five-year research-identity map: an interactive concept-graph of the questions adjacent to the student's paper, with a defensibility score for each next-paper candidate `[~1,500 w / ~20 cells]`

- **Lab 12 (Lab Manual): "Submission Day."** End-to-end submission protocol: clean-machine rebuild verified by a peer; SSRN preprint posted; Schar Young Scholars Journal portal submission completed; MARS deposit submitted; conference-calendar populated; 5-minute "what I learned" exit talk recorded. `[~4,400 w]`
- **Mentor Session 12 (Lei Gao):** *"The decade arc of a paper in the JF pipeline."* Tied to *Rainbow of Credits* (Gao, Liu & Wang, AEA 2025, target *Journal of Finance*) — a paper currently mid-pipeline — and Gao, Gopalakrishnan, Ehrlich & Wang (forthcoming, *Journal of Financial Education*) AI trading simulation. Two papers at different stops on the same publication road. Pre-read, 3 warm-ups, 5-slide deck, 3 stretch questions, reflection. `[~2,300 w]`
- **Assessment W12 + rubric** — the submission packet (manuscript + replication + cover letter + self-referee) graded on the **terminal program rubric**; this is the camp's exit credential. `[~2,800 w]`

**Week 12 subtotal: ~57,500 words** *(chapters 24,600 · problems 10,900 · notebooks 7,800 · lab 4,400 · mentor 2,300 · assessment 2,800 · narrative 1,500 · overhead/figures prose ~3,200)*

---

# APPENDICES

## Appendix A — Math Toolkit (just enough)
- **A.1** Matrix algebra: vectors, matrix multiply, transpose/inverse, rank, positive-definiteness, the spectral/SVD idea at the intuition level. `[~4,200 w]`
- **A.2** Optimization: gradients, first/second-order conditions, constrained optimization & Lagrange, the normal equations as an optimization. `[~3,800 w]`
- **A.3** Asymptotics: convergence in probability/distribution, Slutsky, continuous-mapping, the delta method, sandwich-variance intuition. `[~4,000 w]`
- **A.4** Probability distributions reference (Normal, t, $\chi^2$, F, Bernoulli/Binomial, Poisson) + when each shows up. `[~2,500 w]`

**Appendix A subtotal: ~14,500 words**

## Appendix B — Python + LaTeX Setup
- **B.1** Toolchain: VS Code, conda env (`python=3.11` + pinned stack), Git basics. `[~3,000 w]`
- **B.2** GitHub & GitHub Classroom workflow for the camp. `[~2,200 w]`
- **B.3** WRDS Cloud access + querying licensed data (and the read-only/GMU-infra rules). `[~2,800 w]`
- **B.4** GMU Hopper SLURM templates (batch jobs, A100 GPU for the AI module, Ollama). `[~2,800 w]`
- **B.5** Overleaf + the AEA LaTeX template variant; BibTeX hygiene. `[~2,400 w]`

**Appendix B subtotal: ~13,200 words**

## Appendix C — Data Dictionary Master (~30 data cards)
> Each card: provider, coverage, key identifiers, access path, license/§-on-GMU note, gotchas, a "first 10 rows" sketch, and which chapter/lab uses it. ~700–950 words each.

CRSP · Compustat (Fundamentals Annual/Quarterly) · IBES · Thomson/SEC 13F · TRACE · Mergent FISD · OptionMetrics · Capital IQ · FRED · Call Reports (FFIEC) · FR Y-9C · SEC EDGAR 10-K/10-Q · SEC EDGAR 8-K · SEC EDGAR DEF 14A · SEC EDGAR 13F · SEC EDGAR N-PORT · SEC EDGAR XBRL Financial Statements · Treasury/FINRA · FDIC · HMDA · CFPB Consumer Complaints · Census · BLS · BEA · USPTO PatentsView · USAspending · NOAA/FEMA · yfinance/Stooq/Tiingo/Alpha Vantage · FOMC text/GDELT · Etherscan/CoinGecko/DeFiLlama · ECB/BIS/IMF/World Bank/OECD.

**~33 cards × ~820 w avg ≈ Appendix C subtotal: ~27,000 words**

## Appendix D — Style Guide for Empirical-Finance Writing
- **D.1** Table craft: layout, what goes in notes, reporting t-stats/SEs/stars, significant digits. `[~3,200 w]`
- **D.2** Reporting regressions: which coefficients, $R^2$/within-$R^2$, FE/cluster disclosure, sample lines. `[~2,800 w]`
- **D.3** Robustness sections that persuade; the threats-and-responses table. `[~2,400 w]`
- **D.4** The replication packet standard (data, code, seed, README, environment file). `[~2,400 w]`
- **D.5** Prose style: hedging vs. overclaiming, causal language discipline, citing primary sources. `[~2,200 w]`

**Appendix D subtotal: ~13,000 words**

## Appendix E — Solutions Manual (every problem fully worked)
> 12 weeks × 5 problem sets × ~6 problems = ~360 problems, each with a complete worked solution
> (derivation, code where relevant, interpretation). Counted separately from the problem statements
> above (those counts were statement + solution as a pair); this appendix is the canonical home of the
> full worked solutions, organized by week. Weeks 9–12 solutions are deliverable-shaped (decks,
> memos, manuscripts, packets) rather than purely analytic, so the per-week wordcount is somewhat
> lower despite identical problem-count.

- Solutions, Weeks 1–2 `[~14,000 w]`
- Solutions, Weeks 3–4 `[~15,500 w]`
- Solutions, Weeks 5–6 `[~14,000 w]`
- Solutions, Weeks 7–8 `[~13,500 w]`
- Solutions, Weeks 9–10 `[~12,000 w]`
- Solutions, Weeks 11–12 `[~12,000 w]`

**Appendix E subtotal: ~81,000 words**

**Appendices total: ~148,700 words**

---

# CAPSTONE GALLERY (5 full example papers, 8–12 pp each)
> Publication-style worked exemplars students can model their own paper on. Each ~3,000–3,800 words
> of paper + ~1,000 words of an annotated "how this paper was built" margin commentary.

- **Capstone 1 — Fair Lending on HMDA.** Disparity in mortgage approval/pricing; decomposition + a clean design; ties to Gao & Sun (2019). `[~4,600 w]`
- **Capstone 2 — Common Ownership from 13F.** Constructing common-ownership measures and a disclosure/competition outcome (a student-track variant of the anchor paper's earnings-management outcome); ties to Gao, Han, Kim & Pan (2024), *JCF*, 84:102520. `[~4,600 w]`
- **Capstone 3 — Innovation from USPTO PatentsView.** Patent-based innovation measure and a firm-outcome event study; ties to KPSS (2017). `[~4,400 w]`
- **Capstone 4 — SEC 8-K Text Classification.** Classifying 8-K events with OOS-validated text models and a return reaction study; AI-module methods. `[~4,600 w]`
- **Capstone 5 — FRED Macro Event Study.** A monetary/macro-announcement event study with proper inference. `[~4,400 w]`

**Capstone Gallery subtotal: ~22,600 words**

---

# INSTRUCTOR'S MANUAL (separate document)
- **IM-1** Pacing guide: the 12-week clock — Weeks 1–8 instructional core mapped onto NextGen's 7 Friday Phase-1 sessions plus a transition week, Week 9 ↔ NextGen Phase 2 symposium, Weeks 10–12 ↔ NextGen Phase 3 paper refinement. `[~3,800 w]`
- **IM-2** Grading rubrics (consolidated): problem sets, assessments, capstone paper, presentation, symposium talk + poster, revision memo, submission packet. `[~4,000 w]`
- **IM-3** Common student pitfalls, by week, with diagnostic questions and fixes (including the symposium/revision-phase pitfalls — over-defensive Q&A, scope-creep robustness, intro that re-promises rather than positions). `[~4,200 w]`
- **IM-4** Suggested guest lectures & how to slot them; mentor-session facilitation notes (Weeks 1–12). `[~2,600 w]`
- **IM-5** Answer keys to assessments + sample graded work (anchor papers for the rubric). `[~3,800 w]`
- **IM-6** Equity/access notes: WRDS seats, compute, accommodations; data-licensing compliance; symposium-day accessibility and travel/honorarium policy. `[~2,200 w]`

**Instructor's Manual subtotal: ~20,600 words**

---

# GRAND TOTAL — Summary Table

| Section | Est. words |
|---|---:|
| Front Matter | 11,900 |
| Week 1 — Probability, Sampling, Inference | 62,000 |
| Week 2 — The OLS Engine | 68,000 |
| Week 3 — Causal Inference I (PO, matching, IV) | 70,000 |
| Week 4 — Causal Inference II (DiD, RD, SC, shift-share) | 73,000 |
| Week 5 — Reading the Frontier I | 58,000 |
| Week 6 — Reading the Frontier II + AI Co-Pilot | 62,000 |
| Week 7 — Research Project I (question → PAP) | 60,000 |
| Week 8 — Research Project II (execution → defense) | 61,000 |
| Week 9 — Symposium Week (talk + poster + defense) | 56,500 |
| Week 10 — Post-Conference Revision I (feedback → memo + robustness) | 58,500 |
| Week 11 — Post-Conference Revision II (journal-style craft) | 58,000 |
| Week 12 — Submission Packet, Self-Referee, Next Steps | 57,500 |
| Appendix A — Math Toolkit | 14,500 |
| Appendix B — Python + LaTeX Setup | 13,200 |
| Appendix C — Data Dictionary (~33 cards) | 27,000 |
| Appendix D — Style Guide | 13,000 |
| Appendix E — Solutions Manual | 81,000 |
| Capstone Gallery (5 papers) | 22,600 |
| Instructor's Manual | 20,600 |
| **GRAND TOTAL** | **~948,300** |

> **Word-budget note.** The line-item estimates above sum to ~948,300 words — above the
> revised **400,000–700,000** target band for a 12-week curriculum. This TOC is intentionally the
> *maximal* plan so no deliverable is dropped. The published target is hit by treating the
> **per-chapter prose floor (≈4,000 w)** rather than the ceiling, trimming notebook narration to
> code-comment level, and consolidating solutions, as follows. **Authoritative budget to write to:**
>
> | Section | Target words |
> |---|---:|
> | Front Matter | 10,500 |
> | Weeks 1–8 (8 × ~33,000 avg) | 264,000 |
> | Weeks 9–12 (4 × ~30,000 avg) | 120,000 |
> | Appendices A–D | 55,000 |
> | Appendix E (Solutions, Weeks 1–12) | 60,000 |
> | Capstone Gallery | 18,000 |
> | Instructor's Manual | 16,000 |
> | **PUBLISHED GRAND TOTAL** | **~560,000** |
>
> **The book is written to ~560,000 words.** Weeks 1–8 are budgeted at ~33,000 words each (5 chapters
> at 4,000–5,500 w, 5 problem sets at ~1,800 w each, 5 notebooks at ~1,200 w narration each, one
> lab/reading pack ~3,500 w, mentor session ~2,000 w, assessment ~1,800 w, opening narrative
> ~1,300 w). Weeks 9–12 are budgeted at ~30,000 words each because the deliverables (decks, posters,
> memos, packets) are shorter-form than analytic chapters — 5 chapters at ~4,500 w, 5 problem sets at
> ~1,800 w, 5 notebooks at ~1,200 w narration, one lab ~3,500 w, mentor ~2,000 w, assessment
> ~2,000 w, narrative ~1,400 w. Writing slices MUST hit the **target** column; the maximal column is
> a ceiling, not a quota.

---

### Open verification items ([CHECK] consolidated)
1. Exact page ranges for the Week 5 classics (FF92, FF93, JT93, Petersen 2009, BDM 2004) — years confident, pages to confirm.
2. Week 6 modern papers' exact pages/venues (KPSS 2017, Hoberg–Phillips 2016, Loughran–McDonald 2011, Bartlett et al. 2022) and **Bhutta–Hizmo–Ringo** venue/year (Fed FEDS working paper vs. journal).
3. All Gao citations are used **verbatim** from `CONVENTIONS.md §6` / spec §5 and are **not** flagged.
4. The POM supply-chain-risk → bank-loan-cost manuscript (ms POM-Nov-25-OA-1924) is **not** used in this TOC (not in the CV selected list per spec §5); excluded until confirmed.
