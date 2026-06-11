# Ch 11.4 — The Introduction Rewrite: the Five-Paragraph Structure (Hook / Question / What-We-Do / Findings / Contribution) and How to Diagnose a Sick Intro

You finished the abstract on Friday. The five-sentence skeleton from Chapter 11.1 is in place, the headline number agrees with the publication-grade Table 2 from Chapter 11.2, the event-study plot from Chapter 11.3 sits below the table. Monday morning your advisor's email reads: "Abstract is good — now the intro needs the same treatment." You scroll to page two of your manuscript and find the introduction you drafted in February: eleven paragraphs, two of which are literature review, three of which retread the abstract, and one of which is a stream-of-consciousness about the broader societal implications of fair lending that you wrote at 2am. It is 4,200 words. It is, by every diagnostic, a sick introduction.

Here is the move this chapter turns on. **A publication-grade introduction is exactly five paragraphs long, and each paragraph has exactly one job.** Paragraph 1 is the **Hook** — a single concrete fact, anecdote, or institutional detail that places the reader in the world the paper is about. Paragraph 2 is the **Question** — the precise causal or descriptive question the paper answers, set against the prior literature's gaps. Paragraph 3 is the **What-We-Do** — the design, the data, and the identification strategy, with the assumption named and the evidence for the assumption sketched. Paragraph 4 is the **Findings** — the headline number and its key heterogeneity, with magnitudes that map directly to the abstract's sentence 4 and Table 2. Paragraph 5 is the **Contribution** — a three-strand contribution paragraph that names the three literatures the paper engages and what it adds to each. Five paragraphs. About 1,200 to 1,600 words. No more, no less.

The five-paragraph structure is not a Procrustean bed; it is the *modal* structure of the best-written empirical-finance introductions, and following it gives you a working draft that you can then deviate from when you have a specific reason to. Most papers do not need deviations. Most papers need to *not* deviate, and the discipline of the chapter is the discipline of saying "no, that anecdote belongs in the conclusion, not the hook," "no, that paragraph is a third paragraph on the same point, fold it back," "no, the related-work paragraph belongs in section 2, not in the intro." This chapter is the diagnostic and the rewrite toolkit. Maya's eleven-paragraph February draft will be the patient.

---

## 1. The reveal: why five paragraphs, why this order

Empirical-finance introductions have, for decades, settled on a structure that is more pedagogical than scientific — it is the structure that has been found, by collective trial and error, to *teach* a reader the paper most efficiently. The structure has five jobs, in five paragraphs, because each job is incompressible: skip the hook and the reader does not know why to care; skip the question and the reader does not know what is being asked; skip the what-we-do and the reader cannot judge identification; skip the findings and the reader does not know the headline; skip the contribution and the reader cannot place the paper in the literature.

The order matters because each paragraph depends on the previous. The hook motivates the question; the question motivates the design; the design produces the findings; the findings define what the contribution is. A paper that puts findings before design (a common pathology — "we find that …, using a difference-in-differences design that …") asks the reader to swallow the findings before they have any reason to believe them, and the reader's prior on the result is therefore low. A paper that puts design before question (also common — "we use a staggered DiD on the 2017 examination reform; the question we ask is …") buries the question under method, and the reader has to keep an unanswered "but what *are* you asking?" in working memory through the design paragraph.

The five paragraphs are a *funnel*. Paragraph 1 is the broadest — the institutional fact a 17-year-old could understand. Paragraph 2 narrows to the specific question. Paragraph 3 narrows further to the specific design. Paragraph 4 narrows to the specific numbers. Paragraph 5 widens back out — placing the specific numbers in the broader literature. The visual is an hourglass with the question/design/findings at the narrow waist and the hook and contribution at the widening ends. This is the structure your reader's attention follows naturally; deviating from it imposes cognitive load that costs you readers.

---

## 2. Paragraph 1 — the Hook

The hook is one paragraph (4 to 7 sentences, 100 to 180 words) that gives the reader a concrete reason to care about the paper's question. It is *not* a literature review. It is *not* a definition of terms. It is *not* a paragraph that begins "Fair lending has long been a topic of interest in financial economics." It is a concrete fact, a vivid number, an institutional detail, or a brief anecdote that locates the reader in the world the paper is about.

**The hook earns the reader's attention by being specific.** "Mortgage denial rates in the United States differ across racial groups" is generic; "In 2019, a Black applicant for a conventional mortgage in the Atlanta MSA was 1.7 times as likely to be denied as a White applicant with the same income, credit score, debt-to-income ratio, and loan-to-value ratio (Gao and Sun, 2019)" is specific. The specific version locates the reader: a particular year, a particular city, a particular comparison, a particular magnitude. The reader can picture the applicants.

**The hook ends by foreshadowing the question.** The last sentence of the hook should be the bridge to paragraph 2. For Maya's paper: "What can a regulatory tool — the targeted, intensified fair-lending examination — do about this gap?" That sentence is the hand-off; paragraph 2 picks up "Existing work on supervisory intensity …" and begins narrowing.

