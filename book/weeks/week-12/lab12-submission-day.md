# Lab 12 — Submission Day Lab: Live Packet Upload, SSRN Pre-Print, MARS Deposit, FMA Intent-to-Submit, and the Reproducibility Attestation

Week 11's lab compiled a camera-ready PDF from one command. Chapters 12.1 through 12.5 explained what each component of the submission packet is *for*, why the SSRN preprint matters, how the decade-long arc unfolds, where the conference ecosystem sits, and what waits on the other side of the editor's email. **Today's lab is the lab where you actually press *submit*.**

Here is the move this lab turns on. **The submission of a research paper is not a procedural task you attend to with half your attention; it is a five-window, single-session ritual in which the manuscript that has sat in your repository for fourteen weeks crosses an irreversible threshold into the public record.** Two hours from now your paper will exist on the Schar Young Scholars Journal editorial system, your name will be on the SSRN finance network, your MARS handle will be propagating to Google Scholar, and an FMA Undergraduate Poster Session intent-to-submit will be pending review. The version of you that walks out of this lab is the version that has submitted a research paper.

The lab runs as a *single live session* — four hours, instructor present, cohort sharing one screen for each platform walkthrough and breaking into individual windows for student-specific values. The live format resolves platform idiosyncrasies (Schar expects PDF/A; SSRN's JEL picker has a known UX bug for triple-digit codes; MARS defaults to "All rights reserved" rather than the open license the camp uses) in five minutes that an individual student would spend an hour on. The lab ends with the program's exit interview — a structured conversation between you and Prof. Gao — and the signing of a **reproducibility-attestation document** declaring the manuscript reproducible from the repository and the submission binding.

The analysis needs no internet — the manuscript is already built, the tables generated, the bibliography verified — but the lab is *entirely online* because the submission act is online. **Budget four and a half hours: 30 min setup, 45 min Schar, 30 min SSRN, 30 min MARS, 20 min FMA, 60 min exit interview, 15 min attestation.**

---

## Learning goals

By the end of this lab you will have:

1. **Submitted the complete five-component packet to the Schar Young Scholars Journal** through the ScholarOne editorial portal — manuscript, cover letter, CRediT author statement, data-and-code availability statement, conflicts-of-interest declaration — with the submission ID logged and the receipt PDF archived in your repository under `submission/receipts/`.
2. **Posted the preprint to SSRN** with primary network (Financial Economics Network), secondary networks chosen from Ch 12.2 §4, the JEL codes from your manuscript title page, your ORCID linked, the MARS handle named in the abstract, and the versioning footnote on the title page; the SSRN abstract-page URL logged and the posting confirmation email archived.
3. **Deposited the paper plus replication package in MARS** through the GMU Libraries deposit portal — manuscript PDF, replication ZIP, metadata fields populated, open-license rights statement selected, and the handle assigned; the handle string logged.
4. **Filed the FMA Undergraduate Poster Session intent-to-submit form** for the October FMA annual meeting — abstract entered, advisor signature obtained from Prof. Gao live in the session, registration-fee waiver requested through the FMA's high-school-author program.
5. **Completed the program exit interview** with Prof. Gao — twelve structured questions across substantive learning, methodological identity, venue identity, the one-year plan, and the five-year plan — with the interview recorded (audio only, with consent) and the transcript filed in your private research journal.
6. **Signed the reproducibility-attestation document** — a one-page statement of authorship, reproducibility, originality, and submission-as-binding — wet-signed on paper (or DocuSigned remote), with the signed copy filed both in your repository and with the camp registrar.

The cohort gathers Friday afternoon at 4 PM Eastern for the closing ceremony: each student names the paper they submitted, the SSRN handle, the MARS handle, and the one sentence from their five-year research-identity memo (the sentence from PS 12.5 §6) that they are committing to publicly. The ceremony is the camp's last formal session. The work continues; the camp does not.

---

## Setup — the five-platform reconnaissance

Before any submission window opens, verify that the manuscript and the packet are *ready*. The Lab 11 build manifest is the contract. Open a terminal in your capstone repository and run the five verification commands:

```bash
cd ~/capstone-2026-<you>

# 1. The manuscript still builds.
make clean && make paper
ls -la manuscript/main.pdf  # exists, ~3-5 MB, dated today

# 2. The verified bibliography passes.
make bibcheck
# Expected: "OK: NN citations all verified."

# 3. The replication package is current.
make replication_package
ls -la submission/replication_package.zip
# Expected: ZIP exists, <50 MB, contains src/, data/clean/, manuscript/, README, requirements.txt

# 4. The five packet components are all present.
ls -la submission/packet/
# Expected files:
#   01_manuscript.pdf
#   02_cover_letter.pdf
#   03_credit_statement.pdf
#   04_data_code_availability.pdf
#   05_conflicts_of_interest.pdf

# 5. The git working tree is clean and the commit hash is logged.
git status                       # nothing to commit
git rev-parse --short HEAD       # this hash is the submission-commit hash
git log --oneline -5             # confirm the manuscript-finalization commit is the most recent
```

If any of the five checks fails, *stop and fix it first.* A submission with an unbuildable manuscript is a submission you will have to retract. For synthetic-DGP students, `make replication_package` ships the ZIP from the Week-2 DGP scripts plus the cleaned panel; for licensed-data students, the ZIP contains the code with a `.gitignore`d data-folder marker and WRDS instructions for the referee. Either is acceptable.

Make a backup of `submission/packet/` to a second location (cloud, USB, second laptop). The Murphy's-Law lab is the one where your laptop dies at minute 47.

The five platform URLs, bookmarked in advance:

1. **Schar Young Scholars Journal portal (ScholarOne):** `https://mc.manuscriptcentral.com/scharyoungscholars` (account provisioned under your `<you>@gmu.edu`).
2. **SSRN submission form:** `https://hq.ssrn.com/submissions/CreateNewAbstract.cfm` (account created in Week 5; login with ORCID).
3. **MARS deposit portal:** `https://mars.gmu.edu/submit` (Shibboleth SSO with `<you>@masonlive.gmu.edu`).
4. **FMA Undergraduate Poster Session intent form:** linked from the FMA's "Programs for Students" page; the 2026 intent window is open through July 31.
5. **DocuSign reproducibility-attestation envelope:** the camp registrar sends the envelope at 3:00 PM Eastern on lab day; do not click *Sign* until the instructor walks the cohort through it.

---

## Part 1 — The Schar Young Scholars Journal submission (45 minutes)

This is the longest of the four upload steps because it has the most components and the most-strict validation. Allocate 45 minutes; the instructor walks the cohort through the screens together. Maya's flow is the carrying example; Devon, Priya, Sam, and Leah enter their own values at each step.

### 1.1 Login and corresponding-author confirmation

Login with your `<you>@gmu.edu` email. Click *Start New Submission*. Step 1 confirms the corresponding-author identity; fields are pre-populated. Verify the displayed name matches your cover-letter §1 exactly — the editorial office uses the ScholarOne record. Tick the *Confirm corresponding-author email* checkbox; click the verification link in your inbox.

### 1.2 Step 2 — Manuscript type, title, abstract

Select manuscript type — *Research Article* for camp papers (others are *Methodological Note* and *Replication Study*). Paste the manuscript title (250-character cap). Paste the 245-word abstract; ScholarOne renders the math notation as plain text, so replace `$\beta$` with β and `$\Delta_{\text{post}}$` with Δpost *in the abstract-field paste only* — do not edit the manuscript abstract.

### 1.3 Step 3 — Keywords and JEL codes

Three to seven keywords (free text), three to five JEL codes (hierarchical menu — same codes as your manuscript title page). Maya's keywords: *fair lending, mortgage denial, staggered difference-in-differences, bank supervision, HMDA*. Her JEL codes: G21, G28, J15. The hierarchical picker is sluggish; the instructor demonstrates the click path. Triple-check the codes against the title page — mismatches are flagged by the editorial-office reviewer.

### 1.4 Step 4 — Authors and affiliations

First author is pre-populated. Click *Add Author* and enter Prof. Gao: Lei Gao, Costello College of Business, George Mason University, `lgao9@gmu.edu`, with ORCID. The cohort is acknowledged in the manuscript but not co-authored — do *not* add cohort members to the Step-4 author list.

### 1.5 Step 5 — File uploads (the five components)

Separate uploads of:

- **Main Document**: `submission/packet/01_manuscript.pdf` (≤25 MB). If oversized, compress with `gs -sDEVICE=pdfwrite -dPDFSETTINGS=/prepress -dNOPAUSE -dBATCH -sOutputFile=out.pdf 01_manuscript.pdf`.
- **Cover Letter**: `02_cover_letter.pdf` (≤2 MB).
- **CRediT Author Statement**: `03_credit_statement.pdf` from `nb12.1`; verify all fourteen roles are assigned.
- **Data and Code Availability Statement**: `04_data_code_availability.pdf` (≤2 MB).
- **Conflicts of Interest Declaration**: `05_conflicts_of_interest.pdf`. For Prof. Gao as mentor co-author on a fair-lending-adjacent paper, the document names his Congressional testimony work as relevant disclosure.

After each upload, ScholarOne shows a green checkmark; if it errors, the most common cause is a PDF/A variant the validator rejects. Re-export without the `pdfa` flag.

### 1.6 Step 6 — Suggested reviewers

Two to four suggested reviewers (Ch 12.1 §4.4 discipline). Maya's are three GMU economics PhD students working on banking and fair lending, named by Prof. Gao in prep. Do *not* suggest senior faculty whose papers you cite (they are conflicted out). ScholarOne needs each reviewer's email.

### 1.7 Step 7 — Submit

The summary screen lists every field and the five uploaded files. Read it slowly; most-common late fixes are title typos, math-notation render issues, and JEL-code slips. Click *Submit*. The system displays a confirmation page with submission ID `SYSJ-2026-XXXXX`. **Screenshot to `submission/receipts/01_schar_confirmation.png`.** ScholarOne emails confirmation within five minutes; save as `submission/receipts/01_schar_email.pdf`.

The editorial office acknowledges receipt within one business day; the first decision arrives in 6–10 weeks. The clock starts now.

---

## Part 2 — The SSRN pre-print posting (30 minutes)

SSRN is faster than Schar (eight to fifteen minutes start-to-live in normal conditions) but the metadata discipline is stricter because the SSRN abstract page is what Google Scholar indexes and what citing papers link to.

### 2.1 Login and start

Login through ORCID. Click *Create New Abstract*. The form is one long single-page web form, not a wizard; save a draft every two minutes to avoid losing work to a tab close.

### 2.2 Metadata block

- *Title*, *Abstract*, *Keywords*, *JEL Codes*: same values as Schar. SSRN's JEL picker is a single search-as-you-type box (far better than ScholarOne's); enter "G21, G28, J15" comma-separated.
- *Date Written*: today's date.

