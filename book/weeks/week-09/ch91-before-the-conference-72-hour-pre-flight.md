# Ch 9.1 — Before the Conference: The 72-Hour Pre-Flight

This is the chapter pilots would write if pilots wrote about empirical research.
The seventy-two hours before you stand up to present are not a *continuation*
of the work; they are a different activity, with a different goal, that nervous
students almost always get wrong. The natural instinct — and it is wrong — is
to keep *improving the paper* right up until Saturday morning: one more
robustness check, one more sentence in the abstract, one more table polish.
What this chapter argues, and what every senior researcher you respect already
practices, is the opposite move. **At T-minus-seventy-two hours, you stop
improving and start hardening.** The work is done. Now the job is to make sure
nothing about the work *breaks* between now and the moment the room sees it.
Hardening looks like three things: you freeze the deck, you finalize the
replication packet so it is unimpeachable, and you build the anticipated-questions
matrix that turns the work you already did in Chapters 7.5 and 8.2 into a
script you can read from when the room is too loud to think.

Here is the move the chapter turns on, so you have it before the details.
**The night before the conference is the worst possible time to learn what you
do not know.** The pre-flight is how you find out, in private, with three days
to fix it, what would have ambushed you in public, with zero seconds to fix
it. Every checklist below has the same shape: *what could go wrong, what
signal would have told me, what do I do about it now*. You will be tempted to
skip steps because "of course it works." Pilots have a saying that applies
verbatim: *the airplane does not care how many hours you have on the type*. Run
the checklist. Then run it again.

---

## 1. The slide-freeze and why it is binding

Three days out, you cut the deck. Not "almost finalize" — *cut*. The slides go
into a file you commit, tag, and do not edit again. The tag is the literal,
git-enforced commitment that you will not be the speaker who is still moving
text boxes at the airport. Call the tag `deck-freeze`, point it at the commit
that produced the PDF you will actually project, and from that moment forward
the only thing you change about the talk is *what you say while it is on the
screen*. The deck is locked; the delivery is open. That is the discipline,
and it sounds dogmatic until you have watched a smart presenter blow a talk
because they rewrote slide 4 at 11 p.m. the night before and then forgot, on
stage, which version they had memorized.

The reason is not superstition. It is that **a talk is a motor skill**, and
motor skills compile slowly. Every time you change a slide, the seven or eight
times you have rehearsed the transition into that slide become noise — your
mouth has memorized a sentence that no longer matches what your eyes will see.
A talk you rehearsed five times against a frozen deck will run smoother than a
talk you rehearsed twenty times against a deck that drifted under you. Sam,
practicing the intraday-momentum talk, rewrote his headline slide three times
in the last week and on the day stumbled into a sentence from version one
while looking at version three; the stumble cost him eight seconds, and eight
seconds is two slides in an eight-minute talk. Freeze and rehearse, don't
polish and pray.

What "freeze" actually means, operationally, is four things. **First**, you
build the final PDF — not just the source — and check it into the repo, so
what you ship is what renders, and font-substitution surprises at the venue
projector are impossible. **Second**, you tag the commit (`git tag
deck-freeze`, `git push origin deck-freeze`) so the freeze point is
auditable. **Third**, you compute a SHA-256 of the PDF and write it into your
PS 9.1 submission; the hash is what proves your final talk was the one you
prepared, and it is the digital sibling of the `pap-filed` tag from Chapter
7.3 — the freeze is *the same kind of commitment device*, applied to the
delivery instead of the analysis. **Fourth**, you copy the PDF to two
places that will be in the room with you: a USB stick, and a cloud folder
you can pull from any browser. The Murphy's-law tax for skipping this is
roughly one conference per career, and the cost is unrecoverable. Pay the
two minutes.

