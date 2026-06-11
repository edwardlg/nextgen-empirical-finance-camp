# Ch 9.5 — After the Conference: Capturing Feedback in 24 Hours — the Feedback Ledger and the Triage Rubric

It is Saturday evening. The conference is over. You delivered the talk. You
stood by the poster. You answered the questions, you took the critiques,
you had four hallway conversations that mattered and six that did not. You
are tired in a way that is specific to academic conferences — the depleted
attention of having performed credibility for nine hours straight — and
you want, more than anything, to close the notebook, eat, and sleep. This
chapter is about what you do *before* you do that, and why what you do in
the next twenty-four hours determines whether the conference produced an
outcome or merely an experience.

The reveal of the chapter, said plainly so you can act on it before
fatigue makes you generous with yourself: **the feedback from a conference
is a perishable asset.** Within twenty-four hours, fifty percent of what
you heard is gone — not forgotten exactly, but unrecoverable in the
specificity that makes it useful. *What* the critique was, you may still
remember; *who* said it, you probably do not; *the exact framing they used
that made the critique sting*, you certainly do not, and the framing is
where the operational signal lived. The work of this chapter is to *catch
the perishable asset before it perishes*, organize it into a structure
the next four weeks of revision (Phase 3 of NextGen, Book Weeks 10-12)
will consume, and convert the chaos of Saturday's experience into the
agenda of Monday's work.

There are two artifacts. The **feedback ledger** is the literal write-down
of everything you heard, while you still remember it, structured for
retrieval. The **triage rubric** is the discipline you apply on Sunday —
twelve hours after the ledger — that decides which items in the ledger
become Week 10 work, which become later-paper material, which become
follow-up emails, and which (this is the hardest call) are politely
ignored. Together they convert the conference's noise into a four-week
plan. Without them, the conference fades; with them, the conference
becomes the most efficient input the project will ever receive.

---

## 1. The feedback ledger: what it is, what goes in it

The feedback ledger is a single CSV file — or, if you prefer, a single
plaintext document with consistent structure — that you author *the
evening of the conference and the morning after*. It has one row per piece
of feedback. The row structure is the load-bearing part, because the
structure is what makes retrieval possible later. Use the columns below.

| col | name | what goes here |
|-----|------|----------------|
| 1 | **fid** | A unique identifier, F01 through F-whatever. Used for cross-references in the triage and in your Week 10 task board. |
| 2 | **when** | The moment the feedback arrived: "during talk Q&A", "post-talk approach", "poster session 2:47 p.m.", "lunch with [name]", "lobby Sunday morning". Specific enough that you can reconstruct the context six weeks later. |
| 3 | **who** | The person, named, with affiliation and (ideally) research area. If you don't know the name, the *description* — "tall man in row 4, asked about clustering" — until you can fill in the name from the conference program. Anonymous feedback is weaker than named feedback, but it is not useless; record it anyway. |
| 4 | **verbatim** | The feedback as close to *the exact words used* as you can reconstruct. Not a paraphrase. Not a summary. *Their words*. This is the column that has the highest perishability, and it is the column with the highest downstream value, because the exact framing is where the operational signal lives. |
| 5 | **translation** | What the feedback *means*, in the language of your paper. "*Are the treated and control firms differing pre-treatment*" translates to "*pre-trends threat T3 on the identification memo*". This is the column you fill in Sunday, after sleep — not Saturday, when you are tired. |
| 6 | **bucket** | A through H, the taxonomy from Chapter 9.3 §2. Same eight buckets — number-choice, identification-attack, mechanism, generalization, motivation, data-construction, methodology-curiosity, out-of-scope. The bucket determines the triage move. |
| 7 | **severity** | "Critical", "important", "minor", "courtesy". The severity rubric is §3 below; do not try to fill it Saturday. |
| 8 | **next step** | What you will do about it, with a target date. "Run within-industry FE robustness; report Wednesday." "Email Prof. K Monday with Appendix A excerpt." "Cite in revised intro; defer to Week 11." "Acknowledge in personal thanks; no action needed." |

