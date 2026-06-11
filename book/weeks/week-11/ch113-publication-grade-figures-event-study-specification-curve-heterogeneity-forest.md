# Ch 11.3 — Publication-Grade Figures: the Event-Study Plot, the Specification-Curve Plot, the Heterogeneity Forest — and the Tufte Rules That Apply

Your Table 2 is clean. The headline coefficient sits in a column-three row with three stars, the cluster count is honest, the captions are tight. You scroll forward in the manuscript and run into Figure 1 — an event-study plot you produced in Chapter 7's notebook, with default `matplotlib` styling, three lines of different colors, a legend in the upper-right corner overlapping a confidence band, and no shaded pre-treatment region. The plot communicates the right thing if you already know what to look for; it communicates *nothing* to a referee opening the paper cold. **This chapter is about turning that figure into one a referee will trust.**

Here is the result the chapter turns on. **A publication-grade figure is engineered to make one comparison salient, with everything that is not in service of that comparison either removed or demoted to background.** Edward Tufte's *Visual Display of Quantitative Information* (1983, with subsequent volumes) named the principle: the **data-ink ratio** is the proportion of ink on the page that conveys data, as opposed to grid, frame, axis decoration, and chart-junk. Publication-grade figures maximize the data-ink ratio. The five-line theorem is harsh: every line on a figure must either carry data or carry essential context, and *everything* else must go. This chapter is the application of that theorem to three figures every empirical-finance paper needs — the **event-study plot** (the picture of parallel trends and treatment dynamics), the **specification-curve plot** (the picture of robustness across the spec menu from Chapter 8.1), and the **heterogeneity forest** (the picture of effect heterogeneity across subgroups). Each figure has its own anatomy, its own pitfalls, and its own one-glance test. Each is rendered in `matplotlib` with code you can copy.

Before we start, a moment on style. Many students treat figures as decoration — the table is the science, the figure is the illustration. **This is backward in modern empirical finance.** The event-study plot *is* the parallel-trends argument; if your event study shows pre-period coefficients drifting from zero, no robustness check rescues it. The specification-curve plot *is* the disclosure of forks from Chapter 8.1; without it, your robustness claim is unverifiable. The heterogeneity forest *is* the visual summary of Chapter 10.3's CATEs; the table version, with twelve coefficient rows, requires effort to parse, but the forest is parsed in five seconds. Figures, done right, are the most efficient way to communicate the empirical argument. They earn the same engineering effort as tables.

---

## 1. The reveal: data-ink, the one-glance test, and what publication-grade actually means

Tufte's data-ink ratio is the spine. Computed literally — pixels of data versus pixels of frame — it is a fuzzy quantity. Computed as a *discipline*, it is a checklist: remove the top spine; remove the right spine; suppress the grid (or set it to a very light gray); use a single accent color for the data and gray for context; label axes only with the unit and the variable (not the variable plus the model name plus the dataset); set the title to short or remove it entirely (the figure caption does that work in the manuscript). Each removal you make increases the proportion of ink that conveys the data and decreases the proportion that conveys frame.

The one-glance test for figures is the same as for tables but with different questions. A figure passes the one-glance test if a referee can answer in fifteen seconds:

1. **What is the *x*-axis?** (Time, specification index, subgroup.)
2. **What is the *y*-axis?** (The estimated quantity, in interpretable units.)
3. **What is the comparison being made?** (Pre-treatment vs. post-treatment, baseline vs. variants, group A vs. group B.)
4. **What is the bottom-line claim?** (Effect is concentrated in post-treatment / robust across specs / heterogeneous in subgroup X.)

Most student figures fail at question 4 because the figure was designed to *display data* rather than to *make a claim*. The cure is to design the figure backward from the claim: write a one-sentence caption in plain English first, then engineer the plot so that the claim is visible without reading the caption. The caption becomes a redundancy check; the visual is the argument.

We will work through the three figure types in order: event study (§§2–3), specification curve (§§4–5), heterogeneity forest (§§6–7). Maya's project carries the worked example for all three; Devon, Priya, Sam, and Leah appear in §8 with variants for their projects.

---

## 2. The event-study plot, anatomy

The event-study plot is the visual evidence for the parallel-trends assumption in a DiD design. The data behind it: in the Callaway and Sant'Anna (2021) framework (or the Sun and Abraham (2021) alternative), for each treatment cohort $g$ and each event time $\tau$ (where $\tau < 0$ is pre-treatment and $\tau \geq 0$ is post-treatment), an estimator returns a point estimate $\hat{\delta}_\tau$ and a standard error $\hat{\sigma}_\tau$. The plot shows $\hat{\delta}_\tau$ on the *y*-axis as a function of $\tau$ on the *x*-axis, with a confidence band of $\hat{\delta}_\tau \pm 1.96 \hat{\sigma}_\tau$ around each point.