### 2.3 Networks (Ch 12.2 §4)

One *primary network* (gets the paper in the weekly email) and two to four *secondary networks* (the paper appears in network listings but not the weekly email).

Maya — Primary: Financial Economics Network (FEN); Secondaries: Banking & Financial Institutions, Discrimination Law & Justice, Real Estate. Devon — Primary: FEN; Secondaries: Cryptocurrency, Information Systems & eBusiness, Risk Management. Priya — Primary: Insurance Law & Policy; Secondaries: Climate Change, Sustainability Research. Sam — Primary: Capital Markets: Asset Pricing; Secondaries: Behavioral & Experimental Finance, Market Microstructure. Leah — Primary: Innovation & Patent Law; Secondaries: IO: Productivity, Computational Linguistics. Network is sticky; consult Prof. Gao if uncertain.

### 2.4 Affiliations and co-authors

Your high-school name as primary affiliation; "NextGen 8-Week Empirical-Finance Camp, George Mason University" as secondary. Add Prof. Gao as co-author by ORCID — SSRN links the paper to his author page, where researchers visiting his profile can click through to yours.

### 2.5 Version footnote and MARS cross-link (Ch 12.2 §6)

In the *Comments* field at the bottom (visible only to editorial staff), paste:

> "This is Version 1.0. The corresponding MARS deposit handle is [TO BE FILLED — see Part 3]. Working-paper version produced during the NextGen 8-Week Empirical-Finance Camp at George Mason University, 2026."