Eight columns. The first four you fill *Saturday evening*, with the
information at its freshest. The last four you fill *Sunday morning*,
after you have slept and the temptation to over-react has cooled. The
sequencing is intentional, and §4 below explains why.

```python
# nb9.5 — feedback ledger emitter
# Reveal-the-trick: the ledger is a CSV that the triage rubric later
# joins to your Ch 7.5 threats table on threat-id. Structure now, retrieve later.
import pandas as pd
from pathlib import Path

LEDGER_PATH = Path("paper/qa/feedback_ledger.csv")

# Initialize on conference evening, if not already present.
if not LEDGER_PATH.exists():
    pd.DataFrame(columns=[
        "fid", "when", "who", "verbatim",
        "translation", "bucket", "severity", "next_step",
    ]).to_csv(LEDGER_PATH, index=False)

# Append a row (called repeatedly through the evening as you remember things).
def log_feedback(fid, when, who, verbatim,
                 translation="", bucket="", severity="", next_step=""):
    df = pd.read_csv(LEDGER_PATH)
    df.loc[len(df)] = [fid, when, who, verbatim, translation, bucket, severity, next_step]
    df.to_csv(LEDGER_PATH, index=False)
    return fid

# Saturday evening: fill the FIRST FOUR columns only. Sleep on the rest.
log_feedback(
    fid="F01",
    when="talk Q&A, ~11:14 a.m., second question",
    who="Prof. K. Park, UMich, banking + ML (recognized from name tag)",
    verbatim=(
        "I'm not sure your within-credit-band matching is doing what you "
        "think it's doing — credit bands are coarse and lenders self-select "
        "across them. Have you looked at within-FICO-bin rather than within-band?"
    ),
)
```

The CSV format matters. It matters because the ledger is *queryable* —
on Sunday you filter by bucket, on Monday you filter by severity, in
Week 10 you join it to the Ch 7.5 threats table on threat-id. A
Word document is not queryable; a notebook scribble is not queryable; a
CSV is. Use the CSV format, ugly as it looks compared to your prose. The
discipline of structured retrieval is what makes the ledger an asset
rather than a souvenir.

---

## 2. The Saturday-evening protocol: the first pass

Saturday evening, you sit down with the ledger and you do *not* try to be
clever. You do one thing: you write down everything you can remember, in
the first four columns, before you go to sleep. The discipline rule:
*quantity, not quality*. A row with a half-remembered verbatim is more
useful than no row. A row with the wrong name is more useful than no row
(you can fix the name from the conference program tomorrow). A row that
turns out, on reflection, to be a minor courtesy is more useful than no
row — because the *fact that it was minor* will only be visible in
comparison to the rows that were not. You record everything; the triage
is tomorrow's problem.

A practical sequence for the Saturday-evening pass.

**Pass one: the talk Q&A, by question.** Walk through the question period
in your memory, in order, and write down every question you got. For each
one, the rough verbatim and the questioner if you know them. Do not
worry yet about which were good questions; capture them all. Most students
remember the first two questions and the last one vividly, and the middle
three or four as a blur — which is normal, because the middle is where
adrenaline is highest. *Try* to remember the middle. If you cannot
reconstruct the middle, that itself is a data point — *the middle
questions are gone* — and it is a reason to record audio of future talks
if the venue permits, because the middle questions are often the most
substantive.

**Pass two: the post-talk approaches.** Three to five people came up to
you in the minute after the talk. List them. For each, the substance of
what they said. (Your pocket notebook from Chapter 9.3 §8 should have
captured these already; transcribe from notebook to ledger.)

**Pass three: the poster session conversations.** Go through your
pocket notebook (Chapter 9.4 §4); every line in it becomes one or more
rows in the ledger. The substantive critiques, the leads, the
collaboration threads. Transcribe verbatim — *what they said*, not what
you concluded.

**Pass four: the overheard and the indirect.** Sometimes the most
revealing feedback is what you heard *not* in conversation — what a
fellow student told you they overheard, what the chair mentioned in
passing, what one audience member said to another as they filed out.
These items are weaker (third-hand) but record them too, flagged in the
*who* column as "overheard, indirect" so the triage knows to weight
them appropriately.

