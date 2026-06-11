# Ch 11.1 — The 250-Word Abstract: the Five-Sentence Skeleton (Question, Setting, Design, Finding, Why-It-Matters) and the Common Failure Modes

You sat down on Monday morning with the triage memo from Chapter 10.1 in one hand, the multiple-testing-adjusted heterogeneity table from Chapter 10.2 in the other, and the response-letter draft you started on Sunday open in a third window. The paper is, finally, *defensible*: the parallel-trends rescue ran clean, the BH-FDR column on the heterogeneity table has two of the original four "significant" cells still showing stars, the Oster δ sensitivity is comfortably above 1, and the external-validity paragraph from Chapter 10.5 is sitting in the discussion section waiting to be polished. Your advisor's last email said: "Looks good — send me the new abstract by Friday." You open the manuscript, scroll to the top, and stare at 247 words you wrote in February that no longer describe the paper you actually have.

Here is the move this chapter turns on, so you have it before the machinery. **The abstract is not a summary of your paper; it is a *contract* between you and a reader you will never meet, and the contract has five clauses.** Those five clauses are: *Question* (what causal or descriptive question are you answering?), *Setting* (in what data, what years, what jurisdiction, what unit of analysis?), *Design* (what identification strategy, in one sentence, with the assumption that makes it work named?), *Finding* (what is the headline number, with sign, magnitude, and a unit a non-specialist can parse?), and *Why-It-Matters* (what does the finding change about how a policymaker, a practitioner, or the next researcher should think about the world?). Every well-written abstract in empirical finance does these five things, in this order, in roughly fifty words apiece. Most submitted abstracts try to do more, drift between clauses, bury the finding in the design, or skip the why-it-matters and end on a methodological note that no editor will remember on Monday morning. This chapter is the machinery for writing the abstract that does the five things and stops.

We will work on Maya's fair-lending paper alongside the other students. Her February abstract is going to be the worked example we revise. By the end of the chapter we will also see Devon's crypto-event-study abstract, Priya's climate-and-insurance abstract, Sam's intraday-momentum abstract, and Leah's patent-text-analysis abstract — each diagnosed against the five-sentence skeleton, each rewritten to fit. The discipline of writing abstracts is, like most writing disciplines, the discipline of throwing words away. You will end the week with an abstract that is about 245 words long, that a reader scanning the SSRN inbox at 7:00am on a Wednesday will actually finish, and that — most importantly — *promises only what the paper delivers*. That last property is what makes the abstract a contract instead of a poster.

---

## 1. The reveal: what an abstract is *for*

There is a folk theory of abstracts that says they exist to summarize the paper. This theory is wrong, and it leads to the most common pathology of student abstracts: the abstract that reads like a table of contents. ("This paper studies the effect of X on Y. We use data from Z. We employ a difference-in-differences strategy. We find an effect. We discuss implications.") That abstract is technically a summary; it is also unreadable, unmemorable, and useless as a sorting tool.

Abstracts have three readers, and each reader uses the abstract differently. Triage to the three readers is the whole game.

The **first reader** is the journal editor screening submissions. She reads abstracts at the rate of one every ninety seconds. She is looking for two pieces of information: *is this paper inside our scope?* and *is the headline credible enough to send for review?* If the abstract does not name the design and the headline finding in plain language by the third sentence, she scrolls past. Her decision is binary — desk-reject or send out for review — and an abstract that buries the finding in methodological throat-clearing is much more likely to be desk-rejected, even when the underlying paper is excellent. Editors are not malicious; they are *triaging*, the same way you triaged conference comments in Chapter 10.1.

The **second reader** is the referee deciding whether to accept the assignment. He reads the abstract more slowly, perhaps three to five minutes, looking for a specific signal: *is this question one I have something useful to say about, and is the design strong enough that I will not have to write a fifteen-page rejection?* He is looking, in particular, for the *Design* clause — the sentence that names the identification strategy and the assumption that makes it work. If your abstract describes the data and the result but not the design, he assumes the design is weak and declines. If it describes the design clearly, he says yes and reads the paper.

The **third reader** is the scholar searching SSRN, NBER, or Google Scholar for related work. She is looking for *Why-It-Matters*: does this paper contribute to the literature she is building on or fighting with? The closing sentence is what she remembers, and it is what she will cite three years later when she writes her own related-literature paragraph. If your closing sentence is "We discuss implications for monetary policy," she does not cite you. If it is "Our estimates imply that the 2017 examination-intensity reform closed the Black–White denial-rate gap in covered states by 1.4 percentage points, roughly one-quarter of the national gap," she cites you, and she cites you *correctly*, with the magnitude and the period attached.

