# PS 9.4 — The Poster Version of Your Paper

**Course:** 8-Week Empirical Finance Camp · Week 9 · Problem Set 9.4
**Covers:** Ch 9.4 (The Poster Version of Your Paper), building on Ch 8.5 (the 8-minute deck and the one-click replication packet), Ch 9.3 (the one-figure defense), Ch 7.5 (the contract-form identifying assumption), and Lab 7 / Lab 8 (the reproducible build pipeline). Uses `nb9.4` — a matplotlib `Figure` constructor that builds a single 48×36-inch poster from your existing analysis dataset and figure scripts.
**Type:** Project deliverable, not a numeric problem set. You produce a single 48×36-inch landscape PDF poster — `poster.pdf` — that compresses your paper into a *physical, hallway-readable* object. The poster is built entirely from matplotlib (no PowerPoint, no Affinity Publisher, no LaTeX poster template) using a single `nb9.4` notebook or `make poster` target, so a fresh `make all` regenerates the poster byte-identically. There is no single right answer because the answer is *your* paper's poster — and what is graded is whether the poster is *legible at three feet* (the conference hallway distance), *self-contained* (a stranger walking up understands the question, the design, and the answer without you standing next to it), and *reproducible* (the same Python code that builds slide 3's figure also builds the poster's center panel).

**Total: 100 points.** Point values are stated per part. A model deliverable — Leah's patent-text NLP poster on the Elnahas-Gao-Hossain-Kim (2024) CEO-political-ideology forward-disclosure result, with instructor grading notes keyed to the rubric — is in Appendix E (`E-w9-ps9.4-solutions.md`). Read it *after* you draft your own, the way Ch 9.4 walked through Leah's poster: not to copy, but to calibrate.

A boundary to hold throughout. A poster is not a *shrunken paper*; if you take your 30-page manuscript and squeeze the text small enough to fit a poster, you have built an unreadable object — and the conference hallway will simply route around it. A poster is also not a *blown-up slide deck*; the medium is different. A poster is a *standalone argument that a stranger reads in 60 seconds while standing three feet away*, and what survives that constraint is: the question, the design picture, the headline figure, the contribution. Everything else is decoration. PS 9.4 is the discipline of producing the standalone-60-second-3-feet object, in code, reproducibly, so it carries the same byte-identical numbers as your deck and your paper.

---

## What you submit

Three files, committed to `paper/poster/` in your capstone repository:

1. `poster.pdf` — the 48×36-inch landscape PDF, matplotlib-built, deterministic under the project SEED. This is the file you send to the print shop *and* the file `make poster` regenerates from raw data.
2. `poster.py` — the single Python script that builds the poster from your analysis dataset and existing figure scripts; called by `make poster`.
3. `poster.md` — a short 200-word build memo (Part 5) documenting print specs, the rebuild hash, and the public URL where a hallway viewer can scan a QR code to reach the repo.

The whole deliverable is one poster plus one script plus one short memo. The constraint of a single matplotlib script — no design software in the chain — is what guarantees the poster lives inside the reproducibility pipeline alongside the paper figures.

---

## Part 1 — The poster grid and content compression (25 points)

A 48×36-inch landscape canvas is large in absolute terms but small in *information-bandwidth* terms: a viewer reads roughly 60 seconds before they decide to keep walking or stay. The grid choice and what you put in it are everything.

**(a) Choose and justify the grid (5 pts).** The canonical conference-poster grid for an empirical-finance paper is a **3-column × 3-row** layout with the *center panel oversized* (spanning the two middle cells, or roughly 24×16 inches). State which grid you use; the recommended default for an empirical paper is:

| | Column 1 (left) | Column 2 (center) | Column 3 (right) |
|---|---|---|---|
| **Top row** | Title / authors / affiliations | (spans into center) Question + Why-it-matters | Repo URL + QR code |
| **Middle row** | Design / identification — the one-figure-defense figure (from PS 9.3) | **Headline figure (oversized)** | Robustness — the spec curve (from PS 8.1) |
| **Bottom row** | Data sources + sample | Contribution + what we do *not* claim | Pre-registration / replication note |

