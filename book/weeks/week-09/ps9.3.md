# PS 9.3 — The One-Figure Defense

**Course:** 8-Week Empirical Finance Camp · Week 9 · Problem Set 9.3
**Covers:** Ch 9.3 (The One-Figure Defense), building on Ch 7.5 (the identification memo and the contract-form identifying assumption), Ch 8.5 (slide 3 — the design / identification slide), Ch 8.2 (the visual robustness check), and Ch 8.1 (the spec curve as one possible shape for the figure). Uses `nb9.3` — the one-figure scaffolds notebook, with templates for event-study, RD, IV-first-stage, parallel-trends, and binned-scatter figures.
**Type:** Project deliverable, not a numeric problem set. You produce a single PDF figure — `one-figure.pdf` — accompanied by a short 250-word defense memo (`one-figure.md`) that explains why this figure, alone, would carry your identification argument if everything else were lost. There is no single right answer because the answer is *your* design's load-bearing visual evidence — and what is graded is whether the figure is *self-contained* (a reader can understand the design from it alone, with no surrounding deck), *honest* (it does not hide the parts of the design that fail), and *production-grade* (the same matplotlib code that produced the figure on slide 3 of your conference deck, regenerated deterministically by `make all`).

**Total: 100 points.** Point values are stated per part. A model deliverable — Priya's wildfire-insurance event-study figure for the synthetic-control identification of climate-risk mispricing, with instructor grading notes keyed to the rubric — is in Appendix E (`E-w9-ps9.3-solutions.md`). Read it *after* you draft your own, the way Ch 9.3 walked through Priya's figure: not to copy, but to calibrate.

A boundary worth holding before you start. The "one figure" is not a *summary* figure that compresses everything you did — that figure exists already on slide 4 as your headline result. The one-figure defense is the *identification* figure: the visual argument for why the comparison you made was fair. The headline figure says *here is the number*; the one-figure defense says *here is why you should believe the number is causal*. The two are different deliverables — slide 4 reports the answer, slide 3 reports the argument for the answer. PS 9.3 builds slide 3, in production-grade form, so that if the conference projector eats every other slide you can still walk to the whiteboard, sketch this one, and the room will know what you did.

---

## What you submit

Three files, committed to `paper/figures/` in your capstone repository:

1. `one-figure.pdf` — the figure itself, 6×4 inches, vector PDF, matplotlib-built, deterministic under the project SEED. This is the figure that lives on slide 3 of your conference deck and that `make all` regenerates from raw data.
2. `one-figure.md` — a 250-word defense memo (Part 4) that, read alone, would tell a stranger what the figure is and why it carries the identification argument.
3. `one-figure.py` — the matplotlib script that produced `one-figure.pdf` from your analysis dataset, called by your `Makefile` as part of `make figures`. Standalone: a reviewer can run `python one-figure.py` and get the same PDF, byte-identical (or pixel-identical for a raster render at fixed dpi).

The whole deliverable is one page of writing plus one figure plus one script. The constraint is the point: the discipline of compressing your defense to a single image forces you to ask *which* part of your design is doing the work.

---

## Part 1 — Choose the figure type for your design (15 points)

The visual shape of an identification argument is dictated by the design. Pick *one* from this table — the one whose left column matches your design — and justify the choice in two sentences.

| Your design | The one figure is… | What the figure must *show* the eye |
|---|---|---|
| Difference-in-differences (single or staggered) | **Event-study plot** | flat leads (parallel pre-trends), a visible break at $t=0$, lags that persist |
| Regression discontinuity | **Binned-scatter with fitted-jump-at-cutoff** | a clean discontinuity at the threshold, smooth approach from both sides |
| Instrumental variables | **First-stage scatter or coefficient plot** | the instrument shifts treatment strongly (no weak-instrument concern), and ideally a *reduced-form* scatter that mirrors the structural effect |
| Synthetic control | **Treated-unit vs. synthetic-control time series** | tight pre-period match, post-period divergence, with placebo donor-unit gaps in grey |
| Event study (asset returns) | **Cumulative abnormal returns ± CI band, event-time** | flat pre-event CAR, a visible jump at $t=0$, a stable post-event level |
| Cross-sectional / panel with controls | **Coefficient plot across sequentially-added control sets** | the coefficient is stable as controls are added — *not* drifting toward zero |

**(a) Match (8 pts):** state which design you use and which figure type from the table you chose. If your design does not fit cleanly (a structural-model paper, say), choose the type whose *visual rhetoric* most resembles your identification argument and justify the substitution in one sentence.

**(b) Why this figure carries the argument (4 pts):** in one or two sentences, name *what the eye sees in this figure that no other figure shows*. Priya's synthetic-control plot shows the synthetic California tracking real California penny-for-penny in the pre-period and diverging visibly at the wildfire-mispricing event — *the parallel-trends defense made literal as two overlapping lines that pull apart at a date you can point to.*