You will fill in the MARS handle after Part 3; SSRN allows Comments-field edits within 48 hours of posting. The manuscript title page itself carries the version footnote *"Version 1.0 — Camp submission, 2026-06-XX. MARS handle hdl.handle.net/1920/[TBA]."*; if missing, regenerate with `make paper --version 1.0`.

### 2.6 Upload and submit

Upload `submission/packet/01_manuscript.pdf` (50 MB cap). Read the abstract-page preview SSRN shows. Click *Submit Paper*; the paper enters the moderation queue with queue ID `SSRN-id4XXXXXX`. Screenshot to `submission/receipts/02_ssrn_queue.png`. In 8-24 hours SSRN emails the live URL `https://ssrn.com/abstract=4XXXXXX` — the citable reference for the working-paper version. Save the email as `02_ssrn_live.pdf` and copy the URL into `submission/handles.md`:

```markdown
# Submission handles, registered 2026-06-XX
- Schar submission ID: SYSJ-2026-XXXXX
- SSRN abstract URL: https://ssrn.com/abstract=4XXXXXX
- MARS handle: hdl.handle.net/1920/[after Part 3]
- FMA intent ID: [after Part 4]
- DocuSign envelope ID: [after attestation signing]
```

This file is the single-source-of-truth registry of your submission identifiers.