If your design genuinely needs a different grid — a two-event-study comparison, a regression-discontinuity with two outcome panels — choose it and justify in one sentence. But the default is the default for a reason: the eye reads top-left → top-center → middle-center → right, and the grid above puts the question where the eye lands first and the headline where it dwells longest.

**(b) Title bar — the title test for posters (5 pts).** The title at the top is a *full-sentence claim*, not a noun phrase, exactly per PS 8.5 Part 2(a). *"Do Fair-Lending Exams Shrink the Mortgage Denial Gap?"* is a poster title; *"Examining Fair-Lending Examinations"* is not. The title is set at 72-point sans-serif (Helvetica or equivalent), readable from across a hallway. Author names, affiliations, and the camp/conference go in 36-point underneath.

**(c) Content compression — the 200-word body rule (10 pts).** Across *all* prose panels combined (question, why-it-matters, design caption, headline interpretation, contribution, data note), the total word count is **≤ 200 words**. The discipline is the point: a poster that exceeds 200 words is a paper-shrunk-to-fit, not a poster. Each panel does its job in one or two short sentences:

- **Question (≤30 words):** one sentence, identical phrasing to slide 1 of your deck.
- **Why-it-matters (≤40 words):** one concrete stake with one number for scale; identical phrasing to slide 2 of your deck.
- **Design caption (≤40 words):** the contract-form identifying-assumption sentence from Ch 7.5, sitting under the one-figure-defense figure.
- **Headline interpretation (≤30 words):** the human-units sentence that pairs with the headline figure ("1.8 percentage points, about a fifth of the baseline gap").
- **Contribution (≤40 words):** the new-knowledge sentence and the *what-we-do-not-claim* clause from slide 6.
- **Data/replication note (≤20 words):** one sentence on data sources and a pointer to the repo URL.

A panel that exceeds its budget is rebalanced *to itself*, not by stealing words from another panel — the totals discipline is what produces a hallway-readable poster.

**(d) Figure budget — three figures, no more (5 pts).** The poster carries *exactly three* figures: (i) the design/identification figure from PS 9.3, (ii) the headline figure from slide 4 of your deck, and (iii) the robustness/spec-curve figure from PS 8.1 (or its equivalent for your design). Each is a vector PDF generated by your existing figure scripts and inserted into the poster via `Figure.add_axes` with the figure data re-drawn at poster scale — not pasted as a static PDF, because a pasted PDF cannot be rescaled by the matplotlib font system and will look out of place. Fourth figures are *deleted*, not added — a poster with four figures is overcrowded; a poster with two has one too few; three is the discipline of compression.

---

## Part 2 — Build the poster in matplotlib (35 points)

The poster is built by a single `poster.py` script that produces `poster.pdf` deterministically. The reproducibility bar from Lab 7 and PS 9.3 holds: a fresh clone running `make poster` produces a `poster.pdf` byte-identical to the committed one, and the three figures inside it are the *same data* (regenerated, not re-imaged) as the figures in your paper and deck.

**(a) The script skeleton (10 pts).** `poster.py` follows this structure:

```python
# poster.py — 48x36-inch conference poster, matplotlib-built, regenerated by make poster
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec
import numpy as np
import pandas as pd
from config import SEED

rng = np.random.default_rng(SEED)

# 1. Load the same analysis dataset every figure script uses.
df = pd.read_parquet("data/processed/analysis.parquet")

# 2. 48x36 inches, landscape, 150 dpi (vector PDF — dpi only matters for embedded rasters).
fig = plt.figure(figsize=(48, 36), dpi=150)

# 3. Master GridSpec: 3 rows x 3 cols, with the center cell oversized.
gs = gridspec.GridSpec(
    3, 3, figure=fig,
    height_ratios=[1, 3, 1],          # top thin, middle big, bottom thin
    width_ratios=[1.2, 1.6, 1.2],     # center wider than the columns
    hspace=0.15, wspace=0.10,
)

# 4. Title bar (spanning top row, columns 1-2):
ax_title = fig.add_subplot(gs[0, 0:2])
ax_title.text(0.0, 0.5, "Do Fair-Lending Exams Shrink the Mortgage Denial Gap?",
              fontsize=72, fontweight="bold", va="center")
ax_title.axis("off")

# 5. Question + why-it-matters (top-right merge or middle-of-top):
# 6. Design figure (middle-left), built by calling your existing figure code:
ax_design = fig.add_subplot(gs[1, 0])
draw_one_figure_defense(ax_design, df, rng)   # function imported from one-figure.py

# 7. Headline figure (middle-center, oversized):
ax_headline = fig.add_subplot(gs[1, 1])
draw_headline_figure(ax_headline, df)

# 8. Robustness (middle-right):
ax_robust = fig.add_subplot(gs[1, 2])
draw_spec_curve(ax_robust, df)

# 9. Bottom row text panels (data / contribution / repo+QR).
# ...

fig.savefig("paper/poster/poster.pdf", bbox_inches="tight")
plt.close(fig)
```

Grading on the script:

- **Single script, no design-software chain (4 pts):** `poster.py` is the *only* file in the build chain. No exported PowerPoint, no Affinity, no Illustrator, no Inkscape post-processing. The bar is *if a stranger runs `python poster.py` they get `poster.pdf`* — full stop.
- **Reuses figure functions (3 pts):** the design figure, the headline figure, and the spec curve are drawn by *importing functions* from your existing figure scripts (`one-figure.py`, `event-study.py`, `spec-curve.py`), not by re-implementing them. This guarantees the poster's center panel and slide 4 of your deck are the *same code* drawing the same data.
- **Determinism (3 pts):** uses `np.random.default_rng(SEED)` if any randomness is involved (bootstrap CI bands, for example); the rebuild on a fresh clone hashes to the same SHA-256.

**(b) Typography at poster scale (10 pts).** Fonts that look fine on a slide look comical on a poster, and vice versa. The font discipline:

- **Title:** 72 pt, bold, sans-serif.
- **Section headers (Question, Design, Headline, Robustness, Contribution, Data):** 48 pt, bold.
- **Body text inside panels:** 24 pt regular for the prose; 20 pt for the design-caption / contract-form sentence (it is dense and should not dominate).
- **Figure axis labels:** 28 pt; tick labels 22 pt; legend entries 22 pt.
- **Annotations in figures (e.g., the post-period drop labeled "ATT ≈ −1.8 pp"):** 24 pt, dark grey.

A poster panel with 12-point body text fails the three-feet rule. A poster with 144-point body text looks like a children's book. The numbers above are the calibrated middle. Set them once in `matplotlib.rcParams` at the top of `poster.py` so a global change is one edit, not 47.

**(c) Color and ink discipline (5 pts).** Two-color rule for the data: **one** color for the main series (a dark, conservative color — navy or burgundy, not red), one **grey** for everything secondary (confidence bands, reference lines, placebo distributions). Avoid the matplotlib rainbow default; avoid traffic-light reds and greens (a non-trivial share of viewers are red-green colorblind). Use white space generously between panels — 0.5 inches of margin between adjacent figures is a floor. A cluttered poster is rejected by the hallway eye before the content is even read.

**(d) The QR code and repo URL (5 pts).** The bottom-right (or top-right corner, per the grid in Part 1(a)) carries:

- The repo URL, in 24-point monospace: `github.com/CAMP-ORG/capstone-2026-maya`
- A QR code, generated by `qrcode` (Python package), encoding the URL — about 3×3 inches, placed alongside the URL.

```python
import qrcode
from io import BytesIO
img = qrcode.make("https://github.com/CAMP-ORG/capstone-2026-maya")
img.save("paper/poster/qr.png")
# then inserted into the poster axes with ax.imshow
```

The QR code is the bridge from the static poster to the reproducible packet — a hallway viewer scans, lands on the repo, and can clone-and-`make-all` from there. Without it, the poster is a dead end.

