# Model Deliverable — PS 9.1 (The 72-Hour Pre-Flight Checklist)

**Problem set:** `book/weeks/week-09/ps9.1.md` (PS 9.1, Week 9).
**Chapter:** Ch 9.1 — The 72-Hour Pre-Flight Checklist.

PS 9.1 has no numeric answer key: it is a project deliverable, and what is graded is the *discipline of closing the gates* on a real conference deck and a real replication packet, not a finding. So this appendix entry is not a worked solution but a **model deliverable**: a complete, A-grade 72-hour pre-flight folder for one cast project (Devon's spot-Bitcoin-ETF event study), with every artifact specified by Parts 1–5 of PS 9.1 produced in concrete form, followed by **instructor grading notes** that key each gate to the rubric and call out the moves that earn (and lose) points.

The project is **Devon's spot-Bitcoin-ETF event study** — the daily-frequency CAR design he carried from his Week-7 pre-analysis plan into the Week-8 paper: *does the launch of a U.S. spot Bitcoin ETF reduce the realized volatility of the underlying token?* His primary estimate is the cumulative abnormal change in realized volatility over event days $[0, +20]$, with a Fama-French-style market-model first stage, clustered by event date. Every magnitude below is **illustrative** — the headline CAR-on-volatility figure of roughly $-9$% over the 20-day window, the confidence interval, the hash values — is presented as a worked *pre-flight* example to show what an A-grade pre-flight folder looks like, not as a claimed empirical finding about Bitcoin ETFs; the real numbers come out of `make all` on Devon's pinned data vintage.

---

## THE MODEL DELIVERABLE — `pre-flight/`

The folder structure as committed in Devon's repo:

```
pre-flight/
├── log.md                          # Part 5: the gate-by-gate audit trail
├── slides-vfinal.sha256            # Part 1c: Day -3 deck hash
├── packet.sha256                   # Part 2d: Day -2 packet tarball hash
├── make-all.log                    # Part 2c: stdout of the honesty test on a fresh clone
├── dry-run.mp4                     # Part 3a: 7-minute single-take video (committed as Git LFS)
├── qa-script.md                    # Part 4a: the printed one-page Q&A defense
└── travel-kit.md                   # Part 4b: the conference-day go-bag manifest
```

The `slides-vfinal.pdf` file itself sits in `paper/slides-vfinal.pdf`, with the `vfinal-day-minus-3` tag pointing at the commit that froze it; `packet.tar.gz` is built from `HEAD` on Day −2 and not committed (it is regenerated on demand), but its hash is committed.

---

### Part 1 — Day −3: Lock the deck

#### 1(a) Final content sweep — 18:42 EDT, 2026-08-14

Devon ran the title-test sweep against the seven slides of his deck. Three changes resulted:

- **Slide 3 (design):** title changed from *"Identifying the ETF effect on volatility"* (noun phrase, fails the title test) to *"Our estimate is causal if no other Bitcoin-market shock coincided with the SEC approval date — which we defend with a placebo window and a clean event-day comparison."* The new title is a contract-form sentence (PS 8.5 Part 1(c)).
- **Slide 5 (robustness):** title shortened from a 19-word run-on to a 14-word claim: *"The headline -9% is stable across event-window length, market-model controls, and clustering choices."*
- **Slide 6 (contribution):** added the *what-we-do-not-claim* clause that was missing — *"...we do not show that the volatility reduction is permanent beyond a 60-day horizon."*

The other four slides passed the sweep unchanged. The sweep is logged with the timestamp and the three changes; no further edits permitted.

#### 1(b) Rename to `vfinal` and tag — 19:02 EDT

```bash
mv paper/slides-draft.pdf paper/slides-vfinal.pdf
mv paper/slides-draft.tex paper/slides-vfinal.tex   # Beamer source
git add paper/slides-vfinal.*
git commit -m "deck: freeze v-final at $(git rev-parse HEAD)"
git tag vfinal-day-minus-3
```

Commit hash: `a7c3b91`. Tag annotated: *"deck frozen Day -3, sweep complete; no edits permitted past this point."*

#### 1(c) Hash the locked deck — 19:05 EDT

```bash
$ shasum -a 256 paper/slides-vfinal.pdf | tee pre-flight/slides-vfinal.sha256
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855  paper/slides-vfinal.pdf
```

*(Hash is illustrative — the empty-string SHA-256 used as a placeholder; the real hash is what `shasum` returns on Devon's file.)* The hash is committed; the morning-of check in Part 4(c) will compare against it.

#### 1(d) Aspect-ratio dry-fit — 19:18 EDT

Devon confirmed the conference upload portal specifies 16:9. His Beamer source already used `\documentclass[aspectratio=169]{beamer}`, so the slides render at 16:9 without modification. He took a phone-sized screenshot of slide 4 (the headline event-study CAR plot) — axis labels and CI band visible at thumb-size, the back-of-the-room legibility test passed. Logged.

---

### Part 2 — Day −2: Hash the packet

#### 2(a) Fresh clone — 09:11 EDT, 2026-08-15

```bash
$ cd /tmp && mkdir preflight-1755271860 && cd preflight-1755271860
$ git clone https://github.com/CAMP-ORG/capstone-2026-devon .
$ git rev-parse HEAD
a7c3b91...   # matches vfinal-day-minus-3 plus one bug-fix commit
```

Devon notes: the cloned HEAD (`a7c3b91`) is one commit *ahead* of the `vfinal-day-minus-3` tag — the bug-fix commit (`b1f4a02`) fixed a typo in the README's `make` usage and did not touch the deck or the packet. Acceptable per the PS 9.1 rule that the clone must be at or strictly after the tag, on the same branch.

#### 2(b) Build the pinned environment — 09:13 EDT, 4 min wall time

```bash
$ conda env create -f environment.lock.yml -n preflight
# 4 min 12 s; all packages resolved; no warnings
$ conda activate preflight
$ python --version
Python 3.11.9
```

All packages resolved on first try. The lock file is healthy.

#### 2(c) The honesty test — 09:17 EDT to 09:28 EDT

```bash
$ make clean && make all 2>&1 | tee pre-flight/make-all.log
# ... (full log committed to pre-flight/make-all.log) ...
$ echo $?
0
$ shasum -a 256 paper/paper.pdf
8a4d9c... paper/paper.pdf  # matches committed paper.pdf's hash
```

Wall time: 11 minutes 04 seconds. Exit code: 0. Rebuilt `paper/paper.pdf` is byte-identical to the committed copy.

Devon notes a near-miss in the log: the first `make all` attempt (not the one above) drifted on the headline CAR number by 0.003 percentage points, because the bootstrap confidence interval for the volatility-reduction estimate used a missing `random_state` in a `sklearn.utils.resample` call. Devon traced it (Ch 9.1 §3 diagnostic order: seed first, hand-paste second, library determinism third) and fixed it by adding `random_state=SEED` to the `resample` call. The above run, after the fix, hashes correctly. *This is the kind of near-miss the pre-flight is built to catch.*

#### 2(d) Hash the packet tarball — 09:30 EDT

```bash
$ git archive --format=tar.gz --prefix=packet/ HEAD > /tmp/packet.tar.gz
$ shasum -a 256 /tmp/packet.tar.gz | tee /mnt/e/ccli/8weeks/book/.../pre-flight/packet.sha256
7f4a9c01dd33...  /tmp/packet.tar.gz
$ git add pre-flight/packet.sha256
$ git commit -m "packet: hash on day -2 fresh clone"
$ git tag packet-day-minus-2
```

#### 2(e) Spot-check three numbers — 09:35 EDT

Devon opened `slides-vfinal.pdf` and checked:

| Slide # | Number | In `paper/paper.pdf` | In `paper/tables/main_results.tex` | Match? |
|---|---|---|---|---|
| 4 (headline) | $-9.1\%$ CAR-on-vol over $[0,+20]$ | Table 2, row 1, col 2 | line 14, column 2 | Y |
| 4 (CI) | $[-13.2\%, -5.0\%]$ | Table 2, row 1, col 3 | line 14, column 3 | Y |
| 5 (robustness) | range $[-11.2, -7.4]$ across 12 specs | Table 3, last row | line 22, column 4 | Y |

All three matched to the printed precision. *Result: deck and packet are coherent; no re-hash needed.*

---

### Part 3 — Day −1: The 7-minute dry-run

#### 3(a) Record the single take — 14:00 EDT, 2026-08-16

Devon recorded `dry-run.mp4` against `slides-vfinal.pdf` displayed full-screen, with a phone-stopwatch in the corner of the frame. Total elapsed: **7:08**. Acceptable per the 7:00 ± 0:15 budget. Single take, no restarts.

#### 3(b) Slide-by-slide watch with annotations — 18:00 EDT

| Slide | Elapsed | Observation |
|---|---|---|
| 1 (question) | 0:32 | clean; question delivered without re-phrasing |
| 2 (why) | 0:58 | on budget; the "$1.5 trillion market cap" line lands |
| 3 (design) | 2:35 | ran **1:37**, 22 seconds long — re-explained the market-model first-stage after the picture had already shown it; need to trust the figure on the day |
| 4 (headline) | 3:55 | 1:20, on budget; the -9.1% lands with the CI |
| 5 (robustness) | 4:30 | ran **0:35**, 25 seconds short — rushed the placebo, only said "we tried placebos and they don't fire"; need to add the one-sentence interpretation back in |
| 6 (contribution) | 5:25 | 0:55 on budget; the "we do not claim permanent" clause delivered |
| Close + thanks | 5:32 | on budget |
| Total | 7:08 | (includes the 1:36 spent on the title and opening orientation) |

#### 3(c) Cut-line decision — 18:35 EDT

Devon's PS 8.5 cut-line was "skip slide 5 (robustness) if behind at end of slide 3." After watching the dry-run, he revised: the new cut-line in `qa-script.md` reads:

> *"If at the end of slide 3 the clock reads more than 3:30, I skip slide 5 and replace it with one sentence: 'the headline is stable across event-window, market-model, and clustering choices — the spec curve is in backup if anyone wants to see it.' I never cut slides 3 (design) or 4 (headline)."*

The revision is logged.

#### 3(d) Timing pattern and fix — 18:40 EDT

The pattern: slides 1–4 cumulatively drift 15 seconds long; slide 5 is short. This is a *content* pattern on slide 3 (over-explanation), not a *pace* pattern. Fix: deliberately trust the design figure on slide 3; do not re-narrate what the figure already shows. *No deck edit*; this is a rehearsal change, applied in Day-0 morning rehearsal.

---

### Part 4 — Day 0 morning: Q&A script and travel kit

#### 4(a) `qa-script.md` — printed to one page

```
=== Q&A SCRIPT — Devon R., spot-Bitcoin-ETF event study ===

QUESTION 1 (most likely): "Was the SEC approval really a surprise?
Markets had been pricing it for months."
ANSWER:
  Threat:    yes, that's the central worry.
  Plausible: futures-based ETFs had been live for 2 years; spot was widely expected.
  What I did: defined the event date as the SEC release timestamp, not the
             rumor-day; ran a placebo on the prior 3 false-rumor dates that all
             came back null; computed the abnormal IV from the options market
             on the day showing a jump only on the release date, not the rumor days.
  Residual:  if traders front-ran the *exact* release timestamp by minutes,
             my CAR underestimates; my magnitude is therefore a *lower bound*
             on the true effect.

QUESTION 2 (likely): "Why daily and not intraday? You're missing
the news arrival."
ANSWER:
  Threat:    daily can wash out the announcement effect.
  Plausible: intraday is the cleaner identification for high-frequency events.
  What I did: I tested both; backup slide C shows the intraday version, which
             gives a -10.2% CAR vs. the -9.1% daily — same sign, larger magnitude.
             I report daily as primary because the intraday data is licensed and
             not in the replication packet; daily is fully reproducible.
  Residual:  the daily underestimates by ~1 pp; the choice is data-availability,
             not preference.

LOCATED I-DON'T-KNOW:
  Q: "Does this generalize to Ethereum?"
  A: "I don't know — my design can't speak to that. The Ether spot ETFs hadn't
     launched at my sample's cutoff. My guess is yes, qualitatively, because
     the mechanism (broadening the investor base and adding APs as liquidity
     providers) is structural; but I'd want to re-run on the actual ETH event
     dates before claiming it."

RETREAT POSITION (if the fatal critique lands):
  "If the SEC approval date wasn't a surprise in the sense my placebos test,
  then I cannot claim causal — what I have shown is a stable empirical
  regularity around the ETF launch that future work with the surprise
  identified at higher frequency should test causally."
```

The script is printed on a single page (24 pt sans-serif), folded into the inside-jacket pocket. Tested aloud: each prepared answer reads in 35–40 seconds.

#### 4(b) `travel-kit.md` — the go-bag manifest

```
=== CONFERENCE TRAVEL KIT — Devon R., 2026-08-17 session ===

DECK (three copies):
  [ ] laptop: paper/slides-vfinal.pdf (and .pptx export as backup)
  [ ] USB stick (FAT32, 32GB Kingston): slides-vfinal.pdf + packet.tar.gz
  [ ] cloud: emailed to leigao.gmu@gmail.com + uploaded to Drive
             https://drive.google.com/file/d/[link]/view

PACKET (one canonical link, one local copy):
  [ ] repo URL on contribution slide: github.com/CAMP-ORG/capstone-2026-devon
  [ ] QR code (3x3 inches, printed on poster) encoding the URL
  [ ] packet.tar.gz on USB (hash verified to match pre-flight/packet.sha256)

THE CARD:
  [ ] 1-page identification-memo card (4x6 index card):
      side A: the contract-form identifying-assumption sentence
      side B: the two prepared confounder answers in compressed form

THE SCRIPT:
  [ ] qa-script.md printed, folded in jacket pocket

ADAPTERS:
  [ ] HDMI-to-USB-C (the laptop's native port)
  [ ] HDMI-to-VGA (in case the projector is older)
  [ ] HDMI-to-DisplayPort (in case the room has only DP)
  [ ] presenter remote with built-in laser pointer (Logitech R400)
  [ ] spare AAA batteries for the remote

OPTIONAL BUT BROUGHT:
  [ ] 25 printed handouts (single-sheet: headline figure + 1-paragraph
      summary + repo URL). Handed out AFTER the talk, never before.
  [ ] paper notepad and pen for Q&A note-taking
```

#### 4(c) Morning-of go/no-go — 08:00 EDT, 2026-08-17

```bash
$ shasum -a 256 paper/slides-vfinal.pdf
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855  paper/slides-vfinal.pdf
$ diff slides-vfinal.sha256 <(shasum -a 256 paper/slides-vfinal.pdf | awk '{print $1"  paper/slides-vfinal.pdf"}')
# no output: hashes match
```

**Hash matches the Day −3 hash. Go.** Logged with timestamp.

---

### Part 5 — The pre-flight log (`log.md`)

| Gate | Day | Local time | Command / check | Observation | Pass? |
|---|---|---|---|---|---|
| 1a final sweep | −3 | 2026-08-14 18:42 EDT | manual title test | 3 titles revised (3, 5, 6); contract-form sentence added to slide 3 | Y |
| 1b vfinal commit + tag | −3 | 2026-08-14 19:02 EDT | `git tag vfinal-day-minus-3` at `a7c3b91` | tag created | Y |
| 1c slide hash | −3 | 2026-08-14 19:05 EDT | `shasum -a 256 slides-vfinal.pdf` | `e3b0c44...852b855` recorded in `slides-vfinal.sha256` | Y |
| 1d aspect ratio | −3 | 2026-08-14 19:18 EDT | render check + phone-screenshot legibility | 16:9 confirmed; axes readable | Y |
| 2a fresh clone | −2 | 2026-08-15 09:11 EDT | `git clone` to `/tmp/preflight-1755271860` | HEAD `a7c3b91` + 1 bug-fix commit `b1f4a02` | Y |
| 2b env build | −2 | 2026-08-15 09:13 EDT | `conda env create -f environment.lock.yml` | 4m 12s; all resolved | Y |
| 2c make-all (1st attempt) | −2 | 2026-08-15 09:17 EDT | `make clean && make all` (fresh clone) | CAR drifted 0.003 pp; FAIL | N |
| 2c fix + re-run | −2 | 2026-08-15 09:24 EDT | added `random_state=SEED` to `sklearn.utils.resample` | re-ran; exit 0; PDF byte-identical | Y |
| 2d packet hash | −2 | 2026-08-15 09:30 EDT | `shasum -a 256 packet.tar.gz` | `7f4a9c01dd33...` recorded in `packet.sha256` | Y |
| 2e spot-check 3 numbers | −2 | 2026-08-15 09:35 EDT | manual reconcile slide ↔ paper ↔ table | all 3 match | Y |
| 3a dry-run | −1 | 2026-08-16 14:00 EDT | single-take recording with visible timer | 7:08 total; saved to `dry-run.mp4` | Y |
| 3b watch with annotations | −1 | 2026-08-16 18:00 EDT | slide-by-slide table | slide 3 long (1:37), slide 5 short (0:35) | Y |
| 3c cut-line | −1 | 2026-08-16 18:35 EDT | revised in `qa-script.md` | cut slide 5 not slide 3 if behind | Y |
| 3d pattern fix | −1 | 2026-08-16 18:40 EDT | logged as rehearsal change | trust the design figure on slide 3 | Y |
| 4a Q&A script | 0 | 2026-08-17 06:30 EDT | printed `qa-script.md` to one page | 24 pt sans-serif; in pocket | Y |
| 4b travel kit | 0 | 2026-08-17 06:45 EDT | manifest checked | 3 deck copies, packet on USB, adapters, card, handouts | Y |
| 4c morning-of hash | 0 | 2026-08-17 08:00 EDT | `shasum -a 256 slides-vfinal.pdf` | matches Day −3 hash; GO | Y |

The row showing the failed first `make-all` attempt is the single most honest entry in the log: it records the near-miss, the diagnosis (seed first per Ch 9.1 §3), and the fix that produced a byte-identical rebuild on the second attempt.

---

## INSTRUCTOR GRADING NOTES

### Where this deliverable earns full marks

- **Part 1 (deck lock, 20/20).** The sweep produced *named* revisions (three titles, identified by slide number, with the rule each violated and the corrected form). The freeze is a tagged commit; the hash is recorded; the aspect-ratio dry-fit was logged. This is the bar.
- **Part 2 (packet hash, 25/25 — the heaviest part).** The work was done on a *fresh clone* in a clean temp directory, not in the working copy. The lock file resolved on first try. The honesty test caught a real near-miss (the `resample` seed) and logged the failed first attempt before the successful second — this is exactly the audit-trail discipline the rubric rewards. The spot-check of three numbers reconciled slide ↔ paper ↔ TeX table.
- **Part 3 (dry-run, 25/25).** Single take, 7:08 total, visible timer. The watch-with-annotations identified a *content* pattern on slide 3 (over-explanation) rather than a *pace* pattern, which is the diagnostic distinction the rubric tests. The cut-line was revised on the basis of the dry-run timing, not the pre-rehearsal guess.
- **Part 4 (Q&A + travel kit, 20/20).** The script is one page, formatted to read aloud (large font, the four-part shape laid out in block form, not paragraphs). The travel kit's three deck copies survive any single device failure. The morning-of hash check matched the Day −3 hash — the single-bit certificate that no silent edit slipped in.
- **Part 5 (log, 10/10).** Every gate has a row with a timestamp, a command, an observation citing a file or exit code, and a pass/fail flag. The failed-then-fixed gate 2c shows the discipline: log the failure, fix it, re-run, log the success — never silently overwrite.

### What loses points (illustrative)

- A deck that was edited *after* the Day −3 tag without re-tagging and re-hashing. The smoking gun: the morning-of hash differs from the Day −3 hash, the log does not record a re-tag, and a grader cannot tell what was edited.
- A `make all` honesty test run on the working copy instead of a fresh clone. The rebuild "works" but the test does not exercise the property the gate is designed to verify (that a stranger's machine can rebuild from scratch).
- A dry-run recorded against an *earlier* version of the deck — *"I rehearsed against the draft, not slides-vfinal.pdf"*. The rehearsal then drifts from the conference upload and the practice is wasted.
- A Q&A script that is a paragraph-prose document. It reads on the page but cannot be glanced at in 5 seconds at the lectern; the format is the discipline.
- A log that has rows but no command-output evidence — *"slide hash: looks good"* loses points for unverifiability; *"slide hash: `e3b0c44...852b855`"* earns them.

### The highest-signal single check

**Does the Day −3 slide hash equal the morning-of slide hash?** Devon's deliverable: yes (both `e3b0c44...852b855`). That single bit says no silent edit slipped in between rehearsal and stage — the deck the audience sees is the deck he rehearsed against. A `N` followed by a fix-row would have been acceptable (a forced re-export, properly logged); a missing morning-of check or an `N` without a fix-row is a fail.

*End of model deliverable. This A-grade exemplar is one shape the assignment can take; the structure (Parts 1–5, the seven artifacts, the log discipline) is required of any submission, but the specific commands, hashes, and timing observations will be project-specific. The point of reading the exemplar is to see what the standard looks like in a concrete case, not to copy its details into a project that needs different ones.*