---

## Part 3 — The MARS deposit (30 minutes)

The MARS deposit creates the permanent archival record of the paper at GMU Libraries. The process is shorter than the previous two because MARS' job is to *archive* rather than to *evaluate*, but the metadata discipline is the strictest because the metadata is what becomes the paper's discoverability fingerprint.

### 3.1 Login through Shibboleth

Open `https://mars.gmu.edu/submit`. Click *Submit via Shibboleth*. Enter your `<you>@masonlive.gmu.edu` credentials. The GMU Shibboleth gateway authenticates you and redirects to the MARS deposit landing page.

### 3.2 Choose the collection

MARS organizes deposits into *collections* by department or center. The camp papers go to the **NextGen Empirical-Finance Camp Working Papers** collection, which Prof. Gao established with the GMU Libraries in 2024. Click that collection from the dropdown. The collection is open-access by default; embargo is not applicable to camp working papers.

### 3.3 The Dublin Core metadata

MARS uses Dublin Core metadata (the international standard for digital-repository metadata). The fields are:

- *Title*: same as Schar and SSRN.
- *Author(s)*: enter your name first; click *Add another author* and enter Prof. Gao.
- *Date Issued*: today's date.
- *Date Submitted*: today's date.
- *Abstract*: paste the 245-word abstract. MARS renders plain text; same Greek-letter substitution.
- *Subject (keywords)*: same five keywords as Schar and SSRN.
- *Type*: select "Working Paper" from the type dropdown.
- *Language*: English.
- *Publisher*: "George Mason University, Costello College of Business" (the camp's host college).
- *Identifier (other)*: paste the SSRN abstract URL from Part 2. This is the cross-link: the MARS record points to SSRN, the SSRN record (after the Part 2.5 edit) will point to MARS.
- *Rights*: select "Creative Commons Attribution 4.0 International (CC BY 4.0)" from the dropdown. **Do not** select the default "All rights reserved" — that defeats the openness purpose of the camp deposit.

### 3.4 Upload the manuscript and the replication package

MARS allows multiple files per deposit. Upload two:

- `submission/packet/01_manuscript.pdf` — the manuscript PDF.
- `submission/replication_package.zip` — the replication-package ZIP from the setup step.

Each file gets a *bitstream* identifier within the MARS record. The librarians ingest both; the ZIP becomes downloadable through the MARS record's "Files" tab.

### 3.5 Submit and the librarian review

Click *Submit*. MARS displays a "Submission complete; awaiting librarian review" page with a temporary deposit ID. Screenshot to `submission/receipts/03_mars_pending.png`.

The librarian reviews the deposit for metadata completeness (not for content — MARS does not peer-review). Review typically takes 3–5 business days. When the deposit is approved, the librarian emails you the permanent handle URL of the form `https://hdl.handle.net/1920/XXXXX`. Save the email PDF as `submission/receipts/03_mars_approved.pdf` and paste the handle into `submission/handles.md`.

In the meantime, return to SSRN and edit the Part 2.5 *Comments* field to fill in the MARS handle. The SSRN-MARS cross-link is now bidirectional.

---

## Part 4 — The FMA Undergraduate Poster Session intent-to-submit (20 minutes)

The Financial Management Association's Undergraduate Poster Session is the natural first conference venue for camp papers (Ch 12.4). The 2026 FMA annual meeting is in Orlando, October 22-24. The intent-to-submit form is a Google Form with a July 31 deadline; the *full* abstract submission is due August 31, with an acceptance decision by September 15.

### 4.1 Open the form

The form URL is on the FMA's "Programs for Students" page (`https://www.fma.org/students`); look for the section "Undergraduate and High-School Poster Session 2026." The form opens in a Google Forms page; sign in with any Google account (you can use the camp's `<you>@gmu.edu` Google Workspace account if you have one, or any personal Gmail account).

