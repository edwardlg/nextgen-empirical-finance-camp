# Ch 9.2 — The 8-Minute Talk, Decomposed: Hook, Design, Identification Punchline, One Picture, Threats, Ask

Chapter 8.5 gave you the *six-beat arc* of an empirical talk — question, why,
design, headline, robustness, contribution — and told you to spend roughly
one minute per beat. That chapter built the skeleton. This chapter is what
you do with each bone: how to write the *first sentence* that earns the
audience's attention, how to compress the design into a single defensible
clause, how to make the identification *punchline* land in nine seconds, how
to choose the one picture that is the slide-five headline, how to anticipate
the threats in the way the room will actually probe them, and how to close
with an *ask* — a specific concrete request of the audience — that turns the
end of your talk from a polite stop into an active recruitment of the
people who just gave you eight minutes of their attention.

Here is the move the chapter turns on, so you have it before the details.
**The eight-minute empirical talk is not a miniature paper; it is a six-part
argument with a single load-bearing slide.** If you remove the wrong slide,
the talk collapses; if you remove any other slide, the talk only loses
texture. Knowing *which* slide is load-bearing — and protecting it with
disproportionate care — is the difference between a talk that survives a
hostile room and a talk that does not. For an empirical paper, the load-bearing
slide is almost always the *identification punchline*, because that is where a
sharp audience decides whether the rest of your numbers are worth listening to.
Every other slide either *sets up* the punchline or *survives* it.

We walk the six beats in order, but we walk them with new content: the
*microstructure* of each beat — what the slide actually shows, what the
first sentence is, what the failure mode is, and what the rehearsal cue is.

---

## 1. The hook: the first sentence

The first sentence of an academic talk is the most expensive sentence of the
talk. It is expensive in two senses. *In attention*: the audience is making,
in the first ten seconds, a binary decision about whether to listen, and the
decision is hard to reverse — a room you lose at second eight you do not
recover at minute three. *In credibility*: the first sentence sets a register
— it tells the room what *kind* of paper this is, and how seriously to take
the speaker. A first sentence like "*Today I want to talk about machine
learning and finance*" is a thrown-away ten seconds; a first sentence like
"*In 2008, the SEC briefly banned short-selling of 797 financial stocks, and
nobody fully knows what that ban did to price discovery — so we used the ban
as a natural experiment*" is a *deposit* of credibility you spend the rest of
the talk on.

The hook obeys three rules.

**Rule one: it is a sentence, not a slide title.** "Introduction" is not a
hook. "*The denial rate gap between Black and white mortgage applicants is
12 percentage points after controlling for credit score, income, and
loan-to-value — and that gap has barely moved in twenty-five years*" is a
hook, because it is a *claim a stranger can have an immediate opinion about*.
The hook gives the room a target — a number, a fact, a puzzle — that the
rest of the talk is going to either explain, challenge, or refine. A hook
without a target is a hook without a barb; it slides off.

**Rule two: it contains a number or a name, not an abstraction.** *Concrete
before abstract* (CONVENTIONS §1) is the constitutional rule, and the hook
is where it bites hardest. Maya's fair-lending hook contains "12 percentage
points," not "a substantial gap." Devon's crypto hook contains "the
September 2024 ETF launch," not "recent regulatory developments." Sam's
momentum hook contains "the first thirty minutes of trading on the NYSE,"
not "intraday return patterns." The reason the concrete number works is
that the room *cannot argue with you yet* — they do not know enough — so
the number functions as a *fact to be explained*, and the explanation
becomes the talk. An abstraction, by contrast, invites the room to argue
with you immediately, because abstractions are exactly the wrong size for
the eight-minute format. You have no time to defend "substantial."

