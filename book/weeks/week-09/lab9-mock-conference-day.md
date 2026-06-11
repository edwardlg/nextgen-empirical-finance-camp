# Lab 9 — Mock Conference Day: Full-Rehearsal Symposium

Week 8 ended with three things sitting on disk: a compiled paper, a one-click replication packet, and a deck rehearsed against a timer. Week 9 puts a *room* around those artifacts. The same paper you defended to a peer in Lab 8 will be defended in Lab 9 in front of a panel that has read it, in a session timed to the second, with a structured feedback ledger taking notes on every answer you give. The deliverable at the end of this lab is not another draft — it is the **artifact bundle** you would carry into a real conference: the slides PDF, the poster PDF, the replication packet zipped to a single file, the video of the talk, and the conference-feedback ledger as a CSV. That bundle, exactly as Lab 9 builds it, is what Assessment 9 grades.

The discipline this lab drills is one Chapter 8.5 promised but could only stage in miniature: **a paper survives its first real audience or it does not, and the eight minutes during which it does or doesn't survive are the unit of evaluation.** Defending to one peer in Lab 8 is sparring; defending to a panel that has read the paper, in a session running to a printed program, with three other students watching and a ledger capturing the question and your answer in real time, is the fight. Lab 9 is the rehearsal *of the fight*, executed end-to-end so that on the actual conference day — your Phase 2 NextGen presentation, ~Aug 14, or the Schar Young Scholars venue your paper is headed toward — every move is muscle memory.

One housekeeping note before we start. Nothing in Lab 9 needs the internet. The "panel" is your cohort plus Prof. Gao; the "room" is whatever room your section meets in (or a Zoom breakout if you are remote); the "feedback ledger" is a CSV on disk that you write into during talks and analyze when the day is over. Recording the talk is optional in principle but **required for the artifact bundle** — your phone propped on a chair captures audio and a slide-by-slide video well enough for a self-assessment, and the file lives only on your own machine until you upload the bundle. The lab is designed to run offline on the camp container; if you have no recording device, the alternative is a peer transcribing your talk into a Markdown file in real time, which is a worse video but the same artifact.

---

## Learning goals

By the end of this lab you will be able to:

1. **Run a timed symposium session as the speaker** — eight-minute talk, three-minute Q&A, hard stop on the clock, in front of a panel that has read your paper.
2. **Run a session as a panelist** — read another student's paper cold, prepare two questions from its threats table, and ask them in the role.
3. **Operate the conference-feedback ledger** — a structured CSV where every question and answer is logged with a timestamp, a family tag (identification / robustness / alternative / measurement / writing / scope), and a fatal-vs-survivable triage, by a designated scribe rotated each talk.
4. **Build a research poster from the same `\input{}`ed tables and figures that ship in the paper** — one PDF, single page, regenerable by code from the same `make` pipeline.
5. **Assemble the Week-9 artifact bundle** — `bundle/slides.pdf`, `bundle/poster.pdf`, `bundle/packet.zip`, `bundle/talk.mp4` (or `.md` transcript), `bundle/ledger.csv`, all in one folder ready to upload.
6. **Score yourself against the ledger** — turn the panel's feedback into a written self-assessment that names what landed, what did not, and what the next revision week (Week 10) will fix.

---

## Setup

You already have everything from Lab 8: the compiled paper, the `paper/` folder with code-generated tables and figures, the `Makefile` (or `run_all.py`), and the deck. Lab 9 needs three small additions to that repository — a `poster/` folder, a `bundle/` folder, and a `ledger/` folder — and one tool you may not have used before: `pandoc` for assembling the poster's Markdown into a typeset PDF, already on the camp container.

Probe what is present before you start:

```bash
latexmk --version       # paper compile from Lab 8
pandoc --version        # used by the poster build
ffmpeg -version 2>/dev/null | head -1   # optional: only used if compressing the recording
python -c "import pandas; print(pandas.__version__)"   # for the ledger CSV
```

If `pandoc` is missing on a personal laptop, the poster fallback is the same as Lab 8's LaTeX fallback: ship the source Markdown plus a one-page PDF exported from any markdown viewer or compiled on Overleaf. The deliverable is the PDF; how you produce it is a convenience the bundle does not care about.

