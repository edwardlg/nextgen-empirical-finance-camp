# Ch 10.1 — Triaging Conference Feedback: the Cost / Value / Threat-to-Identification 3×3 and the "Required vs. Welcome vs. Decline" Memo

You walked out of Saturday's conference with a notebook full of comments, a phone full of voice memos, and the queasy feeling that everyone in the room asked a question you cannot yet answer. In Chapter 9.5 you spent the first twenty-four hours after the conference doing exactly what you were told: you wrote every comment down before sleep erased it, you tagged each one with the speaker's role and the apparent intensity, and you closed the laptop on a CSV that looks suspiciously like a Trello board. It is Monday. The CSV has forty-seven rows. You have four weeks to defend the paper as a *submission* — not as a presentation. **This chapter is about the act of triage that turns those forty-seven rows into a plan you can actually execute.**

Here is the move the chapter turns on, so you have it before the machinery. **Not every conference comment deserves a response, and the discipline of triage is the discipline of saying so on the record.** Empirical papers fail in revision for two opposite reasons: authors do nothing with feedback (the result feels brittle, the next reviewer asks the same questions, and the paper dies) or authors do *everything* with feedback (the analysis sprawls, the central claim gets buried under twenty robustness exhibits, the seam between the pre-registered design and the post-hoc additions becomes invisible, and the paper dies a different death). The middle path — *do exactly the things you owe and nothing else, and write down what you declined and why* — is what professional revision looks like. This chapter teaches you the two artifacts that make that middle path tractable: a **3×3 triage matrix** for ranking comments by cost, value, and threat-to-identification, and a **"Required vs. Welcome vs. Decline" memo** that you commit to a file before any new code runs.

We will work in Maya's office with the staggered DiD on fair lending you have been refining since Week 7. Her conference comments are stylized but representative: the discussant pushed on her treated-cluster count; one audience member wanted heterogeneity by examination intensity; a senior colleague mentioned that her control counties might be on a different denial-gap trend; a junior peer asked whether she had tried a different fixed-effect saturation; her advisor scrawled "Oster delta?" on the back of his program; and three other comments range from "have you read this 2024 working paper" to "your slide 12 font is too small." Forty-seven rows is realistic; the temptation to start with the loudest comment first is universal; the right response is the same as for every other dataset you have seen in this book: **build the analytic frame before you touch the data.**

---

## 1. The reveal: what triage actually is

Triage is **resource allocation under irreversible deadlines.** That sentence is borrowed almost verbatim from emergency-room medicine, where the analogy was invented, and it is not metaphor — it is the same problem. You have a fixed quantity of attention (four weeks, perhaps eighty productive hours), a list of patients (comments) with varying severity (threat to your identification), varying cost-to-treat (an hour vs. a week), and varying upside (will it actually improve the paper or just appease one reader). The triage rule in an ER is: **save the patients you can save, who would die without you, in the order in which their condition will deteriorate.** Translated into empirical revision: **answer the comments that, if left unanswered, would kill the paper at a real referee — in the order they will rise to the top of a real referee's pile.**

This translation has three consequences that drive everything that follows.

First, **the severity dimension is not the loudness dimension.** The comment that got the most pushback in the room is often a question about presentation (a confusing slide, an unfortunate framing), not a question about identification. The comment that *will* kill the paper is the one the discussant said in a calm voice, possibly only once, possibly only in the hallway: "Have you thought about whether the timing of these examinations is correlated with the *intensity* of the local mortgage market?" That is a confounding-by-pre-treatment-trend question dressed in mild words, and it is a threat to the identifying assumption you wrote down in Chapter 7.5. Triage must learn to *hear* severity past loudness.

Second, **the cost dimension is real and non-negotiable.** A request to add a second-stage IV using a brand-new instrument is a multi-week project. A request to add a row to a robustness table you already built is forty-five minutes. If you spend the four weeks of revision on the first, you do not get to do the second; if you spend them all on twelve forty-five-minute additions, the second-stage IV does not appear and the discussant's central concern is not addressed. Triage forces the trade-off into daylight.