The anatomy of a good event-study plot, every element justified.

**The horizontal axis is event time, not calendar time.** A common student mistake is to plot calendar year on the *x*-axis ("2014, 2015, …, 2020"), which would only work for a single-cohort DiD. In a staggered design, the same calendar year is event time $\tau = -2$ for one cohort and event time $\tau = +1$ for another. The pooled event-study coefficient at $\tau$ aggregates across cohorts; the *x*-axis must therefore be event time, with $\tau = 0$ being the treatment year for each cohort.

**The vertical axis is the outcome's natural unit.** If the outcome is the denial-rate gap measured in percentage points, the *y*-axis is in percentage points (e.g., from $-3$ to $+2$), not in proportions (from $-0.03$ to $+0.02$). The reader will be comparing values to the abstract's headline number (1.4 percentage points), and the units must match.

**A vertical reference line at $\tau = 0$ separates pre and post.** The line is a thin black dashed vertical. It is the event itself; everything to its left is the test of parallel trends, everything to its right is the dynamic treatment effect.

**A horizontal reference line at $y = 0$ shows the null.** A thin gray horizontal at $y = 0$ lets the reader judge whether the confidence bands cover zero. Without it, the reader has to guess whether the lower band lies above or below the null.

**The pre-treatment region may be lightly shaded.** A pale gray fill from the left edge to $\tau = 0$ visually demarcates the pre-period. This is a Tufte-style mild emphasis; it is not strictly necessary but it speeds the reader's parsing.

**The point estimates are filled circles, the bars are vertical-error-bar pairs.** Whisker-cap-free error bars. Lines connecting the points are *optional* — common in finance papers, less common in some econ subfields. We prefer to omit the connecting line because it suggests interpolation between event times, which is misleading (event-time $\tau = -1.5$ does not exist in the data). The dots alone are visually sufficient.

**No legend on a single-line event study.** The figure shows one series; the caption names it.

**No title.** The caption below the figure in the manuscript carries the title information. Internal titles on figures are double-labeling and waste data-ink.

**No grid, or a very light gridline at major-tick positions only.** A dense grid competes with the data.

Here is the code, with Maya's coefficients from her staggered DiD as the example.

```python
# nb11.3 cell 1 — publication-grade event-study plot for Maya's DiD
import numpy as np
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt

rng = np.random.default_rng(42)

# Suppose the event-study estimator has produced these coefficients & SEs.
# (Real values would come from pf.feols() with the i(event_time, ref=-1) syntax,
# or from the Callaway-Sant'Anna `did` package.)
tau   = np.arange(-4, 5)                  # event times from -4 to +4
delta = np.array([0.10, -0.05, 0.02, 0.00, 0.00, -0.85, -1.20, -1.35, -1.40])  # in percentage points
sigma = np.array([0.35, 0.32, 0.28, 0.25, 0.00, 0.30, 0.32, 0.35, 0.38])

fig, ax = plt.subplots(figsize=(6.5, 4.0))

# Pre-treatment shading (light gray, alpha low)
ax.axvspan(tau.min() - 0.5, -0.5, color="0.92", alpha=1.0, zorder=0)

# Horizontal zero line
ax.axhline(0, color="0.5", lw=0.8, ls="-")

# Vertical event line at tau=0
ax.axvline(0, color="0.2", lw=0.8, ls="--")

# Point estimates and 95% CIs (1.96 * SE)
ax.errorbar(
    tau, delta,
    yerr=1.96 * sigma,
    fmt="o",
    color="black",
    ecolor="black",
    elinewidth=1.2,
    capsize=0,           # no whisker caps
    markersize=6,
    zorder=3,
)

# Labels — sparse and informative
ax.set_xlabel("Event time (years from intensified examination)")
ax.set_ylabel("Black–White denial-rate gap (percentage points)")
ax.set_xticks(tau)

# Remove top and right spines (Tufte; the matplotlib default has all four)
ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)

# Light gridline at y=0 alternative: subtle horizontal at major ticks only
ax.yaxis.grid(True, color="0.85", lw=0.5, zorder=0)

fig.tight_layout()
fig.savefig("fig_maya_event_study.pdf", dpi=300)
```

The figure that results passes the four one-glance tests. The *x*-axis is event time; the *y*-axis is the denial gap in percentage points; the comparison is pre- versus post-treatment; the bottom-line claim is "pre-period coefficients are flat around zero and within CIs of zero, post-period coefficients fall steadily from zero to roughly $-1.4$, validating parallel trends and revealing a dynamic treatment effect." That entire claim is visible without reading any caption text. *That* is publication-grade.