The boundary between "freeze the deck" and "rehearse the talk" is where most
of the seventy-two hours go, and the proportion matters. Roughly, the first
six hours of pre-flight are hardening (this chapter); the remaining sixty-six
are rehearsal against the timer (Ch 9.2), question prep against the matrix
(§3 below), and sleep. *That last one is not a joke.* Cognition under
sleep deprivation degrades in exactly the dimensions a Q&A taxes — working
memory, retrieval speed, emotional regulation under hostile prompts. A
talk rehearsed five times on seven hours of sleep is delivered better than
a talk rehearsed ten times on four hours of sleep. Plan the schedule
accordingly; the last twenty-four hours of pre-flight include one early
night, not one late one.

```bash
# 72-hour mark: freeze the deck.
make slides                                  # rebuild PDF from .qmd / .tex from the same env as Lab 8
sha256sum paper/talk.pdf > paper/talk.pdf.sha256
git add paper/talk.pdf paper/talk.pdf.sha256
git commit -m "deck-freeze: 8-minute talk, conference vN.0"
git tag -a deck-freeze -m "Frozen for $(date -I) conference"
git push origin main deck-freeze
cp paper/talk.pdf ~/conf-backup/talk.pdf    # USB + cloud copy live OUTSIDE the repo
```

One thing the freeze *is not*. It is not a freeze on the *paper*. Chapter 8
already locked the paper at submission; the deck is a derivative of that
paper, and the freeze here is on the derivative. If — between freeze and
conference — you discover an *error* in the paper itself (a wrong sign, a
mis-cited number), you do not silently slip a fix into the talk. You stop,
fix the paper, rebuild the deck from the fix, retag with `deck-freeze-v2`,
and announce the change at the start of the talk. Hidden corrections are
how careers end. Open ones are how trust is earned. The freeze is a
discipline of *visibility*, not silence; nothing changes without leaving a
trace.

---

## 2. The replication packet, finalized

The packet is the second surface a skeptic touches (Chapter 8.5, §5). The
pre-flight is when you stop trusting that it works and start *proving* it
works, on a machine that is not yours. The standard, again, is from
Appendix D: **a stranger, on a fresh machine, runs one command and watches
every table and figure regenerate from raw data to final PDF.** Three days
out, you act as that stranger.

The honesty test has three steps, and they are sequenced for a reason.
**Step one: `make clean && make all` on your own machine.** This is the
weakest of the three tests — your own laptop has whatever lingering caches
the packet might secretly depend on — but it catches the dumb stuff: a hand-pasted
number you forgot about, a missing file in the manifest, a typo in the
Makefile. If this step fails, the packet was never real, and you have just
discovered the gap with three days to close it. Do this every day for the
three days; the discipline is to verify *continuously*, not once.

**Step two: clean clone, fresh env.** Open a new directory, `git clone` your
repo, build the conda env from `environment.lock.yml`, and `make all`. This
catches the "it worked on my machine because of something my machine had"
class of failure — a system-installed binary, a dotfile your repo reaches
for, a Python package you `pip install`-ed once and forgot to add. If the
fresh-clone build fails, your lock file is lying, and you have a few hours
of dependency archaeology to do. Better to do it now than to learn at the
Q&A that someone tried to clone the repo last night and got an `ImportError`.

**Step three: a friend, on a different OS.** Hand the repo URL to a peer who
has never seen the project and ask them to run `make all` and tell you what
happens. This is the *real* test, because it bundles every assumption you
made unconsciously — "of course they have Python 3.11", "of course they have
LaTeX", "of course they have a WRDS login" — and turns them into either
*documented prerequisites in the README* or *failures the peer reports back*.
Maya did this for her fair-lending packet and discovered that her README
said "pull HMDA data" but her code assumed the user already had a 4 GB cached
parquet file from a pull she did six weeks earlier; the data-pull step had
been silently skipped in every `make all` she ran for a month. She found it
at T-minus-sixty hours and fixed it. She would not have found it under the
spotlights.

