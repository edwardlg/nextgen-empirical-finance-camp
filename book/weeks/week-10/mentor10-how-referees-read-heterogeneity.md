# Mentor Session 10 — "How referees read a heterogeneity section."

*Week 10 live session · 60 minutes · led by Prof. Lei Gao · the Phase-3 revision-week mentor*

Yesterday's lab gave you a pipeline. Today we talk about the argument — specifically, the part the next reader (a referee at JFE or JF) leans on hardest. **The heterogeneity section is, more often than any other, the section that separates a paper that survives a first round from one that gets a "reject and resubmit." Not because the headline is wrong — usually it is fine — but because the heterogeneity section is where a careful reader decides whether to trust the author's discipline.**

I have refereed for the *Journal of Financial Economics*, *Review of Financial Studies*, *Management Science*, and a half-dozen field journals. The pattern is consistent across both sides of the desk. A heterogeneity section that reads as *believable* shares four properties that a *data-mined* one does not. Today we name those four properties, run a worked case on Gao, Han, Li & Zhou (2018, *JFE*) on intraday momentum — re-anchored from Mentor 1 for the regime-conditional splits — and walk out with a checklist you apply to your own Lab-10 appendix.

Bring the pre-read, your three Socratic warm-ups, and one printed page from your own Lab-10 appendix — the CATE histogram or the GATE-by-quintile table. We read yours in the room.

---

## (a) Pre-read packet — "Why heterogeneity is the section a referee tests the author's discipline on."

*Read this once before the session. It is one page; read it slowly, because the disposition matters more than the technique today.*

Every empirical paper has a headline number, and every referee learns that the headline number is the easiest claim to make believable. You ran a regression on a clean sample, reported a coefficient, clustered the standard errors honestly, stress-tested the spec — Chapters 8.1 and 8.2 are about how to make the headline bulletproof. By the time a referee picks up the paper, the headline has typically cleared the literature's threshold. **The fight is not over the headline. The fight is over what the paper claims *beyond* the headline.**

Heterogeneity is where that fight is loudest. The reason is structural: the moment you split your sample by a moderator, the multiple-testing problem from Chapter 10.2 enters in force, and the discovery freedom in choosing *which* moderator is enormous. Twenty covariates, two split rules per covariate, forty subgroups, and at $\alpha = 0.05$ you expect two to come up significant under the global null. A heterogeneity table with two significant rows out of forty proves nothing; a heterogeneity table with two significant rows out of *two pre-registered moderators* proves something. The referee's job — done quickly — is to figure out which kind of table they are reading.

**I want you to read a heterogeneity section the way a referee does: skeptically, in five minutes, looking for four signals.** Those signals are the topic of slides 2-5. They are: (1) the moderator was *named in advance*, traceable to the PAP or a theory the introduction names; (2) the pattern is *monotone* in the moderator (dose-response), not one outlier subgroup; (3) the inference is *adjusted* for the family, with the unadjusted column shown so the reader can audit; (4) the *mechanism* implied by the pattern is consistent with the introduction's story, not a post-hoc retrofit. A heterogeneity section that scores well on all four reads as discovery. A section that scores poorly on any one reads as p-hacking, and the referee reads the rest of the paper through that lens.

The disposition to internalize today is the referee's. When you read your own Lab-10 appendix, ask: *if I had picked this paper out of my queue cold, would I trust this heterogeneity section?* Then the harder question — *if not, what would the author have to add to flip my answer?* That second question is almost always answerable in one paragraph or one column. The heterogeneity section that reads as believable is rarely longer than the one that does not, just better disciplined.

---

## (b) Three Socratic warm-up questions

*Come with a written sentence or two for each. These have honest answers and evasive ones, not right and wrong ones.*

1. **The pre-registration audit.** Open your Lab-10 `appendix/cate_features.json` and read the moderators you committed. For each, write *one* sentence naming the introduction-theoretical-reason or threats-table row that motivated it — *before* you saw any split. If you cannot write that sentence honestly for one or more, the moderator is post-hoc and the footnote needs to say so. Which moderator would you most struggle to defend as pre-registered, and why? (Naming one is the honest answer.)

2. **The dose-response test.** Pick the strongest-headline heterogeneity row from your Lab-10 GATE-by-quintile table. Is the pattern across quintiles monotone or a single outlier quintile with the others flat? Write one sentence on which your data show. Then — the harder question — one sentence on what a referee should infer about credibility from a *non-monotone* pattern, even if the headline quintile survives Romano-Wolf. (Hint: confounders that vary smoothly with the moderator produce monotone patterns; a single outlier is more often sample-size noise than a structural feature.)