---

## 3. The event-study plot, common failure modes

Three pathologies show up in student event-study plots more than any others.

**The reference-period missing-marker.** The reference period is, by convention, $\tau = -1$ (the year just before treatment), and the estimator returns 0 for that period by construction. Many plotting scripts then place a point at $(-1, 0)$ with an apparently-zero standard error, which looks like a magically precise estimate. The cure is to either drop the reference period from the plot entirely, or to show it as an open circle with no error bar, or to show a vertical text annotation "Reference" with no marker. The plot above sets $\sigma[\tau = -1] = 0$, which produces no visible error bar; that is acceptable. The worst option is to plot it as a normal point with a zero-width bar, which misleads.

**The over-shaded confidence band.** Some plotting conventions (notably the `seaborn` default) draw a continuous shaded *band* between adjacent CI endpoints, suggesting that the estimate at non-integer event times has a confidence interval. This is misleading; the estimate exists *only* at integer event times. Use error bars at each integer; do not interpolate the band.

**The unlabeled or wrongly-labeled treatment line.** The vertical line at $\tau = 0$ is the treatment. Many students label it "treatment year" inside the plot or — worse — label it with the calendar year of one of the cohorts ("2017") which mistakes the staggered structure. Leave it unlabeled (its position at $\tau = 0$ tells the reader), or label it sparely with a small text annotation above the axis.

Done right, the event-study plot is the single most important figure in a DiD paper. The pre-period flatness is the parallel-trends assumption; the post-period dynamics are the treatment effect. If either is missing or misleading, the design fails.

---

## 4. The specification-curve plot, anatomy

The specification-curve plot from Chapter 8.1 (Simonsohn, Simmons, and Nelson, 2020) shows the headline coefficient across the menu of plausible specifications, sorted from smallest to largest, with a horizontal axis indexing specifications and a panel of horizontal-bar indicators below showing which analytic choice each specification made. **The plot is the visualization of robustness: if 90% of plausible specifications produce a coefficient between $-2.0$ and $-0.8$, the headline is robust; if specifications scatter from $-3.0$ to $+1.0$, the headline depends on choices and the paper has a problem.**

The anatomy of a good specification curve.

**The upper panel shows the coefficient.** The horizontal axis is the specification index (1 to $M$, where $M$ is the total number of specifications in the menu, often 100 to several thousand). The vertical axis is the coefficient. Each specification is a dot. The dots are sorted in ascending order so the curve sweeps from the smallest coefficient on the left to the largest on the right.

**A reference horizontal line at zero.** As with the event-study plot, the null reference line lets the reader judge how many specifications produce coefficients below versus above zero.

**A reference horizontal line at the preferred specification's coefficient.** A dashed line at, say, $y = -1.4$ (Maya's preferred-specification estimate) lets the reader place the preferred specification within the distribution.

**A confidence-interval band at each specification's dot.** This is where specification curves can become busy. The recommended convention is to color the dot black if its 95% CI excludes zero, and gray if its 95% CI includes zero. The reader can scan the curve and count the proportion of significant specifications without parsing individual CIs.

**The lower panel shows the spec-menu choices.** Below the upper panel, a strip of horizontal bars or markers shows which analytic choice each specification used: which sample, which outcome variant, which fixed-effect saturation, which clustering, which winsorization. The lower panel is a tall, narrow grid: rows are choice categories (e.g., "sample: OCC-only, sample: all banks, sample: top-quintile lender, …"), columns are specifications (aligned with the upper panel), and a filled marker at (row, column) indicates that this specification used this choice.

**The reader's eye scans top-to-bottom.** To diagnose which choice is driving a positive coefficient, the reader scans the rightmost specifications (largest coefficients), looks down at the lower panel, and sees which row has filled markers concentrated in those columns. That row identifies the choice that pushes the coefficient up. Symmetric scan on the leftmost specifications identifies the choice that pushes it down. Specification curves done well make the choice-dependence of the headline immediately visible.

Here is the rendering code.