Here is Maya's actual revised hook paragraph (about 160 words):

> *In 2019, a Black applicant for a conventional mortgage in the Atlanta MSA was 1.7 times as likely to be denied as a White applicant with the same income, credit score, debt-to-income ratio, and loan-to-value ratio (Gao and Sun, 2019). Gaps of this magnitude persist across the United States despite decades of fair-housing legislation, generations of legal precedent, and substantial empirical work documenting both the disparate impact of lender discretion and the role of structural credit-score features. In 2017, the Office of the Comptroller of the Currency (OCC) initiated a program of intensified fair-lending examinations, rolling the program out across regional bank-supervisory portfolios over the following three years. The program did not change underwriting law; it changed the *intensity of scrutiny* that lenders faced from their supervisors. Whether — and where, and for whom — that change in scrutiny translated into a measurable change in mortgage denial outcomes is the question this paper answers.*

Read the hook. It anchors the reader (Atlanta, 2019, 1.7x), summarizes the persistent puzzle in one sentence, introduces the specific institutional intervention being studied (2017 OCC reform), distinguishes the mechanism (intensified scrutiny, not changed law), and ends with the question hand-off. Six sentences, one paragraph. The reader knows after 160 words exactly what world the paper is in and what is being asked of them. The hook earned its place.

Common hook pathologies. The **literature-review hook** opens "A growing literature in finance has studied …" — this is the failure mode of Chapter 11.1's abstract diagnostic; it has the same fix (start with the world, not with the literature). The **definition-hook** opens "Fair lending refers to the principle that …" — this is undergraduate-essay style; the reader does not need definitions yet, they need a reason to read. The **chest-thumping hook** opens "This paper makes three contributions to the literature on …" — the reader cannot care about contributions before they know the question; this paragraph belongs in paragraph 5 (Contribution), not paragraph 1. The **anecdote-too-long hook** spends 400 words on a single applicant's story; this is overwriting and the funnel never narrows.

The discipline: one concrete fact, one summary of the puzzle, one bridge to the question. 100–180 words. Stop.

---

## 3. Paragraph 2 — the Question

The question paragraph (5 to 8 sentences, 150 to 250 words) names the precise question the paper answers and situates it against what is and is not known. It is the only place in the introduction where a brief literature reference is required, but the references serve to define the *gap* the paper fills, not to summarize all prior work.

**The first sentence of paragraph 2 names what is known.** This is where Maya can cite Gao and Sun (2019) for the descriptive denial-gap fact, where Munnell, Tootell, Browne, and McEneaney (1996) appear for the foundational Boston Fed study, and where the more recent literature on regulatory supervision (Agarwal, Ben-David, and Yao 2017; Bhutta, Hizmo, and Ringo 2024) appears as the immediate context.

**The middle sentences of paragraph 2 name what is *not* known.** This is the gap. For Maya: "Existing work has documented the persistent denial gap (Gao and Sun, 2019) and characterized the discretionary lender behaviors that drive it (Munnell et al., 1996; Bayer, Ferreira, and Ross, 2018), but the causal effect of *targeted supervisory intensity* on the gap has not been estimated. The closest precedent is Bhutta et al. (2024), who study a related but distinct CRA-driven intervention; the OCC fair-lending examination program differs from CRA in its targeted-by-finding-history structure, and the staggered rollout permits a credibly identified treatment effect."

**The last sentence of paragraph 2 states the question with precision.** "This paper estimates the causal effect of the 2017 OCC intensified fair-lending examination program on the Black–White denial-rate gap in covered counties, with attention to heterogeneity by lender-examination-finding history and county minority-population share."

Three details to internalize. **First**, paragraph 2 cites three to seven papers, no more. The reader cannot keep track of more than this in working memory; deeper coverage belongs in section 2 (the literature review proper). The choice of which papers to cite is therefore strategic: cite the paper that names the puzzle, cite the paper closest to your design, cite the paper farthest from your design but in the broader literature. **Second**, the *gap statement* must be defensible. If you say "the causal effect has not been estimated," you must mean it; if there is a 2022 working paper that estimates a related effect, you need to acknowledge it and explain how your paper differs. Failure to acknowledge a close prior is the most common cause of a referee writing "the author appears unaware of …" — which is a near-fatal failure mode. **Third**, the question stated in the last sentence must match the question in sentence 1 of the abstract. Both should read "estimates the causal effect of the 2017 intensified fair-lending examination program on …"; the abstract and the introduction are contracts with the same reader, and they must agree.

Maya's paragraph 2, revised (about 220 words):