Third, **the value dimension is asymmetric.** The first robustness check that closes a threat has enormous marginal value: it transforms "this might be confounded" into "this is robust to confounding." The fifth robustness check on the same threat has approximately zero marginal value: it persuades no additional reader, and adds a column to a table that already filled with reassurance. Triage must price in *diminishing returns to robustness within a threat category.* You cannot answer the same threat with more checks; once it is answered, move on.

These three forces — severity, cost, marginal value — are the three axes of the 3×3 matrix we are about to build.

---

## 2. The 3×3: Cost × Value × Threat-to-Identification

We will simplify to three discrete levels on each of three axes. The grid that results has 27 cells; only a handful of them require any real cognitive work to fill. The discipline is to assign each comment to one cell of the grid *before* you decide what to do about it. The grid lives in a spreadsheet (or a CSV; see the code below). Its purpose is to take a forty-seven-row gut-feel pile and turn it into a sortable, defensible plan.

### 2.1 Axis 1 — Cost

The cost axis is the easiest to assign because it is the most concrete. We use three buckets, calibrated to the four-week revision window.

- **Low (≤ 4 hours):** a new robustness row using an existing dataset and an existing estimator; a clarifying paragraph in the introduction; a redrawn figure; a citation chase; a font fix on a slide.
- **Medium (½ day to 2 days):** a new variant of the main spec that requires re-pulling data or a meaningful merge; a heterogeneity cut that requires defining and validating subgroups; a placebo test that requires careful sample construction.
- **High (≥ 3 days):** a new identification strategy; a new dataset; a new estimator that requires reading and implementing a method paper; a structural-model addition; a substantial re-writing of the theory section.

These are not estimates of how long the work *should* take; they are estimates of how long it will *actually* take given that you will need to debug, validate, and integrate it into the existing pipeline. The Hofstadter law you met in Chapter 7.2 applies: things take longer than you expect, even when you account for Hofstadter's law. Multiply your first instinct by two and round up. A "low" comment that turns out to require three days of dataset cleaning was actually a medium or high comment that you mis-classified.

### 2.2 Axis 2 — Value

The value axis is the one most students get wrong, because they conflate *value to the paper* with *value to the commenter*. A senior colleague who insists on a citation to their own paper is offering high value to themselves and modest value to you. A junior peer who asks a question that would also occur to a referee is offering high value to you regardless of who they are. Score value from the *paper's* perspective.

- **Low:** addresses no threat in your Chapter 7.5 threats table; does not change a reader's belief about the headline number; does not enable a new claim. Examples: minor stylistic suggestions, fights you do not need to pick, comments that reflect the commenter's own research agenda rather than your paper's needs.
- **Medium:** clarifies something the paper currently muddles; closes a *small* gap in the argument; pre-empts a likely referee complaint without changing the headline. Examples: better motivation in the introduction, an additional control variable that does not move the point estimate but tightens the standard error, a placebo on an outcome you should have placebo-tested already.
- **High:** closes a *named* threat from the threats table; meaningfully changes a reader's posterior on the headline; opens a new claim that the paper can credibly make. Examples: a robustness check that survives the discussant's central worry, a heterogeneity result that the headline alone could not deliver, a mediation analysis that turns "we estimate the effect" into "we estimate the effect *and* the channel."

### 2.3 Axis 3 — Threat to identification

The third axis is the one that determines whether you have a choice at all. It is binary in the limit, but we keep three levels for triage finesse.

- **Threat = none:** the comment is about presentation, motivation, framing, or style. It does not connect to a row in the threats table. The headline number is the same regardless of what you do. Most "have you read this paper" comments live here.
- **Threat = bounded:** the comment names a threat that *is* on the threats table and *is* already addressed in the robustness battery — the comment is asking for a strengthening, not a rescue. The headline number probably survives. Most "did you cluster differently" comments live here.
- **Threat = central:** the comment names a threat to your identifying assumption that, if true, would invalidate the headline result. The comment is asking for a *rescue*. If you cannot answer it, the paper does not get submitted. Examples: a sharp discussant's parallel-trends pushback, an instrument-validity challenge, an unobserved-confounder argument with a plausible omitted variable named.

### 2.4 The 27-cell grid and what each cell means