**Pass five: your own thoughts.** This is the part most students skip
and that matters most. Your own *reflections* — what you noticed while
delivering, what you wished you had said, what you would change — are a
form of feedback, and they are the rawest, freshest version of it. Each
one becomes a row in the ledger, with *who* = "self-reflection" and
*verbatim* = the thought, written down in your own words. Devon's row,
that evening:

> *fid:* F23
> *when:* self-reflection, Saturday evening, hotel
> *who:* self
> *verbatim:* "I rushed the design slide. I felt the time pressure at
> minute three and skipped the unit-of-variation grid I had practiced.
> The two questions that followed — about whether the synthetic-control
> donor pool was reasonable — would not have been asked if the design
> slide had landed."

That row is a useful row. It identifies a delivery failure (skipped a
slide element under pressure), connects it to downstream consequences
(two questions that would not have been asked), and seeds a *rehearsal
correction* for the next conference. It is also, frankly, the kind of
honest self-assessment that students often avoid because it stings. It
stings the most on Saturday evening, when the talk is fresh; that is
exactly why you should write it now, while you can.

Total time for the Saturday-evening pass: ninety minutes, give or take.
You will resist the ninety minutes — *I just want to sleep, I will do this
in the morning* — and the resistance is what the chapter exists to defeat.
The morning is too late. By morning, the *verbatim* column is half noise.
Do it tonight.

A practical mercy: you do *not* need to think on Saturday evening. You
need to *transcribe*. The thinking is Sunday. The split between transcription
and thinking is what makes the protocol survivable when you are tired.

---

## 3. The Sunday-morning protocol: the triage rubric

You woke up. Coffee. The ledger has thirty-some rows in it from last
night, with the first four columns filled in (sometimes well, sometimes
badly). Today's job is the last four columns: *translation*, *bucket*,
*severity*, *next step*. This is the triage, and it converts the ledger
from an archive into a work plan.

**Step one: translation.** For each row, in the *translation* column,
write what the feedback *means in the language of your paper*. Prof.
Park's question about within-band versus within-FICO-bin matching
translates to: *"the matching procedure in §3.2 may be too coarse —
within-band matches may not be apples-to-apples if lenders sort across
bands. Need to re-estimate at finer FICO granularity, or test sensitivity
to band definition."* The translation is what your *thesis-advisor self*
would write — it is the question, decoded into the operational language
of the paper. If you cannot write a translation, the row is either too
vague to act on (mark *translation* = "unclear; revisit with peer") or
out of scope (mark *translation* = "outside paper's design").

**Step two: bucket.** Tag each row with one of the eight buckets from
Chapter 9.3 §2. The bucket determines the *kind* of response the row
might require. A B (identification-attack) row is potentially a
revision-of-the-design row; an A (number-choice) row is potentially a
robustness-table row; an E (motivation) row is potentially an
intro-and-conclusion row; an F (data) row is potentially an
appendix-tightening row. The buckets are the project-management
abstraction over the feedback. Tag them.

**Step three: severity.** This is the hardest column, and it is what the
triage rubric exists for. There are four levels.

> **Critical** = "if this critic is right, the headline doesn't survive.
> Must address before any further dissemination of the paper. Top priority
> for Week 10."
>
> **Important** = "the paper is meaningfully better if I address this.
> Strong incentive to fix in Weeks 10-12, but not blocking on its own."
>
> **Minor** = "a smart point that improves the paper at the margin. Fix if
> there is time in Weeks 10-12; otherwise note for the next revision
> round."
>
> **Courtesy** = "a question or comment that didn't require an answer
> beyond the moment. No paper-side action; possibly a personal thank-you
> if the conversation was substantive."

The severity rubric has decision rules, not vibes. Apply them.