> *That a Black–White mortgage denial gap of this magnitude can persist conditional on observable applicant characteristics has been documented across decades and datasets (Munnell, Tootell, Browne, and McEneaney, 1996; Gao and Sun, 2019; Bayer, Ferreira, and Ross, 2018). What has remained an open question is whether — and through what channel — targeted regulatory supervision can close the gap. The most direct precedent is Bhutta, Hizmo, and Ringo (2024), who study a Community Reinvestment Act (CRA) examination intervention with a different design and a different population: CRA examinations are scheduled and broad-based, the OCC intensified fair-lending examinations are targeted by prior-finding history and rolled out in a staggered fashion. Earlier work on supervisory intensity in banking (Agarwal, Ben-David, and Yao, 2017) suggests that targeted scrutiny can change lender behavior in measurable ways, but no paper of which we are aware has estimated the causal effect of fair-lending-specific examination intensity on disparate mortgage outcomes. This paper estimates that effect using the staggered rollout of the 2017 OCC intensified fair-lending examination program. We ask: how much did the program close the Black–White denial-rate gap in covered counties, and through which mechanism — targeted scrutiny of high-finding-history lenders, or generalized supervisory pressure — did the effect operate?*

Notice the work the paragraph is doing. It names the foundational literature (Munnell et al.); the descriptive literature (Gao and Sun); the relevant lender-behavior literature (Bayer, Ferreira, and Ross); the close precedent that is *not* the same paper (Bhutta et al.); the deeper literature on supervisory intensity (Agarwal, Ben-David, and Yao); and then states the question. The last sentence also previews the mechanism question that will become the heterogeneity analysis in paragraph 4. The reader, after paragraph 2, knows exactly what is being asked and why no one has answered it yet.

---

## 4. Paragraph 3 — the What-We-Do

The what-we-do paragraph (6 to 10 sentences, 200 to 350 words) describes the empirical strategy: the data, the design, the identifying assumption, and the evidence for the assumption. **This is the paragraph where the referee makes up her mind about whether to recommend the paper for revise-and-resubmit or for rejection**, so it is the paragraph that earns the most layout effort.

**The first sentence names the data.** "We use HMDA loan-level data covering 47 million conventional mortgage originations across the universe of U.S. depository institutions from 2014 through 2020, combined with the OCC's published roster of examination histories." Specificity: the dataset by name, the unit of observation, the volume, the time span, the linkage.

**The second sentence names the design.** "We exploit the staggered rollout of the intensified examination program across 614 OCC-supervised counties between 2017 and 2020 in a difference-in-differences framework, with cohort-specific event-study leads and lags following Callaway and Sant'Anna (2021)." Specificity: the variation being exploited, the design family, the variant within the family, the canonical citation for the variant.

**The middle sentences name the identifying assumption.** "Identification of the average treatment effect on treated counties requires that, absent the program, denial-gap trends in covered and uncovered counties would have evolved in parallel. We assess this assumption in three ways: by reporting event-study coefficients for pre-treatment leads, which are statistically indistinguishable from zero (Figure 1); by computing Oster (2019) δ bounds, which indicate that an unobserved confounder would need to be 1.7 times as influential as the full vector of observables to overturn the estimate; and by re-estimating the design under the Sun and Abraham (2021) heterogeneity-robust estimator, with no substantive change in the headline."

**A sentence on robustness and inference.** "We cluster standard errors at the county level (the unit of treatment assignment), and report wild-cluster-bootstrap p-values as a check on small-cluster inference (Cameron and Miller, 2015)."

**The closing sentence previews the mechanism analysis.** "To distinguish targeted-scrutiny from generalized-deterrence mechanisms, we estimate heterogeneous treatment effects by lender prior-finding-history quartile and by county minority-population share, with multiple-testing corrections applied as in Chapter 10.2's family-wise discipline."

Maya's paragraph 3, revised (about 290 words):

> *We use HMDA loan-level data covering 47 million conventional mortgage originations across the universe of U.S. depository institutions from 2014 through 2020, combined with the OCC's published roster of examination histories and the FFIEC supervisory schedule. The variation we exploit is the staggered rollout of the intensified fair-lending examination program across 614 OCC-supervised counties between 2017 and 2020. We estimate a difference-in-differences specification with cohort-specific event-study leads and lags following Callaway and Sant'Anna (2021), with county and lender-by-year fixed effects and standard errors clustered at the county level. The identifying assumption is that, absent the program, denial-gap trends in covered and uncovered counties would have evolved in parallel. We assess this assumption in three ways: by reporting event-study coefficients for pre-treatment leads (Figure 1), which are statistically indistinguishable from zero; by computing Oster (2019) δ bounds, which indicate that an unobserved confounder would need to be 1.7 times as influential as the full vector of observables to overturn the headline result; and by re-estimating the design under the Sun and Abraham (2021) heterogeneity-robust estimator, with no substantive change in the headline coefficient. To distinguish targeted-scrutiny from generalized-deterrence mechanisms, we estimate heterogeneous treatment effects by lender prior-finding-history quartile and by county minority-population share, with multiple-testing corrections from the Benjamini–Hochberg false-discovery-rate procedure applied to the heterogeneity family. A specification-curve analysis across the full menu of plausible sample restrictions, outcome variants, fixed-effect saturations, clustering choices, and winsorization options (Figure 2) confirms that the headline coefficient lies in a tight band that excludes zero in approximately 85% of the specification menu.*

