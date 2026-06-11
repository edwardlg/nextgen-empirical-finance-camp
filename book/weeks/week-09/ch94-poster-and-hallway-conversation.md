# Ch 9.4 — The Poster and the Hallway Conversation: a Different Medium, a Different Argument Structure

The talk is over. Lunch is over. The poster session opens at two o'clock, in
the atrium with the bad lighting and the inadequate easels, and you are
standing next to a 36-by-48-inch piece of paper with your name on it for
the next ninety minutes. The natural temptation — and the one this chapter
exists to correct — is to think of the poster as *the talk, printed*. It is
not. **The poster is a different medium, and it carries a different
argument structure, because the listener interacts with it differently.**
Get the structural difference right and the poster session is the most
useful ninety minutes of the conference; get it wrong and you stand
awkwardly next to a wall of small font while interested people drift past.

Here is the move the chapter turns on. **The talk is a sequence and the
poster is a layout.** The talk runs on rails — slide one, two, three, the
audience cannot back up, cannot skim, cannot pause. The poster is a
*spatial* artifact: a viewer arrives, scans the whole surface in three
seconds, decides whether to engage based on what they see, and — if they
engage — *chooses their own path through the material*. The
viewer-chosen path means that every component of the poster has to make
sense *without* the other components being read first. That is a radically
different design constraint than the talk's "every slide builds on the
previous one." A poster that fights the medium — a poster that reads
top-to-bottom-left-to-right like a paper — fails because it asks the viewer
to be a *reader*, when the viewer is a *grazer*. Design for the grazer;
serve the reader only if asked.

This chapter has three threads. The poster itself, as a visual object with
a different argument structure. The hallway conversation, as a verbal genre
with its own beats — the elevator pitch, the one-minute version, the
five-minute version, the request-for-help. And the *coupling* of the two:
how the poster works *for you* during the conversation, as a prop, a
pointing target, and a memory aid. Get the poster right and the
conversations get easier; get the conversations right and the poster does
its job.

---

## 1. The layout: how a grazer reads a poster in three seconds

Imagine the poster session: thirty posters in a room, two hundred
attendees, ninety minutes. The arithmetic alone tells you the median
viewer spends *three seconds* on your poster before deciding whether to
stop. Three seconds is the budget. Your poster wins or loses in those
three seconds.