**(c) The alternative you rejected (3 pts):** state, in one sentence, the figure type you *did not* choose and why. Sam considered both an event-study CAR plot and a coefficient-stability plot, and chose the CAR plot because his identification rests on the intraday-momentum trading window being the only event — and the CAR plot literally shows the cumulation across the window, while the coefficient plot would have shown *that the coefficient is stable*, which is a different claim.

---

## Part 2 — Build the figure deterministically with matplotlib (35 points)

The figure is built in `one-figure.py` using the project's pinned matplotlib stack (CONVENTIONS §5: `matplotlib.use("Agg")` for non-interactive, `np.random.default_rng(SEED)` from `config.SEED` for any randomness). The reproducibility bar from Lab 7 and PS 8.5 holds: a fresh clone running `make all` produces a `one-figure.pdf` byte-identical to the committed one, and the figure on slide 3 of `slides-vfinal.pdf` is *the same file*.

**(a) The script structure (10 pts).** `one-figure.py` follows this skeleton, with the design-specific body in the middle:

```python
# one-figure.py — slide-3 identification figure, regenerated by make all
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from config import SEED  # the single named seed (PS 8.5 Part 4e)

rng = np.random.default_rng(SEED)

# 1. Load the analysis dataset (NOT raw data — that's 02_build.py's job).
df = pd.read_parquet("data/processed/analysis.parquet")

# 2. Compute what the figure needs (event-time effects, CIs, etc.).
#    All computation here is deterministic OR seeded.
# ...

# 3. Build the figure at 6x4 inches; one panel unless your design genuinely needs two.
fig, ax = plt.subplots(figsize=(6, 4), dpi=150)
# ... draw the design-specific content ...
ax.set_xlabel("event time (years)")
ax.set_ylabel("effect on denial gap (pp)")
ax.axhline(0, color="0.5", lw=0.5)            # reference zero line
ax.axvline(0, color="0.5", lw=0.5, ls="--")   # treatment-onset reference
ax.set_title("")  # title goes in the slide, not the figure
fig.tight_layout()
fig.savefig("paper/figures/one-figure.pdf", bbox_inches="tight")
plt.close(fig)
```

Grading on the script:

- **Determinism (4 pts):** uses the project SEED through `np.random.default_rng(SEED)`; no `np.random.seed()` legacy globals; no system-time-based randomness; no parallelism that re-orders output.
- **No hand-pasted data (3 pts):** the script reads the analysis dataset built by your pipeline; no inline numbers, no hard-coded coefficients. If a number drifts upstream, the figure drifts with it — that is the property that keeps the slide-figure and the paper-table in sync (PS 8.5 Part 4f).
- **Matplotlib defaults respected (3 pts):** no seaborn-style overrides, no rcParams hacking that the rest of the repo does not adopt; the figure looks like every other figure your paper produces, because it *is* one of them.

**(b) The figure itself, drawn (15 pts).** The visual content of the figure must satisfy:

- **One panel unless your design genuinely needs two.** A two-panel figure (an event-study atop a parallel-trends test, say) is acceptable *if* the second panel carries an argument the first does not. A two-panel figure where the second panel is decorative loses points. The point of the exercise is compression.
- **Axes labeled in human units.** "effect on denial gap (pp)" not "$\hat{\beta}$"; "event time (years)" not "k"; "cumulative abnormal return (%)" not "CAR". A figure that lives on a slide is read by ears, not eyes — the axis label must work for someone hearing you say "the y-axis is the percentage-point effect" out loud.
- **Reference lines drawn.** A horizontal zero-line where the null lives; a vertical line at $t=0$ for event studies, or at the cutoff for RD. Without these, the eye has no anchor and the figure becomes decorative.
- **Confidence intervals shown, not implied.** A point estimate without a CI band reads as naïve. Use shaded bands (`ax.fill_between`) for event-time effects; use error-bar markers for discrete coefficients; use the synthetic-control placebo gaps in grey to *be* the implicit uncertainty.
- **Readable from the back of the room.** Use a tick-label font size of at least 9 pt at the final 6×4-inch render; line widths at least 1.2 pt for the main series; markers at least 5 pt. The matplotlib default `rcParams` are *not* readable from row 20 — tune them in the script.
- **Strip the dead ink.** No gridlines unless they carry the argument; no legend on a one-series plot; no third decimal on tick labels; no figure title that duplicates the slide title.

**(c) The legend / annotation rule (5 pts).** Exactly one of the following: an inline annotation (`ax.annotate`) that names what the eye should see, *or* a 2-3 line legend, *or* nothing if the figure is self-explanatory with axes alone. Never all three. The annotation, when used, is one short sentence — *"flat leads → parallel-trends defense"* — placed in a part of the figure with whitespace. The Ch 9.3 §2 rule: *if you need three legends and four annotations, you have not yet chosen what the figure is for.*