### 4.2 The form fields

The intent-to-submit form is shorter than the full abstract submission; it asks for:

- *Author name and affiliation*: enter your name and high-school name; add Prof. Gao as advisor.
- *Paper title*: same as the manuscript.
- *200-word abstract teaser*: a shortened version of the 245-word abstract; trim with Ch 11.1 discipline. The teaser is *not* the same as the full abstract — it is the recruiter pitch, not the abstract.
- *Subfield*: select from FMA's subfield list. Maya selects "Banking and Financial Services"; Devon selects "Cryptocurrency and Digital Assets"; Priya selects "Insurance and Climate Finance"; Sam selects "Asset Pricing"; Leah selects "Innovation Finance."
- *Advisor name, email, and signature*: Prof. Gao is present in the session and signs the field live; for the digital form, his signature is a typed "/Lei Gao/" followed by his email; for the printed-PDF version of the form (which some students send separately), Prof. Gao wet-signs the PDF live.
- *Registration fee waiver request*: tick the box for "High-school author — request waiver." The FMA's high-school-author program waives the registration fee (normally $145 for undergraduates) for high-school authors; the waiver is granted automatically.
- *Travel funding request*: optional; the camp provides a $400 travel stipend that covers domestic FMA travel for one cohort member per year, allocated by Prof. Gao based on financial need and abstract strength.

### 4.3 Submit and the FMA confirmation

Click *Submit*. The Google Form shows a "Thank you" page with an automatic email confirmation; screenshot to `submission/receipts/04_fma_intent.png` and save the email PDF as `submission/receipts/04_fma_intent_email.pdf`.

The full abstract submission is due August 31. The intent form *commits* you to submitting; not following through is a small black mark on your FMA record but not a serious one. The discipline is: file the intent now, draft the full abstract over the next four weeks, submit it on August 30.

Add the FMA intent ID (visible in the confirmation email) to `submission/handles.md`.

---

## Part 5 — The program exit interview (60 minutes)

This is the work of the lab that is *not* about uploading anything. The interview is a sixty-minute structured conversation between you and Prof. Gao, conducted in his office (or, for the remote cohort members, on Zoom), audio-recorded with consent, and transcribed into a private record. The interview is the camp's exit assessment in its richest form; the structured-exit-interview portion of the Week 12 assessment (15 points) is based directly on the quality of your answers here.

### 5.1 The twelve structured questions

The interview proceeds through twelve questions, in this order. Each question gets a five-minute answer; the instructor follows up briefly.