```bash
# T-72 hours: the three-step packet audit.

# (1) Your machine, brutally clean.
make clean && make all
git status                                  # working tree should be CLEAN; if anything moved, find out why

# (2) Fresh clone, fresh env, in /tmp.
cd /tmp && rm -rf fresh && git clone https://github.com/yourname/yourpaper.git fresh
cd fresh
conda env create -f environment.lock.yml -n yourpaper-fresh
conda activate yourpaper-fresh
make all                                    # if this fails, the lock file is incomplete
sha256sum paper/main.pdf                    # should match the SHA you committed last week

# (3) A peer, on their laptop. You don't get to type for them.
#     They send you back: "I ran `make all`. Here is what I saw."
#     If what they saw is not "PDF in 12 minutes", the packet is not yet ready.
```

The bit-identical check matters. If your committed `paper/main.pdf` has SHA
`abc...` and the fresh-clone build produces a PDF with SHA `def...`, you have
*non-determinism in the pipeline*, and you need to find and fix it before
Saturday. The usual suspects are: a missing seed somewhere (Chapter 8.5, §5,
item 5 — `rng = np.random.default_rng(SEED)` everywhere), a timestamp in a
figure caption ("Generated on 2026-06-10"), or a LaTeX engine difference
(latexmk version skew). Find which, kill it, rebuild, recommit. The point
is not aesthetic; the point is that bit-identical reproducibility is the
*only* way a reviewer can tell whether *they* got the right answer when
they rerun your code. Without it, the packet is a polite gesture; with it,
the packet is a proof.

One important update to the packet at the pre-flight stage: **the deck
itself is now part of the packet.** Add `paper/talk.pdf` and the talk source
to the repo, add a `make talk` target to the Makefile, and include the
deck-freeze hash in the README. The reason is that someone in the audience
may ask, after the talk, "can I have the slides?" — and the answer should be
"clone the repo, tag `deck-freeze`, the talk is in `paper/talk.pdf`." That
is one command, the same command, the same discipline. Reproducibility is
not a property the *paper* has; it is a property the *whole bundle* has.

---

## 3. The anticipated-questions matrix

This is the load-bearing pre-flight artifact, and it is where the work of
Chapter 7.5 (the threats-and-responses table) and Chapter 8.2 (the robustness
battery) becomes a script you can run under pressure. The matrix is a single
spreadsheet — one row per anticipated question — with a structured prepared
answer in every cell. You author it in calm; you read from it in stress.

The reveal is simple and worth saying out loud: **the questions you will
get on Saturday were already written down, by you, weeks ago.** They are the
rows of your threats table. They are the columns of your specification curve.
They are the assumptions in your identification memo. The reason senior
researchers are unflappable at the microphone is not raw talent; it is that
they have *already seen the question, in their notes, before the questioner
asked it*. The matrix is how you steal that move.

The matrix has six columns. Walk them as a unit, because the *order* of the
columns is the order in which you should *say* the answer.

| col | name | what goes here |
|-----|------|----------------|
| 1 | **Question (the surface form)** | The question as a hostile-but-competent attendee would actually phrase it. Not "endogeneity"; "Aren't your treated firms just different from control firms in ways you can't observe?" |
| 2 | **What it's really attacking** | Translate the question to a row of your threats table (Ch 7.5) or a robustness choice (Ch 8.2). Name the threat by its threat-ID, so the lookup is mechanical. |
| 3 | **Why it's a fair question** | One sentence, spoken first in your answer, that grants the legitimacy of the worry. *"Yes — that's the natural worry, because [reason]."* This is the credibility move. |
| 4 | **What you did about it** | The specific test, design choice, or robustness check from your paper that addresses it. *"We checked X; you can see it on slide N / in Appendix B.2."* |
| 5 | **The residual concern** | What you still cannot rule out. *"What I can't fully exclude is [Z], though [bound]."* This is column 4 of the threats table, copy-pasted in. |
| 6 | **The retreat position** | If the questioner is right and the critique is fatal — what claim survives? *"If you don't buy the causal reading, the descriptive pattern is still [X], and that's worth knowing."* |