**(d) Render at print quality (5 pts).** Save as vector PDF at the size that will appear on slide 3 (6×4 inches typical) with the slide's font face matching the paper's font face — the figure and the slide should look *of a piece*, not like the figure was airlifted in from a different document. If your conference template uses Helvetica and your matplotlib default is DejaVu Sans, fix the font in the script (`matplotlib.rcParams["font.family"]`) so the figure matches.

---

## Part 3 — Self-containment test (20 points)

The single most important property of the one-figure defense: *a stranger looking at the figure alone, with no slide context, no paper, no caption beyond the figure's own annotations, must be able to reconstruct what your identification argument is.* If they cannot, the figure is doing less work than you think it is.

**(a) The blind-stranger test (10 pts).** Send `one-figure.pdf` *only* — no slides, no paper, no email body — to a peer who has *not* worked on your project. Ask them two questions and record their answers:

1. *"What design do you think this paper uses?"*
2. *"What's the identifying assumption, in one sentence?"*

If the peer answers (1) correctly (event study, DiD, RD, IV, synthetic control), the figure carries the *design*. If they answer (2) with anything resembling your Ch 7.5 contract-form sentence, the figure carries the *argument*. Record both their answers and your evaluation (matched / partially matched / did not match). A figure that fails the blind-stranger test is a figure that, on stage, will fail the projector-eats-the-deck test — and the fix is to add the annotation, the reference line, or the second panel that lets the design read off the figure alone.

If the peer is not available, do the test on yourself by *looking at your own figure with the script and the analysis dataset hidden*, after 24 hours. Self-blinding is weaker than peer-blinding but better than nothing; note which you did.

**(b) The "design slide replaced by this figure" test (5 pts).** Open `slides-vfinal.pdf`, remove slide 3 entirely, and replace it with just `one-figure.pdf` filling the slide. Re-rehearse your slide-3 talking from PS 8.5 Part 1(c) — the *"our estimate is credible if X, defended by Y"* sentence. Does the figure carry the sentence? If the sentence needs the slide's text overlay, the figure is under-built. Add the annotation that lets the figure stand without the text. (You will keep the text on slide 3 in the final deck — but the figure must be able to stand without it.)

**(c) The honest-failure annotation (5 pts).** If your design has a known weak point that the figure *should not hide* — a pre-period that is flat but only after dropping the noisiest cohort, or a synthetic-control donor pool that only matches reasonably on the pre-period level but not the slope — *annotate it on the figure itself, in small print.* Hiding the weakness in the figure means it surfaces in Q&A as an ambush; annotating it disarms the ambush in advance. The annotation can be as short as *"pre-trend test excludes 2020 (COVID-disrupted)"* placed inconspicuously near the relevant axis. Honesty in the figure is part of what the rubric rewards.

---

## Part 4 — The 250-word defense memo (`one-figure.md`) (20 points)

A short prose document that, read alone, would tell a stranger what the figure is and why it carries the identification argument. Word count is tight by design: 250 ± 25 words, three to four paragraphs, no more.

**(a) The four required paragraphs (15 pts):**

1. **What the figure shows (≈60 words):** name the design, the axes, and what the eye should look for. *"This is the event-study plot for Maya's staggered fair-lending DiD. The horizontal axis is event time in years relative to a state's adoption of an examination program; the vertical axis is the effect on the county-year minority–white denial gap, in percentage points. The dots are average effects across cohorts; the shaded band is the 95% confidence interval."*
2. **Why it carries the identification argument (≈80 words):** name the identifying assumption and show how the figure makes it visible. *"The identifying assumption is that, absent the exam programs, treated and never-treated counties' denial gaps would have moved in parallel. The figure defends the assumption visually: the pre-period dots sit flat on the zero line — no diverging pre-trend the eye can see — and the post-period dots drop and stay down. If the assumption failed, the pre-period would tilt; it does not."*
3. **What the figure cannot answer (≈60 words):** the honesty paragraph. *"The figure cannot speak to selection into adoption — why some states chose to adopt and others did not. It also cannot show channel: it shows that exams move the gap, not why. Those questions live in robustness specs (PS 8.2) and in the contribution slide's deliberate scoping clause. The figure carries identification, not mechanism."*
4. **The one sentence you would say aloud while pointing at the figure (≈30 words):** the sentence is the verbal annotation that pairs with the visual annotation in Part 2(c). *"Watch the leads — they sit on zero — and watch the post-adoption dots drop to about minus-1.8 and stay. That gap is the result."*

**(b) Style discipline (5 pts).** No hedging adverbs (*"basically", "essentially", "arguably"* — banned). No two adjectives where one would do. No mention of the rest of the paper — the memo defends the figure *alone*. The 250-word count is enforced with a `wc -w one-figure.md` check; ±25 is the tolerance.