**(e) Print specifications (5 pts).** State in `poster.md` (Part 5) the print specifications:

- **Final size:** 48 inches wide × 36 inches tall, landscape.
- **File format:** vector PDF (no rasterization except the QR code).
- **Color space:** sRGB (your conference's print shop will convert to CMYK; do not pre-convert, you will get muddy colors).
- **Bleed:** none; the matplotlib `bbox_inches="tight"` save is fine for a poster mounted to a board.
- **Font embedding:** confirm that the PDF embeds the fonts used (`matplotlib.rcParams["pdf.fonttype"] = 42` ensures TrueType embedding; the default does not).

Without these specs, the print shop will substitute fonts (your axis labels turn to Times) and the poster you mount is not the poster you built.

---

## Part 3 — The hallway-readability test (15 points)

A poster's job is judged at three feet, not three inches. Run two tests before you commit.

**(a) The three-feet test (8 pts).** Render `poster.pdf` to a screen at 1:8 scale (so a 48-inch poster appears at 6 inches on screen) and stand back from your monitor by an arm's length — that is the equivalent of standing three feet from the printed poster. Can you:

1. Read the title? (Should be effortless.)
2. Identify which panel is the design figure, the headline, the robustness? (Should be effortless from layout alone.)
3. Read the headline-figure axis labels? (Should be possible, perhaps with squinting.)
4. Read the body text in the question / why-it-matters / contribution panels? (Should be possible.)

If any of (1)–(3) fails, fonts are too small; bump up. If (4) fails, prose panels are too dense; cut words. Record the test in `poster.md` with a screenshot at the test scale.

**(b) The walk-by test (4 pts).** Ask a peer to walk past the rendered poster (or its on-screen 1:8 facsimile) at normal walking pace and, *without stopping*, tell you what your paper is about. Record their answer. If they cannot give you the question and the design in one sentence after a 5-second glance, the title bar and the design figure are not pulling their weight; revise. The walk-by-pace constraint is what the hallway *is*; if your poster fails it, the conference hallway will too.

**(c) The 60-second test (3 pts).** A different peer stands at three feet and reads the poster for *exactly 60 seconds*. Ask them to summarize, in one paragraph, what the paper is, what the design is, and what was found. Record their summary. If the summary matches your paper's abstract, the poster works. If it omits the design or the contribution, the panels carrying those failed the 60-second budget and need shorter, sharper text or a more legible figure.

---

## Part 4 — Reproducibility and pipeline integration (15 points)

The poster lives inside the same `make all` pipeline as the paper and the deck; it does not exist as a one-off file edited by hand the week before the conference.

**(a) `Makefile` entry (5 pts):** add the poster to your build target:

```makefile
paper/poster/poster.pdf: data/processed/analysis.parquet src/poster.py src/one-figure.py src/event-study.py src/spec-curve.py
	python src/poster.py

poster: paper/poster/poster.pdf

all: figures paper/paper.pdf poster
```

The poster's dependency line lists *all four* upstream files: the analysis dataset and the three figure scripts whose functions it imports. When any of these change, `make` regenerates the poster — the poster cannot drift behind the paper.

**(b) The byte-identical rebuild check (5 pts):** confirm with a hash that the committed `poster.pdf` is byte-identical to the one a fresh `make all` produces:

```bash
shasum -a 256 paper/poster/poster.pdf | tee paper/poster/poster.sha256
```

Paste the hash into `poster.md`. If the hash drifts on rebuild, find the non-determinism (most often: a font rendering that depends on the system font cache; pin `matplotlib.rcParams["pdf.fonttype"] = 42` to guarantee TrueType embedding which is system-independent).

**(c) The print-shop send-off (5 pts):** the final, hash-confirmed `poster.pdf` is sent to the conference print shop *from the repo*, not from a desktop copy that may have drifted. The send-off is documented in `poster.md` with the order date, the print shop, and confirmation that the file uploaded matches the repo hash. (Many print shops re-render the PDF on upload — they will email you a low-resolution proof; the *proof* should match the repo hash, and you confirm this before clicking "approve.")

---

## Part 5 — The build memo (`poster.md`) (10 points)

A short 200-word document that, read alone, tells a grader (and your future self) what the poster is and how it was built.

The four required paragraphs (≈50 words each):

1. **What the poster shows.** One sentence each on the question, the design, the headline result, and the contribution — essentially a 4-sentence summary of the paper as the poster compresses it.
2. **How it was built.** *"`poster.py` builds `poster.pdf` from `data/processed/analysis.parquet` and imports figure functions from `one-figure.py`, `event-study.py`, and `spec-curve.py`. `make poster` regenerates it; the SHA-256 of the committed PDF is `<hash>`."*
3. **Print specifications and send-off.** The five print specs from Part 2(e), the order date, the print shop, and the proof-hash confirmation.
4. **The three readability tests.** The result of the three-feet test, the walk-by test, and the 60-second test, with the peer's summary recorded (if available).

Word count is 200 ± 20, enforced with `wc -w poster.md`. The memo is short by design — it is documentation, not a redo of the poster.

---

## Submission checklist

Before you commit, confirm:

- [ ] `poster.pdf` (48×36 inches, landscape, vector), `poster.py`, and `poster.md` are committed under `paper/poster/`.
- [ ] The grid follows Part 1(a) (or a justified alternative); the title bar is a full-sentence claim, not a noun phrase.
- [ ] Total prose across all body panels is ≤ 200 words; each panel respects its sub-budget.
- [ ] Exactly three figures (design / headline / robustness), each drawn by importing functions from existing figure scripts.
- [ ] `poster.py` uses `matplotlib.use("Agg")` and `np.random.default_rng(SEED)`; no design-software in the chain; `matplotlib.rcParams["pdf.fonttype"] = 42` is set.
- [ ] Typography per Part 2(b): title 72 pt, headers 48 pt, body 24 pt, axis labels 28 pt, ticks 22 pt; two-color rule honored; generous white space.
- [ ] QR code + repo URL present and scannable from the rendered file (test the QR on your phone).
- [ ] Three readability tests run (three-feet, walk-by, 60-second), with results recorded in `poster.md`.
- [ ] `Makefile` has a `poster` target with the four upstream dependencies; `make poster` rebuilds byte-identically; the SHA-256 is committed.
- [ ] Print specs (size, format, color, bleed, font embedding) stated in `poster.md`; the print-shop send-off is documented with proof-hash confirmation.

---

## How this is graded

Part 1 (grid and content compression, 25) on whether the layout follows the grid and whether the prose budgets are respected. Part 2 (matplotlib build, 35 — the heaviest part) on whether the script is deterministic, reuses figure functions, and renders at poster-scale typography. Part 3 (hallway readability, 15) on whether the three tests are run and the poster passes them. Part 4 (pipeline integration, 15) on whether `make all` regenerates the poster byte-identically and the send-off is documented. Part 5 (build memo, 10) on whether the 200-word memo documents the build and the tests. The highest-signal single check: **does the 60-second test produce a one-paragraph summary that matches your paper's abstract?** A `Y` says the poster is doing its job; a `N` says the panels carrying the question, design, and contribution need shorter, sharper text or more legible figures.

---

## The bridge to PS 9.5

PS 9.4 produces the poster the conference sees; PS 9.5 captures what the conference says *back*. Every comment from a poster viewer — every question at the poster session, every "have you tried X?" — becomes a row in the *post-conference feedback ledger*, which you then triage in a 48-hour memo into "act on now," "act on by Week 11," and "do not act on, here is why." The conference is data; PS 9.5 is how you process that data into the next four weeks of revision.

*End of PS 9.4. The model deliverable is in `book/appendices/E-solutions-manual/E-w9-ps9.4-solutions.md`. Build your own poster first; read the exemplar to calibrate, not to copy. The poster that lives inside the reproducibility pipeline and the poster the conference sees are the same poster — this assignment is you producing it on purpose, in code, not by accident, in PowerPoint.*
