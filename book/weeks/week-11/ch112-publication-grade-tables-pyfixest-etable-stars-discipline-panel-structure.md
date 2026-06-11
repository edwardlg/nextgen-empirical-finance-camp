# Ch 11.2 — Publication-Grade Tables: pyfixest etable to LaTeX, Stars Discipline, Panel Structure, and the One-Glance Test

You have a 248-word abstract that promises a number — 1.4 percentage points, 95% CI 0.8 to 2.0 — and a manuscript draft that contains the number, somewhere, in a table that currently has nineteen columns and three different rounding conventions and a coefficient labeled `__hdfe_2017__interact__OCC` that nobody but you can parse. The abstract is the contract; the *table* is the artifact the referee will turn to first to verify the contract. **If the table fails the one-glance test, the abstract loses credibility no matter how clean the prose was.** This chapter is the discipline that turns the regression output you have into a table the referee will read in fifteen seconds and trust.

Here is the move the chapter turns on. **A publication-grade table is not a regression output; it is a re-engineered presentation of selected regression output, with rows and columns and decimal places and footnotes chosen so that the reader can answer four specific questions in under a minute: *what is the headline coefficient, what is its precision, what is the sample, and what controls were in?*** Every choice you make — how many digits to print, where to put fixed-effect indicators, whether to use stars or full p-values, whether to break the table into panels by outcome or by sample — is in service of those four questions. Most student tables fail the test because they were produced *by* the regression software (the defaults dump everything) instead of *for* the reader (the defaults dump too much). The chapter teaches the production toolkit (`pyfixest`'s `etable()` to LaTeX), the conventions (stars discipline, panel structure, footnote anatomy), and the diagnostic (the one-glance test) — in that order. Maya's headline DiD table, Devon's event-study coefficients, Priya's flood-zone heterogeneity, Sam's intraday-momentum predictive regressions, and Leah's text-similarity spillover regressions will each appear as a worked example.

Before we start the machinery, a sentence about why this matters even though tables feel mechanical. **Tables are where referees decide whether to believe you.** The abstract says the result is 1.4 pp; the table says whether the result moves around as you change specifications, whether the t-statistic survives clustering, whether the sample is what you said it was. A polished table signals "I have done the work and I respect your time." A messy table signals "this paper was hurried." Referees infer rigor from typography. You may resent that this is true; you must still produce the typography.

---

## 1. The reveal: the one-glance test

A table passes the one-glance test if a referee — picking up your paper for the first time, with no idea what your finding is — can answer four questions in under sixty seconds:

1. **What is the headline coefficient?** Sign, magnitude, units.
2. **What is its precision?** Standard error, t-statistic, confidence interval, or stars.
3. **What is the sample?** Number of observations, number of clusters, time span.
4. **What controls and fixed effects were in?** At least at the level of "I see firm fixed effects, year fixed effects, and cluster-robust standard errors."

If the referee cannot answer all four in sixty seconds, the table has failed and the paper is in trouble. The four questions correspond to four design decisions you make when laying the table out: the **headline column** (the one the abstract quotes), the **precision convention** (standard error in parens below, with stars; full p-value in brackets; or t-statistic — pick one and stay consistent), the **sample footer** (a single row labeled "Observations" and a single row labeled "Clusters"), and the **fixed-effects indicators** (a small block of "Yes/No" rows at the bottom showing which fixed effects each column saturates).

The instinct of the student writing his first table is to *include everything*. Every coefficient, every standard error, every R-squared digit, every t-statistic. The instinct is wrong. **Every line on a table competes for the reader's attention; every line that is not earning its place is making the headline coefficient harder to see.** Triage applies here as it did in Chapter 10.1: each row earns its place by helping answer one of the four questions, or it does not earn its place and must go. The headline coefficient on Maya's DiD term is the row the abstract is about; the income-decile control coefficients in the same regression are not the row the abstract is about, and they belong in an online appendix, not on the main table.

We will use Maya's DiD as the recurring example. The four columns of her headline Table 2 will be: (1) the staggered DiD with county and year fixed effects; (2) add lender fixed effects; (3) add lender-by-year fixed effects (her preferred saturation); (4) restrict the sample to OCC-supervised counties only (the "tight" sample). All four columns will report the same headline interaction coefficient — the DiD term — with its standard error in parentheses, clustered at the county level. Below the coefficient block will be the fixed-effects indicator block. Below that, sample-size summary. Below that, a footnote naming clustering and significance levels. This is the layout we will produce, in LaTeX, using `pyfixest`'s `etable()`.

---

## 2. `pyfixest`'s `etable()` for LaTeX: the workhorse

We use `pyfixest` for two reasons that matter for tables in particular. First, `pyfixest`'s `feols()` returns a results object with a uniform interface, so `etable()` can dispatch across a list of models and produce one consistent table. Second, `etable()`'s LaTeX output is journal-clean by default — the `\toprule`/`\midrule`/`\bottomrule` from `booktabs`, no vertical lines, sensible default rounding — and is parameterized for the decisions you actually want to make (which coefficients to display, which fixed effects to show, what stars to use). It is, for empirical finance papers, the closest thing to a free lunch in table production.

Here is the minimal workflow. We have an estimated list of `pyfixest` models — `models = [m1, m2, m3, m4]` — and we want a four-column LaTeX table. The `etable()` call:

```python
# nb11.2 cell 1 — minimal pyfixest etable() to LaTeX
import numpy as np
import pandas as pd
import pyfixest as pf

rng = np.random.default_rng(42)

# Suppose `models` is a list of four fitted pf.feols() results.
tex_table = pf.etable(
    models,
    type="tex",                      # LaTeX output (not gt/df/markdown)
    coef_fmt="b (se)",               # estimate (standard error) under each coefficient
    keep=["treated_post"],          # only show the headline coefficient
    digits=3,                        # three decimal places for coefficients
    digits_stats=0,                  # zero decimals for N
    signif_code=[0.01, 0.05, 0.10],  # stars at 1%, 5%, 10%
    notes=(
        "Standard errors clustered at the county level in parentheses. "
        "*** p<0.01, ** p<0.05, * p<0.10."
    ),
    caption=(
        "Effect of intensified fair-lending examinations on the Black--White "
        "denial-rate gap. Staggered DiD with cohort-specific event-study leads "
        "and lags. HMDA 2014--2020, OCC-supervised counties."
    ),
    label="tab:maya_did_headline",
)

# Write the LaTeX directly to disk:
with open("tab_maya_did_headline.tex", "w") as fh:
    fh.write(tex_table)
```

Three flags do most of the work and deserve commentary.

The **`coef_fmt`** flag controls the *precision convention*. The two journal-standard conventions are `"b (se)"` (estimate above, standard error below in parens, with stars) and `"b\n[ci]"` (estimate above, 95% confidence interval in brackets below, no stars). The first is the *Journal of Finance*, *AER*, *JFE*, *RFS*, *JFQA*, and most finance journals' convention. The second is increasingly preferred at journals that want to de-emphasize stars (notably *AER: Insights*, *JEP*, and many medical and policy journals). Pick one and use it across every table in the paper.

The **`keep`** flag controls *which coefficients show*. By default, `etable()` shows every coefficient. By naming `keep=["treated_post"]` you suppress every coefficient except the headline. This is the single most important typographic decision: in Maya's regression, the income-decile coefficients, the minority-share coefficient, the loan-amount coefficients, and so on are *controls*, not headlines, and they take up forty rows that distract from the one row the abstract is about. Keep what answers the four one-glance questions; drop the rest. (If the editor or referee asks to see the control coefficients, they go in the online appendix, where there is no real estate constraint.)

The **`signif_code`** and **`notes`** flags together govern the *stars discipline*. The three-tier convention — *** at 1%, ** at 5%, * at 10% — is the finance-journal standard. The four-tier convention adds **** at 0.1%; the two-tier convention drops the 10% star. Use the three-tier as default; deviate only if the target journal's published style guide says otherwise. The notes string must name (a) what is in parens, (b) what the stars mean, (c) the clustering structure if any. Three short sentences. Anything longer belongs in the paper's main text or in an "Estimation details" appendix.

That is the entire workflow for one table. Now we turn to the harder decisions: which coefficients to show, how to structure panels, how to handle robustness columns, and how to format the fixed-effects-indicator block.

---

## 3. Stars discipline: when stars help, when they harm

Stars are the most controversial typographic choice in empirical economics, and the most common pathology in student tables is *star inflation*: every coefficient in every column gets three stars because the regressions are over-powered or because the panel is too large or because the standard errors are clustered at the wrong level. A table with stars everywhere conveys no information; it is, statistically, equivalent to a table with no stars at all, because nothing distinguishes the headline coefficient from the controls.

The discipline of stars is the discipline of *making the stars carry information*. Three rules.

**Rule 1: stars are for the headline row, not for control rows.** In a table that shows ten coefficients and seventeen rows, only the row corresponding to the policy treatment, the natural experiment, the headline regressor — only that row's stars are part of the contract with the reader. The control rows' stars are noise. The cleanest tables therefore display *no* stars on control coefficients, even when those coefficients are statistically significant. This rule is easily implemented in `etable()` by using `keep=["treated_post"]` and showing the controls in the fixed-effects-indicator block as Yes/No flags.

**Rule 2: stars must be calibrated to the right inference.** A coefficient that is starred at the 1% level under classical standard errors but not under cluster-robust standard errors is *not* a 1%-significant coefficient. The stars must be calculated using the standard errors you would defend to a referee, which means cluster-robust standard errors when the design is panel or DiD, Newey–West when the design is time-series, HC3 when the design is cross-sectional. `pyfixest`'s `feols()` allows you to specify the cluster structure at estimation, and `etable()` then reports stars based on the standard errors stored on the model object. If you change the cluster structure for robustness, you change the stars; do not display a "main" coefficient with classical-SE stars in column (1) and then a "robust" coefficient with cluster-SE stars in column (2). Either everything is cluster-robust, or you have two tables.

**Rule 3: stars do not substitute for confidence intervals when magnitudes matter.** A coefficient of 0.0001 starred at the 1% level is statistically significant and substantively trivial; a coefficient of 0.1 with a p-value of 0.11 is borderline significant and substantively large. The reader needs to see *both* the magnitude (the coefficient itself, in interpretable units) and the precision (the standard error or CI). Stars compress precision into a discrete signal that loses the magnitude–precision distinction. The fix is *not* to remove stars — that would lose the at-a-glance significance read — but to ensure the table also displays interpretable magnitudes and to discuss magnitudes in the prose, not just stars.

The strongest alternative to the stars convention is the **confidence-interval convention**, in which each coefficient is shown with a 95% CI in brackets below it and no stars are reported. The advantage is that magnitude and precision are both visible and the reader is forced to think in intervals rather than in dichotomous "significant or not" terms. The disadvantage is that the at-a-glance scan ("which columns are starred?") becomes harder. The convention is increasingly common in policy-oriented journals and in fields that have grappled with publication bias from p-hacking. For finance journals as of 2026, stars are still the default; the CI convention is acceptable but unusual. Pick what fits your target journal's style guide.

---

## 4. The fixed-effects indicator block

Every panel regression has a block of fixed effects, and the table needs to communicate *which* fixed effects are in *which* columns. `etable()`'s default is to print the fixed-effect names as "Yes/No" rows below the coefficient block, in the order in which they were specified in the `feols()` calls. The convention is so universal across journals that you should not deviate.

Maya's headline table has four columns with the following fixed-effect saturation:

| Column | County FE | Year FE | Lender FE | Lender × Year FE | Sample |
|--------|-----------|---------|-----------|------------------|--------|
| (1)    | Yes       | Yes     | No        | No               | Full   |
| (2)    | Yes       | Yes     | Yes       | No               | Full   |
| (3)    | Yes       | Yes     | No        | Yes              | Full   |
| (4)    | Yes       | Yes     | No        | Yes              | OCC    |

The block appears below the coefficient block. In LaTeX rendered by `etable()`, it looks like this (annotated for clarity, with `\Yes` and `\No` as TeX macros that you define once in your preamble for visual consistency):

```latex
\midrule
County FE         & Yes & Yes & Yes & Yes \\
Year FE           & Yes & Yes & Yes & Yes \\
Lender FE         & No  & Yes & No  & No  \\
Lender $\times$ Year FE & No  & No  & Yes & Yes \\
Sample            & Full & Full & Full & OCC \\
\midrule
Observations      & 47,123,481 & 47,123,481 & 47,123,481 & 32,891,402 \\
Clusters (county) & 614      & 614       & 614      & 412       \\
$R^2$ within     & 0.182    & 0.187     & 0.194    & 0.201     \\
\bottomrule
```

Two details to internalize. **First**, the sample row is part of the FE block. A column that drops observations to a restricted sample is a column with a different identification (effectively, a different population), and the reader needs to see that on the same row-level discipline as the FE indicators. **Second**, the observations row uses thousands separators. This is non-negotiable: an unseparated "47123481" is unreadable; "47,123,481" reads in half a second. Almost every LaTeX number formatter (siunitx, `{:,d}` in Python, `etable()`'s defaults) handles this; check that your output is doing it before submitting.

A common student error is to omit the cluster count. **Always report the cluster count when standard errors are clustered.** A regression with 47 million observations and 614 county clusters has *effective sample size* closer to 614 than to 47 million, and reviewers know this. Showing the cluster count is part of being honest about your degrees of freedom.

---

## 5. Panel structure: when to break a table into Panel A / Panel B

A single regression table communicates one specification across multiple columns. A *panel-structured* table communicates one specification across multiple *outcomes*, *samples*, or *subgroups* — each panel is a vertical block within the same table, sharing column headers but with different left-hand-side variables.

The canonical use case: Maya's heterogeneity analysis from Chapter 10.3 estimates the same DiD specification (preferred Column 3 from above) on four sub-samples — counties above and below the median minority-population share, and counties with above- and below-median lender-examination-finding histories. Rather than producing four separate tables — which buries the comparison and forces the reader to flip pages — we present one table with four panels. Each panel has its own DiD coefficient and standard-error row; the columns are unified (same set of fixed effects, same clustering); the panel labels appear as in-table mini-headers.

The LaTeX structure looks like this (abbreviated):

```latex
\begin{tabular}{lcccc}
\toprule
                  & (1)        & (2)        & (3)        & (4)        \\
                  & Baseline   & +Lender FE & Preferred  & OCC sample \\
\midrule
\multicolumn{5}{l}{\textbf{Panel A: Above-median minority share counties}} \\
Treated $\times$ Post  & -0.021    & -0.020    & -0.019    & -0.018    \\
                   & (0.004)*** & (0.004)*** & (0.004)*** & (0.005)*** \\
Observations       & 22.4M     & 22.4M     & 22.4M     & 15.8M     \\
\midrule
\multicolumn{5}{l}{\textbf{Panel B: Below-median minority share counties}} \\
Treated $\times$ Post  & -0.005    & -0.004    & -0.004    & -0.003    \\
                   & (0.003)    & (0.003)    & (0.003)    & (0.004)    \\
Observations       & 24.7M     & 24.7M     & 24.7M     & 17.1M     \\
\midrule
% Panels C and D analogous
\bottomrule
\end{tabular}
```

The panel labels (Panel A, Panel B, etc.) are inside the table, set off with `\multicolumn` and bold. The columns are *exactly* the same across panels. The reader can scan vertically down column (3) — the preferred specification — and read off the heterogeneity story in two seconds: -0.019, statistically significant in Panel A; -0.004, not significant in Panel B. That comparison is the whole point of the heterogeneity analysis.

When to use panels:

- **Multiple outcomes from the same design.** If you run the same DiD on denial rates, on loan sizes, and on interest spreads, you can put each outcome in a panel, with the same column structure. The reader can read across panels to see which outcomes are affected.
- **Multiple sub-samples.** Heterogeneity analysis, as in Maya's example above.
- **Pooled vs. by-cohort effects in staggered DiD.** Panel A is the pooled ATT; Panels B–D are the cohort-specific ATTs.

When *not* to use panels:

- **Different specifications of the same outcome.** Those go in columns, not panels. Columns (1)–(4) of Maya's headline table are different fixed-effect saturations; they are *not* panels.
- **Robustness checks.** Robustness goes in a separate table, often Table 3 (the headline) followed by Table 4 (robustness across alternative SEs, samples, etc.). Mixing headline and robustness in one panel-structured table buries the headline.

`pyfixest`'s `etable()` does not produce panel-structured tables out of the box (each call produces one panel); you produce four `etable()` outputs and stitch them into one table with a panel header line, either by manual LaTeX editing or by a small helper function. The helper function is in `nb11.2`; here is the spine:

```python
# nb11.2 cell 2 — panel-structured table from a list of model lists
def panel_table(panels: dict, **etable_kwargs) -> str:
    """
    Build a panel-structured LaTeX table.
    `panels` is a dict mapping panel labels to lists of fitted pyfixest models.
    All lists must have the same length (same column structure across panels).
    """
    bodies = []
    for label, model_list in panels.items():
        body = pf.etable(model_list, type="tex", **etable_kwargs)
        # Strip the top/bottom of each etable() output, keep only the data rows
        body = _strip_tex_wrapper(body)
        panel_header = (
            r"\multicolumn{" + str(len(model_list) + 1) + r"}{l}{\textbf{"
            + label + r"}} \\"
        )
        bodies.append(panel_header + "\n" + body)

    return _wrap_tex(bodies, etable_kwargs.get("caption"), etable_kwargs.get("label"))
```

The full function with the wrapper helpers is in the notebook. The point is: panel structure is a stitching step, not a regression step, and once you have it scripted you can re-render the table after any change to the underlying regressions without re-typesetting by hand.

---

## 6. Worked example: Maya's Table 2, end to end

We will produce Maya's headline Table 2 from start to finish. The input is the `pyfixest` model objects estimated in Chapter 10.3's notebook; the output is a single LaTeX file ready for `\input{}` into the manuscript.

```python
# nb11.2 cell 3 — Maya's Table 2: headline DiD, four columns
import numpy as np
import pandas as pd
import pyfixest as pf

rng = np.random.default_rng(42)

# Assume `df` is the loaded HMDA panel with the constructed variables.
# (Full data-construction code is in nb10.1 of the previous week.)

m1 = pf.feols(
    "denial_gap ~ treated_post | county + year",
    data=df,
    vcov={"CRV1": "county"},
)
m2 = pf.feols(
    "denial_gap ~ treated_post | county + year + lender",
    data=df,
    vcov={"CRV1": "county"},
)
m3 = pf.feols(
    "denial_gap ~ treated_post | county + year + lender^year",
    data=df,
    vcov={"CRV1": "county"},
)
m4 = pf.feols(
    "denial_gap ~ treated_post | county + year + lender^year",
    data=df.query("occ_supervised == 1"),
    vcov={"CRV1": "county"},
)

table2 = pf.etable(
    [m1, m2, m3, m4],
    type="tex",
    coef_fmt="b (se)",
    keep=["treated_post"],
    labels={"treated_post": r"Treated $\times$ Post"},
    digits=3,
    digits_stats=0,
    model_heads=["(1) Baseline", "(2) +Lender FE", "(3) Preferred", "(4) OCC sample"],
    signif_code=[0.01, 0.05, 0.10],
    notes=(
        "Standard errors clustered at the county level in parentheses. "
        "*** p<0.01, ** p<0.05, * p<0.10. "
        "Outcome is the Black--White denial-rate gap, percentage points. "
        "Sample: HMDA 2014--2020, OCC-supervised counties in cols (1)--(3); "
        "OCC-supervised only in col (4)."
    ),
    caption=(
        "Effect of intensified fair-lending examinations on the Black--White "
        "denial-rate gap."
    ),
    label="tab:maya_did_headline",
)

with open("manuscript/tables/tab_maya_did_headline.tex", "w") as fh:
    fh.write(table2)
```

Five details earn special mention.

**The `labels` dict.** `etable()` will print the raw coefficient name (`treated_post`) unless you supply a label. Labels are how you produce the journal-clean phrase the reader will see ("Treated × Post") instead of the snake_case Python variable. Always supply labels; the table is for the reader, not for the developer.

**The `model_heads` list.** Column headers are usually just (1), (2), (3), (4) — minimal. For a paper where the columns differ in a meaningful way, an additional line below the column number (here, "Baseline / +Lender FE / Preferred / OCC sample") tells the reader at a glance what the columns are. This is borderline; many journals dislike anything beyond the column number. Check the target journal's style.

**The `digits_stats` parameter.** `etable()` by default formats sample-size rows with three decimal places, which produces things like "47123481.000" — disastrous. Setting `digits_stats=0` fixes this. Always set it.

**The `vcov={"CRV1": "county"}` argument** to `feols()`. This is where cluster-robust standard errors at the county level are specified. The standard errors that appear in the table are determined by this argument; change it and you change the stars. `pyfixest` supports a wide variety of variance estimators — heteroskedasticity-robust (`{"HC1": ""}` for the default; `{"HC3": ""}` for the small-sample improvement), cluster-robust (one-way and multi-way), and the wild-cluster bootstrap. Pick the one your design demands and document it in the notes.

**The caption is short.** Three lines, no more. The caption answers "what does this table show?"; the notes answer "how was it estimated and what do the numbers mean?". Many students confuse these and write a five-line caption with the entire research-design summary in it. The reader does not read captions that long; she reads the abstract, the column headers, and the coefficient row. Keep captions to two sentences max.

The rendered table — once `\input{}`ed into the manuscript and compiled with `booktabs` and `siunitx` packages loaded — looks roughly like:

```
                              (1)        (2)        (3)        (4)
                           Baseline  +Lender FE Preferred  OCC sample
─────────────────────────────────────────────────────────────────────
Treated × Post              -0.015**  -0.013**  -0.014***  -0.014***
                           (0.006)   (0.005)   (0.004)    (0.004)
─────────────────────────────────────────────────────────────────────
County FE                   Yes       Yes       Yes        Yes
Year FE                     Yes       Yes       Yes        Yes
Lender FE                   No        Yes       No         No
Lender × Year FE            No        No        Yes        Yes
─────────────────────────────────────────────────────────────────────
Observations              47,123,481 47,123,481 47,123,481 32,891,402
Clusters (county)              614        614        614       412
R² within                    0.182      0.187      0.194     0.201
─────────────────────────────────────────────────────────────────────
```

Read the table. The headline coefficient (-0.014, three stars) is the same across the most saturated specifications. The sample size is honest. The cluster count is shown. The fixed-effects block tells the saturation story. The number that appears in the abstract — 1.4 percentage points — corresponds to the column (3) coefficient of -0.014, multiplied by 100 to convert from a proportion to a percentage point. **The table answers the four one-glance questions in fifteen seconds.** It earned its place on Page 12 of the manuscript.

---

## 7. Three tables every empirical paper needs

The publication-grade tables in an empirical paper typically fit into three roles. Knowing the roles helps you plan how many tables your paper needs and what each one is for.

**Role 1 — The Headline Table** (usually Table 2, after the summary statistics in Table 1). This is the table that delivers the abstract's headline number. It has the canonical four-to-six-column structure: progressively saturated specifications, with the preferred specification highlighted (often by bolding the column number or by a footnote). The column headers vary across specifications; the row count is small (one or two coefficient rows plus the FE block plus the sample footer). This is the table the referee opens to first; it earns the most layout effort.

**Role 2 — The Robustness Table** (Table 3 or 4). This shows the headline coefficient across alternative samples, alternative SEs, alternative estimators, alternative outcome definitions, alternative control sets. It has many columns (often eight to twelve) and one or two coefficient rows. The point is *comparison across columns*: the reader's eye scans the headline row left to right, confirming that the coefficient does not move. Robustness tables tolerate higher column counts than headline tables because each column is a one-degree variant and the reader is only checking that it survives.

**Role 3 — The Heterogeneity Table** (Table 4 or 5). This is where panel structure earns its keep. The columns are the same fixed specifications (often just one or two); the panels are different sub-samples or different sub-populations. The reader scans down column (1) across panels, reading off the heterogeneity story. We saw the layout in §5 above.

Beyond these three roles, you might have a mechanism table (instrumented variable estimates, mediator regressions), a placebo table (effects on outcomes that should be unaffected if your design is clean), and a first-stage table (for IV designs). These are paper-specific; the three roles above are universal.

Maya's paper has: Table 1 (summary statistics, see §8 below), Table 2 (headline DiD, four columns), Table 3 (robustness across alternative samples and SEs, twelve columns), Table 4 (heterogeneity by minority-share and examination-history, four panels times four columns), Table 5 (placebo on alternative outcomes that should not be affected, six columns, all coefficients insignificant), Table 6 (Oster δ sensitivity, two columns). Six tables. That is on the high end for a forty-page paper, and three of those (Tables 3, 5, 6) may end up in an appendix in the published version. The discipline is: every table in the main body earns its place by answering a question the abstract raised. Tables that don't earn their place go to appendices.

---

## 8. Summary statistics: the table you cannot skip

Every empirical paper has a summary-statistics table, often Table 1, and it is the table students most often phone in. **Table 1 is the reader's first encounter with your variables**; if it is sloppy, the reader's prior on the paper's quality is set permanently low.

The canonical Table 1 has rows for each variable, columns for sample-mean, standard deviation, 25th-50th-75th percentiles, minimum, maximum, and N. Variable names are in the leftmost column; if some variables are continuous and some are binary, the binary variables show only mean (which equals proportion) and N. The variables are grouped: outcomes first, treatment indicator second, then control variables, then auxiliary fixed-effect-defining variables.

If your design has a treatment-and-control structure, you should also show *balance* — means in the treated and control groups separately, with a difference and a t-statistic on the difference. Balance is the diagnostic that tells the reader whether your design is operating in a regime where the comparison is sensible. A baseline imbalance of 0.4 standard deviations on a key covariate is a red flag and the discussion of how the DiD handles it (e.g., through the fixed-effect structure) needs to appear in the text.

```python
# nb11.2 cell 4 — balanced summary stats with treated/control split and difference test
def balance_table(df: pd.DataFrame, treat: str, vars_to_show: list[str]) -> pd.DataFrame:
    out = []
    for v in vars_to_show:
        t = df.loc[df[treat] == 1, v].dropna()
        c = df.loc[df[treat] == 0, v].dropna()
        diff = t.mean() - c.mean()
        # Welch's t-statistic
        se = np.sqrt(t.var(ddof=1) / len(t) + c.var(ddof=1) / len(c))
        tstat = diff / se if se > 0 else np.nan
        out.append({
            "Variable": v,
            "Treated mean": t.mean(),
            "Treated SD":   t.std(),
            "Control mean": c.mean(),
            "Control SD":   c.std(),
            "Diff":         diff,
            "t-stat":       tstat,
        })
    return pd.DataFrame(out)
```

The output is converted to LaTeX with `pandas`'s `to_latex()` or with `tabulate`, with the same `booktabs` discipline as the other tables. The result is a Table 1 that the reader can verify the sample on (N, period, source) and confirm the design's plausibility (balance) before the headline regression is even reached.

---

## 9. Common failure modes, named

We have seen the positive template. Now the failure modes — the four patterns of bad tables that students produce and that referees mark for revision.

### 9.1 The Spreadsheet Dump

The spreadsheet dump prints every coefficient from every regression, all twenty controls, with three stars on each cluster-irrelevant coefficient. The reader cannot find the headline. The fix is `keep=["treated_post"]` in `etable()`.

**The diagnostic**: can a reader, opening the paper for the first time, identify the headline coefficient within three seconds? If no, the table is a spreadsheet dump.

### 9.2 The Stars-Everywhere Table

The stars-everywhere table has stars on every row of every column because the sample is large and everything is significant. The stars carry no information. The fix is to suppress stars on control rows (by suppressing the controls entirely with `keep=`), and to discuss the magnitude (not the stars) in the text.

**The diagnostic**: how many distinct levels of star are present in the table? If only one (everything is ***), the stars are not informative.

### 9.3 The Inconsistent-Rounding Table

The inconsistent-rounding table has the coefficient at three decimal places, the standard error at two, the t-statistic at four, the R-squared at five, and the sample size with no thousands separator. The fix is to commit to a rounding convention in the table-production script and apply it consistently. `etable()`'s `digits=3, digits_stats=0` handles most of this; the rest is post-processing.

**The diagnostic**: are all coefficients formatted to the same number of decimal places? Are all standard errors formatted to the same number of decimal places? Are sample sizes shown with thousands separators? If any answer is no, the table needs another pass.

### 9.4 The Caption-Doing-the-Heavy-Lifting

The caption-doing-the-heavy-lifting table has a five-line caption that explains the entire research design because the columns and rows alone cannot convey it. The fix is to redesign the table so the column headers and row labels convey the design at a glance, and keep the caption to two sentences. If you need five lines of caption, the table itself is failing.

**The diagnostic**: how long is the caption? If more than 50 words, the caption is doing work the table layout should be doing.

---

## 10. The LaTeX preamble: small details that make tables look professional

Once your `etable()` output is generated, the LaTeX preamble of your manuscript determines whether it renders cleanly. Here is the minimum preamble for publication-grade tables:

```latex
\usepackage{booktabs}    % provides \toprule, \midrule, \bottomrule (no vertical lines, no double-rules)
\usepackage{siunitx}     % aligns numbers on the decimal point
\usepackage{adjustbox}   % \begin{adjustbox}{max width=\textwidth} for wide tables
\usepackage{threeparttable}  % notes block that wraps the table
\sisetup{
  detect-all,
  table-number-alignment = center,
  group-digits = integer,
  group-separator = {,},
  group-minimum-digits = 4,
}
\newcommand{\Yes}{Yes}
\newcommand{\No}{No}
```

Two specifics worth memorizing. `booktabs` produces `\toprule`, `\midrule`, and `\bottomrule` — three horizontal-rule styles with different weights — and explicitly forbids vertical rules and double rules. The result is the clean, white-space-driven look of every modern econ journal table. **Never use `\hline`; never use `|` in tabular column specs.** Both are amateur-hour signals.

`siunitx` aligns numbers on the decimal point in number columns by replacing `tabular` column type `c` with `S` (or `S[table-format=2.3]` for a fixed format). This is the difference between a column where -0.015, -0.013, -0.014 align cleanly on the decimal and a column where they wobble. `etable()` produces output compatible with `S` columns when you ask for it.

`threeparttable` is what wraps the table-plus-notes block so that the notes appear at the column width of the table, not at the page width. It is what makes the notes look like part of the table rather than floating text below it.

---

## 11. The final checklist

Before you commit a table to the manuscript, run the following five-item checklist.

1. **One-glance test.** Pick the table up cold. Can you, in sixty seconds, answer: headline coefficient? precision? sample? controls? If no, redesign.
2. **Stars discipline.** Are stars only on the headline row, or are they cluttering every row? Are they computed with the standard errors you would defend to a referee? If no, fix `keep=` or `vcov=`.
3. **Rounding consistency.** Same decimal places across all coefficients, all SEs, all R-squareds? Thousands separators on N? If no, run the script again with `digits=`, `digits_stats=` set.
4. **Caption length.** Caption ≤ two sentences? Notes ≤ three sentences? If no, redesign.
5. **Cluster honesty.** If standard errors are clustered, is the cluster count shown? Is the clustering structure named in the notes? If no, the table is misleading.

The script in `nb11.2` runs the first four checks programmatically (the script reads the `.tex` file and counts headline coefficients, distinct star levels, decimal places, caption length); the fifth is a human read.

The discipline of tables is the most prosaic part of writing a paper and the most consequential for the referee's first impression. A clean Table 2 buys you fifteen seconds of goodwill. A messy Table 2 costs you the rest of the paper. Apply the checklist; produce the table from the script; let `etable()` and `booktabs` do most of the work. In Chapter 11.3 we turn to the other publication-grade artifact — the figure — and to the small set of plots (event study, specification curve, heterogeneity forest) that every empirical paper needs.

---

## 12. Recap

The reveal: **a publication-grade table is engineered for the one-glance test — headline coefficient, precision, sample, controls — and every typographic choice serves that test.** The workhorse is `pyfixest`'s `etable()` to LaTeX, with `keep=`, `coef_fmt=`, `signif_code=`, and `labels=` doing most of the work. Stars discipline requires that stars carry information; they should be on the headline row, calibrated to the right inference, and never substitute for magnitude reporting. Panel structure handles heterogeneity and multi-outcome presentations; columns handle alternative specifications. The four failure modes — spreadsheet dump, stars everywhere, inconsistent rounding, caption-doing-the-heavy-lifting — each have diagnostic questions.

Three tables every paper needs: headline (Table 2), robustness (Table 3), heterogeneity (Table 4). Plus summary statistics (Table 1) with balance if the design is causal. The LaTeX preamble matters; `booktabs`, `siunitx`, and `threeparttable` are required. Run the five-item checklist before committing the table to the manuscript.

### Glossary

- **One-glance test**: the diagnostic that a publication-grade table must let a referee answer four questions (headline coefficient, precision, sample, controls) in under sixty seconds.
- **Stars discipline**: the principle that stars must be calibrated to the right inference and concentrated on the headline row.
- **Panel structure**: the layout in which one table contains multiple vertical sub-blocks (panels), each estimated on a different sub-sample or with a different outcome, sharing column specifications.
- **`etable()`**: `pyfixest`'s table-rendering function; produces journal-clean LaTeX output from a list of model objects.
- **`booktabs`**: the LaTeX package that produces `\toprule`/`\midrule`/`\bottomrule` and is the modern standard for econ-journal tables.

### Citations

- Callaway, B., and P. H. C. Sant'Anna (2021). "Difference-in-Differences with Multiple Time Periods." *Journal of Econometrics* 225(2): 200–230.
- Cameron, A. C., and D. L. Miller (2015). "A Practitioner's Guide to Cluster-Robust Inference." *Journal of Human Resources* 50(2): 317–372.
- Fischer, A., and M. Wagner (2024). "pyfixest: Fast Fixed-Effects Regression in Python." Working paper, GitHub repository `s3alfisc/pyfixest`. [CHECK]
- Gao, L., and J. Sun (2019). "Lender-Borrower Race-Match Effects on Mortgage Approval." *Proceedings of the National Academy of Sciences* 116(19): 9293–9302.
- Stigler, S. M., and J. M. Wainer (1997). "Improving Tabular Presentations, with Some Help from Galileo, Bacon, and Pearson." *Chance* 10(3): 7–13. [CHECK — Wainer's "Improving Tabular Presentations" lineage]