```python
# nb11.3 cell 2 — specification curve, with lower-panel choice indicators
import numpy as np
import pandas as pd
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt

rng = np.random.default_rng(42)

# Suppose `spec_df` is a DataFrame with one row per specification, columns:
# beta, se, sample, outcome_variant, fe_saturation, clustering, winsorization.
# This DataFrame is the output of nb8.1 — the spec-menu execution.

# Sort by coefficient ascending
spec_df = spec_df.sort_values("beta").reset_index(drop=True)
spec_df["idx"] = np.arange(1, len(spec_df) + 1)
spec_df["sig"] = (spec_df["beta"] + 1.96 * spec_df["se"]) * (spec_df["beta"] - 1.96 * spec_df["se"]) > 0

# Preferred-specification coefficient
beta_preferred = -1.40

fig, (ax_top, ax_bot) = plt.subplots(
    2, 1,
    figsize=(7.5, 5.0),
    sharex=True,
    gridspec_kw={"height_ratios": [3, 2], "hspace": 0.05},
)

# Upper panel: spec curve
ax_top.scatter(
    spec_df["idx"], spec_df["beta"],
    c=np.where(spec_df["sig"], "black", "0.7"),
    s=12,
    zorder=3,
)
ax_top.axhline(0, color="0.5", lw=0.8)
ax_top.axhline(beta_preferred, color="0.2", lw=1.0, ls="--")
ax_top.set_ylabel("Coefficient (percentage points)")
ax_top.spines["top"].set_visible(False)
ax_top.spines["right"].set_visible(False)

# Lower panel: choice indicators
choices = [
    ("Sample: full", spec_df["sample"] == "full"),
    ("Sample: OCC", spec_df["sample"] == "occ"),
    ("Outcome: gap", spec_df["outcome_variant"] == "gap"),
    ("Outcome: denial rate", spec_df["outcome_variant"] == "denial"),
    ("FE: county+year", spec_df["fe_saturation"] == "cy"),
    ("FE: lender×year", spec_df["fe_saturation"] == "ly"),
    ("Cluster: county", spec_df["clustering"] == "county"),
    ("Cluster: county×year", spec_df["clustering"] == "county_year"),
    ("Winsorize: none", spec_df["winsorization"] == "none"),
    ("Winsorize: 1%", spec_df["winsorization"] == "p01"),
]

for row_idx, (label, mask) in enumerate(choices):
    ax_bot.scatter(
        spec_df.loc[mask, "idx"],
        np.full(mask.sum(), len(choices) - row_idx - 1),
        marker="s",
        s=8,
        c="black",
    )

ax_bot.set_yticks(range(len(choices)))
ax_bot.set_yticklabels([c[0] for c in choices][::-1], fontsize=8)
ax_bot.set_xlabel("Specification rank (sorted by coefficient)")
ax_bot.spines["top"].set_visible(False)
ax_bot.spines["right"].set_visible(False)

fig.tight_layout()
fig.savefig("fig_maya_spec_curve.pdf", dpi=300)
```

The reader scans the upper panel, sees that roughly 85% of specifications produce coefficients in the $-2.0$ to $-0.8$ range, with the preferred specification at $-1.4$ near the middle of the cluster of significant estimates. The reader scans the lower panel, sees that the few positive coefficients on the far right correspond to specifications using the "Outcome: denial rate" variant (not the gap variant) and the "Sample: OCC" restriction without winsorization — a corner of the spec menu the author can discuss in a footnote. The robustness story is visible in seconds.

---

## 5. The specification-curve plot, common failure modes

Three pathologies.

**The unsorted spec curve.** If specifications are plotted in the order they were estimated rather than sorted by coefficient value, the curve is just noise and the reader cannot see the distribution. Always sort.

**The missing lower panel.** A spec curve with only the upper panel shows the distribution of coefficients but does not identify which choices drive it. Without the lower panel, the reader cannot diagnose the source of variation, and the figure is half-useful. Always include the lower panel.

**The over-saturated lower panel.** If the lower panel has thirty rows of choice indicators (because the spec menu has thirty dimensions), it becomes unreadable. The cure is to group choices into a small number of meaningful categories (sample, outcome, fixed effects, clustering, winsorization) and keep the row count under twelve. If your spec menu has thirty dimensions, you have probably included dimensions that should not be free — e.g., choices the pre-analysis plan should have committed to. The specification curve is a disclosure tool, not an excuse to vary every choice; it works best when the choices being varied are the ones that *reasonable referees might disagree about*.

A virtue of the spec-curve plot is that it forces the author to think hard about which choices are real degrees of freedom and which are not. A coefficient that survives in 95% of a thoughtfully constructed menu is robust; a coefficient that survives in 95% of a kitchen-sink menu is less informative because most of the kitchen-sink menu was not threatening anyway.

---

## 6. The heterogeneity forest plot, anatomy

The heterogeneity forest, borrowed from clinical-trial reporting, is the visual summary of a CATE (conditional average treatment effect) analysis or a subgroup regression. Each row is a subgroup; each row shows the point estimate as a dot and the 95% CI as a horizontal line through the dot; the rows are arranged top-to-bottom in a meaningful order (e.g., by subgroup definition, or by effect size, or by pre-specified subgroup ordering from the pre-analysis plan).

