# Week 11 Assessment — Manuscript Polish to Publication Standard

Week 10 graded whether your *appendix* survived a referee. Week 11 grades whether your *manuscript* survives one — whether the camera-ready PDF that Lab 11 builds, including the abstract from Chapter 11.1, the tables from Chapter 11.2, the figures from Chapter 11.3, and the introduction from Chapter 11.4, holds together as a publication-grade document. This is the second of three Phase-3 graded artifacts, weighted **80 points**.

The standard from Mentor 11: **a manuscript in a crowded field earns its space by being specific and bounded, not broad and ambitious.** A camera-ready PDF whose contribution sentence names a single closest competitor and a single gap, whose tables and figures share consistent typography, and whose introduction funnels from a concrete hook to a positioned contribution outscores one with stronger results buried in a weaker presentation. Hold yourself to CONVENTIONS §4 and §6 — these are the floor.

Before submitting, read Gao, He & Wu (2023, JFQA) at the abstract level and read its paragraph 5. The discipline you are graded on is the one that paragraph exemplifies: specific, bounded, positioned relative to the closest prior work.

---

## How you submit

The manuscript is *one* deliverable from three sides: the camera-ready PDF, the one-page response memo, and the repository that built both. Submit them as the `manuscript/` and `revision/` folders. The grader clones, types `make clean && make paper && make memo`, verifies the build manifest in the PDF's first-page `\thanks{}` footnote, then reads `manuscript/main.pdf` and `revision/memo11.pdf` together. The repository *is* the submission; every number, table, and figure in the PDF is `\input`ed from a code-generated artifact — never typed.

---

## The deliverable spec

### Deliverable 1 — The camera-ready PDF

**The complete manuscript as a single PDF, AEA single-column format**, compiled by `make paper` from the Lab 11 toolchain. The structure is fixed; the rubric reads it section by section.

**§Abstract (~245 words).** The five-sentence skeleton from Chapter 11.1: Question, Setting, Design, Finding, Why-It-Matters. Each sentence does its named job. The Question sentence's verb matches the Design sentence's identification strategy. The Finding sentence reports the headline magnitude with sign and unit.

**§1 Introduction (5 paragraphs, ~1,400 words).** The five-paragraph structure from Chapter 11.4: Hook, Question, What-We-Do, Findings, Contribution. Paragraph 5 contains the contribution sentence and the literature-positioning move from Mentor 11 — closest competitor named, single gap named, verb matched to design.

**§2 Data, §3 Design, §4 Results, §5 Robustness, §6 Discussion.** The body of the paper. The grader spot-checks for consistency between the abstract's headline and Table 2 column (4); for cross-references resolving (no "??"); for the bibliography in AEA style on the last page; and for the robustness section surfacing the Week-10 battery (at least one named entry per: Romano-Wolf adjustment, CATE pre-registered moderators, mechanism-via-CDE, transportability bound).

**§Tables (~4-6, all generated).** Every table `\input`ed from `manuscript/tables/*.tex`, produced by `src/build/tables.py`. The headline table (Table 2) shows four progressively richer columns of the headline DiD. The heterogeneity table (Table 3) shows the pre-registered moderator dimensions. Standard errors are clustered with the cluster level named in the table notes.

**§Figures (~2-4, all generated).** Every figure `\input`ed from `manuscript/figures/*.pdf`, produced by `src/build/figures.py`, calling `figstyle.apply()` first so typography is shared. Figure 1: event-study leads and lags. Figure 2: specification curve or Romano-Wolf-adjusted heterogeneity forest.

**§Bibliography.** AEA style. Every cited paper in `manuscript/bibliography/verified.bib`; `make bibcheck` fails the build if any citation is unverified or `[CHECK]`-tagged. Prof. Gao's cited papers appear verbatim per his CV.

### Deliverable 2 — The one-page response memo

**A one-page memo, PDF, single-spaced**, written *about* how the Week-10 robustness battery appears in the new manuscript. One page is a hard cap; padding to two earns no extra points, and trimming to half a page does not earn back length budget elsewhere. The memo is structured as four paragraphs.

**¶1 — Surface check (~150 words).** A compressed table or list naming the five Week-10 tests (Romano-Wolf, CATE, CDE, Oster, transport) and where each appears in the new manuscript: section, table or figure number, and how the paper's prose references it. The reader should see at a glance that the appendix battery has *surfaced* in the body, not just sat in the appendix.

**¶2 — The headline-vs-robust gap (~200 words).** One paragraph naming any place where the Week-10 robustness analysis *changed* a headline claim from the pre-Week-10 draft. Did Romano-Wolf knock out a "significant" heterogeneity row? Did the CDE differ from Baron-Kenny enough that the mechanism story needed editing? Did the transportability bound change the discussion section? If yes, name the change. If no, name *what would have changed* if a different parameter (a more conservative Oster $R_{\max}$, a different target population) had been chosen.