A row, in practice, for Priya's wildfire-insurance paper:

> **Q:** *"Aren't insurers leaving fire-prone counties for reasons other than
> wildfire risk — like declining property values?"*
> **(1)** Surface form: omitted-variable bias from confounding county trends.
> **(2)** Translation: Threat T3 from the identification memo — "differential
> pre-trends in unobservables correlated with wildfire exposure."
> **(3)** Fair question: *"Yes — that's exactly the worry, because the
> counties most exposed to fire are also disproportionately rural and
> losing population, and either alone could drive insurer exit."*
> **(4)** What we did: *"We tested it two ways. First, the event-study plot
> on slide 5 — the pre-treatment coefficients on insurer exit are flat in
> the four years before the fire-risk re-rating, so the divergence dates to
> the rating shock, not before. Second, in the appendix table, we re-estimate
> dropping all counties with population decline above 5% per year; the
> coefficient is within 0.2 standard errors of the headline."*
> **(5)** Residual: *"What I can't rule out is a county-specific shock
> coincident with the rating change — say, a contemporaneous water-rights
> ruling — that I haven't observed."*
> **(6)** Retreat: *"If you don't buy the causal reading, the descriptive
> finding — that insurer concentration in high-fire counties collapses
> within two years of a regulatory re-rating — is a robust pattern in its
> own right and worth the policy attention regardless of the channel."*

That is one row. You will write ten to fifteen of them. The discipline is to
*author the row before the question can ambush you*, because once you have
written the row, the live answer is not improvisation; it is *reading*. You
will not literally read — you will paraphrase, because reading aloud sounds
scripted — but the bones are there, and the bones are what fail when you are
nervous, not the phrasing.

How many rows? You target *at least* one row per threat in your Ch 7.5 table
(that is the floor — every threat you named is a question someone might
ask). Then add the predictable methodological questions: standard-error
clustering, sample selection, the choice of fixed effects, the cutoff used
for winsorizing, the seed of the bootstrap. Then add three "*so what*"
questions: why this matters, what the policy implication is, what would
change if your effect doubled. Then add three "*generalization*" questions:
does this hold in other settings, other periods, other markets. Then add
one *trap*: the question that, if the attacker is right, is *fatal* — and
write the retreat row for it explicitly. Total: usually twelve to twenty
rows. That is the matrix.

```python
# nb9.1 — anticipated-Q matrix scaffold
# minimal columns: question, threat_id, fair, did, residual, retreat
import pandas as pd

qmatrix = pd.DataFrame(
    columns=[
        "qid",            # Q01, Q02, ...
        "question",       # surface form, in attacker's voice
        "threat_id",      # link to threats_table.csv from Ch 7.5
        "fair_sentence",  # column 3 (~25 words)
        "did_sentence",   # column 4 (~40 words, names the slide or appendix)
        "residual",       # column 5 (~25 words)
        "retreat",        # column 6 (~30 words; blank if survivable, filled if potentially fatal)
        "severity",       # "survivable" | "fatal-if-right"
    ]
)
# Author at least one row per threat in your Ch 7.5 threats table, then expand.
# The matrix lives at paper/qa/anticipated_questions.csv and ships in the packet (yes, really).
qmatrix.to_csv("paper/qa/anticipated_questions.csv", index=False)
```

A note on *severity*: every row is tagged either *survivable* (a number
choice, a clustering option, a robustness sibling) or *fatal-if-right* (an
identifying-assumption attack). The taxonomy comes back in Chapter 9.3, §3.
The reason to tag at this stage is that **the fatal rows are the ones you
rehearse out loud**, because those are the rows where stumbling under
pressure is worst. The survivable rows you can answer cold; the fatal ones
you need muscle memory for, because the retreat sentence in column 6 is the
hardest thing in the talk to say, and it is hardest because it is the one
that requires you to publicly stop defending something you spent four
months building.