Create the new folders inside your capstone repository:

```bash
cd capstone-2026-<you>
mkdir -p poster bundle ledger
touch poster/.gitkeep bundle/.gitkeep ledger/.gitkeep
```

The Lab 7/8 rule still binds: **the repository travels freely, the licensed bytes do not.** The bundle never contains CRSP/Compustat data; it contains the *recipe* to pull it. If your project is on public data only — HMDA, USPTO, FRED, EDGAR 8-Ks — the packet zips up everything as-is.

---

## Part 1 — The symposium-day session protocol

A real conference session is a contract about time and format that everyone in the room is held to. The protocol below mirrors what the NextGen Phase-2 conference and the Schar Young Scholars symposium actually run, scaled down to a single cohort. Read it once, then execute it.

### 1.1 The session contract

A **session** is a block of four talks, run by a single **session chair**. Each talk is on a contract:

- **8 minutes of speaker time.** The chair holds up a yellow card at 6:00 ("two minutes"), a red card at 7:30 ("wrap"), and a stop sign at 8:00. The clock does not negotiate. A talk that runs to 8:30 has not finished; it has *been cut off*, and that is graded — the talk grade caps at Developing the moment the stop sign is up.
- **3 minutes of structured Q&A.** Two questions from the assigned panel (Part 1.3), one open question from the room. The chair takes the questions in that order and cuts the third question if time runs out.
- **2 minutes of changeover.** The next speaker connects, the scribe rotates, the chair resets the timer.

That is **13 minutes per talk**, **52 minutes per session of four**, plus a 10-minute break — the same 60-to-70 minute envelope as a real conference session. Run the math on your cohort: a section of 12 students fits as three sessions of four; a section of 16 as four sessions. Build the program *before* the day so every student knows exactly when they speak and on whose panel they sit. The program is the load-bearing document of the morning.

### 1.2 The four roles, rotated every talk

Four people are working during each talk; each has a job and only that job. The point of rotation is that across the four-talk session every student plays every role at least once.

| Role | Who | Job during the talk | Job during Q&A |
|---|---|---|---|
| **Speaker** | the student whose paper this is | give the 8-min talk | answer questions from threats-table; concede fatal critiques |
| **Chair** | rotating cohort member | enforce the timer; call on questioners in order | cut off long questions; call time at 3:00 |
| **Panelist** | two assigned readers (see 1.3) | listen with the threats table open | ask one prepared question each, in family order |
| **Scribe** | rotating cohort member | timestamp the talk in 30-second checkpoints | log every Q&A turn into `ledger.csv` |

Prof. Gao sits as a fifth participant in every session and acts as a **silent referee** — he does not chair, he does not panel, he watches. His feedback comes at the end of the day, not during, and it feeds the assessment.

### 1.3 Pre-assigned panelists, pre-read 24 hours ahead

The panelist role only works if the panelists have actually read the paper. So the program publishes, **24 hours before symposium day**, a pairing table:

| Talk | Speaker | Panelist A (reads section 1–4) | Panelist B (reads section 5–7 + appendix) |
|---|---|---|---|
| 1 | Maya | Devon | Priya |
| 2 | Devon | Sam | Leah |
| 3 | Priya | Maya | Sam |
| 4 | Sam | Leah | Devon |
| 5 | Leah | Priya | Maya |
| ... | | | |

Each panelist reads their assigned half closely the night before and arrives with **two written questions**, drawn from the rows of the speaker's Chapter 7.5 threats table (which is in the paper's design section, exactly where Lab 8 put it). One question per panelist is asked live in the 3-minute Q&A; the unasked question is still written into the ledger so the speaker sees it. The point is that the talk is defended against questions the panelists actually thought hard about — not improvised reactions to a slide deck.

### 1.4 The session-chair script

If you are the chair, you are reading the program out loud. Here is the script, abbreviated; it is deliberately rigid, because chairs who improvise let sessions run long.