What can a person see in three seconds? They can see *the headline* (one
big sentence, top center), *the headline figure* (the picture from your
talk's slide five, sized as the largest object on the poster), and the
*shape* of the layout (where the sections are, whether it looks dense or
breathable). They do *not* read paragraphs. They do not read methodology.
They do not read your name. The three-second scan decides one of three
fates: *walk on*, *pause and read more*, *catch your eye and start a
conversation*. The poster's design exists to convert the second and third
of those at the highest rate possible.

The layout that converts best is what physicists and biologists have been
using for thirty years, with subtle variation for empirical economics. A
36-by-48-inch landscape poster, divided into a few large zones.

**The headline band.** The top six inches of the poster, full width. It
contains *one sentence* — your headline result, in the language CONVENTIONS
§1 demands: *concrete before abstract, a number before a Greek letter*.
Maya's: "*After the 2022 algorithmic-disclosure rule, the racial denial gap
in mortgage lending fell 1.8 percentage points — concentrated at the
algorithmic lenders the rule targeted.*" That sentence, in 60- to 72-point
type, is what a grazer sees from across the room. Below it, in smaller
type, your name, the institution (Costello College of Business, George
Mason University), and the paper's URL or QR code. That is the entire
headline band, and it has done 80% of the poster's work before the viewer
has stepped closer.

**The center figure.** The dead center of the poster, occupying the largest
single area, is *one picture*. Same picture as the talk's slide five — the
event-study plot, the dot-and-whisker, the binned RD scatter, the
small-multiples bar chart — sized so the picture is *legible from six feet
away*. This figure carries the headline visually; the grazer who reads the
headline band glances down at the figure and *sees* the result before they
have read any text. The figure has a caption in 28-point type, one
sentence: *"The denial gap (Black vs. white applicants) drops sharply at
the algorithmic-rule date, only at lenders with high pre-period scoring
intensity."* The caption is the gloss; the picture is the evidence.

**The four supporting zones.** Around the headline band and the center
figure, four supporting zones. They are *not* the IMRaD sections of a paper,
because IMRaD is for readers; they are *grazer-friendly chunks*, each
self-contained.

- **Top-left: the question.** Two to three sentences, in 24-point type.
  *What we asked and why it matters.* If the grazer is in the room because
  they care about the topic, this is what tells them yes. If they are not,
  they walk away here — and that is fine, that is the zone *filtering*
  doing its job.
- **Middle-left: the design.** Two to three sentences plus a small
  diagram. *How we made the comparison fair.* This is the identification
  sentence from Chapter 7.5, said the way a peer would say it in a
  hallway. The small diagram is the *unit-of-variation grid* from Chapter
  9.2 §2 — the visual showing what is compared to what, with what fixed.
- **Bottom-left: robustness.** A single specification curve (from Chapter
  8.1), with a one-sentence caption. *The result is stable across [the
  three choices we worried about most].* This zone is the *strike* from
  Chapter 9.2 §5, in spatial form.
- **Right column: implications + contribution.** Two to three sentences.
  *What the result implies; what we are not claiming; what would extend
  it.* This includes the *ask* from Chapter 9.2 §6 — the one specific
  request, in italics, naming what kind of conversation you want to have.

That is the entire poster. Six zones. Three minutes of careful reading,
end-to-end, by a viewer who has stopped to engage; three seconds of
scanning, headline-and-figure, by a viewer who is grazing. Both are
served, in the same artifact, by the layout.

A discipline rule. **A poster is not where you put more.** It is where you
put *less*, with *bigger type* and *more white space*. Every poster that
fails fails by being too dense — too small a font, too many sentences, too
many figures, too narrow a margin. The viewer's eye reads density as "*I
do not have time for this*" and walks on. Strip the poster like you strip
a slide; the test is the same — *if it is not load-bearing, it is not on
the poster*.

```python
# nb9.4 — poster layout helper
# Reveal-the-trick: the figures on the poster are the SAME files as the talk
# and the paper (Ch 8.5 §5), generated by the analysis code, never re-drawn.
# This notebook composes them into a single 36x48 layout for printing.
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt

# All measurements in inches; matplotlib uses figsize=(w, h) in inches.
poster_w, poster_h = 48, 36                       # landscape orientation, US poster standard

fig = plt.figure(figsize=(poster_w, poster_h))

# Headline band: top 6 inches, full width
ax_head = fig.add_axes([0.02, 0.85, 0.96, 0.13]) # left, bottom, width, height (fractions)
ax_head.axis("off")
ax_head.text(
    0.5, 0.6,
    "After the algorithmic-disclosure rule, the racial denial gap fell 1.8 pp\n"
    "— concentrated at the algorithmic lenders the rule targeted.",
    ha="center", va="center", fontsize=64, fontweight="bold",
)
ax_head.text(
    0.5, 0.1,
    "Maya Chen · Costello College of Business, GMU · paper: arxiv.org/abs/...",
    ha="center", va="center", fontsize=22, fontstyle="italic",
)

# Center figure: import paper/figures/headline.pdf (the same file Ch 9.2 §4 generated)
# Use matplotlib's image-read path or just leave a placeholder Axes the layout PDF includes.
ax_fig = fig.add_axes([0.30, 0.32, 0.40, 0.48])
ax_fig.axis("off")
ax_fig.text(0.5, 0.5, "[ paper/figures/headline.pdf goes here ]",
            ha="center", va="center", fontsize=20, color="grey")

# Four supporting zones (skeleton only; fill with real content from your paper)
zones = {
    "Question (top-left)":     [0.02, 0.55, 0.25, 0.28],
    "Design (middle-left)":    [0.02, 0.30, 0.25, 0.23],
    "Robustness (bottom-left)":[0.02, 0.04, 0.25, 0.23],
    "Implications + Ask (right)": [0.73, 0.04, 0.25, 0.78],
}
for label, rect in zones.items():
    ax = fig.add_axes(rect)
    ax.axis("off")
    ax.text(0.02, 0.95, label, fontsize=26, fontweight="bold", va="top")
    ax.text(0.02, 0.85, "[ ~3 sentences, 24-pt type ]", fontsize=18, color="grey", va="top")
    ax.add_patch(plt.Rectangle((0, 0), 1, 1, fill=False, edgecolor="grey", linewidth=1))

fig.savefig("paper/figures/poster.pdf")           # ships in the packet; reproducible from code
```

The code is a *layout* notebook — it composes the same figure files the
paper and talk use. The poster is *built* like every other artifact in the
project: from code, deterministically, with the same SEED. (Ch 8.5 §5 again
— bit-identical pipeline.) This matters because, six weeks from now, when
you need to update the poster for a different conference, you regenerate
it from the code rather than re-formatting in Illustrator. The discipline
is the same discipline; the medium is different.

---

## 2. The argument structure: layout *is* the argument

A talk has a *temporal* argument structure — beat one prepares beat two,
which earns beat three. The poster has a *spatial* argument structure — the
viewer's eye path through the layout *is* the argument, but they choose
the path. So you design the layout so that *any plausible eye path
produces a coherent argument*.

What does that look like in practice? Consider four plausible eye paths
through Maya's poster:

**Path 1: the headline grazer.** They read the headline band, glance at the
center figure, walk on. The headline + figure had to be self-contained,
because that is *all they got*. Maya's headline names the rule, the
effect, the direction, the magnitude, and the concentration — five facts
in one sentence — and the figure shows the same five facts visually. The
grazer leaves with a coherent (if shallow) understanding of the result.

**Path 2: the topic-interested reader.** They read the headline, then move
*left* to the question zone, then *down* to the design zone, then to the
center figure. Top-to-bottom on the left side. This is the path of a
reader interested in *the substantive question*: what was asked, how it
was studied, what was found. The left column has to flow as a *vertical
argument* because this reader will read it top-to-bottom, even though you
did not force them to.

**Path 3: the methods-interested reader.** They read the headline, glance at
the figure, jump down to the *robustness* zone (bottom-left) because that
is what a methods-attuned reader looks for first — *is this real?*. Then,
satisfied, they read the design zone and the question. This is a *bottom-up*
path, and the robustness zone has to be intelligible *first*, before the
reader has seen the design. So the spec-curve caption is self-contained:
*"144 plausible specifications; the headline is within 30% of -1.8 pp;
none crosses zero."* That caption stands alone.

**Path 4: the impact-interested reader.** They read the headline, then jump
to the *right column* — implications and ask. They want to know *who cares
and what's next*. This is the policy reader, the journalist, the senior
researcher scanning for talent. The right column has to be intelligible
*before they have read the design*, because they might not read the
design at all. So the implication sentence stands alone: *"a 1.8-point
reduction in the denial gap is a sixth of the total gap, and it's
identified to a specific policy lever a regulator could in principle
extend to auto lending."* That sentence carries the contribution without
the design context.

All four paths produce a coherent reading. *That is the design constraint.*
A poster where path 3 makes no sense without first reading path 2 is a
poster that loses the methods-attuned reader entirely. A poster where the
right column is incomprehensible without the left column is a poster that
loses the impact reader. The art of poster design is making every zone
*both* self-contained *and* connected to the whole, simultaneously. This
is harder than it sounds, and it is the work the second draft of your
poster will mostly do.

A diagnostic test for the poster — borrow it from web designers, where it
originates as the "*five-second test*": show your poster to five people who
have not seen the work, give them five seconds, take it away, and ask them
what the poster was about. If three of the five can name the *result*
(not the topic — the *result*), the headline band is doing its job. If
fewer than three can, the headline is too long or too abstract. Rewrite.
Then test again. Then print.

---

## 3. The hallway conversation: the three lengths

The poster session is, structurally, a *series of conversations*, not a
sequence of monologues. Each viewer who stops at your poster will, within
five seconds, give you a cue about which version of the talk they want:
the elevator pitch, the one-minute version, or the five-minute walkthrough.
You read the cue, you give them the version they want, you do *not* give
them a version they did not ask for. That last clause is the rule most
poster-presenters violate.

**The elevator pitch (15 seconds).** Someone walks up, makes eye contact,
and says "*what's the paper about?*" or just "*hi*". They want the
30,000-foot version. You give them, in fifteen seconds, *the question, the
finding, and the so-what* — one sentence each. Maya's:

> *"We study whether algorithmic mortgage lending widens or narrows
> the racial denial gap. A 2022 rule forced the algorithmic lenders to
> disclose their models — and after that, the gap fell by 1.8 percentage
> points, just at those lenders. It's the first quasi-experimental
> evidence that disclosure can move the gap, and a candidate channel
> for the CFPB's parallel rule in auto lending."*

That is 65 words, about fifteen seconds. The viewer now has a coherent
mental model — *question, finding, so-what* — and they decide whether to
ask for more. Most will say "*interesting, thanks*" and walk on; some will
ask a follow-up; a few will engage at length. *All three responses are
fine.* The elevator pitch is the filter, not the conversation.

**The one-minute version (60 seconds).** A viewer has stopped, scanned the
poster, and asks "*walk me through it*" or "*tell me more*". They are
giving you a minute. The structure is the six-beat arc from Chapter 9.2,
*compressed*: hook (10s) → question (5s) → design (15s) → result (15s) →
threat / robustness (10s) → ask (5s). You point at the headline band, the
question zone, the design zone, the center figure, the robustness zone,
and finally the right column, in roughly that order — *and the act of
pointing is the visual scaffolding*. The viewer follows your finger
through the poster, and the poster carries the argument while your voice
narrates it. This is the *coupling* of poster and conversation: the poster
is not background; it is your slide deck, deployed spatially.

Devon's one-minute version, on his crypto-ETF paper:

> *"[points at headline band] We ask whether the launch of a spot Bitcoin
> ETF changes the volatility of the underlying token. The intuition is
> that the ETF imports a new, more institutional class of trader, which
> should — depending on whom you ask — either stabilize or destabilize the
> spot market. [points at design zone] We compare the volatility of
> Bitcoin in the months before and after the January 2024 ETF launch
> against a synthetic control built from other large tokens with no ETF,
> using the donor-pool method. [points at figure] The volatility falls
> 18% relative to the synthetic counterfactual, statistically significant
> at conventional levels, and the fall persists through year-end. [points
> at robustness zone] It survives all the cuts you'd want — different
> donor pools, different windows, dropping FTX-aftermath months. [points
> at right column] We read this as evidence that institutional
> participation stabilizes rather than destabilizes the spot market —
> consistent with the older institutional-investors-as-noise-traders
> debate, against the more recent crypto-specific concern that ETFs
> import fast-money flow. The natural extension is the ether ETF, July
> 2024 — and that's what I'd love to talk about if you've worked on it."*

Roughly 215 words, paced to one minute. Notice the structure: it is the
six-beat arc, point-by-point on the poster, with the ask at the end. The
viewer now has the talk's content in distilled form, in a minute, and they
walk away with a clear picture. If they stay, you have the five-minute
version ready.

**The five-minute version.** This is what you give to the viewer who is
genuinely engaged — a fellow researcher who is going to ask substantive
questions. The five-minute version is the *one-minute version, extended at
the design and robustness zones*. You spend more time on the comparison
(the design zone gets two minutes instead of fifteen seconds), more time
on the threats (the robustness zone gets ninety seconds, including
naming the most plausible threat and your response), and more time on the
mechanism (the implications zone gets a minute, naming *why* you think the
result holds). The five-minute version *is* the talk, decompressed back
out, with the poster as the visual aid.

A discipline: do *not* give the five-minute version unprompted. The
viewer who wanted the elevator pitch will be lost in the design zone,
ten seconds in, because the elevator pitch was the *whole thing they
wanted*. Read the cue: if they asked "*what's it about?*", they want the
15-second version; if they said "*tell me more*", they want the 60-second
version; if they said "*walk me through the design*", they want the
5-minute version. Match the version to the cue. The poster session is a
sequence of correctly-matched versions, not a sequence of identical
monologues.

A second discipline: **let the viewer set the pace.** When you finish a
beat — the design zone, say — *pause*. The viewer's response tells you
which way to go. If they nod and ask about identification, go deeper into
the design. If they nod and ask about the result, move on. If they
*disagree*, engage the disagreement. The poster session is a conversation,
not a presentation; the most common failure is treating it as the latter.

---

## 4. The hallway, as a verbal medium

The poster session is one venue for the hallway conversation. The other
venues are the coffee breaks, the line for lunch, the walk between
sessions, and the bar in the evening. The genre is the same — a *brief,
chosen, mutual* conversation — and the skills transfer.

The genre has three beats. **The opener** — how you start a conversation
with someone you have not met. **The question** — how you get to a
substantive exchange in under a minute. **The exit** — how you end the
conversation gracefully when it has run its course.

**The opener** is, in the conference setting, almost always one of three
forms: *"I saw your talk on [topic], and I wanted to ask about [specific
point]"* — *"I'm working on [related topic], and I noticed your work on
[their topic] — what's the connection from your end?"* — or, if you have
not seen them present, *"I'm [Maya], working on fair lending — I noticed
your name tag and recognized your paper on [their topic]."* The opener is
*specific*: a named topic, a named point, a named connection. A generic
opener ("*nice to meet you, what do you work on?*") works at a bar but
fails at a conference, where the registry of attendees gives you the
information to be specific. Use it.