The paragraph does seven jobs in 290 words: names the data, names the variation, names the design, names the assumption, defends the assumption (three ways), names the heterogeneity analysis, names the robustness discipline. A referee reading this paragraph alone could decide whether to accept the assignment, and would probably say yes — because every concern she would have has been preempted by a sentence in this paragraph.

---

## 5. Paragraph 4 — the Findings

The findings paragraph (5 to 8 sentences, 180 to 280 words) reports the headline numbers and the key heterogeneity. It is *not* a tour of the tables; it is a curated selection of the four or five numbers that constitute the paper's contribution.

**The first sentence is the headline number.** Same as sentence 4 of the abstract, possibly with one extra clause. "We find that the intensified examination program reduced the Black–White denial-rate gap by 1.4 percentage points in covered counties (95% confidence interval: 0.8 to 2.0 percentage points), a 23% reduction relative to the pre-treatment gap of 6.1 points and roughly one-quarter of the persistent national gap of 5.5 points documented in Gao and Sun (2019)."

**The second sentence is the temporal structure.** "The effect emerges gradually over the four years following examination intensification (Figure 1), consistent with a behavioral-adjustment lag in lender underwriting practices rather than an instantaneous compliance shift."

**The third sentence is the heterogeneity.** "Effects are concentrated in counties with above-median minority-population shares (a 2.3 percentage-point reduction, compared with 0.2 points in below-median counties) and at lenders with above-median prior-finding histories (a 2.2 point reduction at high-history lenders, compared with 0.3 points at low-history lenders)." This is the result Figure 3 (the heterogeneity forest) makes visible.

**The fourth sentence is the mechanism.** "The interaction of high-minority-share with high-finding-history lenders accounts for nearly all of the average effect, consistent with the program operating through targeted scrutiny of lenders with documented prior compliance concerns in jurisdictions with the largest disparities, rather than through generalized deterrence."

**The fifth sentence is the placebo / robustness reassurance.** "Placebo tests on outcomes that should not be affected by fair-lending examination — loan-to-value ratios, loan terms, and interest-rate spreads — show no significant effects (Table 5), consistent with the program operating specifically on the decision to lend rather than on the terms of lending."

**Optional final sentence: the bounded magnitude / external-validity caveat.** "These estimates apply to OCC-supervised institutions and to the 614 counties in which the program was active during 2017–2020; the external-validity discussion in Section 6 considers how these estimates would transport to Federal-Reserve-supervised banks and to a larger geographic footprint." This sentence is the bridge to paragraph 5 (Contribution) and forecasts the external-validity paragraph from Chapter 10.5.

Maya's paragraph 4, revised (about 260 words):

> *We find that the intensified examination program reduced the Black–White denial-rate gap by 1.4 percentage points in covered counties (95% confidence interval: 0.8 to 2.0), a 23% reduction relative to the pre-treatment gap of 6.1 points and roughly one-quarter of the persistent national gap of 5.5 points documented in Gao and Sun (2019). The effect emerges gradually over the four years following examination intensification (Figure 1), consistent with a behavioral-adjustment lag in lender underwriting practices rather than an instantaneous compliance shift. Effects are concentrated in counties with above-median minority-population shares (a 2.3 percentage-point reduction, compared with 0.2 points in below-median counties) and at lenders with above-median prior-finding histories (2.2 points at high-history lenders versus 0.3 points at low-history lenders); the interaction of high-minority-share counties with high-finding-history lenders accounts for nearly all of the average effect, consistent with the program operating through targeted scrutiny rather than generalized deterrence. Placebo tests on outcomes that should not be affected by fair-lending examination — loan-to-value ratios, loan terms, and interest-rate spreads — show no significant effects (Table 5), consistent with the program operating specifically on the decision to lend rather than on the terms of lending. These estimates apply to OCC-supervised institutions and to the 614 counties in which the program was active during 2017–2020; the external-validity discussion in Section 6 considers how these estimates would transport to Federal-Reserve-supervised banks and to a broader geographic footprint.*

The paragraph reports five distinct empirical results (headline, dynamics, two heterogeneities, placebo) and the external-validity caveat in 260 words. The reader, after paragraph 4, knows all the headline numbers and is positioned to engage with the contribution paragraph that follows.

---

## 6. Paragraph 5 — the Contribution

The contribution paragraph (4 to 6 sentences, 150 to 250 words) names the three (or two, or four) literatures the paper engages and what it adds to each. **This is the paragraph the citing scholar will paraphrase three years from now**, so the contribution must be stated in language that survives paraphrase: a contribution worded vaguely will be cited vaguely or not at all.

**The standard structure is three contribution strands.** The number is conventional — two strands is too thin, four is too many — and three matches the cognitive granularity of the literature most papers engage. For Maya's paper:

**Strand 1 — the fair-lending-disparities literature.** "We contribute to the fair-lending-disparities literature (Munnell et al., 1996; Bayer, Ferreira, and Ross, 2018; Gao and Sun, 2019) by providing the first credibly identified estimate of the causal effect of a targeted regulatory intervention on the Black–White denial gap. Earlier work has documented the gap and identified its determinants; we document a *policy lever* — examination intensity targeted by prior-finding history — that closes roughly one-quarter of the gap in covered counties."

**Strand 2 — the supervisory-intensity-in-banking literature.** "We contribute to the literature on the real effects of bank supervision (Agarwal, Ben-David, and Yao, 2017; Bhutta, Hizmo, and Ringo, 2024) by extending the analysis from the credit-allocation outcomes those papers study to a distributional outcome — the disparity in denial rates across racial groups. The finding that supervisory intensity has measurable distributional consequences expands the policy-relevance of supervisory tools beyond their traditional safety-and-soundness purpose."

**Strand 3 — the methodological / staggered-DiD literature.** "Methodologically, our application combines the Callaway and Sant'Anna (2021) staggered-DiD estimator with multiple-testing-disciplined heterogeneity analysis (Romano and Wolf, 2005; Benjamini and Hochberg, 1995), the Oster (2019) sensitivity bound, and a specification-curve robustness exercise, providing a template for credible heterogeneity analysis in staggered-treatment designs."

Maya's paragraph 5, revised (about 220 words):

> *We contribute to three literatures. First, to the fair-lending-disparities literature (Munnell, Tootell, Browne, and McEneaney, 1996; Bayer, Ferreira, and Ross, 2018; Gao and Sun, 2019), we provide the first credibly identified estimate of the causal effect of a targeted regulatory intervention on the Black–White mortgage-denial gap; earlier work documents the gap and identifies its determinants, while we document a *policy lever* — examination intensity targeted by prior-finding history — that closes roughly one-quarter of the gap in covered counties. Second, to the literature on the real effects of bank supervision (Agarwal, Ben-David, and Yao, 2017; Bhutta, Hizmo, and Ringo, 2024), we extend the analysis from credit-allocation outcomes to a distributional outcome — the disparity in denial rates across racial groups — and show that supervisory intensity has measurable distributional consequences beyond its traditional safety-and-soundness purpose. Third, methodologically, our application combines the Callaway and Sant'Anna (2021) staggered-DiD estimator with multiple-testing-disciplined heterogeneity analysis (Benjamini and Hochberg, 1995; Romano and Wolf, 2005), the Oster (2019) sensitivity bound for unobservable confounding, and a specification-curve robustness exercise across the menu of plausible analytic forks, providing a template for credible heterogeneity analysis in staggered-treatment designs.*

The paragraph names three literatures, three contributions, and seven citations — three of which are foundational to one strand each, and four of which are method citations grouped at the end of strand three. The reader, after paragraph 5, knows exactly which conversations the paper is joining and what it is adding to each.