1. **What is the one-sentence finding of your paper?** *State the paper's headline as it appears in abstract sentence 4. Use the verb that matches your design (identifies / estimates / documents). Test of the Chapter 11.1 abstract discipline.*
2. **What is the assumption your headline depends on?** *Name the central identifying assumption — the one that, if violated, invalidates the headline even when every robustness test passes. Test of the Chapter 7.5 identification-memo discipline.*
3. **Who is the closest competitor to your paper, and what does your paper have that theirs does not?** *Name the closest prior paper by author, year, journal. Name the gap. Test of the Mentor 11 literature-positioning discipline.*
4. **What was the moment in the camp where you most changed your mind?** *Name a specific session — a chapter, a lab, a mentor conversation — where a belief you held coming in shifted to a belief you hold going out. Test of intellectual openness.*
5. **What is the part of empirical finance you are most drawn to, and why?** *Name a substantive area (banking, asset pricing, climate finance, fintech, household finance, innovation, etc.). The answer is for your future research identity, not for the camp record. Test of methodological-identity formation.*
6. **What methodological skill do you most want to develop next?** *Name one of: machine learning for causal inference, structural estimation, text analysis at scale, high-frequency data, market microstructure, network analysis, behavioral experiments. Test of methodological-identity articulation.*
7. **What is your one-year plan for the paper you just submitted?** *Detailed: what conferences, what revisions, what next deposit. Test of Chapter 12.4 conference-planning discipline.*
8. **What is your three-year plan for your research line?** *More speculative: what is the next paper, what is the third paper, what cumulative direction. Test of Chapter 12.5 five-year-identity discipline at the three-year scale.*
9. **What is your five-year plan?** *Most speculative: PhD program, terminal master's, industry research, academic apprenticeship. Test of Chapter 12.5 five-year-identity discipline at the five-year scale.*
10. **Who in the research community is on your list of people you want to learn from?** *Name three to five senior researchers whose work you want to follow, whose papers you want to read carefully, whose seminars you want to attend. Test of relationship-investing discipline.*
11. **What is one thing you wish the camp had done differently?** *Honest answer; the camp uses these for next-year revision. Test of feedback fluency.*
12. **What is the one sentence you want me to remember about you when I am writing your recommendation letter in three years?** *Difficult question; sit with it. Test of self-articulation under pressure.*

### 5.2 Recording and transcription