- **A row is Critical if and only if** the threat, if confirmed, would
  break the *identifying assumption itself*. (Chapter 8.5 §4's
  *fatal-vs-survivable* distinction.) These are the Bucket B rows where
  the threat is *unaddressed* by existing robustness, *plausible* given
  the design, and *testable* (or, if untestable, requires a *retreat*
  rather than a fix). Critical rows are rare; most posters and talks
  produce zero or one of them. If you have a Critical row, Week 10
  begins with it.

- **A row is Important if** the threat is real and addressable, but the
  *direction* of the consequence is unclear or limited — a number that
  might move, a robustness specification you should add, a clarification
  that strengthens an existing argument. Most Bucket B rows that are
  *already covered by existing robustness* but *not surfaced clearly in
  the paper* are Important: the fix is presentation, not analysis. Most
  Bucket F (data) rows that flag a documentation gap rather than an
  analytical one are Important. These are the bulk of Week 10-11 work.

- **A row is Minor if** the fix is a single sentence in the paper, a
  citation to add, a paragraph to tighten. These are the polish layer of
  Week 11-12 — important in aggregate, low in individual cost.

- **A row is Courtesy if** the conversation served a *relational* purpose
  rather than a *paper-improvement* one. The person who asked about
  motivation because they wanted to understand the substantive area; the
  person who pointed out a related paper just to be helpful; the person
  who asked an out-of-scope question because they were thinking out loud.
  These are *not* worthless — they are relationship rows — but they do
  not produce paper revisions.

The rubric is decision rules, not feelings. Apply them honestly, including
to the rows where you would prefer a higher severity ("*this seemed
critical at the time*") and the rows where you would prefer a lower one
("*this was uncomfortable to hear; I will downgrade*"). The rubric exists
*precisely* to short-circuit the emotional reaction, because the emotional
reaction Sunday morning is the wrong reaction to plan Week 10 from.

**Step four: next step.** For each row, what you will do about it, with a
*target date*. The structure is the same as a task tracker: a verb, an
object, an owner (always you, for now), a date. *"Re-estimate Table 3
with within-FICO-bin fixed effects in place of credit-band matching;
target Wednesday."* *"Email Prof. K with Appendix A.4 excerpt and a
specific question on her credit-cards paper; target Monday."* *"Add
citation to Park (2024) in §2.3 intro; target Week 11 polish pass."*
*"Acknowledge in personal thanks; no further action."* Every row has a
next step; the next step has a date. Rows without a next step are
incomplete rows; if you genuinely cannot decide what to do, the next
step is *"discuss with mentor in Week 10 office hours"* — but that is
still a next step, with a date.

```python
# nb9.5 — triage emitter
# Reveal-the-trick: the triage filters the ledger to a four-week task board,
# joined on threat-id to the threats table (Ch 7.5) where applicable.
import pandas as pd

df = pd.read_csv("paper/qa/feedback_ledger.csv")
threats = pd.read_csv("paper/identification/threats_table.csv")  # from Ch 7.5

# Tag rows that map back to existing threats (Bucket B usually), so we know
# which threats now have post-conference reinforcement.
df_b = df[df.bucket == "B"].merge(
    threats[["threat_id", "threat_name", "current_response"]],
    left_on="translation", right_on="threat_id", how="left",
)

# Pull the Critical and Important rows into a Week 10-12 task board.
todo = df[df.severity.isin(["Critical","Important"])].sort_values(
    ["severity","next_step"]
)
todo.to_csv("paper/qa/week_10_12_taskboard.csv", index=False)

# The Courtesy rows go to a separate "follow-ups" file for the Monday emails.
followups = df[df.severity == "Courtesy"]
followups.to_csv("paper/qa/followups.csv", index=False)

print(f"Critical: {(df.severity == 'Critical').sum()}")
print(f"Important: {(df.severity == 'Important').sum()}")
print(f"Minor: {(df.severity == 'Minor').sum()}")
print(f"Courtesy: {(df.severity == 'Courtesy').sum()}")
```

A typical, healthy distribution for a student conference talk: 0-1
Critical, 4-8 Important, 8-15 Minor, 5-10 Courtesy. If you have 5+
Critical rows, you may be over-reading the severity (everything looks
critical in the day-after glow of having been challenged); take a walk
and re-apply the rubric tomorrow. If you have 0 Important rows, you may
be under-reading; the conference almost always produces *some* Important
work, and a zero count usually means the rubric is being applied too
narrowly. The distribution shape is itself diagnostic.

---

## 4. Why Saturday-evening + Sunday-morning, in that order

The split between the two passes — *transcribe Saturday, triage Sunday* —
is the load-bearing process discipline of this chapter. The reasons are
worth saying explicitly so you know not to collapse them.

**The verbatim column is perishable; the bucket column is not.** *What
they said* fades within twelve hours; *which bucket the question fits*
can be classified just as well twelve hours later, when you are rested.
So the Saturday pass captures the perishable, and the Sunday pass
applies the rubric. Doing the Sunday pass on Saturday produces a worse
triage because you are tired; doing the Saturday pass on Sunday produces
a worse ledger because you have lost the verbatims. Each pass on its
proper day.

**Severity reactions are biased by fatigue, in the wrong direction.**
Tired-you over-rates severity, because the questions still feel sharp
and the answers still feel inadequate. Tomorrow-you, rested, rates more
honestly. A row that feels Critical at 9 p.m. Saturday often becomes
Important by 10 a.m. Sunday and Minor by Wednesday. *That cooling is
not denial; it is calibration.* The Sunday pass is when the calibration
happens, and it is what makes the triage usable. If you collapse Sunday
into Saturday, you bake the over-reaction into your Week 10 plan, and
you spend the first week of revision chasing severity that wasn't there.

**Sleep is a feature of the process, not an obstacle to it.** Cognitive
research on memory consolidation is consistent on this point: the
overnight gap is where Saturday's *episodic* memory (specific
verbatims, specific faces) is converted into *semantic* memory (the
abstract content of the critique). The semantic version is exactly what
the triage needs, and you cannot synthesize it without the gap. Trust
the gap.