Two common pathologies of paragraph 5. The **list-of-claims paragraph** asserts six contributions without grouping them into literatures; the reader cannot place any of them. The fix is to force the contributions into three strands grouped by literature, even if it requires combining sub-contributions. The **chest-thumping paragraph** uses superlatives ("we provide *the first* …", "we make *the most important* …") liberally; superlatives invite the reader to disagree (and one or two of them will be wrong, and the wrong one becomes the referee's hook). The fix is to use precise language ("we provide the first credibly identified estimate of …") rather than open superlatives. The **literature-summary paragraph** restates what each cited paper finds rather than what *this* paper adds; the reader does not need the summary, she needs the differentiator.

---

## 7. The full revised introduction, end to end

Stitch the five paragraphs together and Maya's revised introduction is 1,150 words across five paragraphs. (Compared to her February draft of 4,200 words across eleven paragraphs, the revised version is 73% shorter.) The reader who reads only the introduction now knows everything they need to engage with the paper: the institutional setting, the question, the design and assumption, the headline number with heterogeneity, the contribution to three literatures. The remaining sections of the paper (data and methods in detail, results, mechanism, robustness, external validity, conclusion) are now elaborations on the five-paragraph promise.

A useful test: print the introduction. Hand it to your advisor. Ask: after reading just these five paragraphs, do you know what the paper does and what it finds? If yes, the introduction has earned its place. If no — if your advisor asks "but what about X?" where X is one of the five jobs — the failing paragraph is the one to revise.

---

## 8. How to diagnose a sick intro

The five-paragraph structure is the positive template. The negative template — the diagnostic for what is wrong with the intro you actually have — is the focus of this section. Most sick introductions exhibit one or more of six pathologies. We name each, describe the diagnostic, and prescribe the fix.

### 8.1 The Wandering Funnel

**Pathology.** The introduction has more than five paragraphs (often eight to fifteen) and includes paragraphs that do not fit any of the five jobs. The reader cannot tell what each paragraph is for.

**Diagnostic.** Read the introduction and tag each paragraph with one of the five jobs (Hook / Question / What-We-Do / Findings / Contribution) or "Other." If you have any "Other" paragraphs, or two paragraphs tagged with the same job, the structure is broken.

**Fix.** Fold "Other" paragraphs into the appropriate body section (Section 2 for literature, Section 6 for policy discussion, Section 4 for mechanism). Combine duplicate-job paragraphs into one. The discipline of "five paragraphs, one job each" forces cuts.

### 8.2 The Methodological Detour

**Pathology.** Paragraph 3 (What-We-Do) expands into a methodological tutorial — multiple paragraphs on the Callaway and Sant'Anna estimator, on cluster-robust standard errors, on the Sun and Abraham critique. The introduction reads like a methods section.

**Diagnostic.** Count the sentences in paragraph 3 that describe *what we do* versus *why our method is right*. If more than 25% of the sentences are method-defense, the methodological detour is happening.

**Fix.** Move the method defense to Section 3 (Empirical Strategy). The introduction's paragraph 3 names the method and the assumption and the evidence for the assumption — period. The detailed defense of the method's properties belongs deeper in the paper.

### 8.3 The Diffuse Hook

**Pathology.** Paragraph 1 opens with broad statements that could appear in any paper on the topic. "Fair lending has long been a concern of policymakers and academics" or "The Black–White wealth gap remains a persistent feature of the U.S. economy." There is no specific fact, no specific year, no specific institutional detail.

**Diagnostic.** Highlight any *number* or *proper noun* (institution, year, person, place) in the first three sentences. If you have fewer than three highlights, the hook is diffuse.

**Fix.** Find a specific fact and start there. The 1.7x Atlanta number in Maya's revised hook is the fix. The fact has to be on the topic and verifiable; do not fabricate.

### 8.4 The Findings-Free Findings Paragraph

**Pathology.** Paragraph 4 has the structure of a findings paragraph but no actual numbers. "We find statistically significant effects." "Our heterogeneity analysis reveals important variation across subgroups." "The placebo tests support our identification."

**Diagnostic.** Count the numbers in paragraph 4. If there are fewer than four, the findings are missing.

**Fix.** Pull the headline number, the CI, the magnitude of the largest heterogeneity, and the magnitude of the placebo from the tables and put them in the paragraph. The introduction earns the right to claim findings only by reporting them.

### 8.5 The Literature-Review Conscription of the Question Paragraph

**Pathology.** Paragraph 2 has been conscripted into being a mini-literature-review. Twelve citations, none in service of the question, all in service of demonstrating that the author has read widely.

**Diagnostic.** Count the citations in paragraph 2. If there are more than seven, the conscription has happened.

**Fix.** Move all but the three to five most relevant citations to Section 2 (the proper literature review). Paragraph 2's citations should serve one purpose: defining the *gap* that paragraph 2's last sentence asks the paper to fill.

### 8.6 The Contribution Inflation

**Pathology.** Paragraph 5 names six or seven contributions, often overlapping, often grandiose. "We are the first to estimate…", "We provide a comprehensive analysis of…", "We make a fundamental contribution to…", "We open new avenues for future research in…"

**Diagnostic.** Underline every superlative ("first," "most comprehensive," "fundamental," "novel," "unprecedented") in paragraph 5. If you have more than two, the inflation has happened.

**Fix.** Replace each superlative with a precise descriptor ("the first credibly identified estimate of …," "a complementary analysis of …"). The precision is the credibility; the superlative is the suspicion.

---

## 9. A diagnostic script for sick introductions

The diagnostics above can be partially automated. The notebook `nb11.4` implements a function that tags each paragraph and flags candidates for each pathology. It is, like the abstract auditor of Chapter 11.1, a pre-flight checklist rather than a quality certifier — it catches obvious failures so your advisor and your eventual referee do not.

```python
# nb11.4 cell 1 — intro_audit(): a sanity check for the five-paragraph structure.
import re
from collections import Counter

import numpy as np

rng = np.random.default_rng(42)

def intro_audit(text: str) -> dict:
    """
    Diagnose pathologies in an empirical-paper introduction.
    Returns a dict of warnings keyed by pathology name.
    """
    warnings = {}
    # Split on blank lines into paragraphs
    paras = [p.strip() for p in re.split(r"\n\s*\n", text) if p.strip()]
    warnings["paragraph_count"] = len(paras)
    if len(paras) != 5:
        warnings["wandering_funnel"] = (
            f"Introduction has {len(paras)} paragraphs; five-paragraph structure expects 5."
        )

    n_words = len(text.split())
    warnings["word_count"] = n_words
    if n_words > 1800:
        warnings["too_long"] = f"Intro is {n_words} words; target is 1,200–1,600."
    if n_words < 900:
        warnings["too_short"] = f"Intro is {n_words} words; target is 1,200–1,600."

    # Pathology: Diffuse Hook
    if paras:
        first = paras[0]
        first_three = ". ".join(first.split(". ")[:3])
        has_number = bool(re.search(r"\d", first_three))
        has_proper_noun = bool(re.search(r"\b[A-Z][a-z]+(?:\s[A-Z][a-z]+)+", first_three))
        if not (has_number and has_proper_noun):
            warnings["diffuse_hook"] = (
                "First three sentences contain no number/proper-noun pair; "
                "hook may be too generic."
            )

    # Pathology: Findings-Free Findings (assume para 4 if 5 paragraphs)
    if len(paras) >= 4:
        p4 = paras[3]
        n_numbers = len(re.findall(r"\d+(\.\d+)?", p4))
        if n_numbers < 4:
            warnings["findings_free"] = (
                f"Findings paragraph has only {n_numbers} numbers; expect at least 4 "
                "(headline + CI + heterogeneity + placebo)."
            )

    # Pathology: Contribution Inflation (assume para 5 if 5 paragraphs)
    if len(paras) >= 5:
        p5 = paras[4]
        superlatives = [
            "first", "most comprehensive", "fundamental", "novel",
            "unprecedented", "groundbreaking", "the only",
        ]
        super_count = sum(p5.lower().count(s) for s in superlatives)
        if super_count > 2:
            warnings["contribution_inflation"] = (
                f"Contribution paragraph has {super_count} superlatives; "
                "use precise descriptors instead."
            )

    # Pathology: Literature-review conscription of paragraph 2
    if len(paras) >= 2:
        p2 = paras[1]
        # Heuristic: count parenthetical citations of the form "Author, YEAR"
        cite_count = len(re.findall(r"\([A-Z][a-zA-Z\-]+(?:\sand\s[A-Z][a-zA-Z\-]+)?,\s*\d{4}\)", p2))
        if cite_count > 7:
            warnings["question_para_conscripted"] = (
                f"Question paragraph has {cite_count} citations; trim to 3–5."
            )

    return warnings
```

Running this on Maya's February draft returns flags for `wandering_funnel`, `too_long`, `diffuse_hook`, and `contribution_inflation`. Running it on the revised five-paragraph version returns only `paragraph_count: 5, word_count: 1150` and no warnings. The script's role is the same as the abstract auditor's: necessary, not sufficient.

---

## 10. The writing protocol: how to rewrite an intro from a sick draft

You will not rewrite the introduction in one sitting. You will do it in six passes, each about twenty to thirty minutes, with breaks. Here is the protocol.

**Pass 1 — Tag.** Print the existing intro. Beside each paragraph, write H, Q, WWD, F, C, or O (for Other). The O paragraphs are candidates for removal or relocation.

**Pass 2 — Plan.** On a fresh page, write the five-paragraph headers (Hook, Question, What-We-Do, Findings, Contribution). Under each header, write the *one sentence* the paragraph must accomplish. This is the spine.

**Pass 3 — Hook.** Open the fresh page; draft the hook in 100–180 words. Start with a specific number or institutional fact. End with the bridge sentence to paragraph 2.

**Pass 4 — Question, What-We-Do, Findings.** Draft the three middle paragraphs in sequence. Pull numbers from the tables (no placeholders; use the actual numbers from Chapter 11.2's Table 2). Name the assumption in paragraph 3. Name three to five citations in paragraph 2 — no more.

**Pass 5 — Contribution.** Draft the three-strand contribution paragraph. Use the brainstorm from §6 above as a template. Avoid superlatives; use precise descriptors.

**Pass 6 — Audit.** Run `intro_audit()`. Read aloud. Hand to advisor. Apply edits.

Total time: about two and a half hours, spread over a day or two. The introduction you end with will be 70 to 80 percent of the final version.

---

## 11. When the structure legitimately deviates

The five-paragraph structure is the default; exceptions exist.

**Replication papers** often need a paragraph between Question and What-We-Do that explicitly names the paper being replicated and the dimension along which the replication differs. The six-paragraph version is then Hook / Question / Differential-from-Original / What-We-Do / Findings / Contribution.

**Methodological papers** invert paragraphs 3 and 4: the method is the contribution, and the findings are illustrative. The structure is Hook / Question / Method-Contribution / Empirical-Illustration / Contribution.

**Survey papers** and review papers do not follow this structure at all; they typically follow a chronological-and-thematic outline of the field.

**Theory-heavy papers** with an empirical extension sometimes need a paragraph between What-We-Do and Findings that previews the theoretical predictions being tested. The six-paragraph version is then Hook / Question / Theoretical-Prediction / What-We-Do / Findings / Contribution.

In every case, the deviation should be justified by the paper's specific structure, not by the author's stylistic preference. If your draft has eight paragraphs and three are doing one of the five jobs each while the other three are doing two of the jobs in a combined paragraph plus one "Other" paragraph, the right move is almost always to consolidate to five. Default to the structure; deviate only when the paper structurally demands it.

---

## 12. Calibrating: read three introductions in your subfield, score them

The final exercise. **Pick three published papers in your target journal, in the last three years, and score each introduction against the five-paragraph structure.** For each, count paragraphs, tag each paragraph with one of the five jobs, count words per paragraph, and identify which (if any) of the six pathologies appear.

You will discover three things.

First, the best introductions in your subfield almost always follow the five-paragraph structure exactly, with paragraph word counts close to the targets in this chapter.

Second, some published papers have one or two pathologies — most commonly the methodological detour (paragraph 3 is too long) or the contribution inflation (paragraph 5 oversells). Published does not mean exemplary; the pathologies survive because the underlying contribution was strong enough to carry the prose.

Third, the *worst* introductions in your subfield are usually long. Length correlates with sickness. The discipline of fitting your introduction into five paragraphs of 1,200 to 1,600 words is, in practice, the discipline of saying everything the introduction needs to say and nothing else. A 4,200-word introduction is rarely better than the same paper's 1,400-word introduction; usually it is worse, because it has buried the contract under prose.

Maya's revised introduction is on its way to her advisor by Friday afternoon. The five paragraphs are in place; the headline number agrees with the abstract and the table; the contribution is three strands; the pathologies are gone. In Chapter 11.5 we turn from the introduction's contribution paragraph — three citations per strand — to the expanded literature review that will follow it in section 2: the three-strand argument that earns the contribution sentence.

---

## 13. Recap

The reveal: **a publication-grade introduction is exactly five paragraphs, one job each.** Hook (concrete fact + bridge), Question (gap + question), What-We-Do (data + design + assumption + evidence-for-assumption), Findings (numbers + heterogeneity + placebo), Contribution (three literatures, three strands). About 1,200–1,600 words. The funnel: broad → narrow → broad.

Six diagnostic pathologies — wandering funnel, methodological detour, diffuse hook, findings-free findings paragraph, literature-review-conscripted question paragraph, contribution inflation — each have a diagnostic question and a fix. The `intro_audit()` script catches the obvious ones.

The writing protocol: tag, plan, hook, middle three, contribution, audit. Six passes, two and a half hours, 70–80% of the final version.

### Glossary

- **Five-paragraph structure**: Hook / Question / What-We-Do / Findings / Contribution — the canonical structure of an empirical-finance introduction.
- **The funnel**: the conceptual shape of the introduction; broad institutional fact at the top, narrow question and design at the waist, broad literature contribution at the bottom.
- **Three-strand contribution**: the convention of organizing paragraph 5 into three named literature engagements, each with one named contribution.
- **Wandering funnel**: the pathology of an introduction with more than five paragraphs and unclear paragraph-to-job mapping.
- **Contribution inflation**: the pathology of overclaiming in paragraph 5 through superlatives ("first," "most comprehensive," "fundamental," "novel").

### Citations

- Agarwal, S., I. Ben-David, and V. Yao (2017). "Systematic Mistakes in the Mortgage Market and Lack of Financial Sophistication." *Journal of Financial Economics* 123(1): 42–58.
- Bayer, P., F. Ferreira, and S. L. Ross (2018). "What Drives Racial and Ethnic Differences in High-Cost Mortgages? The Role of High-Risk Lenders." *Review of Financial Studies* 31(1): 175–205.
- Benjamini, Y., and Y. Hochberg (1995). "Controlling the False Discovery Rate." *Journal of the Royal Statistical Society B* 57(1): 289–300.
- Bhutta, N., A. Hizmo, and D. Ringo (2024). "How Much Does Racial Bias Affect Mortgage Lending? Evidence from Human and Algorithmic Credit Decisions." *Journal of Finance* (forthcoming). [CHECK]
- Callaway, B., and P. H. C. Sant'Anna (2021). "Difference-in-Differences with Multiple Time Periods." *Journal of Econometrics* 225(2): 200–230.
- Cameron, A. C., and D. L. Miller (2015). "A Practitioner's Guide to Cluster-Robust Inference." *Journal of Human Resources* 50(2): 317–372.
- Gao, L., and J. Sun (2019). "Lender-Borrower Race-Match Effects on Mortgage Approval." *Proceedings of the National Academy of Sciences* 116(19): 9293–9302.
- Munnell, A. H., G. M. B. Tootell, L. E. Browne, and J. McEneaney (1996). "Mortgage Lending in Boston: Interpreting HMDA Data." *American Economic Review* 86(1): 25–53.
- Oster, E. (2019). "Unobservable Selection and Coefficient Stability: Theory and Evidence." *Journal of Business & Economic Statistics* 37(2): 187–204.
- Romano, J. P., and M. Wolf (2005). "Stepwise Multiple Testing as Formalized Data Snooping." *Econometrica* 73(4): 1237–1282.
- Sun, L., and S. Abraham (2021). "Estimating Dynamic Treatment Effects in Event Studies with Heterogeneous Treatment Effects." *Journal of Econometrics* 225(2): 175–199.
