# Ch 12.1 — Submitting to the Schar Young Scholars Journal and the MARS Repository: the Submission Packet, the Cover Letter, and the Author-Statement Mechanics

You finished Week 11 with a manuscript that, for the first time in fourteen weeks, you could read end-to-end without flinching. The abstract is 248 words. Table 2 passes the one-glance test. The introduction's five paragraphs each do one job. The literature review's three-strand braid earns its contribution sentences. The response letter to the conference referees is drafted. The next move is the one most students treat as paperwork and that the rest of this chapter argues is the real launch of your scholarly identity: **submitting the paper into the public record.**

Here is the move this chapter turns on, before the machinery. **A submission is not a single act of attaching a PDF to a form; it is the assembly of a *submission packet* that has to satisfy three separate audiences at the same time — the editor, the archivist, and the future-you who will need to defend authorship in three years.** The packet has five components: the manuscript itself, the cover letter, the author statement, the data-and-code availability statement, and (for the Schar Young Scholars Journal and many adult journals) the conflicts-of-interest declaration. Each component is engineered for a different reader. Most first-time submitters write the manuscript carefully and treat the other four as boilerplate; this is the most common reason submissions get bounced for procedural rather than substantive reasons, and it is the asymmetric mistake — you cannot recover from a desk-reject on procedural grounds without losing two weeks. The discipline of this chapter is the discipline of assembling all five components to publication standard, with checklists for each.

We will work through Maya's fair-lending paper as the carrying example, with Devon, Priya, Sam, and Leah's papers appearing in §§4–6 to show the variant cases. By the end of the chapter you will have a submission packet ready to upload to ScholarOne (the manuscript-management platform used by both the Schar Young Scholars Journal and the MARS repository), with each component checked against the rubric and the timing of the submission planned. The Friday-night submission ritual at the end of the chapter is the discipline that, more than any other procedural move, separates students who submit cleanly from students who submit and then spend two weeks fielding "your file is corrupted, please resubmit" emails from the editorial office.

---

## 1. The reveal: what a submission packet is *for*

A submission packet has three readers, and like the abstract's three readers (Ch 11.1) and the literature review's three readers (Ch 11.5), the structure must satisfy all three.

The **first reader** is the editor or editorial-office assistant doing intake. He spends about three minutes per submission: opens the PDF, checks word count, scans the cover letter for scope-match, glances at the author statement to confirm the corresponding author and the affiliations, and looks for the data-and-code availability statement. His decision is binary — accept for review-pipeline assignment, or return-to-author with a procedural-issue note. The return-to-author rate at editorial offices that track it carefully runs around 12–15% of submissions, and the modal reason is "incomplete submission packet" rather than "out of scope." That number is staggering; one in seven first-time submissions is bounced not because the science is bad but because the paperwork is bad. This chapter is how you avoid being one of them.

The **second reader** is the archivist who ingests your paper into the MARS repository (the George Mason University institutional repository — Mason Archival Repository System). She is checking the metadata: the title field, the author field, the abstract field, the keywords field, the funder-acknowledgment field, the rights-and-license field, and the embargo field. If any of these are wrong, the paper either fails to ingest or ingests with incorrect metadata, which means search engines find it under the wrong query and the citing scholar of three years from now never finds it. The MARS metadata is *not* the same as the manuscript text; it is a parallel record that has to be filled out separately, and most students fill it out hastily. This chapter walks through the metadata field by field.

The **third reader** is the future-you of 2030, opening the published paper to write your tenure file, your grad-school application, or your senior thesis. You will need to know, for every paper you ever publish: who the corresponding author was, what the author-contribution statement said, what data-access conditions applied, what funding was acknowledged, and what the embargo terms were. If you write these things carefully in 2026, the 2030-you opens a clean file and writes a clean tenure file. If you write them sloppily — say, by leaving the author statement as "the authors contributed equally" without naming the specific contributions — the 2030-you spends three days reconstructing what each co-author actually did, and may discover that one of the co-authors remembers the contribution allocation differently. This is the single most common source of authorship disputes in academic finance. The discipline of writing the author statement carefully *at submission time* is the discipline of avoiding the dispute.

The Schar Young Scholars Journal is the in-house, peer-reviewed undergraduate-and-precollege journal at the GMU Schar School and the affiliated Costello College of Business; it accepts the camp's papers as a designated submission stream. The MARS repository (Mason Archival Repository System, hosted by the GMU Libraries) is the parallel deposit channel: it does not peer-review the paper but it preserves it with a stable URL, assigns it a handle (a permanent identifier of the form `https://hdl.handle.net/1920/xxxxx`), and ensures the paper is discoverable through Google Scholar, the OAI-PMH harvest network, and the GMU Libraries discovery service. Most camp papers will be submitted to *both* — Schar Young Scholars Journal for the peer-review credential and MARS for the permanent archival record. The interaction of the two channels is the subject of §3.