```
[0:00]  "Talk 1: <Speaker>, '<Paper title>.' You have 8 minutes. Go."
[6:00]  Hold up yellow card. Say nothing.
[7:30]  Hold up red card. Say nothing.
[8:00]  Hold up stop sign. "Time. Thank you, <Speaker>."
[8:00 → 11:00]  "Panelist A, your question. Panelist B, your question. Room, one open question."
[11:00] "Time. Thank you. Two-minute changeover."
[13:00] Next talk.
```

The chair's hardest skill is the one nobody rehearses: **cutting a long question.** A panelist who builds up a paragraph of context before asking is eating the speaker's clock. The chair's move is polite and firm: *"What's the question?"* — and if the panelist still won't land it, *"Let's hear the speaker's answer."* That is not rudeness; it is the contract.

---

## Part 2 — The conference-feedback ledger

The ledger is what makes Week 9 a graded artifact rather than a memory. Every question, every answer, every timestamp, every family tag goes into a single CSV that you analyze when the day is over and submit as part of the bundle. The schema is fixed, because grading is consistent across the cohort.

### 2.1 The ledger schema

Create `ledger/ledger.csv` with this header row:

```csv
talk_id,speaker,timestamp,role,event_type,family,fatal_or_survivable,text,responder_handling
```

Each column is load-bearing, so name them right.

- **`talk_id`** — a stable integer per talk (1, 2, 3, …) matching the program.
- **`speaker`** — the speaker's initials.
- **`timestamp`** — minutes and seconds from the start of the talk, in `MM:SS`. The scribe reads this off a phone stopwatch.
- **`role`** — who initiated the event: `speaker`, `panelist_A`, `panelist_B`, `room`, `chair`.
- **`event_type`** — one of: `talk_checkpoint` (every 30s during the talk), `question`, `answer`, `concession`, `idk` (an "I don't know"), `interruption`.
- **`family`** — for questions and answers: `identification`, `robustness`, `alternative`, `measurement`, `scope`, `writing`, `delivery`, `other`. The eight families come straight from Chapter 8.5 and Mentor 8.
- **`fatal_or_survivable`** — for questions only: `F` (attacks the comparison), `S` (attacks a number), or blank for non-question events.
- **`text`** — the question or answer in one to two sentences; the scribe does not have to be a stenographer, but the *substance* must be capturable in 20 seconds of typing.
- **`responder_handling`** — for answers only: `prepared` (answer matched a threats-table row), `improvised` (answer was on the fly but solid), `concede` (acknowledged the critique honestly), `deflect` (changed the subject), `bluff` (fabricated a number or claim).

A populated row looks like:

```
3,PS,02:14,panelist_A,question,identification,F,"Could pre-existing trends explain the divergence in the event-study plot?",
3,PS,02:31,speaker,answer,identification,,"Pre-trends slide shows flat leads, all CIs cross zero; residual concern is the assumption itself.",prepared
```

That single pair captures everything the grader needs about that exchange.

### 2.2 The scribe's job, mechanically

During the talk, the scribe writes one `talk_checkpoint` row every 30 seconds with the slide number and one-line note. During Q&A, the scribe captures every question/answer as two rows. A 30-second discipline is genuinely necessary — without it, the scribe's memory smooths over the *pauses* in the talk, which are where the speaker either kept the room or lost it.

Use this minimal Python helper to log without missing checkpoints. It runs offline and writes straight to the CSV:

```python
"""ledger/log_session.py — terminal-based scribe tool.

    python log_session.py --talk 3 --speaker PS
    # then type: q  -> question prompt
    #            a  -> answer prompt
    #            c  -> talk checkpoint (slide number + note)
    #            x  -> end of talk
"""
import argparse, csv, time
from pathlib import Path

LEDGER = Path(__file__).resolve().parent / "ledger.csv"
HEADER = ["talk_id", "speaker", "timestamp", "role", "event_type",
          "family", "fatal_or_survivable", "text", "responder_handling"]

def mmss(seconds: float) -> str:
    m, s = divmod(int(seconds), 60)
    return f"{m:02d}:{s:02d}"

def ensure_header(path: Path) -> None:
    if not path.exists() or path.stat().st_size == 0:
        with path.open("w", newline="") as f:
            csv.writer(f).writerow(HEADER)

def append(row: list) -> None:
    with LEDGER.open("a", newline="") as f:
        csv.writer(f).writerow(row)

def main() -> None:
    ap = argparse.ArgumentParser()
    ap.add_argument("--talk", required=True, type=int)
    ap.add_argument("--speaker", required=True)
    args = ap.parse_args()
    ensure_header(LEDGER)
    print("Press Enter to start the talk timer.")
    input()
    t0 = time.time()
    print("Commands: q = question, a = answer, c = checkpoint, x = end. Ctrl-C to abort.")
    while True:
        cmd = input(f"  [{mmss(time.time() - t0)}] ").strip().lower()
        ts = mmss(time.time() - t0)
        if cmd == "x":
            print("Talk ended.")
            return
        if cmd == "c":
            note = input("    checkpoint note: ").strip()
            append([args.talk, args.speaker, ts, "speaker",
                    "talk_checkpoint", "", "", note, ""])
        elif cmd in ("q", "a"):
            role = input("    role (panelist_A/B / room / speaker / chair): ").strip()
            family = input("    family: ").strip()
            fs = input("    F/S (for question only; blank otherwise): ").strip()
            text = input("    text: ").strip()
            handling = ""
            if cmd == "a":
                handling = input("    handling (prepared/improvised/concede/deflect/bluff): ").strip()
            event = "question" if cmd == "q" else "answer"
            append([args.talk, args.speaker, ts, role, event, family, fs, text, handling])
        else:
            print("    (unknown command, ignored)")

if __name__ == "__main__":
    main()
```

Run it as `python ledger/log_session.py --talk 3 --speaker PS` at the start of each talk. The scribe rotates between talks, so the cohort produces one shared `ledger.csv` for the whole symposium; each speaker extracts their own talk's rows for their bundle.

### 2.3 Reading your own ledger after the session

After the day is done, every speaker reads their own ledger rows and produces three numbers — these go straight into the Assessment 9 self-assessment.

```python
# ledger/score_my_talk.py — extract one speaker's row counts
import argparse
import pandas as pd

ap = argparse.ArgumentParser()
ap.add_argument("--speaker", required=True)
args = ap.parse_args()

df = pd.read_csv("ledger/ledger.csv")
mine = df[df["speaker"] == args.speaker].copy()

questions = mine[mine["event_type"] == "question"]
answers = mine[mine["event_type"] == "answer"]

print(f"Total questions received:        {len(questions)}")
print(f"  Identification (F):            {((questions.family == 'identification') & (questions.fatal_or_survivable == 'F')).sum()}")
print(f"  Robustness (S):                {((questions.family == 'robustness') & (questions.fatal_or_survivable == 'S')).sum()}")
print(f"  Alternative explanation:       {(questions.family == 'alternative').sum()}")
print()
print(f"Answers handled 'prepared':      {(answers.responder_handling == 'prepared').sum()}")
print(f"Answers 'improvised' but solid:  {(answers.responder_handling == 'improvised').sum()}")
print(f"Concessions made:                {(answers.responder_handling == 'concede').sum()}")
print(f"Bluffs (graded against you):     {(answers.responder_handling == 'bluff').sum()}")
```

Three rows say almost everything: how many questions you got that were *fatal*-class, how many you handled from *prepared* threats-table answers (the goal), and how many bluffs the scribe flagged (the failure mode). The self-assessment in Assessment 9 asks for exactly these numbers and a sentence on each.

---

## Part 3 — Building the poster

A poster is a *parallel* artifact to a paper, not a derivative one — it tells the same story in a glance, for a hallway audience that walks by, stops, reads for 30 seconds, and either asks you a question or leaves. The discipline is brutal: one page, the headline number visible from six feet, the design slide as the spine, and zero unread sentences. The good news for your reproducibility is that the poster pulls the *same* `\input{}`ed tables and `\includegraphics{}`ed figures as your paper. No new numbers are computed; the same `make` chain produces both.

### 3.1 The poster anatomy

A research poster has a small number of zones, and the same zones appear on every poster you will see at a real conference:

```
+-----------------------------------------------------------------------------+
| TITLE BLOCK: title (big), authors, affiliation                              |
+-------------------+------------------------------+------------------------+
| MOTIVATION        | DATA & SAMPLE                | HEADLINE RESULT         |
| (the fact + stake)| (one sentence + sample size) | (one figure, BIG)       |
+-------------------+------------------------------+------------------------+
| EMPIRICAL DESIGN  | ROBUSTNESS                   | TAKEAWAY + REPO QR     |
| (eqn + ID assn.)  | (spec curve thumbnail)       | (one sentence + code)   |
+-------------------+------------------------------+------------------------+
```

That is six panels on a 36"×48" sheet, which is the standard NextGen poster size. The center-top panel is where the eye lands first — that is where the **headline figure** goes (your event-study plot, your coefficient plot, the one image that tells the story), and it should be 40% of the visual weight of the whole poster.

### 3.2 Building the poster from Markdown + pandoc

You do not need a poster-specific design tool for this. A Markdown file plus a small pandoc template produces a one-page PDF that is genuinely good enough for the Phase-2 conference and the Schar venue. The trick is the same trick from Lab 8: the poster file *reads* the tables and figures the analysis wrote, never contains numbers itself.

Write to `poster/poster.md`:

```markdown
---
title: "Fair-Lending Examination Programs and the Minority–White Denial Gap"
author: "Maya R., NextGen FinTech Scholars, GMU"
geometry: landscape, margin=0.4in, paperwidth=48in, paperheight=36in
fontsize: 22pt
header-includes:
  - \usepackage{multicol}
  - \usepackage{graphicx}
  - \graphicspath{{../paper/figures/}}
---

\begin{multicols}{3}

# Motivation

The denial gap between minority and white applicants in U.S. mortgage markets has
persisted for decades. Whether state-level fair-lending examination programs
reduce it is a policy question with a measurable answer.

# Data and Sample

HMDA loan-application records, 2010--2022, joined to a hand-coded panel of state
fair-lending examination adoptions (data card: `data-cards/hmda.md`). Sample is
county-year-level for $N$ counties across $T$ years.

# Empirical Design

We estimate
$$\textrm{Gap}_{ct} = \beta\,\textrm{Exam}_{st} + \mathbf{x}'_{ct}\boldsymbol\gamma + \alpha_c + \tau_t + \varepsilon_{ct},$$
clustered by state. The identifying assumption is that the timing of adoption is
unrelated to county-level shocks to the gap, conditional on county and year fixed
effects (see paper §3 for the threats table).

\columnbreak

# Headline Result

\includegraphics[width=\linewidth]{event_study.pdf}

The gap narrows by about 1.8 percentage points after adoption. Pre-period leads
are flat; CIs cross zero in every lead.

# Robustness

\includegraphics[width=\linewidth]{spec_curve.pdf}

The pre-registered point sits near the center of the specification curve. Wild
cluster bootstrap with 30 state clusters preserves significance. Oster $\delta = 0.6$
with $R_{\max}$ swept to 1.

\columnbreak

# Takeaway

The pattern is consistent with examination programs causing a reduction in the
denial gap, under the parallel-trends assumption. The honest reading is a robust
association that survives the obvious selection stories.

# Reproduce This Work

\begin{center}
\includegraphics[width=0.4\linewidth]{../bundle/qr.png}\\
\texttt{github.com/.../capstone-2026-maya}\\
\texttt{make clean \&\& make all}
\end{center}

\end{multicols}
```

Compile to one-page PDF on the camp container:

```bash
cd poster && pandoc poster.md -o poster.pdf --pdf-engine=latexmk
```

If `pandoc` is unavailable, the Overleaf path from Lab 8 works identically — paste the Markdown into Overleaf's importer or convert the file to a one-page LaTeX class (`tikzposter`, `betterposter`) and compile in the browser.

### 3.3 The QR code, generated offline

The "scan to clone the repo" QR code in the takeaway panel is a small but real piece of reproducibility theater: a visitor at the conference can clone your repo from the poster itself. Generate it offline using `qrcode` (pre-installed on the camp container):

```python
# bundle/make_qr.py — offline QR for the repo URL
import qrcode
url = "https://github.com/your-org/capstone-2026-yourhandle"   # your real repo
img = qrcode.make(url)
img.save("bundle/qr.png")
```

The QR is regenerated from this script by `make poster` so the URL is never typed twice.

### 3.4 What does NOT go on a poster