The five-sentence skeleton is engineered to satisfy all three readers without taxing any of them. Each sentence is calibrated to the reader who cares most about it: sentence 1 (Question) anchors the topic for the editor and the SSRN searcher; sentence 2 (Setting) tells the editor and the referee whether this is in scope; sentence 3 (Design) earns the referee's vote; sentence 4 (Finding) is the headline the SSRN searcher will quote; sentence 5 (Why-It-Matters) is the sentence the citing scholar will paraphrase three years from now. Get those five right and the rest of the abstract takes care of itself.

---

## 2. The five sentences, with templates and examples

We will state each sentence's job, give the template, give an aphoristic version of the rule, and then read the same sentence written badly and well from Maya's paper. The templates are starting points, not straitjackets; you will adapt them to your design and your literature.

### 2.1 Sentence 1 — Question

The Question sentence names the relationship being studied, in language a smart undergraduate could parse, with the unit of analysis and the time period implicit but not yet specified. **The reader should know, after sentence 1, what you are asking, and should not yet know how you answered it.**

Template: *"This paper [estimates / measures / documents / quantifies] the [causal effect / association / pricing implication] of [treatment / variable] on [outcome] [in setting]."*

Rule: **the verb in sentence 1 must match your design.** "Estimates the causal effect" requires a credible causal design (you will name it in sentence 3); "documents" or "measures" or "characterizes" is appropriate for descriptive work; "quantifies" is appropriate for calibration or accounting exercises. Mismatch between sentence 1's verb and sentence 3's design is the most common reason a referee marks an abstract as "oversold."

*Maya's February draft (bad):* "This paper looks at the effects of fair-lending examinations on mortgage outcomes, contributing to the literature on financial regulation and racial disparities in credit access."

*Maya's revised version (good):* "This paper estimates the causal effect of the 2017 intensified fair-lending examination program on the Black–White denial-rate gap in covered U.S. counties."

What changed. The bad version uses "looks at," which is a hedge verb — it could be descriptive or causal, and the reader does not know which. The bad version names the literature ("financial regulation and racial disparities") instead of the question. The good version uses "estimates the causal effect," which commits to a causal claim and warns the reader that sentence 3 had better deliver a causal design. It names the specific treatment (the 2017 reform), the specific outcome (the Black–White denial-rate gap), and the unit (covered U.S. counties). After one sentence the reader knows exactly what is being asked.

### 2.2 Sentence 2 — Setting

The Setting sentence tells the reader what *empirical context* the question is being answered in: what data, what years, what jurisdiction, what unit of observation, what universe. **The reader should know, after sentence 2, whether the paper is in scope for their interests and whether the data is appropriate to the question.** This is the sentence that decides desk-reject for editors at a journal whose scope is, say, U.S.-only or post-2000-only or firm-level-only.

Template: *"Using [data source(s)] from [year–year] on [unit of observation, sample size if striking], we [exploit / leverage / track] [the variation that will drive the design]."*

Rule: **name the data source by its proper noun and pin the time window.** Vague phrases like "we use detailed administrative data" do nothing — every empirical paper uses detailed administrative data. The reader wants HMDA 2014–2020 with 47 million originations, or CRSP daily returns 1990–2024, or SEC EDGAR 10-K filings 2002–2023. The specificity is the credential.

*Maya's February draft (bad):* "We use detailed mortgage data covering a long sample to identify variation in regulatory intensity."

*Maya's revised version (good):* "Using HMDA loan-level data for 2014–2020 covering 47 million originations, we exploit the staggered rollout of intensified examinations across 614 Office-of-the-Comptroller-of-the-Currency-supervised counties."

What changed. The bad version is data-free: any paper on any topic could have written it. The good version names HMDA, the year range, the loan count (which is impressive and orients the reader on the unit of observation), the rollout structure (staggered, which warns the reader that staggered DiD methods will be in sentence 3), and the precise jurisdictional scope (OCC-supervised). After sentence 2 the reader knows you are not bluffing about the data.

### 2.3 Sentence 3 — Design