**Rule three: it sets up the question, but it is *not* the question.** This
is the subtle one. Many students confuse the hook with the question slide
(beat 2 of Ch 8.5's arc). The hook *gives the room the puzzle*; the question
slide *names the question you are about to answer*. They are different
moves. Priya's wildfire-insurance talk *hooks* with "*Between 2019 and 2024,
six of the largest insurers stopped writing new policies in California
counties with high wildfire exposure — the insurance market is, in places,
disappearing*," and then *asks* with "*Does wildfire risk explain that exit,
or does something else?*" The hook is the puzzle; the question is the
scalpel. You need both.

A practical drill: write your hook in three drafts.

```
draft 1: the first thing that comes to mind, probably abstract.
draft 2: rewrite with a number and a year.
draft 3: rewrite again, until a 17-year-old in row eight could repeat it
         back to a friend in the hallway five minutes later.
```

If draft three is not a sentence your 17-year-old self would care about, the
hook isn't done yet. Sam's hook went, in drafts:

```
1: "Intraday momentum is an interesting predictability pattern in stock returns."  -- abstract, bored
2: "From 1993 to 2024, the first-half-hour return on the S&P 500 predicts the      -- has dates and a number, but
    last-half-hour return with a correlation of about 0.05, even after costs."        feels like a table caption
3: "If the first thirty minutes of trading on the NYSE go up, the last thirty       -- a 17-year-old hears it,
    minutes go up — and you can bet on this, every day, for thirty years, and          and the puzzle lands
    it still pays. We don't know why."
```

Draft three is the hook. It has a number ("first thirty"), a length of time
("thirty years"), a verb the room understands ("bet"), and a puzzle ("we
don't know why"). Then he goes to the question slide: *what explains
intraday momentum, and is it consistent with limits to arbitrage?* And now
the room is listening.

The failure mode for the hook is not bad writing; it is *over-writing*. A
hook with three clauses and a parenthetical is a hook you cannot deliver
fluently. A nervous speaker's mouth produces short sentences; write your
hook for the nervous mouth, not the calm one. Twelve to twenty words. One
breath.

---

## 2. The design: the comparison you are making, named

Slide three (the design slide, Ch 8.5 §1) is where most empirical talks
either anchor or drift. The natural instinct is to put the regression
equation on the screen and walk through it — and that is the wrong move,
not because the equation is wrong but because the room *cannot read an
equation in sixty seconds*. The design slide does not contain an equation.
The design slide contains *the comparison*, named in one sentence, with one
small picture that illustrates the comparison.

The sentence is the identifying-assumption sentence from Chapter 7.5, said
the way you would say it to someone in the hallway: *"Our estimate compares
[these units] to [these other units] across [this kind of change], and the
comparison is fair as long as [the assumption]."* That is the *whole* design
slide, in one sentence. Everything else on the slide — the picture, the
sample description, the time period — exists to make that sentence
*concrete*.

Maya's design slide:

> *We compare denial rates at the same lender for nearly identical
> applicants — same credit band, same income decile, same loan-to-value
> bracket, same year, same MSA — and ask whether the gap between Black
> and white applicants tracks the lender's algorithmic-scoring intensity.
> The comparison is fair as long as algorithmic intensity is not picking
> up some other lender quality that itself drives the gap.*

That is one sentence, with the assumption inside it, in the same form as the
identification memo. The picture below it is a small two-panel diagram —
"applicants A and B" — showing the within-cell comparison the regression
performs. The room leaves the design slide with one thing: *I understand
how the comparison is being made.* Nothing else matters from this slide.

The failure mode is the *equation-on-screen* talk. Devon's first draft
included the full regression:

$$
\Delta\mathrm{Vol}_{i,t} = \alpha_i + \gamma_t + \beta \cdot \mathrm{ETF}_{i,t} + \mathbf{X}_{i,t}'\boldsymbol{\delta} + \varepsilon_{i,t}
$$

That is correct, and it is *unreadable from row eight in sixty seconds*. The
audience parses "$\Delta\mathrm{Vol}$" — they are now four seconds behind. They
parse "$\alpha_i$" — six seconds behind. They never make it to "$\beta \cdot
\mathrm{ETF}$" before Devon moves to the next slide. The equation belongs in
the paper, where a reader can re-read it. The slide gets the *sentence
version*: *"We compare a token's volatility before and after its spot ETF
launches, against the volatility of similar tokens that never got an ETF,
in the same month."* That sentence *is* the equation, decoded for ears.

There is one piece of mathematical notation that *does* belong on the design
slide, because it travels well: the *unit of variation*. Saying "the
within-firm-within-month variation is the comparison" on the slide, with the
firm and month fixed effects literally drawn as a small grid, gives the room
the *shape* of the comparison — across what dimension is the variation, and
across what dimension is it absorbed. The grid picture is sixty seconds
well spent because it answers, visually, the question "what is being
compared to what?" — which is exactly the question the design slide is for.

A rehearsal cue: stand in front of a mirror and try to say the design
sentence in one breath. If you can't, the sentence is too long, and you
will stumble on it under stress. Rewrite until one breath fits.

---

## 3. The identification punchline

This is the load-bearing slide. Everything else either prepares the room
for the punchline or rides on it. The punchline is the single sentence that
makes the room *believe the design works*. It is not a statement that the
design works; it is *evidence* that the design works, compressed to the size
the talk can hold.

What does "evidence that the design works" actually mean? It depends on the
design.

For a **difference-in-differences**, the punchline is *parallel pre-trends*,
shown as the event-study plot. The four flat coefficients before treatment
are the punchline; you point at them and say *"the treated and control groups
were moving in parallel for the four years before the change — they only
diverge at the change itself."* The plot is the punchline; the sentence is
the gloss.

For an **instrumental variable**, the punchline is *the first-stage F* and a
*one-sentence exclusion argument*. The plot is the first-stage scatter; the
sentence is *"the instrument shifts treatment by [magnitude], and it does so
through [mechanism] that has no plausible direct path to the outcome
because [specific institutional fact]."* You can't prove the exclusion; you
can only argue it; the punchline is the *clean, narrow* version of the
argument.

For a **regression discontinuity**, the punchline is the *binned scatter with
the visible jump at the cutoff* and a one-sentence *manipulation check*.
*"The McCrary density test shows no bunching at the threshold, so units
were not sorting around the cutoff in a way that would break the design."*
The picture is the discontinuity; the sentence is the it-isn't-fake clause.

For a **natural experiment**, the punchline is *the institutional detail
that gives you variation*. Sam, presenting on intraday momentum: *"The NYSE
closing auction at 4:00 p.m. and the opening auction at 9:30 a.m. are run
by different mechanisms, with different participants, so the correlation
between morning and afternoon returns cannot be a mechanical artifact of
the same trading system trading against itself."* That is the institutional
fact the design rests on, and putting it on the slide *is* the punchline.

The punchline has a specific feel when it lands: a quiet moment in the room
where the smartest person stops looking at their phone. That moment is not
accidental. It is the result of compressing the strongest piece of evidence
for your identification into a form a stranger can audit in nine seconds.
Nine seconds is the budget — the length of one slow breath plus a beat —
because the punchline lives inside the larger design slide and you cannot
give it more than that without losing the rhythm of the talk.

The most common failure of the punchline is *hedging*. The nervous speaker
says "*we hope the parallel-trends assumption holds*" or "*the instrument is
arguably exogenous*"; both are punchline-killing verbs. The strong-and-honest
verb is *to demonstrate*: "*we demonstrate parallel pre-trends in the four
years before treatment*", "*the instrument's exclusion rests on the fact
that [X]*". *Demonstrate* what you can demonstrate, and *argue* what you can
argue — but never *hope*, because hope is the verb the room hears as a
confession. (CONVENTIONS §1 again — *causal-language discipline*, lifted
from prose to slides.)

A useful test: ask a peer who has not read your paper to listen to the
design slide and the punchline slide back to back, then ask them in their
own words *what assumption your estimate depends on*. If they cannot, the
punchline failed to land, and the talk needs another rehearsal pass —
because the question period is going to fail at exactly the same point.

---

## 4. One picture: the headline result, visualized

Chapter 8.5 §2 made the case for *table-to-figure translation* in general;
this section is about the *one* picture, the result slide, where the
translation is non-negotiable. The result slide has one job: show *the
number*, with its uncertainty, in a form a listener can read at the speed
of speech.

The default choice is wrong almost always. Students default to a regression
table — five columns, four decimals, standard errors in parentheses —
because that is what their paper has and what their peers' papers have.
That table is the right object for a reader. It is the wrong object for a
listener. So you translate it, and the translation is governed by what
*shape* your headline has.

| if your headline is... | the picture is... | what the eye reads instantly |
|------|------|-----|
| a single coefficient with a CI | dot-and-whisker, the dot is $\hat\beta$, the whisker is the 95% CI | "is it different from zero?" and "how precise?" |
| a coefficient across specifications | coefficient plot — one dot/whisker per spec, lined up | stability as *shape*: a tight vertical cluster |
| a DiD or event-study | event-study plot — coefficients by period, flat-then-jump | parallel pre-trends *and* the treatment effect, in one image |
| an RD | binned scatter with the visible jump at the cutoff | the discontinuity is something you can see |
| a subgroup pattern | small-multiples bar chart, one panel per subgroup | the gap is bigger here than there, at a glance |
| a time series effect | overlaid line plot, treated vs. counterfactual, with shaded CI | divergence at the treatment date |

The result slide is one of these pictures. *Not a table.* Not even a "really
clean table." The slide has the picture, the picture has a one-sentence
title that *is the result* (CONVENTIONS-aligned: "*the denial gap falls 1.8
points after the regulation, and the fall is concentrated in algorithmic
lenders*"), the axes are labeled in plain English ("denial rate, percentage
points"), and the units of the headline are visible in the picture's
annotation — "$\hat\beta = -1.8$ pp, 95% CI $[-2.6,-1.0]$" — so the room can
read the number off the picture without you having to recite it.

```python
# nb9.2 — the headline result, as a publication-ready figure
# Reveal-the-trick: the figure that goes on the slide is the figure
# generated by the analysis code, never re-drawn by hand. Same code path
# as paper/figures/headline.pdf in the packet (Ch 8.5 §5).
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt
import numpy as np

rng = np.random.default_rng(20260815)        # seeded in config.py; identical figure every build

# the result: one estimate, one interval, plotted as a coefficient with whiskers
fig, ax = plt.subplots(figsize=(6.0, 3.5))    # tall enough to read from row eight
beta = -1.8
ci_low, ci_high = -2.6, -1.0
ax.errorbar(
    [beta], [0],
    xerr=[[beta - ci_low], [ci_high - beta]],
    fmt="o", color="black", capsize=4, markersize=8,
)
ax.axvline(0, color="grey", linestyle="--", linewidth=1)
ax.set_xlim(-3.5, 0.5)
ax.set_yticks([])                             # the y-axis carries no information; strip it
ax.set_xlabel("Change in denial gap (percentage points)")
ax.set_title("After the regulation: the denial gap falls 1.8 pp\n(95% CI [-2.6, -1.0]; clustered by lender)")
fig.tight_layout()
fig.savefig("paper/figures/headline.pdf")     # writes the SAME pdf that paper/talk.tex \includegraphics's
```

Two things about this code matter as discipline. *First*, the seed is the
same seed as the rest of the project (Chapter 8.5 §5), set in `config.py`,
not freshly invented for the figure — the figure is part of the
reproducible pipeline, not a one-off artifact. *Second*, the figure file
is the *same file* that the paper's LaTeX includes; the talk and the paper
share their figures, byte-for-byte, because the alternative — drawing
the figure twice and risking divergence — is exactly the kind of
hand-edit Chapter 8.5 §5 forbids.

The result slide carries a temptation: to show *more than one* result. Don't.
The single headline is the result; secondary results live in backup slides
(see §6 below) and in the paper. The room remembers one number from your
talk; choose it deliberately, frame it once, and let it sit there long
enough — five to ten seconds of silence after you say it — that the room
actually absorbs it. The silence is hard the first time; rehearse it.

---

## 5. Threats: the robustness slide, as a strike, not a defense

The threats slide is beat five of the arc, and Chapter 8.5 §1 already framed
its job: *show that the headline did not depend on a single arbitrary
choice*. This chapter sharpens the framing. The threats slide is not a
*defense*; it is a *pre-emptive strike*. The difference is rhetorical and
practical.

A defensive threats slide says: "*here are some other specifications, in
case you ask*". The room hears: *the speaker is bracing for trouble*. It
projects anxiety, and anxiety is contagious.

A strike-mode threats slide says: "*we tested the three choices a careful
reader would worry about — clustering, sample restriction, and the
fixed-effects specification — and the result moves by less than half a
standard error in every case*." The room hears: *the speaker already
thought about this harder than the questioner is about to.* The questioner
who was going to ask "did you try clustering by industry?" looks at the
slide, sees it on the spec curve, and asks something else. You have *used
up* a hostile question with a slide.

The practical move: pick the *three* robustness checks that the most
hostile reader of your paper would ask about, and show them on one slide,
together. The mechanism is the specification curve from Chapter 8.1 — a
column of dots-and-whiskers, one per specification, with a reference line
at zero and another at the headline. The eye reads the *shape* (the cluster
is tight, the cluster does not cross zero) faster than the brain can read
the labels. Below the curve, in one line, the sentence: *"across all 144
plausible specifications, the headline is within 30% of -1.8 pp; none
crosses zero."*

Sam's threats slide for intraday momentum showed three checks: (i) different
holding windows (10 min, 15 min, 30 min) — same direction; (ii) excluding
the 2008-2009 financial crisis — same direction; (iii) excluding the
fifty most-traded stocks — same direction. All three together as one
coefficient plot, labeled, with a zero line. The sentence under the plot:
*"the result survives every alternative cut we tried; it is not driven by
microstructure noise, by the crisis, or by the most heavily traded names."*
That sentence is a *strike*, because it *anticipates the three questions
the audience is most likely to ask*, and it answers them before they are
asked. A questioner who *was* going to ask about microstructure noise is now
looking at the slide and choosing a different question. Good. That is the
slide's job.

The discipline rule for this slide: **do not show robustness checks the
result does not pass.** A robustness check that *fails* is information you
must report in the paper (CONVENTIONS §6 — no quiet failures) and in your
threats table (Ch 7.5), but it is *not* a slide artifact. The slide is for
the checks you *passed*; the failures live in the answer to "did you check
$X$?" — where you say honestly, "*yes, and that one moves the headline by
half, which is why we treat the smaller subsample as the headline rather
than the pooled estimate.*" That answer is much stronger than burying the
failure; it shows you knew, and chose, and can defend the choice. But it is
an answer, not a slide.

---

## 6. The ask: what you want from the room

This is the move that distinguishes a competent talk from a memorable one.
Most empirical talks end with a *summary* — a recap of what you showed, a
restatement of the contribution, and a polite "thank you, questions?" That
is fine, and it is *insufficient*. The room just gave you eight minutes of
attention; they are now warm. The polite "thank you" is what you say if you
do not want to ask anything of them. The *ask* is what you say if you do.

The ask is one sentence at the end of the contribution slide, before the
"questions?" beat. It is specific. It is concrete. It is a thing the room
can actually do for you in the next ten minutes (during Q&A) or ten weeks
(after the conference). And it is *named*, so the room knows you mean it.

Three forms the ask takes, by stage of project.

**Form one: the* methodological ask*.** *"If you've worked with HMDA data on
fair-lending questions, I'd like to ask you in Q&A about whether the
matching on credit-score bands is doing what I think it's doing — I'm
not fully sure."* This is what Maya says, and it is powerful because it
publicly invites the most senior fair-lending researcher in the room to
*teach her in front of everyone*, which they will, because experts love
being asked the question that requires expertise. The cost is humility;
the payoff is *exactly the conversation she needs to have* — and she has
it, on the record, with the room as witness.

**Form two: the *data ask*.** *"I'm currently working with on-chain data
through 2024; if anyone has worked with the post-2024 wallet-clustering
heuristics, I'd love to compare notes after the session."* This is what
Devon says. It is a hallway invitation, made specific, with a named
technical hook. People who have what he is asking for will find him at
lunch. Without the ask, they wouldn't have known to.

**Form three: the *collaboration ask*.** *"This paper looks at U.S. property
insurance under wildfire risk; the natural next step is Australia, and I
don't have the institutional knowledge to do the Australia version alone.
If you do, I'd love to talk."* This is what Priya says. Sometimes the ask
*works* — somebody from the University of Melbourne walks up to her at the
poster session — and sometimes it doesn't. The downside is zero; the
upside is a collaborator she could not have found by emailing.

The ask is *not* "I'd love any feedback you have" — that is a non-ask, and
the room hears it as a closing pleasantry. The ask is a specific request,
named at the right level of granularity that the right person in the room
self-identifies and acts on it. Putting an ask in your talk is also a
useful discipline for *you*: it forces you to know, in advance, what kind of
help you need, which is itself a useful framing for the revision work that
Weeks 10-12 will do.

The ask sits at the end of the contribution slide, in italics, *under* the
"what we showed" sentence. It looks like:

> **Contribution.** We show that the denial gap falls 1.8 percentage points
> after the algorithmic-disclosure regulation, concentrated at lenders
> with the highest pre-period model intensity, consistent with a
> compliance-driven re-tuning channel.
>
> *Ask:* if you've worked with HMDA data on fair-lending questions, I'd
> like to ask you in Q&A about whether the within-credit-band matching is
> doing what I think it's doing.

Two sentences. Specific. Honest. Inviting. That is the close.

---

## 7. Backup slides, and the budget of the unsaid

The eight-minute talk has six slides, plus a title and an acknowledgments
slide that bracket the talk; that is the talk. But behind the talk, in the
deck, you carry *backup slides* — material you do not show but can flip to
if a question requires it. The backup slides are a credibility cache.

What goes in the backup. *The full regression table* the headline figure
summarizes, so when a questioner asks "what's the coefficient on size?",
you flip to it. *The full event-study plot* with all leads and lags, so
when a questioner asks "what about pre-trends in year minus eight?", you
flip to it. *The placebo specification*, so when a questioner asks "did you
run a placebo test?", you flip to it. *The institutional-detail figure*
that documents the natural experiment, so when a questioner asks "remind me
what changed in 2008?", you flip to it.

Backup slides are *labeled in the file*, so you can navigate to them — a
table of contents on slide 0, or just a habit of remembering "table B2 is
slide 23, the placebo is slide 25." The skill is to make the flip *visible*
— "let me pull up that table" — and *short*. The room reads the flip as a
signal that you *have the answer*, and you do; the backup slide is just
where you keep it.

The discipline that bounds the backup slides: **the backup is what you
*could* say, not what you *will* say.** You do not narrate the backup. You
do not anticipate which backup will be asked for; you carry them in case.
A talk with twenty backup slides and six live slides is well-prepared. A
talk with twenty *live* slides and six minutes is failed planning. The
budget of the unsaid is large; the budget of the said is six slides. Hold
the line.

---

## 8. Rehearsal: making the bones load-bearing

A talk is rehearsed three times against a timer, minimum. Chapter 8.5 §3
said this; Chapter 9.1 §1 said it again. This chapter adds the
*microstructure* of the rehearsal.

Pass one is **against a wall**, alone, at full volume. The goal is to
discover the sentences that do not survive being said out loud — the
five-clause sentence on slide 4, the technical term you mispronounce, the
transition into the punchline that does not have a natural breath in it.
Rewrite until every sentence can be said at full volume, in one breath,
without a stumble.

Pass two is **against a peer**, who does not know your paper. The goal is
to discover the gaps the peer reveals — *what didn't make sense*. They
will be more honest than your professor, because they have less to lose
and more to gain (their own talk will benefit from the same exercise).
After they hear it, ask them three questions, in order: *what is the
question I am answering? what is the comparison I am making? what is the
single number I want you to remember?* If they cannot answer all three,
something is wrong with the corresponding slide, and you find out which.

Pass three is **against the clock**, with your deck on the actual hardware
you will present on (or as close as you can get). Target 7:30. If you are
over 7:30, you cut — not from the middle, where the design lives, but from
the motivation, which is where the time leak is on every rehearsal
recording I have ever watched. Pre-decide the cut line (Chapter 8.5 §3) so
you don't improvise it on stage.

A useful exercise for pass three is to *record yourself on video*, watch
it back, and notice three things: where your voice goes up at the end of a
declarative sentence (an unconscious questioning intonation that the room
reads as uncertainty); where you say "um" more than once per slide (a
sign you have not internalized the transition); where you look at your
slides instead of the camera (which the room reads as "I am reading my
slides"). Each of these has a fix, and the fix only works if you saw
yourself do it. Eight minutes of video for eight minutes of talk is the
best rehearsal investment in the entire seventy-two-hour pre-flight.

---

## 9. The six beats together, as a single argument

Let us put the six beats next to each other one more time, and notice the
*shape* the talk takes when they are aligned.

| beat | slide | one-sentence content | beat does what |
|------|------|------|------|
| Hook | 1 | a concrete number / fact / puzzle the room cannot ignore | earns attention |
| Question | 2 | what we are asking, in one clean sentence | locates the scalpel |
| Design | 3 | the comparison we make, in one sentence, with one picture | makes the comparison auditable |
| Identification punchline | 4 | the *evidence* the comparison is fair, in nine seconds | makes the audience *believe* the comparison |
| One picture (the result) | 5 | the headline number, visualized, with its uncertainty | makes the answer legible |
| Threats | 6 | the spec curve / robustness panel + one sentence of stability | strikes the predictable hostile questions pre-emptively |
| Contribution + Ask | 7 | what we know now, what we don't, and one specific request | closes the loop; recruits the room |

Notice that the *load* is in beats 3 and 4 — the design and the
identification punchline. The headline (beat 5) is what the room *thinks*
they are listening for; the design (beat 3) is what they actually evaluate
you on. A talk that puts disproportionate care into the design and
punchline, and *less* care into the hook and the contribution, ends up
stronger than a talk that polishes the bookends and leaves the middle
hand-wavy. Polish the middle. The bookends carry less weight than they
feel like they do.

The deeper principle this chapter has been circling: **the eight-minute
talk is an act of compression, and what you compress is the *argument*, not
the *findings*.** The findings are in the paper. The argument is what you
came to deliver — *here is a comparison; here is why it is fair; here is
what it shows; here is what could break it; and here is what I want from
you.* When the six beats hold that argument, end to end, in eight minutes,
the talk works. When they don't, no amount of design polish on individual
slides saves it. Get the argument right first; *then* polish the slides.

---

## Your Turn

This chapter has two deliverables — one written, one performed — and they
are graded together.

- **nb9.2 — talk timer and arc-budget tool.** Build the six-slide deck (plus
  title, plus acknowledgments, plus backup), and run it three times against
  the notebook's stopwatch. The notebook writes a `paper/qa/rehearsal.log`
  with per-slide times and a flag for any slide more than 30 seconds over
  budget. Use the log to identify your time leaks; rewrite until the talk
  fits in 7:30.
- **PS 9.2 — the six-slide arc + dry-run video.** Submit the deck (PDF),
  the rehearsal log, and a 7:30 video of pass-three rehearsal. The
  rubric grades the *six beats* — does the hook earn attention? does the
  design slide name the comparison? does the punchline land? does the
  result picture replace a table? does the threats slide strike rather
  than defend? does the ask exist? — not the production value.
- **Lab 9, Phase B.** The recorded full-arc dry-run, watched on video
  with a partner, with each beat individually evaluated against the rubric.
  The partner asks three questions at the end: what was the question, what
  was the comparison, what is the headline number. If they cannot answer
  all three from the talk, find the slide that failed and fix it.

### A closing reflection

Of the six beats, *which is currently the weakest in your talk*? Be honest;
the rehearsal video tells you. Spend the largest single block of remaining
prep time on that beat, because the talk is bottlenecked at its weakest
beat, not its average. If the weak beat is the punchline (it usually is, for
empirical work), the fix is rarely the slide — it is the *sentence*. Rewrite
the punchline sentence until you can say it in one breath, with conviction,
and the picture under it is the cleanest piece of evidence your design
produces. The audience does not need to be convinced by everything you
show; they need to be convinced by *one thing*, and the punchline is that
thing.

---

### References

- McConnell, P. (2009). The Craft of Scientific Presentations. Springer.
  (The single-idea-per-slide rule; the title-as-sentence discipline.)
- Heath, C., & Heath, D. (2007). *Made to Stick: Why Some Ideas Survive
  and Others Die.* Random House. (Concrete-before-abstract as a delivery
  principle; the hook with a number.)
- Tufte, E. R. (2006). *The Cognitive Style of PowerPoint: Pitching Out
  Corrupts Within* (2nd ed.). Graphics Press. (The table-to-figure
  argument; why dense slides defeat live attention.)
- Doumont, J.-L. (2009). *Trees, Maps, and Theorems: Effective Communication
  for Rational Minds.* Principiæ. (The structural arc of a technical talk;
  beat-level discipline.)
- See also Chapters 7.5 (identification memo and threats table — the source
  of the design slide and the threats slide), 8.1 (specification curve —
  the visual for the threats slide), 8.2 (robustness battery — the content
  of the threats slide), 8.5 (the six-beat arc this chapter sharpens), and
  Ch 9.1 §3 (the anticipated-questions matrix — the prep that the threats
  slide pre-empts).