**¶3 — The honest sentence (~150 words).** The one limitation the full Week-10 battery does *not* address — the assumption that, if violated, would invalidate the headline even though every test passed. Maya's: *"the entire battery rests on the staggered-DiD parallel-trends assumption; if adopting states were on a steeper pre-treatment trend, every test in this appendix would still report the same numbers and the headline would still be wrong."* Restate in the context of the new manuscript: where does §5 or §6 acknowledge this limitation, and how does the abstract's last sentence hedge accordingly?

**¶4 — The positioning sentence (~100 words).** Apply the Mentor 11 discipline. Name the closest competitor by author, year, and journal. Write the one-sentence contribution sentence from paragraph 5, then the one-sentence positioning move naming what your design has that the closest competitor's does not. If the contribution sentence improved between draft and camera-ready, note the improvement; if not, note why the original was already defensible.

### Three rules that apply to both deliverables

1. **Every number in the PDF is `\input`ed from a generated artifact. No number typed in prose.** Typed numbers cap the reproducibility row at Developing.
2. **Causal-language discipline applies to every verb in the abstract, the introduction, and the memo.** Three or more verb-design mismatches cap the causal-language row at Developing.
3. **Build manifest visible.** The PDF's first-page `\thanks{}` footnote prints the git commit, the seed, the panel SHA-256, and the build timestamp. Missing manifest caps the reproducibility row at Missing.

---

## The analytic rubric (100 points, scaled to 80 for the gradebook)

The rubric is scored out of 100 points across six rows, then **multiplied by 0.80** to produce the gradebook score. Row weights follow the assessment topic's split (abstract 15 / tables 20 / figures 15 / intro 20 / lit review 10 = 80) plus a 20-point reproducibility-and-discipline floor that runs through every artifact.

| Criterion | Excellent | Proficient (~75%) | Developing (~50%) | Missing (0-25%) | Pts |
|---|---|---|---|---|---|
| **Abstract — five-sentence skeleton** (Ch 11.1). All five sentences present and doing their named jobs; S1 verb matches S3 design; S4 names sign, magnitude, unit; S5 is paraphrase-worthy; length 230-260 words. | One slip: S2 vague on data source, OR S5 ends on a methodological note. | Two sentences blur; S3 names method family but not assumption; OR length outside 200-280. | Three+ sentences missing or mislabeled; OR S1 verb mismatches S3 design. | **15** |
| **Tables — generated, consistent, AEA-fit** (Ch 11.2; Lab 11). Every table `\input`ed from `tables/*.tex` via `pyfixest.etable()`; stars-discipline (1%/5%/10%) in caption; SE flavor and clustering named in notes; ≤ 5 columns; display labels readable. | One slip: SE flavor unnamed in one table, OR one raw variable label. | One table typed by hand, OR star-discipline inconsistent, OR a `\resizebox` workaround. | A headline table typed, OR no clustering named, OR table number in prose disagrees with caption. | **20** |
| **Figures — generated, shared typography** (Ch 11.3; Lab 11). Every figure `\input`ed from `figures/*.pdf` via `figures.py` calling `figstyle.apply()`; PDF vector; shared palette; figure font matches body; widths = 6.0 in. | One slip: one figure PNG, OR one off-palette color. | `figstyle.apply()` missing in one function, OR one squeezed figure. | Figures inserted as PNG screenshots, OR visibly inconsistent typography. | **15** |
| **Introduction — five-paragraph funnel** (Ch 11.4; Mentor 11). All five paragraphs (Hook, Question, What-We-Do, Findings, Contribution) present and doing their jobs; ¶5 names the closest competitor explicitly; contribution sentence ≤ 30 words, single gap; ¶3 names the identification assumption; ¶1 hook is a concrete fact, not literature-review opening. | One slip: ¶2 cites > 7 papers (over-survey), OR ¶5 names two gaps. | Three+ paragraphs blur jobs; ¶5 names no closest-competitor; OR ¶1 opens with "A growing literature in finance has studied..." | Not five paragraphs (stream-of-consciousness); OR ¶5 overclaims a causal effect. | **20** |
| **Literature positioning — contribution-sentence audit** (Mentor 11; memo ¶4). Closest competitor named by author/year/journal; positioning move names what your design has that competitor's does not; verb matches design (estimates/identifies for causal; documents/characterizes for descriptive). | One slip: positioning move names two competitors, OR verb one degree too strong/weak. | Closest competitor named but positioning generic ("differs in design"); OR multiple gaps without prioritizing. | No closest-competitor named, OR causal verb on observational design. | **10** |
| **Reproducibility & causal-language floor** (Lab 11; CONVENTIONS §4-5). `make clean && make paper` rebuilds on fresh clone; manifest visible in first-page footnote; every number `\input`ed; `make bibcheck` passes (no `[CHECK]` tags); SEED threaded; env pinned. | One prose magnitude typed but matches table, OR one minor causal-language slip in §6. | Re-run needs a manual step (bibcheck fails on a citation in `unverified.bib`, OR `pdflatex main` by hand). | `make clean && make paper` does not reproduce, OR a hardcoded API key, OR three+ verb-design mismatches. | **20** |

**Total: 100 points, scaled to 80.** The intro row (20) and the tables row (20) are tied for heaviest: the intro is where Mentor 11's positioning lives, the tables are where Chapter 11.2's generated-not-typed discipline lives. The reproducibility floor (20) is heavier than any single content row because a non-reproducing build undermines every claim above it.