With three levels on each of three axes, the grid has 27 cells. Most of them have an obvious verdict.

The verdict logic, in plain English: **anything that is threat-central is *Required*, regardless of cost.** You owe a response to a central threat. The only question is how — and we will see in §3 that the response can be analytic (run the test) or rhetorical (explain why the test cannot be run cleanly and bound the bias instead). **Anything that is high-value-and-low-cost is *Required*** even if the threat is bounded or absent, because the marginal-value-per-hour is too good to skip; these are the wins you bank in week one. **Anything that is low-cost-and-medium-value is *Welcome*** — do it if you have slack, skip it without guilt if you do not. **Anything that is high-cost-and-low-value, or low-cost-and-no-threat-and-low-value, is *Decline*** — you write a sentence in the response memo explaining why and you move on.

The hardest cells are the medium-cost, medium-value, bounded-threat cells: a comment that asks for a real but not-essential strengthening that will cost you a day or two. The rule we recommend is: **if it would survive a referee asking the same question, decline with explanation; if a referee would persist, do it.** That is a judgment call, and you will improve at it through Weeks 10–12 and across many papers afterward. The memo in §4 is what makes the judgment call defensible.

Here is what the assignment looks like for six of Maya's forty-seven comments, after triage.

| # | Comment (paraphrased) | Cost | Value | Threat | Cell | Verdict |
|---|---|---|---|---|---|---|
| 1 | Discussant: "Are adopting states on a different pre-trend?" | Med | High | Central | M-H-C | **Required** |
| 2 | Audience: "Heterogeneity by examination intensity?" | Med | High | None | M-H-N | **Required** |
| 3 | Advisor: "Oster δ for unobservables?" | Low | High | Central | L-H-C | **Required** |
| 4 | Peer: "Try TWFE with year-by-region FE?" | Low | Med | Bounded | L-M-B | **Welcome** |
| 5 | Audience: "Cite Smith (2024) working paper" | Low | Low | None | L-L-N | **Welcome** |
| 6 | Senior colleague: "Re-frame intro around their AER" | High | Low | None | H-L-N | **Decline** |

Read down the verdict column and you see the four weeks: the three Required items are the spine of the revision (one is the chapter-7.5 parallel-trends rescue from Chapter 10.5 of this week's book; one is the heterogeneity analysis you will see in Chapter 10.3; one is the Oster sensitivity that lives in Chapter 8.2's robustness battery). The two Welcome items go into a "if-time-allows" lane at the end of week three. The one Decline gets a one-sentence reason in the memo and disappears from the to-do list.

---

## 3. Listening for severity past loudness

The triage grid is only as good as the assignments you put into it, and the hardest assignment is the threat-axis one. **You must learn to translate spoken comments into the threats-table vocabulary you wrote in Chapter 7.5.** This translation step is where most students fail, because conference comments are rarely phrased in identification-strategy terms — they are phrased in the commenter's *own* analytic instincts. You have to do the work of reading what they meant.

Consider how three common phrasings map onto threats.