---

## 4. What can go wrong, and the pre-mortem

A pre-mortem is the discipline of imagining, in advance, the worst plausible
version of the talk and asking *what would have caused that*. It is not
catastrophizing; it is the empirical-research version of pre-flight, applied
to social rather than technical failure. Gary Klein, who introduced the
pre-mortem to organizational decision-making, argues that the move shifts
the cognitive frame from *defending a plan* to *finding its weaknesses* —
because the planner who looks at their own plan looking for what is *wrong*
sees things the planner looking for what is *right* will not. The shift is
small in description and large in effect: the same person, asked to imagine
that the talk has already failed and to explain *why*, generates a list of
risks that the same person, asked to imagine the talk going well, would
not have generated. The asymmetry is real, and it is what makes the
pre-mortem a useful discipline rather than a redundant one.

The goal is not to feel anxious; it is to feel *prepared*. Spend twenty
minutes, three days out, writing the following in your notebook. Do this
in *prose*, not as a list, because the prose forces you to articulate the
*chain* — what would have caused the failure, what signal you would have
seen, what fix is still available. A bullet list lets you off the hook
with a thin enumeration; the prose makes you commit.

*Imagine it is Saturday at 4 p.m. The talk went badly. List the three things
that caused it.* For most students, the answers cluster into the same
half-dozen categories, and each has a specific fix that can only be done
before the day.

**The projector did not render the deck correctly.** Fix: bring the PDF (not
the source), bring it on a USB and in a cloud folder, and arrive an hour
early to test it on the conference machine. This is the cheapest mitigation
on this list and the one most often skipped because "it'll be fine."

**You ran out of time before the result.** Fix: in rehearsal (Chapter 9.2,
§3), you discovered that minute six was where the time budget was leaking,
pre-decided the cut, and now the talk fits in seven minutes with two
minutes of slack. If you have not done this, do it tonight. (Recall the
target from Ch 8.5: rehearse to seven, deliver in eight — the spare minute
is your insurance, not your content.)

**A question hit a threat you hadn't matrix-ed.** Fix: the matrix from §3 is
deliberately oversized; you write fifteen rows and use ten, because the five
that don't get asked were still useful as warm-up, and they sometimes do get
asked. The "novel" hostile question rarely is — almost every question is a
variant of something already in your threats table.

**You bluffed an answer you didn't know.** Fix: the three honest answers
from Chapter 9.3 — *"I don't know,"* *"It's in the paper,"* *"Good point"* —
are scripted, rehearsed, and *practiced out loud* until they sound natural,
because under pressure the default human move is to manufacture confidence,
and you have to make the honest response the *easier* response by having
said it twenty times in private first.

**The headline number was wrong.** Fix: this is what the bit-identical packet
audit in §2 was for. If `make all` on a fresh clone produced the exact PDF
you are projecting, the number is the number. If it did not, you have an
emergency, and the emergency is to fix the discrepancy *before* the talk,
not to project a number that you can no longer reproduce.

**You forgot to credit a coauthor / mentor / data source.** Fix: the first
slide names the team and the data source, by name. The acknowledgments slide
at the end thanks the funders and the people who fielded your dumb questions.
These are sixty seconds of your time and they are the cheapest reputation
investment you will ever make.

**You arrived to a different schedule than you expected.** Fix: confirm,
with the chair by email, the *time*, the *room*, and the *talk length*
the day before. Conferences resequence sessions, room assignments shift
when AV equipment fails, talk lengths get adjusted when a speaker cancels.
The schedule you printed two weeks ago is not the schedule that holds; the
email confirmation the day before is. Ask the chair. Print the
confirmation. Bring the printout in case the venue Wi-Fi is unusable when
you arrive (which, periodically, it is).