The anatomy of a good forest plot.

**The vertical axis is the list of subgroups.** From top to bottom: the overall ATT first, then the subgroup-specific estimates grouped by moderator. For Maya's analysis: overall ATT at the top, then four rows for minority-share quartiles (Q1, Q2, Q3, Q4), then four rows for examination-history quartiles, then a binary cut for urban/rural, then a binary cut for CRA-overlap.

**The horizontal axis is the estimate in interpretable units.** Same units as the headline; Maya's plot uses percentage points.

**A vertical reference line at zero.** The null reference; subgroups whose CI crosses zero are not statistically significant.

**A vertical reference line at the overall ATT.** A dashed line at the overall ATT (here, $-1.4$ pp) lets the reader judge which subgroups have effects larger or smaller than the average.

**The dots are filled circles, the lines are horizontal CI ranges, the line widths are uniform.** Some forest plots vary dot sizes by sample size (larger sample = larger dot). This is a useful visual cue if your subgroups have very different sample sizes; if subgroups are roughly balanced, uniform dots are cleaner.

**A header row sub-label or grouping bracket.** When subgroups come from multiple moderators (minority share, examination history, urban/rural), the rows for each moderator are grouped with a small header or with light horizontal-bracket emphasis. The reader can then scan moderator-by-moderator.

**No grid; no internal title.** Same Tufte discipline as the event study.

Here is the code.

```python
# nb11.3 cell 3 — heterogeneity forest plot for Maya's CATEs
import numpy as np
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt

rng = np.random.default_rng(42)

# Suppose `forest_df` is a DataFrame with columns: subgroup_label, group_label, beta, se.
# (Real values would come from nb10.3 — subgroup ATTs.)
forest_df = pd.DataFrame({
    "subgroup_label": [
        "Overall ATT",
        "Minority share Q1", "Minority share Q2", "Minority share Q3", "Minority share Q4",
        "Exam-history Q1", "Exam-history Q2", "Exam-history Q3", "Exam-history Q4",
        "Urban", "Rural",
        "CRA-overlap", "No CRA-overlap",
    ],
    "beta":  [-1.40, -0.20, -0.85, -1.60, -2.30, -0.30, -0.95, -1.55, -2.20, -1.80, -0.85, -1.50, -1.20],
    "se":    [ 0.28,  0.35,  0.32,  0.30,  0.34,  0.33,  0.30,  0.32,  0.36,  0.30,  0.35,  0.31,  0.32],
})

# Use position from bottom to top so labels read top-to-bottom in display
y = np.arange(len(forest_df))[::-1]
beta_overall = forest_df.loc[0, "beta"]

fig, ax = plt.subplots(figsize=(6.5, 5.0))

ax.errorbar(
    forest_df["beta"], y,
    xerr=1.96 * forest_df["se"],
    fmt="o",
    color="black",
    ecolor="black",
    elinewidth=1.0,
    capsize=0,
    markersize=6,
)

ax.axvline(0, color="0.5", lw=0.8)
ax.axvline(beta_overall, color="0.2", lw=0.8, ls="--")

ax.set_yticks(y)
ax.set_yticklabels(forest_df["subgroup_label"], fontsize=9)
ax.set_xlabel("Effect on Black–White denial-rate gap (percentage points)")
ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)
ax.spines["left"].set_visible(False)
ax.tick_params(left=False)

# Light horizontal separator above each moderator group
for sep_y in [0.5, 4.5, 8.5, 10.5]:
    ax.axhline(sep_y, color="0.85", lw=0.5)

fig.tight_layout()
fig.savefig("fig_maya_heterogeneity_forest.pdf", dpi=300)
```

Reading the plot top to bottom, the reader sees: the overall ATT at $-1.4$; the minority-share gradient (effect grows from $-0.2$ in Q1 to $-2.3$ in Q4, monotonic, larger effects in high-minority counties); the examination-history gradient (similar monotonic pattern, larger effects at lenders with worse prior records); the urban-vs-rural cut (urban larger); the CRA-overlap cut (small difference). The forest plot tells the heterogeneity story in five seconds in a way that a twelve-row table cannot.

---

## 7. The heterogeneity forest plot, common failure modes

Three pathologies.

**The arbitrary subgroup ordering.** If subgroups are listed in alphabetical or random order, the reader cannot scan a pattern. Order by moderator (group all minority-share rows together, all exam-history rows together) and within a moderator order by the underlying quantile (Q1 to Q4). Pre-specified orderings from the pre-analysis plan override default orderings.

**The unmatched reference line.** If the dashed vertical line at the overall ATT is at, say, $-1.5$ but the table value of the overall ATT is $-1.4$, the figure and the table disagree. Always pull the reference value from the same source as the headline table.