A poster is a place where bad instincts metastasize. Resist these three: (a) **walls of text** — if a hallway reader cannot understand the panel in 20 seconds, the panel is wrong, not the reader; (b) **a regression table** — tables on a poster are unreadable from a meter away; translate them to a coefficient plot (Chapter 8.3 §8); (c) **the literature review** — there is no room for it. A poster has *one* sentence of motivation, *one* of design, *one* of result, and *one* of caveat, plus the headline figure and the QR. Anything else is a paper section pretending to be a poster panel.

---

## Part 4 — The artifact bundle

The bundle is the single folder that submits as the Week 9 deliverable. It is built by code, not assembled by hand, because the rule from Lab 8 still holds: anything you assemble by hand drifts. Every artifact in the bundle is regenerated from `make bundle` (or `python build_bundle.py`).

### 4.1 The bundle layout

```
bundle/
├── slides.pdf              # the 8-min deck, exported from Keynote/PowerPoint/Beamer to PDF
├── poster.pdf              # the one-page poster (Part 3)
├── packet.zip              # the replication packet (excluding the bundle/ itself!)
├── talk.mp4                # the recorded talk (or talk_transcript.md if no recording)
├── ledger.csv              # the speaker's own rows from the symposium ledger
├── qr.png                  # the offline-generated QR code
└── manifest.json           # what's in the bundle, with file hashes
```

The **manifest** is the load-bearing file — it lists every artifact, its size, and its SHA-256 hash, so a grader cloning the repo can verify the bundle they see matches the bundle the student submitted.

### 4.2 The bundle build script

Write to `build_bundle.py` at the repo root:

```python
"""build_bundle.py — assemble bundle/ from on-disk artifacts and write a manifest.

    python build_bundle.py
"""
import hashlib, json, shutil, subprocess
from pathlib import Path

ROOT = Path(__file__).resolve().parent
BUNDLE = ROOT / "bundle"
BUNDLE.mkdir(exist_ok=True)

# 1) Copy slides.pdf in from wherever your deck lives (e.g., paper/slides.pdf or talks/).
SOURCES = {
    "slides.pdf": ROOT / "talks" / "slides.pdf",       # speaker exports here
    "poster.pdf": ROOT / "poster" / "poster.pdf",      # Part 3
    "qr.png":     ROOT / "bundle" / "qr.png",          # already in place
}
for name, src in SOURCES.items():
    if not src.exists():
        raise SystemExit(f"Missing required artifact: {src}")
    if src != BUNDLE / name:
        shutil.copy2(src, BUNDLE / name)

# 2) Zip the replication packet (everything tracked in git, minus bundle/ itself).
print("[bundle] zipping replication packet...")
out_zip = BUNDLE / "packet.zip"
if out_zip.exists():
    out_zip.unlink()
# Use git archive so we ship exactly what's tracked, never local junk.
subprocess.run(
    ["git", "archive", "--format=zip", "--prefix=packet/", "-o", str(out_zip), "HEAD"],
    cwd=ROOT, check=True,
)

# 3) Extract this speaker's rows from the symposium ledger.
my_speaker = "PS"   # set this to your initials at the top of the script
import pandas as pd
ledger = pd.read_csv(ROOT / "ledger" / "ledger.csv")
mine = ledger[ledger["speaker"] == my_speaker]
mine.to_csv(BUNDLE / "ledger.csv", index=False)

# 4) Confirm talk.mp4 exists or fall back to a transcript.
talk = BUNDLE / "talk.mp4"
transcript = BUNDLE / "talk_transcript.md"
if not talk.exists() and not transcript.exists():
    raise SystemExit("Either bundle/talk.mp4 or bundle/talk_transcript.md is required.")

# 5) Hash every artifact and write the manifest.
def sha256(path: Path) -> str:
    h = hashlib.sha256()
    with path.open("rb") as f:
        for chunk in iter(lambda: f.read(1 << 16), b""):
            h.update(chunk)
    return h.hexdigest()

manifest = {
    "speaker": my_speaker,
    "git_commit": subprocess.check_output(["git", "rev-parse", "HEAD"], cwd=ROOT).decode().strip(),
    "artifacts": [],
}
for p in sorted(BUNDLE.iterdir()):
    if p.name == "manifest.json":
        continue
    manifest["artifacts"].append({
        "name": p.name,
        "bytes": p.stat().st_size,
        "sha256": sha256(p),
    })
(BUNDLE / "manifest.json").write_text(json.dumps(manifest, indent=2))
print(f"[bundle] wrote manifest with {len(manifest['artifacts'])} artifacts.")
```