3. **The mechanism-consistency check.** Your heterogeneity result implies a *mechanism* — the process is more active in the subgroup where the effect is stronger. Write the implied mechanism in one sentence. Does it match the introduction's story? If yes, the heterogeneity reinforces the headline. If no, you must either revise the introduction or report the contradiction honestly. What does your Lab-10 result imply about your introduction's story, and what would you need to change about the introduction to make them hold together?

---

## (c) Five-slide deck (speak-from scaffold)

**Slide 1 — "Heterogeneity is where the referee tests your discipline."**
- The headline is usually defensible by Week 8. The heterogeneity section is where a referee decides whether to trust *the rest* of the paper.
- The reason is structural: the multiple-testing problem enters in force; discovery freedom is large; the temptation to fish is largest. A practiced referee can tell in five minutes whether the heterogeneity is pre-registered or post-hoc.
- The four signals: **(1) pre-registered moderator; (2) monotone pattern; (3) adjusted inference with unadjusted column shown; (4) mechanism consistent with the introduction.** Score well on all four = discovery. Score poorly on any = p-hacking, and the rest of the paper is read through that lens.

**Slide 2 — Signal 1: Was the moderator named in advance?**
- Every moderator must trace to *something committed before the data spoke*: a PAP row, a Ch 7.5 threats-table row, a sentence in the introduction citing a theoretical paper. A moderator appearing first in the heterogeneity appendix is post-hoc, and the referee knows it.
- The audit a referee runs: grep the introduction for the moderator; grep the PAP. If neither contains it, the appendix footnote had better explicitly say "post-hoc," and the abstract had better not lean on the result.
- When a moderator *is* post-hoc (a conference comment forced it), name it: *"This cut was added in response to a discussant; its p-value is not adjusted for the broader family of post-hoc cuts considered."* Do not let it do load-bearing work in the abstract.

**Slide 3 — Signal 2: Is the pattern monotone?**
- "Larger in the top tercile, zero elsewhere" is much weaker than "rises monotonically across terciles." Monotone is harder to confound (the confounder would have to track the moderator in lock-step) and harder to dismiss as a sampling artifact.
- Diagnostic: per-cell point estimate, per-cell sample size, and a one-sided test of monotonicity. A monotone pattern surviving multiple-test adjustment is the *positive identifying evidence* a heterogeneity section can deliver — the same logic as Hill's criteria in epidemiology.
- The failure mode: bimodal heterogeneity — strong in two non-adjacent subgroups, weak between — is usually a sampling artifact or an omitted-variable issue. Say so rather than starring two coefficients out of four.

**Slide 4 — Signal 3: Is the inference adjusted, and is the unadjusted column visible?**
- Ch 10.2 covered four adjustments — Bonferroni, Holm, BH-FDR, Romano-Wolf — and Lab 10 wired Romano-Wolf in. The discipline: **report both the unadjusted and adjusted columns in the same table.** Hiding the unadjusted column is the move of someone who hopes the reader will not notice three of four "significant" rows fail the adjustment.
- Fifteen-second referee diagnostic: count stars in each column, ratio them. Close to one = robust to FWER. Small = the headline should be the *one* row that survives, not the four that did not.
- Name the adjustment in the caption and cite the method paper. Romano-Wolf is most powerful when tests are correlated; Bonferroni is more conservative; do not make the referee guess which you used.

**Slide 5 — Signal 4: Does the implied mechanism match the introduction's story?**
- A heterogeneity result is a *claim about the mechanism*. "Stronger in intense-examination counties" implies intensity is the active ingredient. If the introduction told an intensity story, the heterogeneity reinforces it. If the introduction told a *publication-of-findings* story and the heterogeneity says intensity, the paper contradicts itself and no amount of robustness fixes that.
- The audit: read the introduction, infer the implied mechanism, then read the heterogeneity section and check agreement. Disagreement is a red flag; agreement is reinforcement.
- When heterogeneity surprises you, revise the introduction. A paper whose heterogeneity *redirects* the story is a paper that found a real result and is updating accordingly. A paper that lets the two sections say different things has not been edited carefully enough.

---

## (d) Three stretch questions — Gao, Han, Li & Zhou (2018) on intraday momentum, read for the heterogeneity

These tie today's theme to one of my own papers, used as a worked case from the heterogeneity angle. The citation, used verbatim:

> Gao, L., Han, Y., Li, S. Z., & Zhou, G. (2018). Intraday momentum: The first half-hour return predicts the last half-hour return. *Journal of Financial Economics*, 129(2), 394-414.