**Your laptop ran out of battery, or your adapter did not fit the room's
projector cable.** Fix: bring the *charger*, bring the *USB-C-to-HDMI
adapter*, bring the *USB-A-to-USB-C adapter*, and bring the PDF on a *USB
stick* so the venue's machine can present without your laptop at all.
The total weight is about three hundred grams; the total cost is twenty
dollars; the failure mode it prevents is, every conference season, the
single most common live-presentation disaster. Pay the twenty dollars.

Write your three. Fix them. Sleep.

---

## 5. The day-of itinerary (and why you write it down now)

The last pre-flight artifact is the literal hour-by-hour itinerary for
conference day. You write this three days out because on the day itself you
will not be capable of planning; adrenaline narrows the planning window, and
a written plan is what stays useful when planning ability does not. The
itinerary is not a wish list; it is an audit trail of where you and the
deck are at every hour.

The itinerary's job is not to be precise; it is to be *present*. A
written-down hour-by-hour plan, even a slightly wrong one, runs in your
head as a stable anchor against the chaos of conference day; an unwritten
plan dissolves under the first surprise. Three days out, you have the
clearest view of the day you will ever have, because you are not yet
inside it; write the view down while you can still see it.

A template, with the actual hours filled in for an 11:00 a.m. talk:

```
06:30  Wake. Coffee. Eat actual food, not a granola bar.
07:30  Final rehearsal #1, full talk, against the timer. Target: 7:30.
08:15  Shower. Wear the shirt without the logo.
09:00  Travel. The deck is on USB + cloud + laptop.
09:45  Arrive venue. Find the session room. Locate the AV person.
10:00  Test projector. Open paper/talk.pdf from USB. Confirm aspect ratio
       (4:3 vs 16:9 — this has wrecked more talks than nerves have) and
       font rendering on the actual screen.
10:15  Sit in the back of the prior session, with water, not with notes.
10:50  Move to the front. Open deck. Plug in. Test clicker.
11:00  Talk.
11:08  Q&A. Matrix is on your tablet in the front row.
11:25  Done. Step off stage; drink water; do not check your phone.
12:00  Lunch. Sit with someone you don't know. (See Ch 9.4 on hallway.)
14:00  Poster session, if scheduled (Ch 9.4 details).
17:00  Hotel. Open notebook. Start the feedback ledger (Ch 9.5).
20:00  Eat. Sleep early. The ledger is not finished yet, but the day is.
```

Two notes on the itinerary that are not optional. First, the *projector
test* at 10:00 is not optional, ever, even at a venue you have presented at
before. Aspect-ratio surprises, color-profile surprises, font-substitution
surprises, and HDMI-adapter-missing surprises happen to senior researchers
every conference season. They take two minutes to test for and twenty
minutes to recover from, so test. Second, the *feedback ledger at 17:00* is
when the work of Chapter 9.5 begins — not the next morning, not Monday.
Memory of who said what fades within hours of the talk. The ledger is the
device that catches the fading; the itinerary is what reminds you to open
it before the fade.

A third note, less universal but worth flagging: the *meal pacing* on
the itinerary matters in a way that is invisible until it has gone wrong.
You will not be hungry at 6:30 a.m.; you will be ravenous at 11:30 a.m.;
the talk is at 11:00. Eat at 6:30 anyway. The Q&A demands working memory,
and working memory under low blood sugar is the single most modifiable
factor in how the questions go. The granola bar in your bag is not a
substitute for breakfast; eat protein, eat at the time you wrote down,
not at the time hunger arrives. The same logic governs water — sip
through the morning, not a single bottle at 10:45 — because being too
hydrated at exactly the wrong moment of an eight-minute talk is its own
small disaster. These are unromantic considerations and they make a
real difference; senior researchers who give one or two talks a month
have internalized them, and the internalization is what the itinerary
externalizes for you.

---

## 6. Pre-flight, all together