**The question** is what converts a polite exchange into a substantive
one. The best hallway questions are *small and concrete*: not "*what do
you think about my whole identification strategy?*" (too big, too needy)
but "*one thing I've been chewing on is whether the within-lender variation
is really doing what I think it's doing — your paper on the algorithmic-lending
literature uses a similar within-firm comparison; how do you think about
that?*" The small, concrete question has a high response rate because it
respects the other person's time and gives them a specific thing to
respond to. The big, vague question has a low response rate because the
respondent has to figure out *what you actually want to know* before they
can help, and they may not bother.

**The exit** is the part students most often handle badly. The conversation
has run its course; both parties know it; neither wants to be rude. The
graceful exit is *named*: "*I really appreciate the time — I'm going to
catch the next session, but I'd love to follow up by email if you have a
minute next week*" — and then *follow up by email next week*. The email is
the *whole point* of the hallway conversation, because the value of the
conversation is realized over weeks and months, not in the ninety seconds
you spent at the coffee station. The exit names the next step; the next
step is what makes the conversation matter. A conversation without a next
step is, retrospectively, a missed opportunity; one with a next step is a
nascent collaboration.

A practical move: carry a notebook (paper, in your pocket). Write down,
during the conversation, the *name, the substance, and the next step* —
three things, one line each, before you walk away. Memory will lose the
name within an hour; the notebook will not.