The reverse direction also matters. The Sunday pass should *not* be
postponed to Monday or later, because the ledger's *translations* depend
on the verbatims still being fresh enough to interpret. By Tuesday, the
verbatims read as cryptic to your own eye — you cannot reconstruct what
the questioner actually meant — and the translation column degrades.
Sunday morning is the operational window. Block it on your calendar
*before* the conference, not after.

---

## 5. The Monday emails

Among the rows in your ledger, three to five are tagged for *follow-up
email this week*. These are the most consequential emails of your
post-conference work, because they convert single conversations into
*ongoing* relationships. The conversion rate from conference contact to
working relationship is roughly an order of magnitude higher when the
follow-up happens within forty-eight hours of the conversation; the
curve drops off sharply after that. So Monday is the deadline, and the
emails go out Monday.

The structure of a good follow-up email has four parts.

**Part one: the located thank-you.** Not "*thank you for our chat*", which
is generic. *"Thank you for the question about within-FICO-bin matching
on Saturday — it sharpened the part of the paper I was most worried
about.*" The located thank-you signals that you *remember the
substance*, which is what makes the email worth opening.

**Part two: the substantive content.** The reason for the email beyond
the thank-you. Either an attachment (the appendix table they asked
about), a question (a follow-up to the conversation), or a proposal (a
next step, like a longer conversation). *"I'm attaching the within-band
sensitivity analysis from Appendix A; I'd be curious whether the
finer-grained version in Table A.6 addresses your concern, or whether
you think the coarseness is still doing damage even within a single
band.*"

**Part three: the asked-for next step.** Specific, low-cost, and offered
*as a request, not a demand*. *"If you have ten minutes in the next two
weeks, I'd love to ask a follow-up question; happy to come to your
office hours, or any time that works.*" The asked-for next step gives
the recipient an easy thing to say yes to.

**Part four: a friendly close, with your contact info inline.** *"Either
way, thank you again for the question — best, Maya. Office hours:
Wednesday 2-4 p.m., or any time by appointment.*"

Three to five emails. Each is roughly three sentences plus a sentence of
attachment-pointer. They take fifteen minutes total to write. They are
the highest-ROI Monday-morning task of the entire post-conference week.