The paper documents a high-frequency cross-time predictability pattern in U.S. equities: first-half-hour returns forecast last-half-hour returns, controlling for the middle. Mentor 1 anchored on the *baseline* predictability result. We re-anchor today for what the paper does *next*: the cross-sectional and regime splits — volatility regimes, volume regimes, stock characteristics — that take the result from "an interesting pattern" to "a pattern with a mechanism" and determine whether the paper survives the *JFE* referee process.

**Reason about how a published intraday-momentum paper writes its heterogeneity against the four signals — not about what the paper specifically found. Do NOT invent or recite specific magnitudes, t-statistics, or sample sizes. Frame answers as "how I would defend"; mark anything needing confirmation against the published version as `[CHECK]`.**

1. **Signal 1 applied to volatility-regime splits.** Intraday momentum should — by the theory the introduction cites — be stronger when overnight information accumulation is larger, which is precisely the high-volatility regime. A volatility-regime split is therefore *pre-registered-by-theory*: the moderator was named before the heterogeneity table by the mechanism. (a) Why does this kind of split read more credibly to a *JFE* referee than one added in response to a discussant's question? (b) Suppose your own capstone has a moderator added in response to a Lab-9 discussant. Write the ~3-sentence appendix footnote that names the post-hoc origin honestly while preserving the result's value. (c) Why is honest-post-hoc reporting almost never worse for the paper than no reporting?

2. **Signal 2 applied to a possible dose-response in liquidity.** Suppose the paper reports intraday-momentum strength by liquidity quintile. One plausible pattern is monotone in liquidity (strongest in most-liquid, weakest in least-liquid). Another is U-shaped (strong at both extremes, weak in the middle). (a) Which is easier to defend at a *JFE* referee, and why? (b) If the actual pattern were the U-shape, write one paragraph defending it honestly — including the alternative explanations (sampling artifact in extreme buckets, omitted variable correlated with liquidity, genuinely different mechanism at extremes) and which you can rule out and which you cannot. (c) Why is a paragraph that *names everything and rules out nothing* more valuable to a referee than one that picks an explanation and runs?

3. **Signal 4 applied to the mechanism the introduction promised.** The paper's introduction motivates intraday momentum with overnight information accumulation, first-half-hour price discovery, and end-of-day rebalancing. The heterogeneity must deliver patterns consistent with that — stronger when overnight info matters more (volatility), stronger when price discovery is more informative (volume), stronger where end-of-day rebalancing is prevalent (institutional ownership). Suppose your own capstone has a heterogeneity result whose mechanism *contradicts* the introduction. (a) Which two of (i) revise the introduction, (ii) revise the heterogeneity reporting, (iii) drop the heterogeneity claim, (iv) drop the headline are the honest options? Which is *almost never* honest? (b) Write the ~150-word introduction-revision that lets the two tell a consistent story re-anchored on what the data delivered. (c) Why is *willingness to revise the introduction in response to heterogeneity* one of the strongest signals of authorial discipline a referee sees, and why is it almost always rewarded?

---

## (e) Post-session reflection prompt

Before the next mentor session, write a 400-600 word reflection — saved as `revision/mentor10_reflection.md` — that does three things.

First, **audit your Lab-10 appendix against the four signals.** Score each clean / partial / weak, and quote the *exact paragraph or table column* in your appendix that earned each score. The Assessment 10 grader will do this audit; doing it yourself first catches the gaps before someone else does.

Second, **identify the worst-scoring signal and write the concrete revision step.** Not "improve the heterogeneity section" — concrete: *"minority-share continuous moderator is not in the PAP; add the post-hoc footnote to Table A2 and remove the claim from the abstract."*

Third, **write the one sentence about your heterogeneity you can now say truthfully and could not have said before today.** Confidence ("the dose-response survives Romano-Wolf and matches §1.3, so heterogeneity reinforces the headline") or restraint ("the split I built around is, on honest inspection, post-hoc"). Either is right when true. The wrong sentence is the one you wrote before today.

The reflection makes the session a *graded* artifact. It feeds Assessment 10's causal-language-discipline row directly: skipping it caps that row at *Developing* on its own, because without it the grader has no evidence that the session's discipline reached the page.

The intraday-momentum paper survived the *JFE* process because its heterogeneity did what the four signals require — regimes named by theory, patterns monotone (`[CHECK]` magnitudes), inference adjusted, mechanism matched. Your capstone is under review by your future self, the Assessment 10 grader, and — for those headed to Schar Young Scholars — an editor who reads through the same lens. The discipline is the same whether the paper is the camp capstone or the JFE submission. The room is different; the bar is the same.