**The crowded plot.** A forest plot with thirty subgroup rows is unreadable. Cap at twelve or fifteen rows; if your heterogeneity analysis has more, split into two forest plots by moderator family.

---

## 8. Across the cohort: the same three figures for the other students

The three figures generalize. Each of Devon, Priya, Sam, and Leah needs a variant of each. Brief notes on the project-specific adaptations.

**Devon (crypto event study).** The event-study plot here is literally an event-study (minute-level around the May 2022 TerraUSD de-peg). The *x*-axis is minutes from the event; the *y*-axis is the log-return cumulated from event time. Devon's plot is essentially the financial-economics event-study format from Brown and Warner (1985), adapted to the higher-frequency setting. Same anatomy: vertical line at minute 0, horizontal at zero, error bars per minute. Specification curve: across alternative event windows ($[-30, +30]$ minutes vs. $[-15, +15]$ minutes vs. $[-60, +60]$ minutes), across alternative benchmark portfolios (algorithmic-only vs. all-stablecoin), across alternative volatility weighting. Forest plot: heterogeneity across stablecoin types (algorithmic, fiat-collateralized, crypto-collateralized).

**Priya (climate insurance).** Event-study plot on the flood-zone re-mapping has the same anatomy as Maya's, with calendar years rescaled to event-time-from-remapping. Specification curve across alternative outcome definitions (premium dollar amounts vs. log premium vs. premium-to-property-value ratio). Forest plot: heterogeneity by elevation-grade quartile, by prior-claim history, by reinsurance-coverage tier.

**Sam (intraday momentum).** Sam's project is not a treatment-effect design; the "event-study" equivalent is the *intraday return persistence curve* — the autocorrelation function of intraday half-hour returns from minute 60 (first half-hour of trading) out to minute 390 (close), plotted as a bar at each lag with the CIs of Gao, Han, Li, and Zhou (2018)'s predictive-regression coefficients. Specification curve: across alternative half-hour windows (using the first 30 minutes vs. the first 60 minutes vs. the first 90 minutes), alternative cost models (zero-cost vs. round-trip 2bp vs. 5bp), alternative samples (full sample vs. crisis-excluding sample). Forest plot is less natural for Sam's design; his heterogeneity is across calendar regimes (high-volatility days vs. low-volatility days, weekly-rebalancing day-of-week effects), and a small two-panel barchart serves him better than a forest.

**Leah (patent text similarity).** Event-study analogue is the spillover dynamics around a patent's grant — the cumulative-abnormal-citation curve in event-quarter time. Specification curve across alternative text-similarity measures (TF-IDF cosine vs. BERT embeddings vs. patent-class jaccard), alternative spillover windows, alternative firm-pair samples. Forest plot: heterogeneity by technology class (six rows), by firm size quartile (four rows), by R&D intensity (binary).

In every project, the three figures earn their place. The event-study analogue shows the temporal structure; the specification curve shows robustness; the forest shows heterogeneity. The specific shape adapts to the design.

---

## 9. The Tufte rules that apply (and the ones that don't)

Tufte's *Visual Display* offers many principles; most apply to publication-grade econ figures, a few do not. Here are the ones we apply.

**Maximize the data-ink ratio.** Discussed at length. Remove chart-junk; demote frame; let the data speak.

**Use small multiples where comparison is the point.** For Maya's heterogeneity-by-cohort plot, a 2×2 grid of small event-study plots (one per cohort) is more informative than four overlaid lines on a single plot. Small multiples replace legend gymnastics with title gymnastics, and the reader can scan the grid for cross-cohort comparison.

**Color carries information, not decoration.** A figure with five colors that mean nothing is a figure with five colors of chart-junk. If you have one accent color (use it for the data series being argued about) and one neutral color (gray, for context), that is enough. Color-blind-safe palettes (the Wong palette, the Viridis ramp) are the default in 2026; do not use red-green together.

**Label directly when possible.** Inline labels on lines beat legends. A line that says "Treated" directly on the line is easier to parse than a legend in the upper right. (For two-line plots, this is usually feasible; for spec curves and forests, internal labels are awkward and a small axis label substitutes.)