A subtle point: send *separate emails* to each person, not a single
group email with everyone CC'd. The substance of each follow-up is
specific to the conversation; a group email loses the located thank-you,
because the located thank-you cannot be located if it is broadcast.
Three separate emails, three minutes each.

---

## 6. The conversion from ledger to Week 10 plan

By Sunday afternoon, the ledger has all eight columns filled in and the
Critical/Important rows have been pulled into `paper/qa/week_10_12_taskboard.csv`.
That file is the *input* to Week 10, and Week 10 of the camp book is
built around consuming it. Here is the conversion, in one paragraph,
because it is the bridge between this week and the next.

A *Critical* row from the conference becomes a Week 10 deliverable: either
the new robustness specification, the redone analysis, or — in the worst
case — the *retreat-and-rewrite* memo that converts the causal claim
into the descriptive one. *Important* rows become Week 10-11 work,
spread across the four revision weeks by topic: the design-clarification
rows in Week 10, the new tables in Week 10-11, the intro and discussion
revisions in Week 11, the polish in Week 12. *Minor* rows become a
single-sentence task list for Week 11-12 polish. *Courtesy* rows
generate the Monday emails and otherwise do not enter the work plan.

The bridge: at the start of Week 10, you walk into your first mentor
meeting with *one document* — the taskboard CSV — and the conversation
is structured around it. *Here is what I heard. Here is how I sorted it.
Here is what I'm going to do about it.* That conversation is the most
productive single hour you will have in Phase 3, because the work is
already organized; the mentor's job becomes calibration — *yes, that's
Critical*, or *no, that's Important not Critical* — rather than
discovery. The discovery happened on Saturday; the organization happened
on Sunday; the calibration happens on Monday; the work happens through
Week 10-12.

A discipline rule: **the ledger is the source of truth for Week 10-12.**
You do not add new critiques from your own re-reading of the paper in
Week 11; you add new *rows to the ledger*, tagged "self-discovered"
in the *who* column, and triage them through the same rubric. The ledger
is the *project memory* of the revision phase; it is what makes Week 12's
final paper a *coherent response* to Week 9's feedback rather than an
unrelated polish pass. Treat it as such.

---

## 7. The closure, and what the chapter has been about

Step back. Week 9 has been about the *conference* as a thing that
happens: the pre-flight that prepares you for it (Ch 9.1), the eight
minutes of talk that delivers your argument (Ch 9.2), the question
period that tests it (Ch 9.3), the poster session that broadens it (Ch
9.4), and now — this chapter — the twenty-four hours that captures what
the conference gave back. Every chapter in the week is connected by one
discipline: *the conference is an event, but the value of the event is
in what survives it*. The pre-flight produces the survival of the
*delivery*. The talk produces the survival of the *argument*. The Q&A
produces the survival of the *defense*. The poster produces the survival
of the *conversation*. And this chapter produces the survival of the
*feedback* — the only one of the five that depends entirely on what you
do *after* the event, in private, under fatigue, with twenty-four hours
to act before the asset perishes.

The deeper claim — and it is the lesson the whole twelve-week NextGen
arc is pointed at, not just this week — is that **research is a chain of
hand-offs, and the artifact that survives each hand-off is what determines
the quality of the next.** From data to dataset (Ch 7.4) to analysis (Ch
8.1-8.2) to paper (Ch 8.3) to talk (Ch 9.2) to feedback (Ch 9.5) to
revision (Weeks 10-12) — each hand-off has a perishable input and a
durable output, and the discipline of the hand-off is the discipline of
*capturing the input in a form the next stage can consume*. The ledger
is that capture for the conference-to-revision hand-off. Without it,
the revision phase begins from a blurry memory of "what people said at
the conference"; with it, the revision phase begins from a structured,
queryable, triage-tagged list of named tasks. The difference is the
difference between a paper that improves systematically and a paper that
drifts.