---

## Instructor answer key / model-answer sketch

The model answer is Maya's full camera-ready PDF and her one-page response memo.

**Abstract (15 pts).** Five sentences, 247 words. S1 (Question): *"This paper estimates the causal effect of the 2017 OCC intensified fair-lending examination program on the Black–White denial-rate gap in covered U.S. counties."* S2 (Setting): HMDA 2014-2020, 47 million originations, OCC-supervised universe, staggered rollout. S3 (Design): Callaway-Sant'Anna staggered DiD, parallel-trends assumption, F-tests on pre-period leads and Oster $\delta = 1.7$. S4 (Finding): 3.1pp reduction, s.e. 0.7, concentrated in lenders with above-median pre-period finding histories. S5 (Why-It-Matters): the policy implication with magnitude and time period.

**Tables (20 pts).** Four tables, all `\input`ed. Table 1: descriptive statistics with balance column. Table 2: headline DiD with four progressively richer columns; column (4) coefficient `-0.031`, cluster-robust s.e. `0.007`, three stars, cluster-robust at county level named in the footnote. Table 3: heterogeneity-by-examination-history with monotone pattern. Table 4: Romano-Wolf-adjusted heterogeneity with unadjusted and adjusted p-values side by side. All formatted via `pyfixest.etable()`; variable labels display-friendly; stars discipline in every caption.

**Figures (15 pts).** Figure 1: event-study with leads -5 to +5, pre-period coefficients near zero, post-period negative and growing, 95% CIs plotted. Figure 2: specification curve across 64 spec choices sorted, headline spec marked. Both call `figstyle.apply()` first; both use PALETTE `treated` blue and `null` gray; both 6.0 inches; both PDF vector. Body font matches manuscript serif.

**Introduction (20 pts).** Five paragraphs, ~1,420 words. ¶1 (Hook) opens with Atlanta 2019 and the 1.7x denial-rate ratio (Gao and Sun 2019). ¶2 (Question) cites Gao and Sun (2019), Munnell et al. (1996), Bayer-Ferreira-Ross (2018), Bhutta-Hizmo-Ringo (2024). ¶3 (What-We-Do) names the staggered DiD, parallel-trends assumption, F-test evidence, Oster $\delta$ sensitivity. ¶4 (Findings) names the 3.1pp headline and the monotone heterogeneity. ¶5 (Contribution) names Bhutta et al. (2024) explicitly, names the single gap (*targeted-by-finding-history rather than scheduled-and-broad-based*), uses *identifies* matching the credible DiD.

**Literature positioning (10 pts).** Memo ¶4: *"The closest competitor is Bhutta, Hizmo, and Ringo (2024) in the* JFE*, which estimates the effect of CRA examinations on aggregate lending volume. This paper identifies the causal effect of fair-lending-specific examination intensity — targeted-by-finding-history rather than scheduled-and-broad-based — on the racial denial gap rather than aggregate volume."*

**Reproducibility floor (20 pts).** `make clean && make paper` rebuilds `manuscript/main.pdf` in ~140 seconds. The first-page `\thanks{}` footnote reads "git=a3f9c21 panel-sha256=8d4ce0f1ab27 seed=42 built=2026-06-10 09:14:33". Every number `\input`ed; `make bibcheck` passes silently. Abstract S1's *estimates the causal effect of* matches S3's *staggered DiD ... under parallel trends*; ¶5 *identifies* matches ¶3's design; memo ¶3 uses the subjunctive *would still be wrong* rather than *is wrong* (overclaim) or *might be wrong* (underclaim).

---

## Failure modes the grader sees, in order of frequency

- **The abstract that reads as a table of contents.** Sentence 3 is "We use a difference-in-differences design" rather than naming the assumption. *Fix:* re-read Chapter 11.1 §2.3.
- **The introduction that buries the contribution.** ¶5 is two pages of literature review with the contribution sentence half-hidden. *Fix:* ¶5 starts with the contribution sentence; the literature review proper lives in section 2.
- **The contribution sentence that overclaims.** "This paper is the first to identify..." when the literature has an obvious closest-competitor. *Fix:* Mentor 11's closest-competitor audit.
- **The tables that look like Jupyter output.** Raw variable names, no clustering named, stars-discipline inconsistent. *Fix:* `pyfixest.etable()` with populated `labels=` and `notes=`.
- **The figures that switch fonts.** *Fix:* every figure function calls `figstyle.apply()` first; every figure imports `PALETTE`.
- **The build that does not reproduce.** A typed number disagrees with the regenerated table. *Fix:* grep the manuscript for any number not from `\input`.
- **The memo that flatters the work.** ¶3 reads "our identification is robust to all the tests" — the opposite of an honest sentence. *Fix:* name a *real* limitation.

An Excellent submission shows discipline in the small details — the assumption named in the abstract's sentence 3, the closest competitor named in ¶5, the standard-error flavor in every table footnote, the shared figure typography, the build manifest in the PDF's first page. Together they constitute the difference between a manuscript that reads as a *capstone* and one that reads as a *paper a journal might publish*.