Add a `make bundle` target to your `Makefile`:

```makefile
.PHONY: bundle
bundle: all poster/poster.pdf
	python build_bundle.py
```

That target depends on `all` (Lab 8's full rebuild) and on `poster/poster.pdf`, so a fresh-clone test — `make clean && make bundle` — regenerates everything from raw bytes to bundle in one command. That is what Assessment 9's reproducibility row tests.

### 4.3 The honesty test for the bundle

The same `make clean` ritual from Lab 8, extended one step:

```bash
make clean
make bundle
ls -la bundle/
python -c "import json; m=json.load(open('bundle/manifest.json')); print(len(m['artifacts']), 'artifacts'); [print(a['name'], a['bytes']) for a in m['artifacts']]"
```

The bundle should rebuild every artifact, the manifest should list six or seven files, and every byte size should be consistent across runs. If `slides.pdf` is missing from `talks/`, the script *raises* — better a failed build than a silently incomplete bundle.

---

## Part 5 — Running the day, in real time

This part is the prose checklist for the symposium itself. Read it the morning of, then execute it.

### 5.1 60 minutes before

- Speakers: open your deck, scroll to the first slide, plug into the projector / screen-share, leave it there. Do this *now*, not when you walk up.
- Panelists: re-read your assigned half of the paper, re-read your two prepared questions, put them on a notecard.
- Scribe: open the terminal, `cd ledger`, `python log_session.py --talk 1 --speaker XX` ready to fire.
- Chair: print the program. Hold it. Look at the wall clock.

### 5.2 The four-talk session, in order

For each talk, the same loop:

1. Chair calls the talk. Scribe presses Enter to start the timer.
2. Speaker talks for 8 minutes against the chair's clock and the cards.
3. Scribe logs a checkpoint every 30 seconds. ("Slide 3 — design — clean.")
4. Chair calls time at 8:00. Panelist A asks. Speaker answers. Scribe logs both.
5. Panelist B asks. Speaker answers. Scribe logs both.
6. Room question. Speaker answers. Scribe logs both.
7. Chair calls time at 11:00. Scribe presses `x` to end the talk.
8. Two-minute changeover. Next speaker plugs in.

The discipline is in the *not-improvising*. The chair does not extend the clock for a "really good question." The scribe does not skip a checkpoint because the talk is going well. The panelist does not skip their prepared question because the room asked something similar. The protocol is the grade.

### 5.3 The 10-minute break between sessions

Use it. Pour water. Re-pair laptops. The cohort that comes back from break two minutes late loses the whole day's schedule. The chair holds the break to ten minutes the same way they hold the talk to eight.

### 5.4 End-of-day debrief (~30 minutes)

After the last session, the whole cohort sits together with Prof. Gao for a debrief. This is *not* a critique of individual talks — that comes in the assessment. The debrief surfaces *patterns*: which family of question kept appearing across talks? Which talks ran long, and which slide ate the clock? Which concessions were honest and which were dodges in disguise? Prof. Gao closes with the one observation he flagged during the day, which goes into every speaker's self-assessment as a piece of evidence to respond to.

---

## You're done when…

Use this checklist. A box is checked only when you can point at the file that proves it.

- [ ] **Slides PDF exists in `bundle/slides.pdf`.** Same 8-minute deck from Lab 8, exported to PDF, fits the time, includes the design slide and the headline figure (not a table).
- [ ] **Poster PDF exists in `bundle/poster.pdf`.** One page, regenerated by `make poster`, pulls the same `figures/event_study.pdf` and `figures/spec_curve.pdf` the paper pulls. The headline figure occupies ~40% of the visual weight.
- [ ] **Packet zip exists in `bundle/packet.zip`.** Generated by `git archive HEAD` (not by hand-zipping a folder), unzips to a `packet/` directory whose `make all` regenerates the paper PDF on a fresh clone.
- [ ] **Talk recording or transcript exists.** `bundle/talk.mp4` (preferred) or `bundle/talk_transcript.md` (fallback). Captures the full 8 minutes of talk plus the 3 minutes of Q&A.
- [ ] **Ledger CSV exists.** `bundle/ledger.csv` contains *your* talk's rows from the cohort's `ledger/ledger.csv`. At minimum: 16 checkpoint rows (one every 30s for 8 minutes), 2 panelist questions + answers, 1 room question + answer.
- [ ] **Manifest exists and hashes match.** `bundle/manifest.json` lists every artifact with size and SHA-256; the commit hash matches the current `HEAD`.
- [ ] **Bundle rebuilds clean.** `make clean && make bundle` reproduces the bundle byte-for-byte (modulo the PDF metadata Lab 8 already taught you to pin).
- [ ] **Self-scored ledger numbers ready.** You ran `score_my_talk.py` and have three numbers in front of you: total fatal-class questions, total prepared-handling answers, total bluffs. These feed Assessment 9's self-assessment.

---

## Connecting to Assessment 9 — the symposium-performance grade

This lab is the build bench; **Assessment 9 is the conference performance itself**, graded as a single 100-point exercise across the five artifacts the bundle holds and the self-assessment that reads the ledger back to you. The mapping is direct, so treat this checklist as a pre-grade audit.

Assessment 9 asks: does the slides PDF tell the six-beat story in 8 minutes? (Part 5, recorded.) Does the poster carry the same story in one page with no new numbers? (Part 3.) Does the packet rebuild on a fresh clone? (Part 4 — `make clean && make bundle`.) Does the talk delivery hold the room in a way the recording confirms? (Part 5.1–5.2, the chair's enforcement.) Did the Q&A go to the panelists' prepared questions, and did the speaker handle them as prepared / improvised / conceded rather than bluffed? (Part 2, the ledger.)

And the self-assessment, which is half of Assessment 9's writing component: you read your own ledger, count your prepared-handling answers and your concessions, locate the one question you bluffed (everyone bluffs once; the grade is on whether you noticed), and write the paragraph that says — honestly — what landed, what didn't, and what the Week 10 revision sprint will fix. That paragraph is the bridge from the conference into Phase 3 of the program, where the paper goes from "presented" to "ready to submit." A speaker who reads their ledger honestly and writes "the alternative-explanation panelist landed on something my paper does not yet address, and Week 10 builds the placebo that splits the two stories" is showing exactly the move Phase 3 will require.

You started Lab 8 having computed an estimate you could defend on paper. You finished Lab 9 having defended it in front of a panel that read the paper, in a room running on a printed program, with every question and answer logged in a ledger you can read back. The bundle on disk is the artifact a real conference produces. The talk file is the moment the paper became a *result*, in the only sense of that word that counts: a claim you defended out loud, in front of people who came to disbelieve, and the room walked out the other side.

The Phase-2 conference on August 14 is real. The Schar Young Scholars symposium where some of these papers will land is real. So is the moment a referee at a real journal opens the packet zip and types `make all`. Lab 9 is the dress rehearsal for all three. Build the bundle. Submit it. Then go present.

---

### References

- American Economic Association. *Sample References and Author Resources.* `https://www.aeaweb.org/journals/policies/templates` `[CHECK]` exact template filenames against the version the camp distributes.
- Gentzkow, M., & Shapiro, J. M. (2014). *Code and Data for the Social Sciences: A Practitioner's Guide.* University of Chicago. (Run-order, `make`, and the one-command-rebuild discipline; the poster-from-`\input{}`ed-figures pattern follows the same rule.)
- Morrison, M. (2019). Better Scientific Poster. `https://osf.io/ef53g/` `[CHECK]` — the single-column "billboard" template is one alternative to the three-column layout described in §3.1; the bundle accepts either as long as the headline figure is dominant and the QR is present.
- Wilson, G., Bryan, J., Cranston, K., Kitzes, J., Nederbragt, L., & Teal, T. K. (2017). Good Enough Practices in Scientific Computing. *PLoS Computational Biology*, 13(6), e1005510.