With your consent, Prof. Gao records the audio (one of his AirPods plus the laptop's built-in microphone produces adequate quality). The recording is *private to you and Prof. Gao* and is destroyed after the transcription is filed. The transcription is produced by Whisper running offline on the camp's local server; it is delivered to your camp email within 24 hours of the interview.

The transcript is saved in your private research journal under `journal/2026-06-XX-exit-interview.md` along with any notes you took during the conversation. The journal is private; nothing from the interview becomes part of the public submission record. The interview is for *you* and for the recommendation letter Prof. Gao writes three years from now.

### 5.3 The recommendation-letter pact

At the end of the interview, Prof. Gao confirms what he tells every camp graduate: **he will write a strong recommendation letter for you for any program or position for which he is qualified to assess your work**, in 2027, 2029, 2031, and beyond. The letter draws on the interview transcript, the camp portfolio (manuscript, presentation, code repository), and any subsequent work you share with him as your research continues. The letter is a long-term commitment; it is part of what the camp is *for*. The condition is that you keep him informed about your work — a check-in email at least annually, with the new venue or position you are applying for — so that the letter reflects the most current version of you.

This pact is not paperwork. It is the long-game investment that distinguishes the camp from a one-summer credential. The five-year research-identity statement you wrote (PS 12.5) is your accountability to yourself; the recommendation-letter pact is Prof. Gao's accountability to you. Both are real; both bind.

---

## Part 6 — The reproducibility-attestation signing (15 minutes)

The attestation is a one-page document the camp registrar maintains for every submitted paper. It is the camp's compliance instrument — for the IRB record (the camp is operating under an IRB-approved educational protocol), for the FERPA record (the student is the author of record and consents to the public deposit of their work), and for the integrity record (the student attests that the work is theirs and that the claims are reproducible).

### 6.1 The attestation text

The attestation is on camp letterhead and reads:

> "I, [STUDENT NAME], affirm under the academic-integrity standards of the NextGen 8-Week Empirical-Finance Camp at George Mason University and the GMU Honor Code:
>
> 1. The manuscript "[TITLE]" submitted on [DATE] to the Schar Young Scholars Journal, SSRN, and the Mason Archival Repository System (MARS) is my own original work, produced under the mentorship of Prof. Lei Gao.
> 2. All data sources are cited accurately; all licensed-data uses comply with the relevant data-use agreements (HMDA, CRSP, Compustat, FRED, etc., as applicable to my paper).
> 3. The empirical claims in the manuscript are reproducible from the public replication package deposited at MARS handle [HANDLE], using the code in the repository at git commit [HASH], with random seed 42.
> 4. The CRediT author statement is accurate; the author-contribution allocation between myself and Prof. Gao reflects the actual division of labor.
> 5. I have not previously submitted this work or substantially similar work to any other journal, repository, or conference except as disclosed in the cover letter.
> 6. I understand that the submission is binding: the manuscript is now in the public record, and any retraction or correction will go through the journal's and repository's standard correction-of-record processes.
>
> Signed, [STUDENT NAME], [DATE]
> Mentor witness, Prof. Lei Gao, [DATE]"

### 6.2 The signing

For in-person students: the document is printed; you sign with a black ink pen in the office; Prof. Gao signs as witness; the camp registrar scans the signed document and files the PDF in the camp record and in your repository under `submission/receipts/06_attestation_signed.pdf`.

For remote students: the document is sent through DocuSign; the envelope arrives at 3:00 PM Eastern; the instructor walks the cohort through the signing live; Prof. Gao countersigns within five minutes; DocuSign emails the completed envelope PDF, which is filed in the same place.

Add the DocuSign envelope ID (or, for in-person, the camp registrar's filing reference number) to `submission/handles.md`.

---

## Part 7 — The closing ceremony

The cohort gathers Friday afternoon at 4 PM Eastern, in the camp's main classroom for in-person students and on Zoom for remote students. Prof. Gao opens with a brief reflection on the cohort's work (~10 minutes). Each student then takes 60 seconds at the microphone (or the Zoom screen) to name:

1. The paper they submitted, by title.
2. The SSRN abstract URL.
3. The MARS handle (or "pending" if MARS approval has not arrived).
4. The one sentence from their five-year research-identity memo that they are committing to publicly.

Prof. Gao closes the ceremony with the camp's two-line commitment to each graduate: the recommendation-letter pact (Part 5.3) and the camp's standing invitation for graduates to return as mentors when they are old enough (typically the summer between sophomore and junior year of college).

The ceremony adjourns. The cohort photo is taken (a tradition since 2022). Dinner follows at a restaurant of the cohort's choosing; the camp covers the meal.

---

## Deliverables

By Saturday end-of-day, your capstone repository contains:

- `submission/handles.md` — the registry of all submission identifiers (Schar ID, SSRN URL, MARS handle, FMA intent ID, DocuSign envelope ID).
- `submission/receipts/` — six files: `01_schar_confirmation.png` + `01_schar_email.pdf`, `02_ssrn_queue.png` + `02_ssrn_live.pdf`, `03_mars_pending.png` + `03_mars_approved.pdf` (the latter as soon as it arrives), `04_fma_intent.png` + `04_fma_intent_email.pdf`, and `06_attestation_signed.pdf`.
- `journal/2026-06-XX-exit-interview.md` — the exit-interview transcript and your notes (private, not pushed to any public branch).
- `reflections/lab12.md` — a 500-word reflection on the day, capturing what surprised you, what was harder than expected, and what you commit to doing next (this is the only public Lab 12 reflection).

The instructor reviews these on Monday morning. By that point your Schar submission is in the editorial queue, your SSRN posting is live, your MARS handle is propagating, your FMA intent is recorded, and you have *submitted a research paper*. The camp's job is done.