The conference is over. The ledger is filled in. The Monday emails are
sent. Week 10 begins tomorrow. You walk into Week 10 with a clear set of
inputs — the taskboard, the threats table, the spec curve, the paper as
it currently stands — and a clear set of outputs — the addressed
critiques, the strengthened design, the tightened argument, the cleaner
prose. The conference, retrospectively, did its job. So did you.

---

## Your Turn

This week's deliverables close Phase 2 of NextGen (the conference) and
open Phase 3 (the revision). Treat the ledger as the literal pivot.

- **nb9.5 — feedback ledger and triage emitter.** Build the ledger CSV
  Saturday evening (first four columns); run the triage Sunday morning
  (last four columns). The notebook writes
  `paper/qa/feedback_ledger.csv`, `paper/qa/week_10_12_taskboard.csv`,
  and `paper/qa/followups.csv`. All three ship in the packet — the
  ledger is part of the project's permanent record, not a scratch file.
- **PS 9.5 — post-conference feedback ledger + four-week revision plan.**
  Submit the filled-in ledger (all eight columns for all rows), the
  taskboard (Critical and Important rows only, with dates), and a
  one-page narrative — *what changed in your view of the paper from
  Friday to Sunday*, written in prose. The narrative is graded on
  *calibration*: does the change in view track the rubric, or does it
  track the emotional reaction?
- **Lab 9, Phase E.** The Phase E lab is the literal Saturday-evening +
  Sunday-morning protocol, applied to a *recorded* peer Q&A from Lab 9
  Phase C. The recording becomes the input; the ledger becomes the
  output. The grading rubric is whether the eight columns are filled in
  with the right granularity, the severity ratings are *defensible* (a
  peer reviewing the rubric would agree), and the Week 10-12 taskboard
  is *actionable* (each row could be a Monday morning task).

### A closing reflection

Open the ledger one last time Sunday afternoon. Look at the *Critical*
rows. If there are any, ask yourself the hardest question of the camp:
*does the headline of my paper survive these critiques, as I currently
have it written?* If yes, the conference confirmed the paper. If no, the
conference asked you to retreat to the descriptive claim (Ch 9.3 §6),
and Week 10 begins with a *rewrite*, not a *robustness check*. Both are
honest outcomes; both are publishable; both are improvements over what
you walked into the conference with. The shame would be not knowing the
answer. You know it now.

---

### References

- Allen, D. (2001). *Getting Things Done: The Art of Stress-Free
  Productivity.* Penguin. (The capture-then-process discipline; the
  two-pass model of triage that the Saturday/Sunday split implements.)
- Walker, M. P. (2017). *Why We Sleep: Unlocking the Power of Sleep and
  Dreams.* Scribner. (Memory consolidation across the overnight gap;
  why the Saturday-Sunday split is cognitive, not merely logistical.)
- Klein, G. (1999). *Sources of Power: How People Make Decisions.* MIT
  Press. (Rapid classification under load; the bucket-and-severity
  rubric as an aid to professional judgment under fatigue.)
- Cialdini, R. B. (2008). *Influence: Science and Practice* (5th ed.).
  Pearson. (Why the follow-up email within forty-eight hours converts
  at an order of magnitude higher rate; the reciprocity window.)
- Hofmann, A. H. (2013). *Scientific Writing and Communication: Papers,
  Proposals, and Presentations* (2nd ed.). Oxford University Press.
  (The conference-to-revision hand-off as a documented academic
  practice; the role of the feedback ledger in publication workflow.)
- See also Chapters 7.5 (the threats table — the ledger's *translation*
  column joins back to it), 8.1 (the specification curve — the
  reference object for Bucket A robustness rows), 8.2 (the robustness
  battery — where new Critical-row tests get added), 9.1 §3 (the
  anticipated-questions matrix — the *predicted* version of the ledger),
  9.3 (the three honest answers — every Saturday Q&A row's verbatim is
  an instance of one of the buckets), and 9.4 §4 (the pocket notebook
  from the poster session — the transcription source for many ledger
  rows). Week 10's opening chapter consumes
  `paper/qa/week_10_12_taskboard.csv` as its primary input.