```
[poster session, 2:47 p.m., Sat]
- Prof. K (UMich, banking + ML), interested in *within-credit-band* matching;
  said her co-author has worked on similar identification for credit cards.
- Next: email Monday, attach the matching diagnostics from Appendix A.
```

That is three lines. Multiply by the ten conversations you'll have at the
conference, and you have a working list of follow-ups for the week. The
notebook is *the bridge* between the conference and the revision work of
Weeks 10-12; the bridge does not exist if you do not write it down.

---

## 5. The poster as a prop: pointing, body, position

The poster does work *for* you during the conversation. Use it.

**Pointing is the visual scaffolding.** When you describe the design, point
at the design zone. When you describe the result, *touch* the headline
figure — not just gesture toward it; place a finger near the y-axis crossing
or the cutoff line, the specific feature you are describing. The viewer's
eye follows the finger; the conversation gains a shared focus. Without
pointing, the conversation is two people standing next to a poster talking
about the poster; with pointing, the conversation is *in* the poster, and
the poster carries the load.

**Body position matters more than you think.** Stand slightly to the side
of the poster, not directly in front of it, so the viewer can see the
poster *and* you simultaneously. If you stand in front, the poster is
hidden when you speak, and the viewer has to choose between reading and
listening. If you stand too far to the side, you are physically detached
from the artifact and the gesture-pointing breaks down. The right position
is about ninety degrees to the poster's plane, close enough that your
gestures land on the relevant zones, far enough that the viewer can see
the whole layout when they want to. Try this in rehearsal; the right
position feels slightly performative the first time and natural by the
fifth.