**"Have you thought about endogeneity?"** is the worst phrasing in empirical economics and unfortunately the most common. Used by a senior person, it can mean anything from "I think there is an omitted variable" to "I think your sample selection biases the estimate" to "I want you to read my paper on a related instrumental variable." Triage requires you to ask, in your head or in a follow-up email: *which of the four canonical threats — omitted variable, reverse causality, measurement error, selection — are you naming?* Until you can map the comment to one of those, it stays *unranked* on the grid. (In Maya's case, the discussant who used this phrase turned out to mean: "Your treated states adopted examinations in years when their mortgage markets were already in transition; the pre-trend is real, and you need to address it." That is parallel-trends, not endogeneity-in-general, and once translated it goes to M-H-Central.)

**"Did you try X?"** is usually a robustness-flavored comment dressed as a question. The right translation is: *what threat is X addressing, and is that threat in my table?* If X (say, two-way clustering) addresses a threat (cluster-correlation under treatment) that is already in your robustness battery (Chapter 8.2), the comment is bounded and the verdict will lean Welcome. If X addresses a threat you have not yet addressed, severity goes up.

**"What about heterogeneity?"** is rarely an identification challenge; it is usually a request for additional claims the paper could make. Translation: *what subgroup is being requested, and what would the heterogeneity tell us about the mechanism?* If the subgroup is theoretically motivated (Maya's exam-intensity cut), the value is high; if the subgroup is post-hoc fishing ("split on race × age × income × geography"), the value is low and the threat to inference is *multiple testing*, which is exactly the topic of Chapter 10.2. The grid handles this naturally: a fishing-style heterogeneity request is M-L-Bounded and triages to Decline.

**"Your standard errors look optimistic"** is a comment about the variance of your estimator, not its identification. Translation: *is the commenter naming a clustering level, a serial-correlation pattern, a few-treated-clusters issue, or something else?* In Maya's case, the comment in the room came with the specific phrase "only a handful of treated states," which maps directly to the wild-cluster-bootstrap row of Chapter 8.2's robustness battery — bounded threat, high value, low cost — and triages to Required.

The general rule: **a comment that cannot be translated into a threats-table row is a presentation comment, not an identification comment.** Score it L-N or M-N on the threat axis and triage accordingly. Many comments that *feel* devastating in the moment turn out to be presentation comments after translation; this is good news, and the grid will tell you.

---

## 4. The "Required / Welcome / Decline" memo

The grid is a private artifact. The memo is the *public* artifact that turns the grid into a commitment. You commit it to your repo, you share it with your advisor, and you treat it as the work-plan for the next four weeks. **The memo has three sections: Required, Welcome, Decline. Each comment appears in exactly one section, with two lines: what the comment was, and what you will do (or not do) about it.**

The memo for Maya's six rows from §2.4 reads like this:

> **Required (must complete before submission)**
> 1. *Discussant pushed on parallel trends across adopting cohorts.* I will (a) run the Callaway–Sant'Anna event-study pre-treatment leads and report the joint test of zero leads; (b) add an honest-DiD bound on violations of parallel trends (Rambachan & Roth 2023);[^rr2023] (c) re-estimate against a not-yet-treated control set only. See revised §6 and new Appendix C.2.
> 2. *Audience requested heterogeneity by examination intensity.* I will define intensity using the FFIEC field on examination scope (see Ch 10.3), pre-register the three intensity bins before estimation, and report a causal-forest CATE on the bin-level treatment-effect heterogeneity test. See revised §7 and new Appendix C.3.
> 3. *Advisor flagged unobservable-bias sensitivity.* I will run the Oster (2019) δ calculation against $R^2_{\max} = 1.3 \cdot R^2$ and the Cinelli–Hazlett (2020) sensitivity contour plot. See revised Table 5 footnote and new Appendix C.4.
>
> **Welcome (will complete if time permits in weeks 3–4)**
> 4. *Peer suggested TWFE with year-by-region FE.* I will add this as a robustness column to Table 5, noting that the C–S estimator already accommodates the equivalent of a year-by-cohort interaction.
> 5. *Audience requested Smith (2024) citation.* I will add the citation to footnote 3 of the introduction.
>
> **Decline (will not pursue; reason recorded)**
> 6. *Senior colleague suggested re-framing intro around their AER.* The proposed framing centers a related but distinct research question; the current intro frames the paper around the fair-lending policy literature, which is the literature the paper directly contributes to. We retain the current framing and add a footnote acknowledgement of the related line.

Three features of this memo are deliberate.

**First**, every Required item has a concrete deliverable named: a section, an appendix, a table footnote, a method, a citation. The memo is a list of *promises*, and you will be held to those promises by the next person who reads the revised paper — your advisor, your co-author, the editor, the referee. Vagueness here ("I will check whether the result is robust") will get you nowhere; specificity ("I will run Rambachan–Roth honest-DiD with smoothness parameter $\bar{M} = 0.02$") is the unit of accountability.

**Second**, every Decline has a reason. *Not* a justification ("the senior colleague was wrong"); a reason ("the proposed reframing centers a different question"). This is the same discipline as the threats-and-responses table from Chapter 7.5: column three was "what we do about it," and "we decline to address it because X" is a perfectly valid entry in column three, *provided X is a real reason a reader can evaluate.* The memo is your forum for those reasons.

**Third**, the memo is committed to the repo, dated, and version-controlled. Conference triage that happens only in your head is forgotten by week three; conference triage that exists as `revision/triage-memo-2026-08-22.md` is durable. When a co-author six months later asks "did anyone push on the pre-trends?" you can grep your own memo for "parallel trends" and find the row, the verdict, and the appendix where the response lives. We will use this memo again in Chapter 10.5 when we tackle external validity, and in Week 11 when we write the response-to-referee letter for the journal submission.

---

## 5. Code: the triage CSV and the memo generator

You committed a feedback ledger in Chapter 9.5 as `feedback-ledger.csv`. The triage step adds three columns — cost, value, threat — and computes the verdict. The memo is rendered from the ledger by a small Python script. The point of the code is *not* to automate the judgment (the judgment is yours); it is to make the bookkeeping cheap enough that you actually do it.

```python
# triage.py — turn a feedback ledger into a Required/Welcome/Decline memo.
# Usage: python triage.py feedback-ledger.csv > revision/triage-memo-$(date +%F).md
import sys
import pandas as pd
from pathlib import Path

COST_LEVELS   = {"low": 1, "med": 2, "high": 3}
VALUE_LEVELS  = {"low": 1, "med": 2, "high": 3}
THREAT_LEVELS = {"none": 0, "bounded": 1, "central": 2}

def verdict(row) -> str:
    """Apply the cell-level rules from §2.4."""
    c = COST_LEVELS[row["cost"].strip().lower()]
    v = VALUE_LEVELS[row["value"].strip().lower()]
    t = THREAT_LEVELS[row["threat"].strip().lower()]
    # Rule 1: any central-threat comment is Required.
    if t == 2:
        return "Required"
    # Rule 2: high-value-and-low-cost is Required regardless of threat.
    if v == 3 and c == 1:
        return "Required"
    # Rule 3: high-cost-and-low-value is Decline.
    if c == 3 and v == 1:
        return "Decline"
    # Rule 4: no-threat-and-low-value is Decline.
    if t == 0 and v == 1:
        return "Decline"
    # Rule 5: everything else is Welcome.
    return "Welcome"

def render_memo(df: pd.DataFrame) -> str:
    """Render the three sections in Required, Welcome, Decline order."""
    sections = ["Required", "Welcome", "Decline"]
    lines = ["# Revision triage memo", ""]
    for s in sections:
        sub = df[df["verdict"] == s]
        lines.append(f"## {s} ({len(sub)})")
        for _, r in sub.iterrows():
            lines.append(f"- **#{r['id']}** ({r['speaker_role']}): {r['comment']}")
            lines.append(f"  - Action: {r['action']}")
        lines.append("")
    return "\n".join(lines)

def main(path: str) -> None:
    df = pd.read_csv(path)
    required_cols = {"id", "comment", "speaker_role", "cost", "value", "threat", "action"}
    missing = required_cols - set(df.columns)
    if missing:
        raise SystemExit(f"feedback-ledger.csv missing columns: {sorted(missing)}")
    df = df.copy()
    df["verdict"] = df.apply(verdict, axis=1)
    print(render_memo(df))

if __name__ == "__main__":
    main(sys.argv[1] if len(sys.argv) > 1 else "feedback-ledger.csv")
```

A few notes on this code. The function `verdict` encodes only five rules and falls through to "Welcome" by default; that is intentional, because Welcome is the right default for any comment that is neither lethal-if-ignored nor obvious-to-skip. The verdict is computed from the three discrete labels you assigned by hand — the script does no machine learning, no scoring beyond what you have already done — because the point is to make your judgment *visible and re-rankable*, not to replace it. If you change your mind about a comment's value (a common experience after week one of revision), you edit the CSV and re-render the memo; the version-control history of the memo will tell the story of how your understanding evolved.

The memo file lives at `revision/triage-memo-YYYY-MM-DD.md`. Every Monday of the revision month, you re-render it (a fresh date) and commit. By the time you submit the paper, you have four versions of the memo and a clear paper trail showing what you decided to address, what you decided to decline, and how those decisions changed across the four weeks. That paper trail is invaluable when a co-author asks "did we ever consider X?" — you can grep for X and find the row, the verdict, and the date the verdict was assigned.

---

## 6. When triage fails: three classic mistakes

Even with the grid and the memo, students fall into three predictable failure modes. We name them here so you can catch yourself.

**The "everything is required" mistake.** Beginners triage every comment as Required because they cannot bear to decline anything. The result is a four-week sprint that produces seventeen new robustness rows, a forty-page appendix, and no real progress on the central threat. The grid prevents this if you use it honestly: if every row is M-H-Central, you are not triaging, you are flinching. Force yourself to assign at least one Decline per ten comments; if you cannot find one, your value-axis calibration is too generous.

**The "decline what hurts" mistake.** The opposite failure: students decline the comments that would require the most work, regardless of severity. This is rationalized as time management ("I only have four weeks") but it is actually conflict avoidance. The grid catches this because *cost is not a triage axis on its own* — a high-cost, high-value, central-threat comment is Required, full stop, even if it consumes three weeks. If your declines cluster in the high-cost column, your triage is biased toward laziness.

**The "triage once, never revisit" mistake.** Triage on Monday of week one is provisional. By Wednesday of week two, you will have learned things — a robustness test ran cleaner than expected, or a heterogeneity result revealed a new threat, or a referee at a different conference asked a question that recasts an earlier comment. The memo must be a *living* document. Re-triage at the start of each week of the revision month. Each new version of the memo is dated, committed, and explicit about what changed. This is the same discipline you applied to the pre-analysis plan in Chapter 7.3, where amendments were dated and version-controlled; revision triage inherits that discipline directly.

---

## 7. Sam, Devon, Priya, Leah: triage looks different in different designs

A brief tour of how the same grid is used by your four classmates whose papers run on different identification strategies. The grid is the same; the *threats column* is different, and that changes which comments become Required.

**Sam (intraday momentum, near-real-time markets).** Sam's central threat is *survivorship in the high-frequency data feed* (Chapter 7.4): the tickers his pipeline retrieves at minute 31 of the trading day are not the same tickers it would have retrieved live. A comment from his discussant — "are you sure the high-momentum stocks at 10:00 a.m. are the same ones that *were* high-momentum at 10:00 a.m.?" — translates into a central-threat row on his grid, and the Required response is a point-in-time replication using the FINRA short-interest snapshot. A comment about font size on slide twelve translates to L-L-N and gets declined.

**Devon (DeFi adoption).** Devon's central threat is the *unobserved-confounder* threat in cross-chain analyses (because chains differ on many axes other than the regulatory event he is studying). A comment that asks him to add a synthetic-control analysis becomes M-H-Central — Required. A comment asking him to add a Twitter-sentiment control becomes L-L-Bounded (the threat is real but already addressed by chain-level fixed effects) — Welcome at best.

**Priya (climate-shock insurance).** Priya's central threat is *measurement error in the climate-event variable* (Chapter 2.5 on classical and non-classical measurement error). A comment asking her to use a different reanalysis product (ERA5 vs. MERRA-2) becomes M-H-Bounded — Required if the comment names the specific event-classification she might be miscoding. A comment asking her to "say more about climate change in general" becomes H-L-N — Decline.

**Leah (patent-language innovation).** Leah's central threat is *the construction validity of the text-derived novelty score* itself (Chapter 5.4). A comment that asks her to validate the score against a held-out hand-coded sample becomes M-H-Central — Required. A comment that asks her to use a different transformer model for embedding becomes H-M-Bounded — Welcome at best.

Notice the pattern: **the comments that *should* become Required are the ones that name your central threat in your language.** The comments that *feel* Required (because they were loud, or came from a senior person, or made you uncomfortable in the room) are often Welcome at best after honest translation. The grid is your protection against this confusion.

---

## 8. What you owe the room: the response paragraph and the public record

Triage is not only an internal exercise. When you submit the paper, the cover letter (Week 11, Chapter 11.3) names which conference and which discussant feedback you addressed; when the paper appears in print, the acknowledgements footnote thanks the people whose comments shaped the revision. **The triage memo is the *source* for both of those acknowledgements.** Every Required item becomes a sentence in the response letter ("Following the discussant's comment, we have added..."); every Welcome item becomes a sentence in the acknowledgements footnote ("We thank [name] for the suggestion to..."); every Decline becomes — and this is the hardest discipline — *also* a sentence somewhere, either in a response letter or in a private follow-up email, that says "We considered your suggestion to X; we chose Y for reason Z."

This last point is not optional. The senior colleague whose framing suggestion you declined will read the paper, notice that you did not adopt their framing, and reach one of two conclusions: either (a) you considered their suggestion and chose otherwise for principled reasons (good outcome — they respect you), or (b) you ignored them (bad outcome — they remember). A one-sentence email, sent within seventy-two hours of the conference, that says "I thought hard about your suggestion to reframe the intro around X; for the audience and contribution we are targeting, I think the current frame works better, but I wanted to acknowledge that I heard you and weighed it" — that email is the public face of the Decline row in the memo. It costs you ninety seconds. It saves you an enemy.

---

## 9. The seam from Week 9 to Week 10

This chapter is the bridge between two phases of your work. In Week 9 you presented a paper; in Week 10 you submit one. The feedback ledger from Chapter 9.5 was the *raw input* to triage; the memo you produce in this chapter is the *contract* that drives Chapters 10.2 through 10.5 and all of Weeks 11 and 12. Every chapter that follows is the operationalization of one row or one cluster of rows from this memo.

- Chapter 10.2 is the rescue for the *multiple-testing* threat that lurks in many "have you tried X?" comments — when those comments get triaged into Welcome because they are individually low-cost, they cluster into a real inferential threat collectively, and 10.2 is how you defuse it.
- Chapter 10.3 is the operationalization of every heterogeneity comment, with the pre-registration discipline that keeps a Required heterogeneity row from drifting into a fishing expedition.
- Chapter 10.4 is the operationalization of every mediation comment ("what is the channel?") — and crucially, the warning against the bad-controls form of mediation that some commenters will request and that you should sometimes decline.
- Chapter 10.5 is the operationalization of every external-validity comment ("does this generalize to 2030, to other markets, to other populations?"), and connects back to the threats table from Chapter 7.5.

The rest of Week 10 is the menu of tools you will deploy against the Required items. Use the grid to choose which tools you actually need; use the memo to commit to those choices in writing; use the code in this chapter to keep your bookkeeping honest.

---

## 10. Worked checklist before you leave this chapter

Before you start Chapter 10.2, you should have on disk:

1. A `revision/triage-memo-YYYY-MM-DD.md` file with three sections, every comment from the conference ledger assigned to exactly one section, every Required item with a concrete deliverable, every Decline with a reason.
2. A `revision/feedback-ledger.csv` with the three new columns (cost, value, threat) filled in for every row.
3. A re-rendered `revision/triage-memo-YYYY-MM-DD.md` committed to git with a commit message like `triage: 47 conference comments, 3 required, 5 welcome, 39 decline`.
4. A one-paragraph email sent to every Decline-row commenter (or at least every Decline-row senior commenter), within 72 hours of the conference, acknowledging their suggestion and explaining your choice. You do not have to *agree*; you have to be *heard to consider*.
5. A calendar with the three Required items mapped to weeks 1–3 of the revision month, with a buffer week (week 4) for integration, proof, and the response letter.

You now have a plan. The next four chapters are the tools.

---

[^rr2023]: Rambachan, A. and Roth, J. (2023). "A More Credible Approach to Parallel Trends." *Review of Economic Studies* 90(5):2555–2591.

---

**Chapter cross-references.** Built on Ch 7.5 (the identification memo whose threats table is the vocabulary you translate comments into); Ch 8.1 (the specification curve whose forks discipline the "did you try X" comments); Ch 8.2 (the robustness battery your Required items live in); Ch 9.5 (the feedback ledger that is this chapter's raw input). Feeds Ch 10.2 (multiple testing for the post-hoc-X comments), Ch 10.3 (heterogeneity for the subgroup comments), Ch 10.4 (mechanism for the channel comments), Ch 10.5 (external validity for the generalization comments), and Ch 11.3 (the response letter that turns this memo into a public deliverable).