**Show the data.** Tufte hates summary-only displays. For a small dataset (Maya's subgroup analysis has thirteen subgroups), showing every dot is preferable to showing only means. For large datasets, a smoothed density or a violin plot can replace the spaghetti plot but should still show some indicator of underlying variation.

Two Tuftean rules we *do not* fully apply in modern empirical-finance figures:

**Tufte's "remove the axes" rule.** Tufte sometimes advocates removing axis lines entirely, leaving only tick marks. Modern econ journals usually keep at least the bottom and left spines because the figure is small and the spines help with orientation. Remove the top and right spines as a compromise.

**Tufte's preference for very high information density.** Tufte's exemplars (the Napoleonic-Russia map, the Cholera-pump map) pack enormous information per square inch. Most econ figures are simpler — one comparison, one panel — and the high-density aesthetic is wrong for them. Apply density discipline (no clutter) but do not artificially cram multiple plots onto one page just to be Tuftean.

---

## 10. Production discipline: vector formats, font sizes, and file conventions

Three production rules that finish the figure.

**Vector formats, not raster.** Save figures as PDF or SVG, not PNG. Vector formats scale without pixelation, embed cleanly in LaTeX, and are what every journal copy-editor will request. The `fig.savefig("fig.pdf", dpi=300)` call in the examples above produces vector PDF; `dpi=300` is the dot-per-inch metric for any embedded raster elements (mostly irrelevant when output is vector but harmless).

**Font sizes match the body text.** A figure produced at `figsize=(6.5, 4.0)` (inches) and `\textwidth` typeset at ten-point body text needs axis labels around eight to ten point, tick labels around seven to nine point, annotations around seven point. The `matplotlib` defaults are too large; set them explicitly. The minimum readable size on a printed page is roughly seven point. **Do not produce a figure at `figsize=(12, 8)` and then shrink it to fit the column.** Produce at the size the figure will be displayed; the fonts will then be the right size.

**File-naming convention.** Every figure file is named after the manuscript element it occupies: `fig_maya_event_study.pdf`, `fig_maya_spec_curve.pdf`, `fig_maya_heterogeneity_forest.pdf`. The script that produces each figure is named the same way (`fig_maya_event_study.py` or `nb11.3` cell 1 with a comment header). The manuscript's `\includegraphics` lines reference the files by exact name. This pays off when a reviewer asks "can you re-render figure 3 with a wider CI band?" — you change one parameter in one script and the PDF regenerates.

The replication packet from Chapter 8.5 should include, for each figure, both the rendered PDF and the script that rendered it. A replicator should be able to run the script on a fresh conda environment and reproduce the figure to the byte (which is why seeding all randomness with `rng = np.random.default_rng(42)` and using `matplotlib.use("Agg")` are mandatory).

---

## 11. The figure-caption anatomy

Captions in the manuscript are short, two to four lines. The anatomy:

**Line 1 — what the figure is.** "Event-study estimates of the effect of intensified fair-lending examinations on the Black–White denial-rate gap."

**Line 2 — the source / sample.** "HMDA 2014–2020, OCC-supervised counties; staggered DiD with cohort-specific event-study leads and lags."

**Line 3 — the inference convention.** "Bars are 95% confidence intervals from cluster-robust standard errors at the county level."

**Line 4 (optional) — the bottom-line claim.** "Pre-treatment coefficients are statistically indistinguishable from zero; post-treatment coefficients decline monotonically to approximately $-1.4$ percentage points by event year $+4$."

The optional line 4 is the redundancy check: it states the claim in words so a reader who skims captions catches the result without studying the figure. Some journals dislike it (they prefer the figure to speak for itself); some encourage it. Default to including it; remove on the journal's request.

---

## 12. Common failure modes, named

Five pathologies summarize the chapter's negative template.

### 12.1 The default-matplotlib figure

The default-matplotlib figure has the default `rc_params`: ugly blue line, all four spines, top-and-right title bar, gridlines everywhere, default-size fonts that are too large for the column. The fix is the styling block from §§2 and 10: `spines["top"].set_visible(False)`, `spines["right"].set_visible(False)`, sparse grid, black-and-gray accent palette, correct figure size, vector output. Many labs commit a `matplotlibrc` file with these defaults so every figure starts publication-grade.

### 12.2 The legend-overlapping-the-data figure

The legend covers a confidence band, an event-time-zero point, or the most important subgroup row. The fix is `loc="best"` only if the figure is simple; for any figure with central whitespace constraints, place the legend manually (`bbox_to_anchor=(1.05, 1.0)`) or use inline labels as in the Tufte direct-labeling discipline.

### 12.3 The unlabeled-axis figure

The vertical axis just says "Coefficient" without a unit. The reader does not know whether the coefficient is percentage points, log-returns, dollar-per-loan, or something else. The fix is to label the axis with the unit explicitly: "Coefficient on Treated × Post (percentage points)."

### 12.4 The over-decorated event-study

The event-study has a title in the figure, gridlines everywhere, three colored lines for three different specifications, a legend in the upper right, error bars in two colors with caps and dashed connecting lines. The fix is the Tufte demotion: drop the title, drop the grid (except a very light one), drop the legend (use small multiples for multiple specifications), suppress caps, single accent color.

### 12.5 The mismatched figure-and-table

The event-study plot shows a post-treatment coefficient of $-1.6$ at event year $+4$, but the headline table reports the pooled ATT as $-1.4$. The discrepancy is fine *if explained* (the pooled ATT averages across event years; the year-$+4$ coefficient is the long-run effect alone), but unexplained it confuses the reader and undermines the contract. The fix is to ensure the figure caption explains the relationship: "The pooled ATT in Table 2 is the average across event years 0–4; this figure shows the year-by-year decomposition."

---

## 13. The final checklist

Before you commit a figure to the manuscript, run the following six-item checklist.

1. **One-glance test.** Pick the figure up cold. Can you, in fifteen seconds, identify the *x*-axis, the *y*-axis, the comparison, and the bottom-line claim? If no, redesign.
2. **Tufte test.** Are top and right spines off? Is the grid suppressed or very light? Is one accent color used? If no, restyle.
3. **Vector format.** Saved as PDF or SVG? At the figure's actual display size? If no, re-save.
4. **Axis labels with units.** Both *x* and *y* axes labeled? Units in the label? If no, add.
5. **Reference lines.** Horizontal zero line where appropriate? Vertical event line for event studies? Dashed reference at the preferred-spec coefficient for spec curves? Dashed reference at the overall ATT for forest plots? If no, add.
6. **Figure-table consistency.** Does the headline number in the figure match the headline number in the table? If no, reconcile.

The notebook `nb11.3` runs the first three checks programmatically (it inspects the saved PDF's bounding box, the rendered axis spines, and the colors used). The remaining checks are human.

The discipline of figures is the discipline of designing-from-the-claim-backward. Write the one-sentence caption; engineer the plot so the claim is visible without reading the caption; treat the caption as a redundancy check. In Chapter 11.4 we turn from the artifacts (table, figure, abstract) to the manuscript itself — the introduction whose five paragraphs determine whether a reader keeps reading past page two.

---

## 14. Recap

The reveal: **a publication-grade figure is engineered to make one comparison salient — and everything that is not in service of that comparison is removed or demoted.** The Tufte discipline (data-ink ratio, spine demotion, single accent color, direct labels) is the operationalization. Three figures every empirical-finance paper needs: event-study plot (the picture of parallel trends and treatment dynamics), specification-curve plot (the picture of robustness across the spec menu), heterogeneity forest plot (the picture of effect heterogeneity across subgroups). Each has its own anatomy and its own pitfalls. The five failure modes — default matplotlib, legend overlaps, unlabeled axes, over-decoration, figure-table mismatch — each have a fix.

Production discipline: vector formats, fonts sized for display, file-naming convention. Captions in four lines: what, source, inference convention, optional claim. Run the six-item checklist before commit.

### Glossary

- **Data-ink ratio**: Tufte's principle that the proportion of ink on the page conveying data (vs. frame, grid, decoration) should be maximized.
- **Event-study plot**: visual evidence for parallel trends and dynamic treatment effects in a DiD design; event-time *x*-axis, outcome *y*-axis, vertical line at $\tau = 0$.
- **Specification-curve plot**: visualization of the headline coefficient across the spec menu from Chapter 8.1, with a lower-panel choice indicator.
- **Heterogeneity forest plot**: visualization of subgroup ATTs as horizontal dots-with-CIs, ordered by subgroup, with a vertical reference line at the overall ATT.
- **Small multiples**: a grid of small parallel plots that replaces a single multi-line plot when comparison is the goal.

### Citations

- Brown, S. J., and J. B. Warner (1985). "Using Daily Stock Returns: The Case of Event Studies." *Journal of Financial Economics* 14(1): 3–31.
- Callaway, B., and P. H. C. Sant'Anna (2021). "Difference-in-Differences with Multiple Time Periods." *Journal of Econometrics* 225(2): 200–230.
- Gao, L., Y. Han, S. M. Li, and G. Zhou (2018). "Market Intraday Momentum." *Journal of Financial Economics* 129(2): 394–414.
- Simonsohn, U., J. P. Simmons, and L. D. Nelson (2020). "Specification Curve Analysis." *Nature Human Behaviour* 4(11): 1208–1214.
- Sun, L., and S. Abraham (2021). "Estimating Dynamic Treatment Effects in Event Studies with Heterogeneous Treatment Effects." *Journal of Econometrics* 225(2): 175–199.
- Tufte, E. R. (1983). *The Visual Display of Quantitative Information*. Cheshire, CT: Graphics Press.
- Wong, B. (2011). "Points of View: Color Blindness." *Nature Methods* 8(6): 441.