**Eye contact with the viewer, not the poster.** This is the single
hardest physical discipline at a poster session, because *the poster is
the natural place for your eyes to go* — it is what you are talking about.
But the viewer is the person you are talking to, and a presenter who
looks at the poster while speaking signals *I am presenting to the poster*
rather than *to you*. Look at the viewer when you are speaking, with brief
glances at the poster when you point — the inverse of the natural impulse.
This takes deliberate practice; it is not automatic.

**Position for one viewer; position for two viewers; position for five.**
A single viewer gets the conversational angle described above. Two
viewers, side by side, get a slightly more open angle so both can see —
you stand a bit farther from the poster, gesture larger. Five viewers
(this happens; the poster session has a star-of-the-room effect when a
result is interesting) gets the *talk position* — you step back, the
viewers form a small arc, and the conversation becomes a brief
mini-presentation, with the poster as the screen. You shift between the
modes by reading the size of the audience; the size grows and shrinks
during the session, and your position adapts.

---

## 6. The success metric: not "did people stop?"

A common mistake is to judge the poster session by foot traffic — *how
many people stopped at my poster?* That is the wrong metric. The right
metric is *what conversations did I have, and what next steps did they
generate?* A poster session where five people stopped and three resulted
in named next steps is a better session than one where fifty people
walked past, glanced, and walked on.