---

## 2. The five components of the packet, named

Before we walk through the assembly of each, here are the five components named, in the order the editor will read them.

**Component 1 — the manuscript.** A single PDF, typeset to publication standard. For the Schar Young Scholars Journal this means: double-spaced 12-point Times or 11-point Computer Modern (your LaTeX `book/article` default), one-inch margins, page numbers, line numbers (yes, enable them — referees use them in comments), tables and figures embedded near first reference rather than dumped at the end, references in Chicago or APA style depending on the journal's preference. The Schar Young Scholars Journal uses Chicago author-date; we will assume that throughout.

**Component 2 — the cover letter.** A one-page letter to the editor, written in business prose, that does five jobs: (a) names the paper and proposes a category (research article, methodological note, replication study), (b) states one sentence on the contribution, (c) states one sentence on why the paper is appropriate for this journal in particular, (d) names suggested reviewers (and optionally non-preferred reviewers), and (e) attests to the paper's originality and exclusive-submission status. The cover letter is shorter than students expect — under 400 words is the target — and is read by the editor in under 60 seconds.

**Component 3 — the author statement.** A separate document (sometimes called the "author contribution statement" or "CRediT statement," using the [Contributor Roles Taxonomy](https://credit.niso.org/) maintained by NISO) that names each author's role using fourteen standardized verbs: *Conceptualization, Data curation, Formal analysis, Funding acquisition, Investigation, Methodology, Project administration, Resources, Software, Supervision, Validation, Visualization, Writing — original draft, Writing — review and editing*. Every author appears next to at least one role; no role is unattributed; the corresponding author is named. CRediT is now standard at most empirical-finance journals and *required* at the Schar Young Scholars Journal.

**Component 4 — the data-and-code availability statement.** A paragraph (sometimes a separate document, sometimes embedded in the manuscript's last section) that names every data source by its proper noun, states the licensing terms (proprietary, restricted, public), states whether code is available and where, and names the replication-package handle (the MARS handle, the Harvard Dataverse handle, or the journal's own data repository). The Schar Young Scholars Journal follows the [DA-RT](http://www.dartstatement.org/) (Data Access and Research Transparency) guidelines: every paper must have one, and "available upon request" is no longer acceptable language.

**Component 5 — the conflicts-of-interest declaration.** A short paragraph declaring any financial, professional, or personal interests that a reasonable reader would want to know about. For HS-aged authors this is usually a one-sentence "no conflicts to declare." For Prof. Gao as the mentor co-author, this is the sentence where he discloses any consulting relationships, expert-witness work (e.g., his Congressional testimony on fair lending), or board roles. The journal expects honesty here; the discipline is to write it as if a referee will check.

---

## 3. The two-channel submission: Schar Young Scholars Journal *and* MARS

The interaction of the two channels is the structural decision that shapes everything else.

The **Schar Young Scholars Journal** is a peer-reviewed venue. You submit, it goes to two referees, they return reviews in 8–12 weeks, the editor returns a decision (desk-reject, revise-and-resubmit, conditional accept, accept). If accepted, the paper appears in a numbered issue with a citable DOI (Digital Object Identifier — the persistent URL string of the form `https://doi.org/10.XXXX/yyyy.zzzz` that the journal registers with Crossref). The DOI is the credential that makes the paper *citable* in the formal academic sense. Without a DOI a paper exists, but other papers cannot cite it cleanly in a reference list.

The **MARS repository** is an archive, not a journal. You deposit, the librarians ingest, and the paper appears at a stable URL within 5–10 business days, with a *handle* (`https://hdl.handle.net/1920/xxxxx`) but not a DOI. The handle is permanent and resolvable; it is what makes the paper *discoverable* (Google Scholar indexes MARS; institutional repositories are part of the OAI-PMH harvest network). The handle is *not*, however, a DOI, which is why most authors who want the citation credential also seek a journal publication (or an SSRN posting, which can register a DOI through SSRN's own arrangement with Crossref — see Ch 12.2).

The decision tree is:

- **If the paper is camp-only and will not seek further publication.** Submit to Schar Young Scholars Journal *and* deposit in MARS. The journal gives the peer-review credential and the DOI; MARS gives the permanent archival record with the handle. Both are open-access for camp papers; there is no embargo. This is the modal path for camp papers from students who are graduating high school and not continuing the research line.

- **If the paper is the seed of a longer-term project — say, you will continue working on it in college, eventually targeting a graduate-school working paper or a junior-faculty paper.** Submit to Schar Young Scholars Journal *and* deposit in MARS *and* (Ch 12.2) post a preprint to SSRN. The Schar venue gives the early-career publication credential; MARS gives the archival permanence; SSRN gives the time-stamped priority claim and a working-paper version that you can update as the research evolves. This is the path Prof. Gao recommends for any student who is even *possibly* continuing.

- **If the paper has identified a result that you think is targeting a top economics or finance journal eventually (the Rainbow-of-Credits trajectory, see Ch 12.3).** Skip the Schar Young Scholars Journal and go straight to SSRN + MARS deposit + working-paper status. The reason: published papers are not (without exceptional handling) eligible for resubmission to top journals, so a Schar publication on a paper that you think might one day fit *Journal of Finance* would foreclose that path. This is rare for camp papers but possible.

For Maya's paper, the answer is the second case: she is interested in continuing the fair-lending work in college, and Prof. Gao judges the paper to be of standalone interest. So her submission is to all three: Schar Young Scholars Journal, MARS, and SSRN.

---

## 4. Writing the cover letter — the four-paragraph structure

The cover letter is short, but every sentence does a job. The four-paragraph structure is the workhorse: identification paragraph, contribution paragraph, fit paragraph, attestations paragraph.

### 4.1 Paragraph 1 — identification

This is two sentences. The first sentence names the paper, the category, and the corresponding author. The second sentence names the co-authors and their affiliations.

*Maya's letter, Paragraph 1:*

> "We are pleased to submit the manuscript "The 2017 Fair-Lending Examination Reform and the Black–White Mortgage-Denial Gap: Evidence from a Staggered Rollout across 614 Counties" for consideration as a Research Article in the Schar Young Scholars Journal. The corresponding author is Maya Patel (Thomas Jefferson High School for Science and Technology, mpatel@tjhsst.edu); co-authors are Prof. Lei Gao (Costello College of Business, George Mason University) and the NextGen 8-Week Camp cohort listed in the manuscript's acknowledgments."

Notes. The category is named explicitly ("Research Article" — others are "Methodological Note," "Replication Study," "Data Resource Article"). The corresponding author's email is given. The mentor co-author's affiliation is precise. The acknowledgments handling for the cohort is named (the cohort is acknowledged but not co-authored; we will revisit this in §5).

### 4.2 Paragraph 2 — contribution

This is one or two sentences (rarely three). It is the contribution paragraph from your introduction's paragraph 5, compressed into the elevator-pitch version. Do not rewrite the abstract here; that would be redundant and would waste the editor's time.

*Maya's letter, Paragraph 2:*

> "This paper provides the first credibly identified estimate of the effect of intensified fair-lending supervision on the racial denial gap. Using a staggered difference-in-differences estimator on HMDA 2014–2020 data covering 47 million originations across 614 OCC-supervised counties, we estimate that the 2017 examination reform closed roughly one-quarter of the persistent national gap documented in Gao and Sun (2019), with effects concentrated in counties with above-median minority-population shares."

Notes. The contribution claim ("first credibly identified estimate") is named with the discipline of Ch 11.4 — no superlatives the paper cannot defend. The data, design, and magnitude are named in one compressed sentence. The link to Gao and Sun (2019) places the result in the citing literature; the editor of a fair-lending-relevant journal knows that paper.

### 4.3 Paragraph 3 — fit with the venue

This is one or two sentences. Why this journal? You answer in the language the journal uses to describe its scope. The Schar Young Scholars Journal describes its scope as "peer-reviewed empirical research by precollege and early-undergraduate authors on questions of public policy, economics, finance, and political economy, with priority for work that engages the GMU research community."

*Maya's letter, Paragraph 3:*

> "The paper fits the journal's scope as an empirical-finance contribution by a precollege author, developed within the NextGen 8-Week Camp at George Mason University under the mentorship of a faculty member in the Costello College of Business. The methodological choices, the data work, and the writing were the author's; the mentor provided guidance on identification, robustness, and exposition. The paper engages a public-policy question with a direct policy implication, fitting the journal's policy-relevance criterion."

Notes. The scope-match is named in the journal's own language ("empirical-finance contribution by a precollege author"). The author-mentor relationship is disclosed (we will say more in §6 — the author-statement discipline). The policy relevance is named.

### 4.4 Paragraph 4 — attestations and suggested reviewers

This is one sentence of attestation plus a short list of suggested reviewers.

*Maya's letter, Paragraph 4:*

> "We attest that this manuscript has not been published elsewhere and is not under consideration at another journal; the data and code will be deposited in MARS upon acceptance with a 6-month embargo to allow conference dissemination. We suggest the following potential reviewers: [Reviewer A — fair-lending expertise], [Reviewer B — staggered DiD methodology expertise], [Reviewer C — banking-supervision real-effects expertise]; we have no non-preferred reviewers to declare."

Notes. The exclusivity attestation is one sentence (every journal requires it). The data-and-code commitment is named with the embargo terms specified (6 months is the standard for camp papers that have presented at conferences and want time to revise before the data is public). Suggested reviewers are named in three slots, one per literature strand from Ch 11.5; this is a polite signal to the editor that you understand who would be qualified to review the paper. *Do not* suggest reviewers with whom you have a conflict of interest (advisors, co-authors, anyone you have been in regular contact with in the last 36 months). The journal's database checks.

The complete letter is under 400 words and fits on one page when typeset.

---

## 5. The author statement — CRediT in detail

The author statement is the document students most often write hastily. The discipline of writing it carefully is the single most important procedural move in the chapter. Here is why.

The Schar Young Scholars Journal uses the CRediT taxonomy of fourteen roles. Each author is mapped to one or more roles. *Every role must be assigned to at least one author; no role may be left unassigned.* This sounds bureaucratic but it has a real function: it forces a conversation among the authors about who did what *before* the paper is published, which is when memories are fresh and disagreements are resolvable. If the conversation is deferred until later — when a co-author is asked at a job talk "what was your specific contribution?" — the conversation can become an argument, and the argument can become a public dispute. *Writing CRediT carefully at submission time is conflict-prevention.*

Here is Maya's CRediT statement, written carefully:

> **Maya Patel:** Conceptualization (lead), Data curation (lead), Formal analysis (lead), Investigation (lead), Methodology (equal), Software (lead), Validation (equal), Visualization (lead), Writing — original draft (lead), Writing — review and editing (equal).
>
> **Prof. Lei Gao:** Conceptualization (supporting), Methodology (equal), Project administration (lead), Resources (lead), Supervision (lead), Validation (equal), Writing — review and editing (equal), Funding acquisition (lead).

Notes. The four-tier intensity descriptors (lead / equal / supporting / not applicable) are CRediT-standard. *Lead* means the author had primary responsibility; *equal* means multiple authors shared the role; *supporting* means the author contributed but was not primarily responsible; *not applicable* means the role was not relevant to the paper. Every role must have at least one "lead" or "equal" assigned. In Maya's statement, *Funding acquisition* is "lead" for Gao because the camp infrastructure is GMU-funded; *Resources* is "lead" for Gao because the WRDS and HMDA access is institutional; *Investigation* is "lead" for Maya because she did the data work; *Writing — original draft* is "lead" for Maya because she wrote the manuscript and Gao revised. The statement is honest and detailed.

One non-obvious detail. The other camp students are *acknowledged but not co-authored*. The journal's authorship policy follows the [ICMJE](http://www.icmje.org/recommendations/) (International Committee of Medical Journal Editors) criterion that authorship requires substantial contributions to (a) conception or design, (b) data acquisition or analysis, (c) drafting or critically revising the manuscript, *and* (d) approving the final version *and* (e) accountability for the work. The other camp students gave feedback on Maya's paper during the symposium and lab sessions; this is helpful but does not rise to authorship under ICMJE. They are acknowledged by name in the Acknowledgments section. Writing the authorship line carefully — separating the two authors who meet the criteria from the cohort of acknowledged contributors — is a discipline that the journal expects and that the future-Maya will be glad to have done.

---

## 6. The data-and-code availability statement

This is where most papers in empirical finance now fail or pass on the increasingly strict DA-RT standards. The Schar Young Scholars Journal follows DA-RT and requires a paragraph that addresses six questions: (1) what data were used? (2) where is the data publicly available, or what restricted-access channel produced it? (3) is the cleaned dataset available, and where? (4) is the analysis code available, and where? (5) what license applies? (6) is there an embargo, and if so, when does it lift?

For Maya's paper, the statement reads:

> **Data and Code Availability.** This paper uses three data sources. *Home Mortgage Disclosure Act (HMDA) loan-level data for 2014–2020* are publicly available from the Federal Financial Institutions Examination Council at [https://ffiec.cfpb.gov/data-publication/](https://ffiec.cfpb.gov/data-publication/); we use the Loan Application Register (LAR) files for all reporting institutions. *Office of the Comptroller of the Currency (OCC) examination-intensity records* are partially public (the names of examined institutions and the calendar quarters of examinations are public via OCC press releases and Federal Reserve supervisory disclosures); the cross-walk to county-level coverage was constructed by the authors from OCC's annual Community Reinvestment Act performance evaluations. *American Community Survey (ACS) 5-year estimates for 2014–2020* are publicly available from the U.S. Census Bureau at [https://www.census.gov/programs-surveys/acs](https://www.census.gov/programs-surveys/acs).
>
> The cleaned dataset (LAR–OCC–ACS merge) and the full Python replication code are deposited in the Mason Archival Repository System (MARS) with handle `https://hdl.handle.net/1920/[assigned-upon-deposit]`, under a Creative Commons Attribution 4.0 International (CC-BY 4.0) license. The replication package includes a `README.md` with one-command reproduction instructions, a `requirements.txt` pinning the Python 3.11 environment, and a `Makefile` that regenerates all tables and figures. A 6-month embargo applies from the date of publication, after which the data and code are unrestricted.

Notes. Each data source is named, with a URL. The cleaned dataset is differentiated from the raw data — the *construction* of the merged dataset is a contribution, and the cleaned merge is what enables replication. The code is named with its hosting location. The license is named (CC-BY 4.0 is the standard for the camp). The embargo is named and bounded. The replication package is described at the level of detail that a referee can check ("one-command reproduction" is a claim that the referee can test).

The single phrase that should *never* appear in a data-and-code availability statement is "available from the author on request." This phrase is now treated by most journals as equivalent to "not available," because the empirical literature on data-on-request has shown that authors fulfill such requests less than 20% of the time (King 1995; Vlaeminck 2013; Christensen and Miguel 2018). Write the deposit instead.

---

## 7. The Schar Young Scholars Journal ScholarOne workflow, step by step

ScholarOne (a Clarivate product) is the manuscript-management platform used by the Schar Young Scholars Journal and most peer-reviewed journals in economics and finance. The first-time submission process has nine steps. Each is short, but each can fail if you do not have the right file ready.

**Step 1 — create the ScholarOne account.** Visit `https://mc.manuscriptcentral.com/scharyoungscholars`, click "Create Account," fill in name, email, affiliation, and ORCID. *Always have an ORCID.* The ORCID (`https://orcid.org`) is a persistent author identifier that distinguishes you from every other "Maya Patel" in academic publishing forever. Sign up takes three minutes. Use your school email or a permanent personal email (Gmail is fine), not an email that will expire when you graduate.

**Step 2 — start a new submission.** Click "Author Center" → "Start New Submission." Choose the manuscript category: "Research Article" for Maya's paper.

**Step 3 — enter title, abstract, and keywords.** Paste the title (use sentence case for the journal's house style, not title case; check the author guidelines). Paste the abstract (the same 248-word abstract from Ch 11.1). Enter 5–8 keywords; for Maya's paper: "fair lending; mortgage denial; bank supervision; staggered difference-in-differences; HMDA; racial disparities; Community Reinvestment Act; identification." Keywords drive search and indexing, so use the terms a future scholar would Google.

**Step 4 — enter authors and affiliations.** Add all co-authors, in order, with affiliations and emails. Designate the corresponding author. Verify that each author's ORCID is on file.

**Step 5 — upload manuscript and supplementary files.** Upload the main PDF, the cover letter PDF, the author statement PDF, the data-and-code availability statement PDF, and the supplementary materials (the data appendix, the additional robustness tables, the code repository ZIP). Each file gets a file-designation tag.

**Step 6 — answer the editorial questions.** ScholarOne asks: is the paper under consideration elsewhere? have any of the figures been published elsewhere? is human-subjects approval required? are there conflicts of interest? For Maya's paper the answers are: no, no, no, no. The IRB question is worth a moment of care: the paper uses HMDA data, which is publicly available aggregated regulatory data; there is no human-subjects intervention; no IRB is required. Document this in the submission.

**Step 7 — suggest reviewers.** Enter the three suggested reviewers from the cover letter, with affiliations and emails. *Do not* suggest reviewers who have a conflict of interest (your advisor, your co-authors, anyone you've been in contact with recently). ScholarOne's automated check will flag obvious conflicts.

**Step 8 — review the submission.** ScholarOne builds a single PDF combining all your uploaded files, formatted with the journal's house style. Review it carefully. Look for: page numbers visible? line numbers visible? tables and figures placed correctly? references rendered correctly? metadata (title, authors, abstract) matching what you entered? If anything is wrong, go back and fix; do not submit a broken file and email the editor later.

**Step 9 — submit.** Click "Submit." You will receive a confirmation email within minutes with a manuscript number (typically of the form `SYSJ-2026-0123`). Save the manuscript number; you will reference it in every subsequent communication.

The whole process, done carefully with all files ready, takes 90 minutes. Done sloppily it takes three hours and produces a submission the editorial office bounces back. Have all five components of the packet finalized *before* you start the ScholarOne workflow.

---

## 8. The MARS deposit, step by step

The MARS deposit is parallel to the ScholarOne submission and uses a different interface — DSpace, the institutional-repository software hosted by GMU Libraries. The MARS workflow has six steps.

**Step 1 — log in to MARS.** Visit `https://mars.gmu.edu`, log in with your GMU NetID (the camp issues a sponsored NetID for participating students; if you do not have one, your camp coordinator does). Click "Submit New Item" in the appropriate collection — for camp papers, the collection is "NextGen Camp Research Papers."

**Step 2 — enter metadata.** This is the substantive part of the MARS deposit. The DSpace metadata fields follow Dublin Core (a metadata standard maintained by the Dublin Core Metadata Initiative) and include: *dc.title* (the title), *dc.creator* (each author, family-name comma given-name format, one entry per author), *dc.subject* (the keywords, one per row), *dc.description.abstract* (the full abstract), *dc.publisher* (the Schar Young Scholars Journal if accepted; otherwise "George Mason University NextGen 8-Week Camp"), *dc.date.issued* (the deposit date), *dc.type* (Research Paper), *dc.identifier.citation* (the full citation, including the journal name once known), *dc.language.iso* (en for English), *dc.rights* (Creative Commons Attribution 4.0 International), *dc.rights.uri* (`https://creativecommons.org/licenses/by/4.0/`), and *dc.relation.ispartof* ("NextGen 8-Week Camp Working Paper Series," if applicable).

The metadata is *not the same* as the manuscript text. The metadata is a parallel record that drives discovery. Fill it out carefully.

**Step 3 — upload files.** Upload the manuscript PDF, the supplementary materials, and the replication package (as a single ZIP). MARS will assign a handle (`https://hdl.handle.net/1920/xxxxx`) once the deposit is reviewed.

**Step 4 — apply license.** Select the Creative Commons Attribution 4.0 International license from the dropdown. This is the camp's standard license: it allows reuse with attribution, which maximizes the discoverability and downstream use of the paper while protecting the author's right to be credited.

**Step 5 — set embargo (if any).** If you are simultaneously submitting to a journal that requires exclusivity until publication, set the embargo to lift on the journal's publication date (typically 6 months from submission). MARS's embargo system holds the file private until the embargo date, then makes it public automatically. For Maya's paper, the embargo is 6 months, matching the cover letter's commitment.

**Step 6 — submit for review.** MARS librarians review each deposit before it goes live; this review is for metadata quality and file integrity, not for academic content. Review time is typically 3–5 business days. Once approved, the handle is assigned and the paper is live.

The MARS deposit is *additive* to the journal submission, not a substitute. You do both.

---

## 9. The Friday-night submission ritual

The submission ritual is the discipline of submitting at the right time, in the right state of mind, with the right verification.

Submit on a Friday afternoon, not a Sunday night. The reason is logistical: the editorial office is staffed Monday–Friday, so a Friday-afternoon submission gets the editor's intake Monday morning when she is fresh, rather than buried in the weekend backlog. Sunday-night submissions are a tell that the author was rushing.

Before clicking submit, complete the eight-item verification:

1. The manuscript PDF opens cleanly on three different devices (your laptop, your phone, a borrowed tablet). PDFs sometimes corrupt during export; verify before submission, not after.
2. The page count, word count, and figure count match what you reported in the metadata fields. ScholarOne checks these and bounces submissions where they disagree.
3. All hyperlinks in the manuscript resolve. Click each one. References to URLs that have moved are a small embarrassment that takes ten minutes to fix; references that are broken in the published version are a larger embarrassment that takes a corrigendum to fix.
4. The reference list is complete and matches the in-text citations. The most common reason a reference-list audit fails is that you cited a paper in the introduction in February, removed it from Section 2 in March, and forgot to remove the reference. Run a citation-checker (`pandoc-citeproc`, or `bibtexbrowser`, or just `grep` your cite-keys) to verify.
5. The author statement matches the author list on the title page. (Common bug: you added a co-author late and forgot to update the CRediT statement.)
6. The data-and-code availability statement matches what you actually deposited. If you said "code in MARS," the code is actually in MARS.
7. The cover letter names the journal correctly. (Common bug: you adapted a cover letter from a previous submission and forgot to swap the journal name.)
8. Your email forwarding works. The editor will send the manuscript-number confirmation within minutes; if you don't receive it within an hour, ScholarOne is sometimes the problem, and you want to know.

Then submit. Then close the laptop. Do not check the ScholarOne status page for at least one week — there will be no news, and refreshing accomplishes nothing.

---

## 10. The author-statement mechanics for mentor co-authorship

We return to one detail that needs more care: the author-statement mechanics when the mentor is a co-author. This is the situation for every camp paper — Prof. Gao is a co-author on Maya's, Devon's, Priya's, Sam's, and Leah's papers, alongside the student. The CRediT statement has to honestly represent who did what.

The discipline is this. The student is the *lead* on *Conceptualization*, *Data curation*, *Formal analysis*, *Investigation*, *Software*, *Visualization*, and *Writing — original draft*. The mentor is the *lead* on *Project administration*, *Resources*, *Supervision*, and (typically) *Funding acquisition*. The two are *equal* on *Methodology*, *Validation*, and *Writing — review and editing*.

If a student was unable to do the data work themselves (say, the data was too proprietary to be touched by a precollege author and the mentor ran the regressions), the CRediT statement must be honest about that. *"Lead"* on *Formal analysis* should not be assigned to the student if the mentor did the analysis. The temptation to over-assign credit to the student — out of well-intentioned generosity, or out of a desire to make the paper look more student-led than it was — is real and should be resisted. The discipline is honesty.

This is also where the conflict-of-interest declaration earns its keep. For Maya's paper, Prof. Gao discloses:

> **Conflicts of interest.** Prof. Lei Gao serves as the Faculty Director of the NextGen 8-Week Camp at the Costello College of Business, the mentor relationship under which this paper was developed. The student first author received no financial compensation for the work; the mentor's compensation is the regular faculty salary that supports his GMU research and teaching activities. The mentor has no financial or consulting relationship with any party (lender, regulator, advocacy group) that has an interest in the substantive question of fair-lending supervision. No conflicts to declare beyond the mentor relationship itself.

This is honest, complete, and short. It discloses the structural conflict (the mentor relationship), the compensation arrangement (no payment to the student, regular salary to the mentor), and the absence of substantive conflicts. The Schar Young Scholars Journal editor reads this and moves on.

---

## 11. Devon, Priya, Sam, and Leah — variant cases

Maya's paper is the modal camp paper: clean two-author CRediT, public data, no IRB, single-channel submission to Schar + MARS + (next chapter) SSRN. The other four cases have one variant each worth seeing.

**Devon's crypto-event-study paper** uses on-chain Ethereum data scraped from `etherscan.io` via the public API. The data-and-code availability statement names the API endpoint, the date range of the scrape (because etherscan's free tier rate-limits and the data is dynamic — a reader replicating in 2027 will see a different blockchain state), and the snapshot date. The replication package includes the raw JSON blobs, not just the cleaned panel, because the etherscan API may not return identical results on re-query. Devon's CRediT statement is identical in structure to Maya's; his cover letter's "fit" paragraph engages the journal's interest in fintech and digital-asset research.

**Priya's climate-and-insurance paper** uses NOAA storm-event data, FEMA disaster declarations, and S&P Capital IQ insurance-company financials. The S&P data is *proprietary*. The data-and-code availability statement must say so explicitly: "The S&P Capital IQ data are accessed under GMU's institutional subscription and cannot be redistributed; the manuscript reports a sample-construction procedure that another researcher with S&P access can re-execute, and the analysis code is deposited in MARS without the underlying data, with synthetic test data for code-verification purposes." This is the honest disclosure of a restricted-data situation; it satisfies DA-RT while respecting the data license. The reviewer will check that the procedure is documented in enough detail to be re-executable.

**Sam's intraday-momentum paper** uses CRSP TAQ (Trade and Quote) data and TRTH (Thomson Reuters Tick History) data — both heavily proprietary, both stored on GMU's Hopper compute infrastructure. The data-and-code availability statement names the proprietary status, the institutional access channel (WRDS), and the on-Hopper-only constraint. The replication package is the code only; the data must be re-accessed by anyone replicating. The cover letter explicitly notes that "the analysis was conducted within GMU's WRDS environment and the data did not leave the institution's secure infrastructure" — this is a standard disclosure for licensed-data papers.

**Leah's patent-text-analysis paper** uses USPTO PatentsView data (public) plus the Google Patents Public Datasets BigQuery tables (public). Leah's paper is the easiest case: everything is public, everything can be redistributed, the replication package is complete and self-contained. The CRediT statement assigns *Software* as "lead" to Leah, reflecting the substantial NLP pipeline she wrote — a contribution beyond the typical regression-only paper.

Each variant case adapts the modal Maya template to the specific data, mentor relationship, and ethical constraints of the paper. The discipline of writing the submission packet *for the specific paper* — rather than copy-pasting a template — is what produces a clean submission.

---

## 12. What success and failure look like

Submission day produces an emotional response that students do not expect. The relief of finally clicking submit is followed, within hours, by a low-grade anxiety that the file was corrupted, the editor will hate the paper, the data has a bug, the assumption is wrong. This is normal. It is also unproductive. *The work is done.* The next move is not to recheck the submission; the next move is to start the SSRN posting (Ch 12.2), think about the conference circuit (Ch 12.4), and let the editor work.

Success looks like: a manuscript-number confirmation email within an hour; a "your manuscript is in editorial review" status update within five business days; an editor's decision (sent for review, revise-and-resubmit, conditional accept, or desk-reject) within four to six weeks; if sent for review, two referee reports within twelve to sixteen weeks. The Schar Young Scholars Journal targets a 14-week median turnaround from submission to first decision — fast by the standards of adult journals (where the median is closer to 24 weeks in finance), and explicitly designed to fit a precollege author's timeline.

Failure modes — the ones the discipline of this chapter is designed to prevent — look like: a return-to-author email three days after submission saying the file is corrupted, or the CRediT statement is incomplete, or the data-and-code availability statement uses prohibited language, or the cover letter is generic. Each of these costs two weeks. The eight-item Friday-night verification (§9) is the prophylaxis.

The submission packet is also a piece of writing that has value beyond this paper. Six months from now, when you submit your next paper — whether a college-class paper, a research-assistantship paper, or a college-newspaper op-ed — the cover-letter template, the CRediT structure, and the data-and-code availability discipline transfer. The submission packet is a skill, not a one-off artifact. Practice it well on Maya's paper and it will serve you for the next decade.

---

## 13. The commit checklist

The five-item commit checklist for this chapter — apply it before clicking submit.

1. **The cover letter is under 400 words, four paragraphs (identification, contribution, fit, attestations), and names the journal correctly.** Read it aloud; if a sentence makes you flinch, rewrite it.
2. **The CRediT author statement is complete: every one of the fourteen roles has at least one author assigned, no role is unassigned, the intensity descriptors (lead/equal/supporting) are honest, and the corresponding author is named.** Run the CRediT-completeness check (`nb12.1`'s `credit_audit()` function).
3. **The data-and-code availability statement names every data source by proper noun, names the licensing terms, names the replication-package handle, and contains no instance of the phrase "available from the author on request."** Grep for the forbidden phrase before submission.
4. **The conflicts-of-interest declaration discloses the mentor relationship and any other structural conflicts honestly.** If your mentor is a co-author, this paragraph exists.
5. **The eight-item Friday-night verification is run.** Each item is checked off in writing in your lab notebook before you click submit.

Submit on Friday at 4pm. Confirm the manuscript number arrives. Close the laptop. Move on to Ch 12.2.

---

## 14. Cross-references and what is next

This chapter built on **Ch 7.5** (the identification memo — the assumption named in Maya's cover letter's contribution paragraph is the assumption from the Ch 7.5 memo), **Ch 8.1** (the specification curve — the figure named in the manuscript's supplementary materials referenced in the submission), **Ch 8.2** (the robustness battery — the source of the robustness tables in the submitted manuscript), **Ch 9.5** (the feedback ledger — whose entries seeded the Week 10 triage and the response letter to the conference referees attached to the submission), **Ch 10.5** (the external-validity paragraph — embedded in the manuscript's discussion section), and **Ch 11.1–11.5** (the manuscript that the submission packet wraps).

The next chapter (Ch 12.2) is about the SSRN preprint: the posting decision, the versioning discipline, the question of whether SSRN posting registers a DOI, and the reasons preprints matter for precollege authors. Chapter 12.3 is about the decade-long arc of a single paper from working-paper status to top journal publication, with the Rainbow-of-Credits municipal-borrowing paper (Gao, Liu, and Wang) as the honest case study. Chapter 12.4 is about the conference circuit beyond the camp's symposium — FMA Undergraduate Poster, AEA Pipeline, SFS Cavalcade — and what each rewards. Chapter 12.5 closes the week and the camp by asking what comes *after* submission: the reviewer wait, the desk-reject, the revise-and-resubmit, and how to build the five-year research identity that survives all three.

Maya submitted at 4:07pm on the Friday of Week 12. The manuscript number was `SYSJ-2026-0089`. The editor's intake email arrived Monday at 9:03am. The paper was assigned to two reviewers by Wednesday. The first review came back six weeks later. The second review came back eight weeks later. The revise-and-resubmit decision letter arrived ten weeks after submission. She is now thinking about how to write the response letter — which is Ch 12.5's topic, ten weeks early but on the same arc.

The submission is not the end of the paper. It is the beginning of the paper's public life.