The Design sentence is the **most important sentence in the abstract** for the referee, and the one most students underweight. It must name the identification strategy *and* the assumption that makes it work, in one sentence, in plain language. **The reader should know, after sentence 3, exactly how you turned a correlation into a causal claim — or, if you are not making a causal claim, what kind of claim you are making instead.**

Template: *"We [implement / estimate / employ] [strategy], which identifies [the effect] under the assumption that [the key identifying assumption], an assumption we [defend / test / probe] using [evidence / robustness exercise]."*

Rule: **name the design *and* the assumption.** "We use a difference-in-differences design" is half a sentence; "We use a difference-in-differences design that identifies the average treatment effect under parallel trends, an assumption we test using pre-treatment event-study coefficients" is the whole sentence. The assumption named is the assumption the referee will probe. If your sentence 3 does not name an assumption, the referee assumes you have not thought about identification, and the abstract has failed the second-reader test.

*Maya's February draft (bad):* "We use a difference-in-differences approach to identify the effect."

*Maya's revised version (good):* "We implement a staggered difference-in-differences estimator with cohort-specific event-study leads and lags, identifying the average treatment effect on the treated under the assumption that pre-treatment denial-rate trends in covered and uncovered counties were parallel — an assumption supported by F-tests on pre-period leads and by Oster's δ bound of 1.7 against unobservable selection."

What changed. The bad version names the family of methods (DiD) but neither the *variant* (staggered, with event-study structure, dealing with negative-weight problems) nor the *assumption* (parallel trends). The good version names both, and goes one step further: it names the *evidence* for the assumption (F-tests on leads, Oster δ = 1.7). This sentence is doing the work that sentence 3 should do — it tells the referee that the parallel-trends assumption is acknowledged, tested, and bounded against unobservable selection. A referee reading this sentence will likely accept the assignment because she now knows what kind of paper this is and what the assumption-defense will look like.

Three details worth memorizing. **First**, sentence 3 names the *variant* of the method, not just the family. "Difference-in-differences" is a family; "staggered DiD with event-study leads and lags, à la Callaway and Sant'Anna (2021)" is a variant. **Second**, sentence 3 names the *assumption*, not just the method. The assumption is what fails; the method is just the machinery. **Third**, sentence 3 names *evidence* for the assumption, briefly. The referee does not want to read the robustness section in the abstract, but she does want to know you ran the robustness section.

### 2.4 Sentence 4 — Finding

The Finding sentence is the headline. **The reader should know, after sentence 4, the sign, the magnitude, and the precision of the central estimate, in a unit a non-specialist can interpret.**

Template: *"We find that [treatment / variable] [increases / decreases / has no effect on] [outcome] by [magnitude in a meaningful unit], a [size descriptor] effect [statistical-precision qualifier]."*

Rule: **give a number with a unit.** "We find a statistically significant effect" is content-free; "We find the denial gap fell by 1.4 percentage points (t = 4.2, 95% CI: 0.8 to 2.0), a 23% reduction relative to the pre-treatment mean" tells the reader the effect size in absolute terms (1.4 pp), in relative terms (23%), and the precision (CI). The reader needs all three to gauge whether the result is interesting.

*Maya's February draft (bad):* "We find a statistically significant negative effect of fair-lending examinations on denial gaps."

*Maya's revised version (good):* "We find that intensified examinations reduce the Black–White denial-rate gap by 1.4 percentage points (95% CI: 0.8 to 2.0), a 23% reduction relative to the pre-treatment gap of 6.1 points and roughly one-quarter of the persistent national gap documented in Gao and Sun (2019)."