What counts as a useful conversation? Three kinds.

**The substantive critique.** Somebody finds a real flaw in your design —
or a real strength you had not articulated — and tells you. This is gold.
You write it in the notebook, named, with the next step ("re-run the
robustness with industry fixed effects; email Prof. K on Monday with the
result"). The substantive critique converts directly into Week 10's
revision work via the feedback ledger (Ch 9.5).

**The lead.** Somebody points you to a paper you should know, a dataset
you have not seen, a person you should email. Devon, at the poster
session, was pointed to a 2022 working paper on ether liquidity that he
had missed in his literature review; he wrote it down, read it Sunday
night, and discovered that one of his robustness specifications was
exactly the test someone else had done with a different design. The lead
saved him a redundant paragraph in the introduction and gave him a
citation he needed.

**The collaboration thread.** Somebody says, in effect, "*I have what you
need*" — data, expertise, an institutional connection. These are
rarer than the first two, and they are the highest-value conversations
of the session. The rule, again, is to *name the next step* before the
conversation ends, and to *follow up within a week*. Most collaboration
threads die in the gap between conference and follow-up; the discipline
of the email-on-Monday is what saves them.

A failure mode: equating *stopping at the poster* with *the conversation
mattered*. Foot traffic is a noisy signal; the substance of the
conversations is the actual outcome. A presenter who tracks foot traffic
optimizes for the wrong thing (a flashier headline, more cartoony
figures); a presenter who tracks named next steps optimizes for what
actually matters (the depth of engagement).

---

## 7. After the poster: the same writing discipline

The poster session ends. You take the poster down. You roll it up. You
walk away. The same discipline as Chapter 9.3 §8 applies: *write down,
immediately, what you heard*. The notebook is the bridge to Chapter 9.5.
Every named conversation gets its own line; every named critique gets its
own row in the feedback ledger; every named lead gets logged as a citation
to chase. Twenty-four hours from now, you will have forgotten which
critique came from whom, and which lead was about what, if you have not
written it down. The poster did its work; now the notebook does.

A specific discipline: **before sleep that night, send three follow-up
emails.** Three is the right number — small enough that you can do it
when you are tired, large enough that you do not lose the most valuable
conversations to the fade. The three emails are: the most substantive
critique-giver (with the version-of-the-result-they-asked-about attached),
the most useful lead-giver (with a thank-you and a question about the
lead), and the most credible collaboration thread (with a specific
proposal for a next conversation). Three emails, three sentences each,
sent the same night. The conversion rate from conference contact to
working relationship is roughly an order of magnitude higher when the
follow-up happens within forty-eight hours; the curve drops sharply
after.

---

## 8. The poster and the talk as one continuous performance

Step back. The talk (Chapter 9.2) and the poster (this chapter) are not
two separate deliverables; they are *the same argument*, presented in two
media, to two slightly different audiences. The talk is presented
*synchronously* to a captive audience of fifty in a tiered classroom; the
poster is presented *asynchronously* to a self-selected audience of one
or two or five in a noisy atrium. Same argument, two media. The argument
is the six-beat arc — hook, question, design, identification punchline,
result, threats, ask — and the *function* of each beat is the same in
both media. What changes is the *interaction model*: the talk runs on
rails, the poster lets the viewer choose the path.

This means the work invested in Chapter 9.2 is *not duplicated* by the
work of this chapter. The slide-five figure becomes the poster's center
figure. The threats slide becomes the poster's robustness zone. The
identification punchline becomes the poster's design zone. The ask is
the same ask, in italics, in the right column. Every piece of the poster
*already exists* in your packet; the poster is a *reformatting* exercise,
not a *new content* exercise, and treating it as such saves you a
significant block of time the week before the conference.

The deeper claim — and this is the principle that organizes the whole
week — is that **every artifact of the research project is a different
projection of the same underlying argument, and the discipline is to
keep the projections consistent.** The paper is the longest projection;
the talk is the talk's projection; the poster is the poster's projection;
the elevator pitch is the elevator pitch's projection. They all share a
*spine* — the hook, the design, the punchline, the result, the threats —
and they differ only in the *granularity* at which the spine is
articulated. Get the spine right and every projection becomes easier;
get the spine wrong and no amount of formatting saves any of them.

---

## Your Turn

Two deliverables and a verbal exercise.

- **nb9.4 — poster layout helper.** Use the notebook to compose your
  poster from the figure files already in `paper/figures/` (no new
  figures invented — the discipline is reuse from the packet). Print at
  reduced size (11 x 17 in.) for a draft; print at full size (36 x 48 in.)
  for the conference. The notebook writes `paper/figures/poster.pdf`, which
  ships in the packet alongside the talk PDF (Ch 9.1 §1).
- **PS 9.4 — poster + 90-second elevator pitch.** Submit the poster PDF
  and a recorded ninety-second elevator pitch (audio is sufficient; no
  video required). The poster is graded on the *headline band* (does a
  grazer get the result in three seconds?), the *eye-path coherence*
  (do the four supporting zones each stand alone?), and the *ask* (is it
  specific?). The elevator pitch is graded on the question-finding-so-what
  structure and on whether it fits in ninety seconds.
- **Lab 9, Phase D.** The Phase D lab is the in-person poster session,
  recorded: a peer plays the grazer, you give the elevator pitch; the
  peer plays the topic-interested reader, you give the one-minute
  version; the peer plays the methods-attuned reader, you give the
  five-minute version. The recording is reviewed for the *cue-reading*
  skill: did you correctly match the version to the cue?

### A closing reflection

Walk up to your printed poster — full size, at the conference, or in a
hallway at school for the rehearsal — and stand six feet back. Look at
it the way a grazer would. Can you read the headline? Can you see the
result in the center figure? Can you tell, in three seconds, what the
paper is about? If the answer to any of those is no, your poster is too
dense or too abstract or too small. Fix it now. The conference grazer
will not, in the room, give you a second chance.

---

### References

- Briscoe, M. H. (1996). *Preparing Scientific Illustrations: A Guide to
  Better Posters, Presentations, and Publications* (2nd ed.). Springer.
  (The headline band; the eye-path; the typographical hierarchy of
  scientific posters.)
- Hess, G. R., Tosney, K. W., & Liegel, L. H. (2009). Creating effective
  poster presentations. *American Biology Teacher*, 71(1), 9–17. (The
  five-second test; zone-based layouts; the grazer model.)
- Krug, S. (2014). *Don't Make Me Think, Revisited* (3rd ed.). New
  Riders. (Web-usability principles that translate directly to poster
  scanning; the three-second decision model originates here.)
- Tufte, E. R. (2001). *The Visual Display of Quantitative Information*
  (2nd ed.). Graphics Press. (Data-ink ratio; small multiples; the
  discipline that the poster's center figure embodies.)
- Wainer, H. (1984). How to Display Data Badly. *The American
  Statistician*, 38(2), 137–147. (The negative-example tradition; what
  not to put on a poster, in case it tempts you.)
- See also Chapters 7.5 (identification memo — source of the design zone),
  8.1 (specification curve — source of the robustness zone), 8.5 §5 (the
  one-click packet — the poster is part of it now), 9.1 §1 (the deck-freeze
  — the poster freezes at the same time), 9.2 (the six-beat arc — the
  spine the poster reformulates spatially), 9.3 §8 (the after-the-talk
  notebook — the same discipline applies after the poster session), and
  9.5 (the feedback ledger — where the conversations of the poster session
  become inputs to Weeks 10-12).