Three days out, the pre-flight is one decision and three artifacts. The
decision is the *freeze*: you stop improving the work and start hardening
the delivery, and you stop now, with three days to make the hardening hold,
not three hours. The three artifacts are the *frozen deck* (a tagged commit,
a SHA-256, a USB-and-cloud backup), the *audited packet* (one command, bit-identical
rebuild, a peer-tested fresh clone), and the *anticipated-questions matrix*
(twelve to twenty rows, severity-tagged, with the fatal rows rehearsed out
loud). With those three, you walk into the room *not* as a person who hopes
the work holds up — you walk in as a person who has already stress-tested
exactly how it could fail, with three days of slack to fix what showed up.

The deeper claim — the one this whole chapter wants to install — is that
**every research delivery is a system, and systems are made reliable by
discipline, not by talent.** A great talk does not happen because a great
talker walked into the room; it happens because a careful researcher
pre-mortemed the failure modes, wrote them down, fixed the fixable ones,
and rehearsed the ones that could not be fixed in advance until the
response sounded natural. The talent shows up *during* the talk; the
discipline shows up in the seventy-two hours before, when nobody is
watching.

Chapter 9.2 is what you say. This chapter was what you do so that what you
say lands. They are inseparable; together they are the talk.

---

## Your Turn

The pre-flight is a checklist, and a checklist that isn't run is no checklist
at all. Do all three.

- **nb9.1 — pre-flight runner.** Walk it end-to-end, three days before any
  real talk you give: freeze the deck, compute the SHA, tag the commit; run
  the three-step packet audit (own machine, fresh clone, peer); author the
  anticipated-questions matrix with at least one row per row of your Ch 7.5
  threats table. The notebook records, in `paper/qa/preflight.log`, the
  exact timestamps and SHAs — so if anything moves between freeze and
  presentation, the log shows it.
- **PS 9.1 — pre-flight packet.** Submit the deck-freeze hash, the
  fresh-clone rebuild log (with timing), the peer's report from the
  fresh-clone test, and the anticipated-questions matrix CSV with at least
  one row per threat-ID.
- **Lab 9, Phase A.** The first phase of the Week 9 lab is the literal
  three-day pre-flight, run against your actual talk for the conference.
  The lab's deliverable is the *audit trail*: the three-step packet log,
  the matrix, the itinerary. You are graded on the discipline, not on the
  talk yet — the talk is Phase B.

### A closing reflection

Ask yourself the pre-mortem question, in writing, before you close the
chapter: *if my talk on Saturday goes badly, what are the three most likely
causes — and which of those three can I still fix in the next seventy-two
hours?* Then fix them. The act of writing the three down is itself most of
the work; the fixes, once named, are usually small. The cost of skipping
this question is a Saturday afternoon you cannot get back.

---

### References

- Gawande, A. (2009). *The Checklist Manifesto: How to Get Things Right.*
  Metropolitan Books. (Aviation pre-flight as a template for high-stakes
  delivery; the "checklist that catches the things a smart person would
  catch *if they remembered to think about it*.")
- Klein, G. (2007). Performing a Project Premortem. *Harvard Business
  Review*, 85(9), 18–19. (The pre-mortem method, applied here at §4.)
- Olken, B. A. (2015). Promises and Perils of Pre-Analysis Plans.
  *Journal of Economic Perspectives*, 29(3), 61–80. (Pre-commitment as
  a discipline; the `pap-filed` tag of Chapter 7.3 generalizes to the
  `deck-freeze` tag here.)
- Reinhart, A. (2015). *Statistics Done Wrong: The Woefully Complete
  Guide.* No Starch Press. (Multiple-testing and reproducibility
  failures that the packet audit is designed to prevent.)
- See also Chapters 7.3 (pre-analysis-plan as commitment device), 7.5
  (identification memo and threats-and-responses table — the seed of the
  anticipated-questions matrix), 8.2 (robustness battery — the source of
  the "we checked" answers), and 8.5 (the eight-minute talk and the
  one-click packet — the work the pre-flight protects).