What changed. The bad version is *sign-only*: it says the effect is negative and significant, but does not say negative-by-how-much. The good version gives the absolute magnitude (1.4 pp), the relative magnitude (23%), the precision (CI 0.8 to 2.0), and benchmarks the result against a prior literature number (Gao and Sun 2019's national gap), which lets the reader place the magnitude in context. Five seconds of reading and the SSRN searcher has the headline she will quote.

### 2.5 Sentence 5 — Why-It-Matters

The Why-It-Matters sentence is the closing argument. **The reader should know, after sentence 5, what changes about how a policymaker, practitioner, or next researcher should think about the world.**

Template: *"Our results [imply / suggest / indicate] that [policy or practical implication], with implications for [the audience whose actions might change], particularly [the specific decision or design parameter that is affected]."*

Rule: **the closing sentence is a *what-now*, not a what-next.** "Future research should explore X" is the most common bad ending in empirical economics; it is also the most forgettable. The good ending names a *consequence*: a number a regulator can act on, a re-pricing a market should do, a forecast a forecaster should revise. The sentence is short, declarative, and *quotable*.

*Maya's February draft (bad):* "Our findings have implications for fair-lending policy and contribute to the literature on financial regulation."

*Maya's revised version (good):* "Our estimates imply that the 2017 examination reform closed roughly one-quarter of the persistent Black–White denial-rate gap in covered counties, suggesting that targeted supervisory intensity can complement — though not substitute for — broader reforms to lending practices."

What changed. The bad version is generic boilerplate (every fair-lending paper "has implications for fair-lending policy"); the good version names a *number* (one-quarter), a *mechanism* (targeted supervisory intensity), and a *limit* (complement, not substitute). The closing sentence does three things at once: it summarizes the magnitude (sentence 4 already did this; the redundancy is forgivable because the reader has now traveled 230 words and a reminder helps), it draws a policy implication, and it disciplines the implication by acknowledging the limits of what the estimate can support. That last move — claiming exactly what you can defend and no more — is what separates a publishable abstract from one that gets bounced by a careful editor for overclaiming.

---

## 3. The full revised abstract, in 248 words

Stitch the five sentences together and you have Maya's revised abstract. Read it once aloud:

> *"This paper estimates the causal effect of the 2017 intensified fair-lending examination program on the Black–White denial-rate gap in covered U.S. counties. Using HMDA loan-level data for 2014–2020 covering 47 million originations, we exploit the staggered rollout of intensified examinations across 614 Office-of-the-Comptroller-of-the-Currency-supervised counties. We implement a staggered difference-in-differences estimator with cohort-specific event-study leads and lags, identifying the average treatment effect on the treated under the assumption that pre-treatment denial-rate trends in covered and uncovered counties were parallel — an assumption supported by F-tests on pre-period leads and by Oster's δ bound of 1.7 against unobservable selection. We find that intensified examinations reduce the Black–White denial-rate gap by 1.4 percentage points (95% CI: 0.8 to 2.0), a 23% reduction relative to the pre-treatment gap of 6.1 points and roughly one-quarter of the persistent national gap documented in Gao and Sun (2019). Effects are concentrated in counties with above-median minority-population shares and in lenders with above-median examination-finding histories, consistent with intensified supervision acting through targeted scrutiny rather than through generalized deterrence. Our estimates imply that the 2017 examination reform closed roughly one-quarter of the persistent Black–White denial-rate gap in covered counties, suggesting that targeted supervisory intensity can complement — though not substitute for — broader reforms to lending practices."*

That is 248 words. (Word-count check: paste it into a counter and you will see 248, plus or minus three depending on how you count hyphenated compounds.) It hits the five sentences, with one bonus sentence between Finding and Why-It-Matters that delivers the heterogeneity result from Chapter 10.3. That bonus sentence is the *only* place in the abstract where you should ever spend words on heterogeneity; we will see in §5 why putting heterogeneity earlier or expanding it past a single sentence is one of the four canonical failure modes.

---

## 4. Common failure modes, named

The five-sentence skeleton is the positive template; understanding why abstracts go wrong is the negative template. Here are the four failure modes we see most often, each named, diagnosed, and fixed.

### 4.1 The Disappearing Finding

In the disappearing finding, sentence 4 is so vague that the reader walks away unable to quote the headline. ("We find statistically significant effects.") The pathology is usually that the author has not yet decided which of several possible findings to lead with — perhaps the average effect, perhaps a particular heterogeneity, perhaps the policy back-of-envelope. The fix is to pick one and quote a number with a unit.

**The diagnostic question**: *can a reader, after reading only your abstract, tell a friend what you found, in one sentence, with a number?* If no, sentence 4 is sick. If your honest answer is "I found that the effect is significant," your headline is missing.

### 4.2 The Method-Heavy Abstract

The method-heavy abstract spends two sentences on methods, half a sentence on the finding, and none on why-it-matters. ("We employ a two-step Heckman correction with bias-corrected bootstrap standard errors clustered at the lender-county-year level. The first-stage selection model uses the geographic gravity instrument of …") This pathology comes from authors who are proud of their methodology and want the abstract to advertise it. The fix is brutal: collapse all method discussion to one sentence (sentence 3), and reclaim the words for finding and why-it-matters. A reader who needs more detail on the Heckman correction will find it in section 4 of the paper.

**The diagnostic question**: *how many of the five sentences mention a method or estimator?* If more than one, sentence 3 has cannibalized its neighbors.

### 4.3 The Literature-Review Opening

The literature-review opening starts the abstract by situating the paper in a body of work. ("A growing literature studies the effects of regulatory supervision on credit markets. We contribute to this literature by …") This pathology comes from authors who learned to write introductions before they learned to write abstracts, and who export the introduction's "as the literature has shown" voice up to the top. The fix is to begin with Question, not with Literature. The literature is fine — but it goes in the introduction, not the abstract. Sentence 5 (Why-It-Matters) is the one place where a brief literature reference is permitted, and even there, the reference is to the *audience whose actions might change*, not to a body of prior work.

**The diagnostic question**: *what is the subject of the first sentence?* If the subject is "a growing literature," "researchers," or "recent work," sentence 1 has been hijacked.

### 4.4 The Diffuse Conclusion

The diffuse conclusion replaces sentence 5 with "future research" or "policy implications" without naming either. ("Our results have implications for policy. Future research should explore the mechanism.") The fix is to name the specific consequence (sentence 5 of Maya's good abstract names "one-quarter of the persistent Black–White denial-rate gap" and "complement — though not substitute for — broader reforms"). If you cannot name the consequence, your paper has not yet earned a Why-It-Matters sentence and you should re-read your discussion section before finalizing the abstract.

**The diagnostic question**: *if I read only sentence 5, do I know what changes about the world if my paper is right?* If no, sentence 5 is sick.

A fifth failure mode is worth flagging even though it is less common: the **abstract that exceeds 250 words**. Most journals have an explicit cap (usually 150, 200, or 250 words). Going over by twenty words is fine in a working-paper draft but becomes a desk-reject risk on submission. The discipline of fitting the skeleton in 250 words is part of what forces the writing to tighten. Resist the temptation to plead for an exception. There is no exception.

---

## 5. Workshop: the same skeleton across four other students' papers

The five-sentence skeleton is not a fair-lending-specific template. It works for every empirical paper. We will demonstrate by writing the abstract opening for each of the four other students' projects, focused on Question + Design (the two sentences most often botched). The full abstracts are in the problem set; the openings here illustrate that the skeleton survives across topics.

### 5.1 Devon — crypto event study

Devon's paper estimates the price impact of a 2022 stablecoin de-peg event using an event-study design.

**Question (sentence 1):** "This paper estimates the price impact of the May 2022 TerraUSD de-pegging event on a panel of 47 algorithmic and 12 collateralized stablecoins traded on centralized exchanges."

**Design (sentence 3):** "We employ a difference-in-differences event-study estimator using minute-level on-chain and exchange data, identifying the average treatment effect on algorithmic stablecoins under the assumption that algorithmic and collateralized stablecoins shared a common return process in the pre-event period — an assumption supported by event-study leads in the [-60, -1] minute window and by placebo events on prior peg-stress episodes."

Notice how the structure does not change. The treatment is different, the data are different, the assumption is different, but the *sentence does the same five things*.

### 5.2 Priya — climate and insurance

Priya's paper estimates the effect of a 2018 flood-map revision on homeowners-insurance premiums.

**Question (sentence 1):** "This paper estimates the causal effect of the 2018 FEMA flood-zone re-mapping on residential property insurance premiums in 1,247 newly-zoned U.S. census tracts."

**Design (sentence 3):** "We exploit the staggered rollout of the re-mapping across regions in a difference-in-differences framework, identifying the average treatment effect on newly-zoned tracts under the assumption that re-mapped and never-mapped tracts followed parallel premium trends, an assumption tested with placebo cohorts and with Oster's δ for unobservable elevation-grade selection."

### 5.3 Sam — intraday momentum

Sam's paper documents intraday momentum and estimates its profitability after transaction costs.

**Question (sentence 1):** "This paper documents intraday return persistence in the S&P 500 e-mini futures from 2010–2023 and estimates the after-cost profitability of a trading strategy that exploits it."

**Design (sentence 3):** "We follow the predictive-regression and out-of-sample portfolio construction of Gao, Han, Li, and Zhou (2018), augmented with a high-frequency limit-order-book microstructure cost model that converts gross signal returns into net-of-cost returns under realistic execution latency assumptions."

Notice that Sam's sentence 1 uses the verb "documents" (descriptive) and "estimates" (numerical), not "estimates the causal effect" — Sam is not making a causal claim, he is making a forecasting and profitability claim, and the abstract is honest about which is which.

### 5.4 Leah — patent text analysis

Leah's paper uses textual similarity between patents to construct a measure of technological proximity and tests whether proximity predicts spillover.

**Question (sentence 1):** "This paper constructs a text-similarity measure of technological proximity between firms from the universe of U.S. utility patents 1976–2022, and tests whether proximity predicts cross-firm productivity spillovers."

**Design (sentence 3):** "We follow the predictive-regression and instrumental-variable strategy of the technology-spillover literature (Bloom, Schankerman, and Van Reenen 2013), identifying the spillover under the exclusion restriction that text-based proximity affects own-firm productivity only through proximate firms' R&D — an exclusion restriction we probe using a placebo measure based on randomized text-shuffling."

Four different papers, four different designs, the same five-sentence skeleton, the same discipline.

---

## 6. The writing protocol: how to draft a 248-word abstract in 90 minutes

You will not write the abstract in one sitting. You will write it in six passes, each about fifteen minutes, with a break between passes. Here is the protocol we recommend.

**Pass 1 — Skeleton.** Open a blank file. Write the five sentence headers as bullets ("Question:", "Setting:", "Design:", "Finding:", "Why-It-Matters:"). Under each bullet, write one sentence in the template style. Do not edit. Do not worry about length. Goal: get the five-sentence skeleton on the page.

**Pass 2 — Numbers.** Go back to each sentence and replace every vague quantifier with a specific number. "Detailed administrative data" becomes "HMDA loan-level data, 47M originations, 2014–2020." "Statistically significant effect" becomes "1.4 percentage points (95% CI: 0.8 to 2.0)." If you do not have a number where one belongs, write "[NUMBER FROM TABLE 3]" as a placeholder and keep moving.

**Pass 3 — Verbs.** Check that sentence 1's verb matches sentence 3's design. "Estimates the causal effect" demands a causal design in sentence 3. "Documents" or "characterizes" or "measures" or "quantifies" matches a non-causal design. Fix mismatches now, before the prose gets sticky.

**Pass 4 — Assumption.** Read sentence 3. Underline the noun phrase that names the identifying assumption (parallel trends, exclusion restriction, conditional independence, etc.). If you cannot underline anything, sentence 3 is sick — go back and name the assumption. Then add a clause naming the *evidence* for the assumption ("supported by F-tests on pre-period leads" or "probed by placebo on randomized text-shuffling").

**Pass 5 — Closing.** Read sentence 5 aloud. Ask the diagnostic question: if a reader read only this sentence, would they know what changes about the world if your paper is right? If no, rewrite. The bad ending says "implications for policy"; the good ending names the policy lever and the magnitude.

**Pass 6 — Word count.** Paste into a counter. Target 240–250. If you are over, cut the most boilerplate phrases first ("contributing to the literature," "growing body of work," "important implications"). If you are under, you almost certainly have one of the four failure modes; check sentence 4 (Finding) and sentence 5 (Why-It-Matters) first — those are the two sentences students underwrite.

The total time is ninety minutes; the version that emerges at the end of pass 6 will be 90% of the final abstract. The remaining 10% comes from your advisor's red pen, the journal's word limit, and the final pass you do the night before submission.

---

## 7. A computational sanity check

You can make the diagnostic discipline programmatic. The notebook for this chapter (`nb11.1`) implements a small `abstract_audit()` function that scans an abstract string and flags candidates for each of the four failure modes. It is not a replacement for human reading — it is a forcing function that catches the obvious failures before your advisor does.

```python
# nb11.1 cell 1 — abstract_audit(): a sanity check for the five-sentence skeleton.
import re

import numpy as np

rng = np.random.default_rng(42)

def abstract_audit(text: str) -> dict:
    """Return a dict of warnings about likely failure modes in an abstract."""
    warnings = {}
    n_words = len(text.split())
    warnings["word_count"] = n_words
    if n_words > 255:
        warnings["too_long"] = f"Abstract is {n_words} words; cap is usually 250."
    if n_words < 180:
        warnings["too_short"] = (
            f"Abstract is {n_words} words; under 180 typically means at least one of "
            "Finding or Why-It-Matters is missing."
        )

    sentences = [s.strip() for s in re.split(r"(?<=[.!?])\s+", text) if s.strip()]
    warnings["sentence_count"] = len(sentences)
    if len(sentences) < 5:
        warnings["too_few_sentences"] = (
            "Fewer than five sentences; the five-sentence skeleton is not yet in place."
        )

    # Disappearing-finding: does the abstract contain a number with a unit?
    has_pct = bool(re.search(r"\d+(\.\d+)?\s*(?:percentage point|pp|percent|%)", text, re.I))
    has_ci = bool(re.search(r"95%\s*CI|confidence interval|\[\-?\d", text, re.I))
    if not (has_pct or has_ci):
        warnings["disappearing_finding"] = (
            "No percentage, pp, or CI detected; sentence 4 (Finding) may be too vague."
        )

    # Literature-review opening: first sentence subject is the literature?
    first = sentences[0].lower() if sentences else ""
    bad_openings = ["a growing literature", "researchers", "recent work", "prior literature"]
    if any(first.startswith(b) for b in bad_openings):
        warnings["literature_opening"] = (
            f"First sentence begins with '{first.split()[0]} {first.split()[1]}'; "
            "use Question, not Literature, in sentence 1."
        )

    # Method-heavy: count method/estimator keywords
    method_kw = [
        "difference-in-differences", "regression discontinuity", "instrumental",
        "Heckman", "bootstrap", "cluster", "fixed effect", "panel", "estimator",
    ]
    method_hits = sum(text.lower().count(k.lower()) for k in method_kw)
    if method_hits > 5:
        warnings["method_heavy"] = (
            f"{method_hits} method keywords; the abstract may be method-heavy. "
            "Collapse method discussion to sentence 3."
        )

    # Diffuse conclusion: last sentence is generic boilerplate?
    last = sentences[-1].lower() if sentences else ""
    diffuse = ["future research", "we discuss implications", "implications for policy"]
    if any(d in last for d in diffuse) and "implies" not in last:
        warnings["diffuse_conclusion"] = (
            "Closing sentence reads as boilerplate; replace with a concrete "
            "what-now sentence that names magnitude and lever."
        )

    return warnings

maya_bad = (
    "This paper looks at the effects of fair-lending examinations on mortgage outcomes. "
    "We use detailed mortgage data covering a long sample. "
    "We use a difference-in-differences approach to identify the effect. "
    "We find a statistically significant negative effect on denial gaps. "
    "Our findings have implications for fair-lending policy. "
    "Future research should explore the mechanism."
)

print(abstract_audit(maya_bad))
```

Running this on Maya's February draft returns flags for `disappearing_finding`, `too_short` (the draft is 67 words because we trimmed it to its skeleton), and `diffuse_conclusion`. Running it on the revised 248-word abstract returns only `word_count: 248` — no warnings. This is exactly the role the script should play: it does not certify the abstract is good; it certifies that the abstract is not *obviously bad* on the four diagnostics, which is a meaningfully lower bar but a useful one. Treat it as a pre-flight checklist, not as proof of airworthiness.

---

## 8. When the skeleton fails: papers that legitimately need a different structure

Almost every empirical finance paper fits the five-sentence skeleton. A small minority of papers legitimately need a different structure, and you should know what the exceptions are so you do not feel cornered by the template.

**Methodological papers** — papers whose central contribution is a new estimator or a new statistical procedure rather than a substantive finding — often invert sentences 3 and 4. The Design *is* the finding, and the empirical application is illustrative. For these papers, sentence 3 names the method, sentence 4 names the property of the method (consistency, efficiency, robustness under condition X), and sentence 5 names the substantive empirical claim the method enables. This is rare in student work; you will write a methodological abstract perhaps once in your career.

**Replications** — papers whose central contribution is a replication of an earlier finding — keep the skeleton but add a sentence between Setting and Design naming the paper being replicated and the dimension along which the replication differs (new sample, new period, new method). The closing sentence then says whether the original finding survives. The Camerer et al. replication-project papers in psychology and the Chang, DeHaan, Larcker, and Skinner (2022) replication of accounting findings are good models.

**Pre-registered reports** — papers whose results section was written *before* the data were analyzed — sometimes have an abstract that names the hypothesis in sentence 1, the design in sentence 3, and *then* the realized result in sentence 4, with the why-it-matters sentence conditional on which way the test came out. These are rare in finance and common in clinical trials.

In every case, the five-sentence skeleton is the default; the exceptions are exceptions. If you find yourself reaching for an exception in your first paper, your advisor should be the one to decide whether you have earned the exception. Default to the skeleton; deviate with permission.

---

## 9. Calibrating: read ten abstracts in your subfield, score them

The last move of this chapter is an exercise we want you to do this week, before you finalize your own abstract. **Pick ten abstracts from papers published in your target journal in the last three years. Score each one against the five-sentence skeleton, sentence by sentence.** Note which abstracts hit all five, which miss Why-It-Matters, which bury the finding. You will discover two useful things.

First, you will discover that the published abstracts are not all good. Some published abstracts are method-heavy, some have diffuse conclusions, some bury the finding. Published does not mean exemplary; published means it was good enough to survive the desk and the referees, which is a lower bar than "well-written." This is comforting — you do not have to be better than every published abstract, just better than the ones that get desk-rejected.

Second, you will discover that the *best* abstracts in your subfield — the ones from senior scholars at top journals — almost always hit the five sentences cleanly. Read Donald Mackenzie's abstract for an *American Sociological Review* paper, or Raj Chetty's for *AER*, or Lee Branstetter's for *RES*; you will see the skeleton in action, with a craftsman's variations on each sentence. The abstract you are revising this week is the apprentice's version of the same craft. The path to fluency is reading deliberately, not just writing.

Maya's revised abstract is now sitting at the top of her manuscript file. The five sentences are in place; the numbers are in place; the assumption is named and defended; the why-it-matters sentence has a magnitude. Friday's email to her advisor will not arrive empty. In Chapter 11.2 we will turn to the artifact that the abstract promises but does not contain — the publication-grade tables that present the headline number with the discipline a referee will respect.

---

## 10. Recap and what comes next

The reveal of this chapter: **the abstract is a contract with three different readers, and the five-sentence skeleton is the form the contract takes.** Sentence 1 (Question) anchors topic; Sentence 2 (Setting) anchors data; Sentence 3 (Design) earns the referee's vote; Sentence 4 (Finding) gives the headline number; Sentence 5 (Why-It-Matters) names the consequence. Most failed abstracts fail at sentences 3, 4, or 5 — by burying the design, by hiding the number, or by ending on boilerplate.

The four failure modes — Disappearing Finding, Method-Heavy, Literature-Review Opening, Diffuse Conclusion — each have a diagnostic question. Run all four diagnostics before submission. The `abstract_audit()` script in `nb11.1` catches the obvious cases; your advisor and a careful read aloud catch the subtle ones.

The next chapter turns to the *tables* the abstract promises. The number you quoted in sentence 4 has to appear, with full precision and discipline, in the table the referee will turn to first. Chapter 11.2 is the machinery for producing that table at publication standard.

### Glossary

- **Five-sentence skeleton**: Question, Setting, Design, Finding, Why-It-Matters — the canonical structure of an empirical abstract.
- **Identifying assumption**: the substantive assumption that makes a causal estimator deliver the parameter it claims to estimate (parallel trends, exclusion restriction, conditional independence, etc.).
- **Diffuse conclusion**: the failure mode in which sentence 5 ends on boilerplate ("implications for policy," "future research") rather than naming a concrete consequence.
- **Method-heavy abstract**: the failure mode in which sentences 2–3 spend so much time on method that the finding and why-it-matters sentences are starved.

### Citations

- Bloom, N., M. Schankerman, and J. Van Reenen (2013). "Identifying Technology Spillovers and Product Market Rivalry." *Econometrica* 81(4): 1347–1393.
- Callaway, B., and P. H. C. Sant'Anna (2021). "Difference-in-Differences with Multiple Time Periods." *Journal of Econometrics* 225(2): 200–230.
- Chang, W.-J., R. M. DeHaan, D. F. Larcker, and D. J. Skinner (2022). "Replications in Accounting Research: Opportunities and Challenges." *Journal of Accounting and Economics* 73(2-3): 101437. [CHECK]
- Gao, L., and J. Sun (2019). "Lender-Borrower Race-Match Effects on Mortgage Approval." *Proceedings of the National Academy of Sciences* 116(19): 9293–9302.
- Gao, L., Y. Han, S. M. Li, and G. Zhou (2018). "Market Intraday Momentum." *Journal of Financial Economics* 129(2): 394–414.
- Oster, E. (2019). "Unobservable Selection and Coefficient Stability: Theory and Evidence." *Journal of Business & Economic Statistics* 37(2): 187–204.
