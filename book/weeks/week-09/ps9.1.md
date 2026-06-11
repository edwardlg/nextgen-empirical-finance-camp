# PS 9.1 — The 72-Hour Pre-Flight Checklist

**Course:** 8-Week Empirical Finance Camp · Week 9 · Problem Set 9.1
**Covers:** Ch 9.1 (The 72-Hour Pre-Flight Checklist), standing on Lab 8 (the manuscript-and-repo defense), Ch 8.5 (the 8-minute deck + one-click replication packet), and Ch 7.5 (the identification memo that becomes the spine of every answer you give in the Q&A). Uses no notebook: this is the human checklist you run, in person, in the three days before you stand up at the conference.
**Type:** Project deliverable, not a numeric problem set. You execute a fixed 72-hour pre-flight sequence on *your* capstone deck and *your* capstone packet — three calendar days, each with its own gate — and you submit the artifacts the gates produce: a versioned slides file with a content hash, a packet hash, a 7-minute dry-run video, and a single "pre-flight log" that records the time, command, and observation for each gate. There is no single right answer because the answer is *whether the gates closed on your project*, not a number — and what is graded is the *discipline of the closure*: did you actually run `make clean && make all` against a fresh clone, or did you read the failure and pretend it didn't happen?

**Total: 100 points.** Point values are stated per part. A model deliverable — a complete, A-grade 72-hour log for one cast project (Devon's spot-Bitcoin-ETF event study), with instructor grading notes keyed to the rubric — is in Appendix E (`E-w9-ps9.1-solutions.md`). Read it *after* you draft your own, the way Ch 9.1 walked through the dry-run protocol: not to copy, but to calibrate.

A boundary to hold throughout. This deliverable is **not** about polishing the slides further — Ch 8.5 already locked the deck's content into one idea per slide and one figure per result, and PS 8.5 already produced `paper/slides.pdf` and the replication packet. PS 9.1 is about *freezing* what you have, *hashing* what you froze, and *rehearsing against the version you froze* — so that on conference morning the file you upload is byte-identical to the file you rehearsed against, and the packet a stranger clones is byte-identical to the one that produced the slide-4 figure. Polishing creep is the failure mode this assignment exists to prevent: the student who keeps tweaking the headline figure at 11:47 p.m. the night before discovers, in the green room, that their final-final-v3 deck no longer matches the packet it cites. The whole 72-hour drill is a defense against that student being you.

---

## What you submit

A single folder, `pre-flight/`, committed to your capstone repository, containing **five artifacts** plus a **log**:

1. `slides-vfinal.pdf` (or `.pptx`) — the *frozen* deck, renamed `vfinal` only after Day-1 lock and never edited again. The Day-2 dry-run is recorded against *this* file; the conference upload is *this* file (Part 1).
2. `packet.sha256` — the SHA-256 hash of the replication-packet tarball (`make dist` or `git archive HEAD`), produced *after* the final `make clean && make all` honesty test on a fresh clone (Part 2).
3. `dry-run.mp4` (or a YouTube/Drive link in `dry-run.txt`) — the **7-minute** dry-run video you recorded against `slides-vfinal.pdf`, on Day 2, with a visible timer (Part 3).
4. `qa-script.md` — the printed Q&A defense sheet: the two hardest questions from your PS 8.5 anticipated answers, plus the "located I don't know" and the retreat position, formatted to read aloud (Part 4).
5. `travel-kit.md` — the conference-day go-bag manifest (Part 5): printed slide handouts, backup USB with `slides-vfinal.pdf` and the packet tarball, the laptop adapter list, a 1-page identification-memo card, and the offline copy of `qa-script.md`.

Plus the **pre-flight log itself**, `pre-flight/log.md`: a single Markdown table with one row per gate, recording the timestamp, the command (or check) you ran, and the observation. The log is the audit trail; a gate without a log entry is, for the rubric, a gate that did not close.

The whole `pre-flight/` folder is two to three pages of writing plus the binary artifacts. Commit each artifact in the commit where its gate closed, so `git log -- pre-flight/` reads as the timeline of the 72 hours.

---

## Part 1 — Day −3: Lock the deck (`slides-vfinal`) (20 points)

The single sin this part prevents: **silent edits to the deck between rehearsal and stage.** A deck that changes after rehearsal is a deck you have not rehearsed.

**(a) Final content sweep against the deck rubric (8 pts).** Before you freeze, do one — and only one — sweep against the PS 8.5 deck rubric: every slide title is a full-sentence claim (not a noun phrase); the design/identification slide shows the contract-form sentence and not the regression equation; the headline slide shows one number with a confidence interval as a figure; the robustness slide is a spec-curve-style coefficient grid; the contribution slide names what you do *not* claim. Anything that fails this sweep gets fixed *now*, not Day-2 night, and never Day-3 morning. State, in the log, which titles changed and why. If nothing changed, log that too — *"final sweep at 18:42 EDT; no titles modified; deck content frozen."* A clean sweep is a strong entry, not an empty one.

**(b) Rename to `vfinal` and commit (4 pts).** Rename the file `paper/slides-vfinal.pdf` (and the source `slides-vfinal.pptx`/`slides-vfinal.tex`). Commit with a message of the form `deck: freeze v-final at $(git rev-parse HEAD)`. The rename is symbolic *and* operational: from this commit forward, anyone who edits `slides-vfinal.*` has just broken the contract and the log must record it. Tag the commit `vfinal-day-minus-3`. The `v-final` filename is the same one Ch 9.1 warned you against using *as a verb* — here it is used as a *lock*, set once at a logged moment, never as a stand-in for "I'm tweaking it again." If you edit the deck after this tag, the tag moves to a new commit and the log records why; you do not silently overwrite.

**(c) Hash the locked deck (4 pts).** Compute the SHA-256 of `slides-vfinal.pdf`:

```bash
shasum -a 256 paper/slides-vfinal.pdf | tee pre-flight/slides-vfinal.sha256
```

Paste the hash into the log. *This is the byte you defend* — the conference-morning upload is byte-identical to this hash, or the gate failed.

**(d) Dry-fit the slide template on the conference projector aspect ratio (4 pts).** Confirm the slide aspect ratio (16:9 vs. 4:3) matches the conference's specified projector. A 4:3 deck shown on a 16:9 projector renders with black bars and tiny figures readable from row two only; this is the avoidable failure mode that has eaten one minute of every twentieth talk in living memory. Render `slides-vfinal.pdf` at the target ratio and visually check the headline figure is legible from a screenshot scaled to a phone screen — that is the back-of-the-room test in miniature. Log the conference-format spec you confirmed.

---

## Part 2 — Day −2: Hash the packet (`make clean && make all` on a fresh clone) (25 points)

This is the *honesty test* from PS 8.5 Part 4(f), re-run from scratch on Day −2 against a clone that has never seen your working directory. The single sin this part prevents: a packet that "works on my machine" because of a stale derived file that a fresh stranger does not have.

**(a) Fresh clone in a clean temp directory (5 pts).** From a directory that contains *none* of your project files (e.g., a brand-new temp folder), run:

```bash
git clone <your-repo-url> /tmp/preflight-$(date +%s) && cd /tmp/preflight-*
```

Log the destination path and the commit hash you cloned (`git rev-parse HEAD`). This must be the same commit your `vfinal-day-minus-3` tag points at *or* a strictly later commit on the same branch — never a divergent local branch, never your working tree.

**(b) Build the pinned environment from `environment.lock.yml` (4 pts).** Recreate the environment from the locked file PS 8.5 Part 4(d) required:

```bash
conda env create -f environment.lock.yml -n preflight && conda activate preflight
```

Log the time the build took and any package that failed to resolve. If something failed to resolve, the lock file has drifted from the world and you must fix it *now*, before conference morning — by repinning to a resolvable lockfile and re-running this step. Do **not** ship a packet whose lock file does not solve; the failure mode is a reviewer who clones your repo on Day-+1, gets a resolver error, and walks away.

**(c) The honesty test: `make clean && make all` (8 pts).** With the fresh clone and the resolved environment, run:

```bash
make clean && make all 2>&1 | tee pre-flight/make-all.log
```

Three observations go in the log: the *total wall-clock time*, the *exit code* (`echo $?` — must be `0`), and whether the rebuilt `paper/paper.pdf` is byte-identical to the committed one. If the rebuilt PDF does not match — a drifted number, a different figure, a regenerated table — find the cause **now**, not on the plane. The Ch 9.1 §3 diagnostic order applies: check the seed first (a missing `np.random.default_rng(SEED)` is the most common culprit), check for a hand-pasted number second, check for a non-deterministic library third (`statsmodels` is deterministic; `sklearn`'s parallel jobs are not without `random_state`). Fix and re-run until the rebuilt PDF matches.

**(d) Hash the packet tarball (4 pts).** Build the distributable archive from the *fresh clone's `HEAD`*:

```bash
git archive --format=tar.gz --prefix=packet/ HEAD > packet.tar.gz
shasum -a 256 packet.tar.gz | tee pre-flight/packet.sha256
```

Paste the hash into the log. This is what a referee clones from on Day +1; it must hash to this value. Commit `pre-flight/packet.sha256` to the *original* repo (not the temp clone) and tag the commit `packet-day-minus-2`.

**(e) Spot-check three numbers against `slides-vfinal` (4 pts).** Open `slides-vfinal.pdf` and pick three numbers: the headline estimate from slide 4, the confidence-interval bounds, and one robustness number from slide 5. Find each in the rebuilt `paper/paper.pdf` (and in the regenerated `paper/tables/main_results.tex`). All three must match to the printed precision. Log the three (number, slide, paper-page-line). If any disagree, you have a drift between the deck and the packet — Ch 9.1's worst-case scenario — and you fix the deck *now* to match the packet (the packet is the ground truth; the deck is the claim *about* the packet). Re-tag `vfinal-day-minus-3` to the new commit and re-hash the slides; log the re-tag.

---

## Part 3 — Day −1: The 7-minute dry-run video (25 points)

A talk in your head is not a talk. The single sin this part prevents: discovering on stage, at minute six, that your eighth slide is the one you should have cut.

**(a) Record the dry-run, end-to-end, against `slides-vfinal.pdf` (10 pts).** Open `slides-vfinal.pdf` (the *frozen* one, not a tweaked copy), start a visible on-screen timer at 0:00, and deliver the talk straight through — no restarts, no edits, no second takes for "I flubbed slide 3." The recording is a *single take*, because the conference is a single take. Target 7:00 ± 0:15; budget exactly one minute per slide (per Ch 8.5 §3, the eighth minute is insurance, not content). Save as `dry-run.mp4` or upload privately to YouTube/Drive and put the link in `dry-run.txt`. Log the total elapsed time and the date.

**(b) Watch your own video, annotated (8 pts).** Watch it once *with the sound on*, slide-by-slide, and write in the log a single sentence per slide of the form: *"slide N — elapsed X:XX — observation."* The observation is brutally honest: *"slide 3 ran 1:42, fifteen seconds long because I re-explained parallel trends after I had already shown the picture"*; *"slide 5 ran 0:35, twenty seconds short because I rushed through the placebo without saying what the placebo showed."* This is not vanity review; it is the timing forensics the §3 cut-line was designed for.

**(c) Decide and document the cut line (4 pts).** Per PS 8.5 Part 1, you already pre-decided one cut line — the one slide you skip if the clock is against you. Confirm that decision *or revise it* based on the dry-run timing in (b). Write it in `qa-script.md`: *"if at the end of slide 3 the clock reads more than 3:30, I skip slide 5 (robustness) and say one sentence in its place: 'the result is stable across clustering, control-group, and bandwidth choices — happy to walk through the curve in Q&A.'"* The cut line is the *spec* for "what would I do if I were 30 seconds behind?", written when you are calm. Never cut the design/identification slide (3) or the headline slide (4); cutting either kills the argument.

**(d) Timing distribution and the over-/under-time fixes (3 pts).** Note in the log the *cumulative* time at the end of each slide. A pattern of "every slide drifts 10 seconds long" is a *pace* problem fixable by deliberately slowing the opening and trimming slide 5; a pattern of "slides 1–4 are fine and slide 6 is two minutes long" is a *content* problem fixable by cutting one bullet, not by talking faster. Name which pattern your video shows, and write the one fix you will apply in the in-the-moment rehearsal Day-0 morning — but **do not edit the deck**. The fix is a rehearsal change, not a content change; `slides-vfinal.pdf` and its hash are now frozen.

---

## Part 4 — Day 0 morning: Q&A script and travel kit (20 points)

Two short artifacts you carry into the room.

**(a) Q&A defense script, printed (10 pts).** From your PS 8.5 Part 3 answers and your PS 9.2 anticipated-questions matrix (drafted in parallel), distill `qa-script.md` to *one page* containing:

- The **two hardest "what about [confound]?" answers** in the four-part template (threat → plausible → what you did → residual concern), short enough to read aloud in 30 seconds each.
- The **one "located I don't know"** — the question you cannot answer, with the *located* honest non-answer that names the mechanism and the check you would run.
- The **single sentence retreat position**: the concession-and-survives sentence you say *if* the fatal critique lands. *"We can't claim causal; what we have shown is a stable empirical regularity that future work with [the better design] should test causally."* This sentence is what keeps you composed in the worst case.

Print it. Yes, paper — the laptop's battery dies, the green room has no charger, and a phone is conspicuous on stage. The page goes in your pocket.

**(b) Travel kit `travel-kit.md` (6 pts).** A short manifest the size of a packing list:

- **The deck, three ways:** `slides-vfinal.pdf` on the laptop, on a USB stick (FAT32-formatted, no Mac-specific filesystem), and emailed to yourself. Three copies prevent one technical failure from canceling your talk.
- **The packet tarball** (`packet.tar.gz` with hash matching `pre-flight/packet.sha256`) on the USB and in a cloud link — the Q&A questioner who wants to clone it later gets one URL on the contribution slide.
- **The 1-page identification-memo card:** a printed copy of your Ch 7.5 identifying-assumption sentence and your two prepared confounder answers — the spine of the talk, on a card.
- **Adapters:** the HDMI, USB-C, and VGA dongles for whatever the conference projector might present. (The dongle that did not fit was responsible for cancelling at least one talk in the last decade; the contingency is cheap.)
- **A printed handout (optional but encouraged):** a single sheet that is the headline figure with one paragraph of context and the repo URL. Hands you these out *after* the talk, not before; never before, or the room reads the punch line before you tell the joke.

**(c) The morning-of go/no-go (4 pts).** Two hours before your talk, run one final check, logged: open `slides-vfinal.pdf` and confirm its SHA-256 matches `pre-flight/slides-vfinal.sha256` from Day −3. *If the hash matches, you are go.* If not, something silently edited your deck (a re-export from PowerPoint, a font-substitution re-render, a "helpful" Drive sync) — restore from the Day −3 commit by `git checkout vfinal-day-minus-3 -- paper/slides-vfinal.pdf` and re-hash. Log the result. You do not walk on stage with a deck whose hash does not match.

---

## Part 5 — The pre-flight log (`log.md`) (10 points)

The log is the audit trail. Without it, every claim above is unverifiable. The minimum row format:

| Gate | Day | Local time | Command / check | Observation | Pass? |
|---|---|---|---|---|---|
| 1a final sweep | −3 | 2026-08-14 18:42 EDT | manual title test | all 7 titles are full-sentence claims; slide 5 title shortened from 19→14 words | Y |
| 1c slide hash | −3 | 2026-08-14 19:05 EDT | `shasum -a 256 slides-vfinal.pdf` | `e3b0c44…852b855` (stored in `slides-vfinal.sha256`) | Y |
| 2c make-all | −2 | 2026-08-15 09:11 EDT | `make clean && make all` (fresh clone) | exit 0; 11m 04s; PDF byte-identical | Y |
| 2d packet hash | −2 | 2026-08-15 09:25 EDT | `shasum -a 256 packet.tar.gz` | `7f4a9c…01dd33` | Y |
| 3a dry-run | −1 | 2026-08-16 14:00 EDT | single-take recording, visible timer | 7:08 total; slide 3 long, slide 5 short | Y |
| 4c morning-of | 0 | 2026-08-17 08:00 EDT | `shasum -a 256 slides-vfinal.pdf` | hash matches Day −3 | Y |

Every gate from Parts 1–4 has a row. A failed gate is logged honestly as `Pass? N`, with the row immediately following describing the fix and the re-run.

Grading on the log:

- **Completeness (5 pts):** every required gate has a row; failed gates are recorded and re-run rows follow.
- **Verifiability (5 pts):** each row's "Observation" cites a file, a hash, or an exit code a grader can independently check — not a self-assessment like "looked good."

---

## Submission checklist

Before you commit, confirm:

- [ ] `pre-flight/slides-vfinal.pdf` exists, is the frozen Day −3 deck, and `pre-flight/slides-vfinal.sha256` records its hash; the tag `vfinal-day-minus-3` points at the commit where it was frozen (and re-tagged if Part 2(e) forced an edit).
- [ ] `make clean && make all` ran on a *fresh clone* on Day −2 with exit code 0 and a byte-identical rebuilt `paper/paper.pdf`; `pre-flight/make-all.log` is committed.
- [ ] `pre-flight/packet.sha256` records the hash of `packet.tar.gz` built from the Day −2 commit; the tag `packet-day-minus-2` points at it.
- [ ] `dry-run.mp4` (or `dry-run.txt` with a working link) records the single-take 7-minute talk against `slides-vfinal.pdf` with a visible timer; total time is logged.
- [ ] `qa-script.md` is one page: two prepared confounder answers, one located "I don't know," and one retreat-position sentence — formatted to read aloud, never paragraphs of prose.
- [ ] `travel-kit.md` manifests the three deck copies, the packet on USB + cloud link, the identification-memo card, and the adapter list.
- [ ] The morning-of hash check ran two hours before your talk and matches the Day −3 hash; the row is in the log.
- [ ] `pre-flight/log.md` has one row per gate (Parts 1–4) with timestamp, command, observation, and pass/fail; any failed gate is followed by a fix-and-re-run row.

---

## How this is graded

Part 1 (deck lock, 20) on whether the deck froze and stayed frozen — the hash on Day 0 morning must match the hash on Day −3. Part 2 (packet hash, 25 — the heaviest part) on whether the honesty test ran on a *fresh clone* and the slide-cited numbers match the packet-produced numbers. Part 3 (dry-run video, 25) on whether the single-take talk happened, was watched, and produced a logged cut line and timing fix. Part 4 (Q&A script + travel kit, 20) on whether you can walk to the lectern with paper in your pocket. Part 5 (log, 10) on whether a grader can audit every claim. The highest-signal single check, the one that decides borderline cases: **does the Day −3 slide hash equal the morning-of slide hash?** A `Y` there is the single-bit certificate that no silent edit slipped in; an `N` followed by a fix-row is honest and acceptable; a missing row is the same as a `N` you concealed, and is graded as such.

---

## The bridge to PS 9.2

PS 9.1 gives you a frozen deck and a hashed packet; PS 9.2 gives you the *questions* you will be asked about them. The Q&A defense sheet in Part 4 is a *placeholder* for the full anticipated-questions matrix PS 9.2 builds — twelve questions minimum, each mapped to the slide it lands on and the backup slide that answers it. The two hardest answers from that matrix become the two answers in your Day-0 `qa-script.md`. You cannot rehearse against questions you have not written down; PS 9.2 is the writing-down.

*End of PS 9.1. The model deliverable is in `book/appendices/E-solutions-manual/E-w9-ps9.1-solutions.md`. Run your own 72-hour drill first; read the exemplar to calibrate, not to copy. The hash that closes the gate and the discipline that produces it are the same thing — this assignment is you proving, in writing, that the deck you upload is the deck you rehearsed.*
