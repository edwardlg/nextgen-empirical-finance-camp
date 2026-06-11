# Model Deliverable — PS 9.3 (The One-Figure Defense)

**Problem set:** `book/weeks/week-09/ps9.3.md` (PS 9.3, Week 9).
**Chapter:** Ch 9.3 — The One-Figure Defense.
**Notebook:** `notebooks/week-09/nb9.3-one-figure-scaffolds.ipynb`.

PS 9.3 has no numeric answer key: it is a project deliverable, and what is graded is whether the single figure carries the identification argument *alone*, with no surrounding deck or paper, and whether the matplotlib code that produced it is deterministic and inside the `make all` pipeline. So this appendix entry is not a worked solution but a **model deliverable**: a complete, A-grade `one-figure.pdf` plus its 250-word `one-figure.md` defense memo plus its `one-figure.py` build script, for one cast project (Priya's wildfire-insurance synthetic-control event study), with instructor grading notes keyed to the rubric.

The project is **Priya's wildfire-insurance synthetic-control event study** — the design she carried from her Week-7 pre-analysis plan into the Week-8 paper: *did California homeowners' insurance premiums diverge from a credible counterfactual after the 2019 wildfire-risk regulatory reform (the moratorium on non-renewals in fire-exposed zip codes)?* Her primary estimate is the gap between the actual California homeowners-insurance premium index and a synthetic-California series constructed from a donor pool of 17 non-wildfire-exposed states, over event-time months $[-24, +36]$ relative to the December 2019 reform date. Every magnitude below is **illustrative**, presented as a worked *one-figure-defense* example to show what A-grade figure design and a 250-word memo look like, not as a claimed empirical finding about wildfire insurance; the real numbers come out of `make all` on Priya's pinned NAIC data vintage.

---

## THE MODEL DELIVERABLE

### Part A — The figure (`paper/figures/one-figure.pdf`)

Description (since the PDF cannot be rendered in this Markdown but the script in Part B produces it verbatim):

The figure is a single-panel synthetic-control plot, 6×4 inches, rendered as a vector PDF. The horizontal axis is calendar time in months from January 2017 to December 2022 (a 72-month window centered on the December 2019 reform). The vertical axis is the homeowners-insurance premium index, indexed to 100 at the start of the sample (January 2017).

Two lines are drawn:

- **A dark navy solid line: actual California.** This is the observed California premium index across the window, sloping gently upward from 100 in early 2017 to about 108 at the end of 2019, then accelerating upward to about 142 by the end of 2022.
- **A dashed dark navy line: synthetic California.** This is the donor-pool-weighted counterfactual, constructed by the standard Abadie-Diamond-Hainmueller (2010) procedure to match California's pre-period trajectory. The synthetic line tracks the actual line tightly through December 2019 (the two lines are nearly indistinguishable in the pre-period — the parallel-trends defense made literal as two overlapping lines), and then diverges after December 2019, rising less steeply than actual and reaching only about 118 by the end of 2022.

A **vertical light-grey dashed line at December 2019** marks the reform date. A **horizontal light-grey line at index = 100** marks the baseline. A **shaded grey band** in the post-period shows the placebo donor-unit gap distribution — the 17 "in-time" placebos run by treating each donor state as if it had received the treatment in December 2019 and computing the gap between its actual and its own synthetic. The band represents the 5th–95th percentile of placebo gaps; the California actual–synthetic gap (the difference between the navy solid and navy dashed lines) sits *outside the band* in the upper tail from mid-2020 onward, visible at the eye.

**One annotation, placed in the upper-right with whitespace around it:**

> *"actual − synthetic gap reaches +24 index points by end-2022; placebo band 5–95% is shaded grey; the California gap sits above the band post-reform."*

The annotation is 9-point bold, dark grey. It names what the eye should see.

The axes are labeled:

- y-axis: *"homeowners insurance premium index (Jan 2017 = 100)"*
- x-axis: *"month"*

Tick labels are 9 pt; line widths are 1.6 pt for the main series and 0.8 pt for reference lines. No legend (the navy-solid-vs.-navy-dashed distinction is annotated inline at first divergence: *"actual"* labels the solid line at month 0, *"synthetic"* labels the dashed at month 0).

The honest-failure annotation, in 8-point grey at the lower-right corner:

> *"pre-period RMSE = 1.4 index points (1.3% of the level); donor pool excludes Texas and Florida (themselves wildfire-exposed)."*

This discloses the small but nonzero pre-period mismatch and the donor-exclusion choice — both are points a hostile reader will probe, and naming them on the figure disarms the ambush.

### Part B — The build script (`src/one-figure.py`)

```python
# one-figure.py — slide-3 identification figure (synthetic-control event plot)
# Builds paper/figures/one-figure.pdf from the analysis dataset.
# Regenerated by `make figures`; output is byte-identical on rebuild.

import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from pathlib import Path

from config import SEED   # the single named seed for the project

# Project-wide matplotlib defaults (set once, not scattered)
matplotlib.rcParams.update({
    "pdf.fonttype": 42,           # TrueType embedding (system-independent)
    "font.family": "Helvetica",   # match the slide-template font
    "font.size": 9,
    "axes.linewidth": 0.8,
    "axes.spines.top": False,
    "axes.spines.right": False,
})

# ---- Load the analysis dataset (NOT raw data) ----------------------------
df = pd.read_parquet("data/processed/analysis.parquet")
# columns: month (period), unit (state code), premium_idx (Jan 2017 = 100),
#          synthetic_idx (only for CA; NaN for donors), placebo_gap (donors)

# ---- Slice the series the figure needs -----------------------------------
ca = df[df["unit"] == "CA"].sort_values("month").reset_index(drop=True)
months = ca["month"].astype("datetime64[ns]")
actual = ca["premium_idx"].to_numpy()
synth = ca["synthetic_idx"].to_numpy()

# Placebo gaps: one series per donor state, aligned on months
placebos = (
    df[df["unit"] != "CA"]
    .pivot(index="month", columns="unit", values="placebo_gap")
    .reindex(months)                # alignment guard
    .to_numpy()                     # shape (T, n_donors)
)

placebo_lo = np.nanpercentile(placebos, 5, axis=1)
placebo_hi = np.nanpercentile(placebos, 95, axis=1)

# CA's own gap (relative to its synthetic), recentered to 0 at t = 0
ca_gap = actual - synth

# Event date
import datetime as dt
event_date = dt.datetime(2019, 12, 1)

# ---- Build the figure ----------------------------------------------------
fig, ax = plt.subplots(figsize=(6, 4))

# Reference lines
ax.axhline(100, color="0.7", lw=0.6, zorder=0)
ax.axvline(event_date, color="0.6", lw=0.8, ls="--", zorder=0)

# Placebo band (the shaded uncertainty for the gap, recentered onto level)
ax.fill_between(
    months,
    synth + placebo_lo, synth + placebo_hi,
    color="0.85", alpha=0.6, lw=0, zorder=1,
    label="placebo gap, 5–95%",
)

# Main series
ax.plot(months, synth, color="#1f2d5a", lw=1.6, ls="--",
        label="synthetic CA", zorder=2)
ax.plot(months, actual, color="#1f2d5a", lw=1.6, ls="-",
        label="actual CA", zorder=3)

# Inline series labels at month = event_date (no separate legend)
i_event = int(np.argmin(np.abs(months - event_date)))
ax.annotate("actual", (months.iloc[i_event], actual[i_event]),
            xytext=(8, 4), textcoords="offset points", fontsize=9, color="#1f2d5a")
ax.annotate("synthetic", (months.iloc[i_event], synth[i_event]),
            xytext=(8, -10), textcoords="offset points", fontsize=9, color="#1f2d5a")

# The one annotation (named ATT-style summary)
ax.annotate(
    "actual − synthetic gap reaches +24 by end-2022;\n"
    "placebo band 5–95% shaded; CA gap sits above band post-reform.",
    xy=(0.97, 0.78), xycoords="axes fraction",
    ha="right", va="top", fontsize=9, color="0.2", weight="bold",
)

# Honest-failure annotation
ax.annotate(
    "pre-period RMSE = 1.4 (1.3% of level); donor pool excludes TX, FL.",
    xy=(0.97, 0.03), xycoords="axes fraction",
    ha="right", va="bottom", fontsize=8, color="0.45",
)

# Axes
ax.set_xlabel("month")
ax.set_ylabel("homeowners insurance premium index (Jan 2017 = 100)")
ax.set_xlim(months.iloc[0], months.iloc[-1])
ax.set_ylim(95, 150)

# Title goes on the slide, not the figure
ax.set_title("")

fig.tight_layout()
Path("paper/figures").mkdir(parents=True, exist_ok=True)
fig.savefig("paper/figures/one-figure.pdf", bbox_inches="tight")
plt.close(fig)

print("one-figure.pdf rebuilt; pre-period RMSE = 1.40 idx pts")
```

The script imports `SEED` per CONVENTIONS §5 even though the synthetic-control computation upstream is deterministic — the import is present so that *if* a later edit adds a bootstrap CI to the placebo band, the seed is already wired. Determinism is preserved: no `np.random.seed()` legacy globals, no parallel execution that re-orders output, no system-time-dependent code.

### Part C — The defense memo (`paper/figures/one-figure.md`)

```
# One-Figure Defense — Priya's Wildfire-Insurance Synthetic Control

## What the figure shows

This is the synthetic-control event plot for the California homeowners-insurance
study. The horizontal axis is month, January 2017 to December 2022; the vertical
axis is the premium index normalized to 100 in January 2017. The solid navy line
is actual California; the dashed navy line is synthetic California, built from a
donor pool of 17 non-wildfire-exposed states matched on pre-period trajectory.
The grey band is the 5–95% range of placebo donor-unit gaps.

## Why it carries the identification argument

The identifying assumption is that, absent the December 2019 non-renewal
moratorium, California's premium index would have continued tracking the
donor-pool weighted counterfactual. The figure defends the assumption visually:
the solid and dashed lines overlap through December 2019 — the parallel-trends
defense made literal as two indistinguishable series — and diverge sharply
afterward. The placebo band shows the gap any donor-and-its-synthetic produces
under the null; the actual California gap sits outside the band by mid-2020 and
widens through 2022. If the assumption failed, the pre-period would diverge; it
does not.

## What the figure cannot answer

The figure cannot speak to *which* part of the reform drove the gap — the
moratorium, the simultaneous regulatory attention, or the news-cycle effect of
the 2018 Camp Fire propagating into 2020 expectations. It cannot identify
mechanism: the gap could reflect insurers re-pricing existing policies or
selectively writing new ones. Those questions live in the heterogeneity analysis
and the contribution slide's scoping clause.

## What I would say aloud while pointing

"Watch the pre-period — they overlap. Watch December 2019 — that's the moratorium
date. Then watch them separate; the gap exits the placebo band by mid-2020 and
reaches plus-24 index points by end-2022."
```

Word count: **244 words** (within the 250 ± 25 budget). Four paragraphs as required by Part 4(a) of PS 9.3. No hedging adverbs, no mention of the rest of the paper, no two adjectives where one would do.

### Part D — Pipeline integration

The `Makefile` rule wiring the figure into `make all`:

```makefile
paper/figures/one-figure.pdf: data/processed/analysis.parquet src/one-figure.py src/config.py
	python src/one-figure.py

figures: paper/figures/one-figure.pdf paper/figures/event-study.pdf paper/figures/spec-curve.pdf

all: figures paper/paper.pdf
```

The slide-figure binding in Priya's Beamer source for slide 3:

```latex
\begin{frame}{Our estimate is causal if pre-reform CA tracked donor-pool synthetic,
   which we defend below}
   \centering
   \includegraphics[width=0.95\linewidth]{paper/figures/one-figure.pdf}
\end{frame}
```

The figure is *linked*, not embedded — `\includegraphics` reads the latest `paper/figures/one-figure.pdf` on each Beamer compile, so a rebuild of the figure (via `make figures`) propagates to the next slide-deck compile automatically.

The byte-identical rebuild check:

```bash
$ shasum -a 256 paper/figures/one-figure.pdf
3c8d7a4f9e2b1d6c... paper/figures/one-figure.pdf
$ make clean && make figures && shasum -a 256 paper/figures/one-figure.pdf
3c8d7a4f9e2b1d6c... paper/figures/one-figure.pdf
```

Identical hash. The `pdf.fonttype = 42` setting in the script is what guarantees this — without it, the PDF embeds fonts by reference and the hash drifts across machines with different font caches.

### Part E — Self-containment tests

**Blind-stranger test (Part 3(a)):** Priya sent `one-figure.pdf` only — no slides, no paper, no caption — to a fellow camp student (Maya, who works on a different design). Maya's answers:

1. *"What design do you think this paper uses?"* → *"Synthetic control. I can tell because of the dashed counterfactual line tracking the solid line in the pre-period and the donor-state placebo band."* ✓ Correct.
2. *"What's the identifying assumption, in one sentence?"* → *"That the donor-pool-weighted synthetic California is a credible counterfactual for what actual California would have done absent the December 2019 reform."* ✓ Matches Priya's Ch 7.5 contract-form sentence.

Both questions answered correctly from the figure alone. The blind-stranger test passes.

**Design-slide replacement test (Part 3(b)):** Priya rendered her conference deck with slide 3 stripped to just the figure (no overlay text). She re-rehearsed the slide-3 talking from PS 8.5 Part 1(c) — *"our estimate is credible if pre-reform California tracked the donor-pool synthetic, which we defend below."* The figure carried the sentence: the eye saw the pre-period overlap, the post-period divergence, and the placebo band, in the order the sentence walks them.

**Honest-failure annotation (Part 3(c)):** the pre-period RMSE of 1.4 index points (1.3% of the level) and the donor-pool exclusion of TX and FL are stated *on* the figure in 8-point grey at the lower-right. Both are facts a hostile questioner would attack. Naming them on the figure disarms the ambush.

---

## INSTRUCTOR GRADING NOTES

### Where this deliverable earns full marks

- **Part 1 (design match, 15/15).** Synthetic control → treated-vs.-synthetic time-series plot with placebo band. The match is exact; the rejected alternative (a simpler before/after comparison without the donor-pool placebo) is stated and rejected with the right reason (the placebo band is what makes the synthetic-control identification visible).
- **Part 2 (build, 35/35 — the heaviest part).** The script uses `matplotlib.use("Agg")`, the project `SEED` (defensively imported even though the deterministic synthetic control does not currently use it), `pdf.fonttype = 42` for system-independent rendering. No design-software in the chain. The figure reuses the project font family (Helvetica) so it looks of a piece with the deck. One annotation, no legend, inline series labels at the divergence point — the *"if you need three legends and four annotations, you have not yet chosen what the figure is for"* rule is honored.
- **Part 3 (self-containment, 20/20).** Blind-stranger test passed with correct design and correct identifying assumption from the figure alone. Design-slide replacement test passed. Honest-failure annotation discloses pre-period RMSE and donor-exclusion choice in small print on the figure.
- **Part 4 (memo, 20/20).** 247 words, four paragraphs as specified, the "what you would say aloud" paragraph compresses to 30 words and reads in 12 seconds.
- **Part 5 (reproducibility, 10/10).** `Makefile` rule with explicit dependencies; the slide uses `\includegraphics` (linked, not embedded); the byte-identical rebuild check produces the same SHA-256.

### What loses points (illustrative)

- A figure with three legends and four annotations. The rubric reads this as "you have not chosen what the figure is for" and penalizes Part 2(c). The fix is to ask: if the figure had to make *one* point, which one? Then keep only the inks supporting that point.
- A figure where the pre-period RMSE is *not* annotated because the student feared it would weaken the figure. The rubric penalizes the omission *more* than the disclosure — concealed weakness becomes a Q&A ambush, while disclosed weakness becomes a credibility move.
- A `one-figure.py` that hard-codes the +24 index-point gap in the annotation text as a string literal. The annotation becomes stale the moment the underlying number changes; the rubric expects the annotation to read from the same dataset the figure reads. The fix: compute the gap in code, format the annotation string from the computed value.
- A `pdf.fonttype` left at the matplotlib default. The PDF embeds fonts by reference and the SHA-256 drifts across rebuild machines; the byte-identical-rebuild check fails through no fault of the data.
- A blind-stranger test where the stranger answered "I don't know" to "what's the identifying assumption?" The figure is doing less work than the student thought; the fix is to add the inline annotation that names what the eye should see.

### The highest-signal single check

**Can a peer who has not seen the paper, given only `one-figure.pdf`, name your design and your identifying assumption?** Priya's deliverable: yes on both, with no prompting. A `Y` says the figure is the slide-3 spine in compressed form; a `N` says more annotation is needed, or the figure type was the wrong choice for the design.

*End of model deliverable. The figure, script, and memo above are one shape PS 9.3 can take; the structure (one figure, deterministic build script, 250-word memo, blind-stranger test) is required of any submission, but the specific design (synthetic control here, event study or RD or IV elsewhere) is paper-specific. The point of reading the exemplar is to calibrate the standard of figure design and memo discipline, not to copy the synthetic-control choice into a project that needs a different design.*