---

## Part 5 — Reproducibility and pipeline integration (10 points)

The figure must regenerate from raw data when `make all` runs on a fresh clone (PS 8.5 Part 4f), and the figure on slide 3 of `slides-vfinal.pdf` must be the *same file* as `paper/figures/one-figure.pdf`.

**(a) `Makefile` entry (4 pts):** add the figure to your build target:

```makefile
paper/figures/one-figure.pdf: data/processed/analysis.parquet src/one-figure.py
	python src/one-figure.py

figures: paper/figures/one-figure.pdf paper/figures/event-study.pdf paper/figures/spec-curve.pdf

all: figures paper/paper.pdf
```

The dependency line is what makes `make` regenerate the figure when the analysis dataset changes — never let the figure drift behind the data.

**(b) Slide-figure binding (4 pts):** in `slides-vfinal.pptx` or `.tex`, slide 3 references `paper/figures/one-figure.pdf` *as a linked file*, not as an embedded copy. (In Beamer: `\includegraphics{paper/figures/one-figure.pdf}`. In PowerPoint: insert-link, not insert-embed.) When `make all` rebuilds the figure, slide 3's image updates on the next render of the deck. State in `one-figure.md` how your deck is bound to the figure file — *"slide 3 links to `paper/figures/one-figure.pdf`; rebuilding the figure with `make figures` updates the slide on next deck render."*

**(c) The byte-identical rebuild check (2 pts):** confirm, with a hash, that the committed `one-figure.pdf` is byte-identical to the one a fresh `make all` produces. Note the SHA-256 in `one-figure.md` (or in the PS 9.1 pre-flight log). If the hash drifts on rebuild, the script has a non-determinism — diagnose per PS 9.1 Part 2(c).

---

## Submission checklist

Before you commit, confirm:

- [ ] `one-figure.pdf`, `one-figure.md`, and `one-figure.py` are all committed under `paper/figures/` (or wherever your repo holds figures).
- [ ] The figure type chosen matches your design (Part 1 table), with a one-sentence justification and a one-sentence rejected alternative.
- [ ] The matplotlib script uses `matplotlib.use("Agg")`, the project `SEED` via `np.random.default_rng(SEED)`, and reads from the analysis dataset, not hard-coded numbers.
- [ ] The figure has labeled axes in human units, a reference zero/cutoff line, confidence intervals shown (not implied), readable font sizes at the render scale, and dead ink stripped.
- [ ] One of {annotation, short legend, nothing} — not all three.
- [ ] The blind-stranger test was run on a peer (or, weaker, self-blinded after 24 hours), with both answers recorded and the evaluation noted.
- [ ] The figure has been visually placed *alone* on slide 3 in a test render, and the slide-3 talking sentence still lands.
- [ ] Any known weakness is annotated honestly *on* the figure, not hidden.
- [ ] `one-figure.md` is 250 ± 25 words, four paragraphs, with the required content per (4a).
- [ ] `Makefile` has a `paper/figures/one-figure.pdf` rule; slide 3 of `slides-vfinal.pdf` links to (not embeds) the figure file; the rebuild is byte-identical.

---

## How this is graded

Part 1 (design match and figure type choice, 15) on whether the figure-shape matches the identification design. Part 2 (build the figure, 35 — the heaviest part) on whether the matplotlib script is deterministic, the figure is production-grade, and the visual carries the design. Part 3 (self-containment, 20) on whether the blind-stranger test passed and any weakness is annotated honestly. Part 4 (defense memo, 20) on whether the 250-word memo, read alone, defends the figure. Part 5 (reproducibility, 10) on whether `make all` regenerates the figure byte-identically and the slide links to (not embeds) the file. The highest-signal single check: **a peer who has not seen your paper, given only `one-figure.pdf`, can name your design and your identifying assumption.** A `Y` says the figure is doing its job; a `N` says you have more annotating to do.

---

## The bridge to PS 9.4

PS 9.3 compressed your defense to one figure for a *slide*; PS 9.4 explodes the *whole paper* onto a *poster* — a 48×36-inch object that lives in a hallway, that a stranger walks up to, that *must* survive the same projector-eats-the-deck condition: every key claim, every key figure, all visible at arm's length, all regenerable from `make poster`. The one-figure defense becomes the *center* of the poster, surrounded by the rest of the paper's argument compressed into the surrounding panels.

*End of PS 9.3. The model deliverable is in `book/appendices/E-solutions-manual/E-w9-ps9.3-solutions.md`. Build your own figure first; read the exemplar to calibrate, not to copy. The figure that survives projector failure and the figure that wins your defense are the same figure — this assignment is you producing it on purpose, not by accident.*
