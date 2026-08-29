# S7 — Legacy / Team-Project Ownership Clarification

**Status:** INTERNAL, PRIVATE. Lives only in
`sales-performance-business-analytics-private`. S1–S6 were not modified.

## A. Confirmed Project History

The project genuinely originated as a team/group project — confirmed
directly by the project owner, not inferred from the repository. The
repository itself cannot independently prove or disprove this (its git
history is a single squashed "Initial release" commit under one author,
so it provides no forensic evidence either way). The team origin is
established by the owner's direct statement, and this document treats it
as ground truth without adding any further detail the owner has not
confirmed.

## B. Legacy Directory Meaning

Based only on verified repository evidence: `legacy/` contains
`business_sales_dashboard.png`, `sales_analysis.ipynb`, and
`sales_data.csv`, all with filesystem modification timestamps predating
the rest of the project's working files. `dataset/sales_data.csv` is a
copy of the same original data (confirmed by checksum: identical to
`legacy/sales_data.csv`, and distinct from `data/clean/sales_data_clean.csv`).
The public README already described these as "the original team's"
artifacts before this stage; that wording is now confirmed accurate and
has been clarified (Section E). No file inside `legacy/` was modified,
renamed, or deleted by this or any prior stage.

## C. Current Project Positioning

The repository should be described, honestly, as: **a team-originated
project that I (personally) took further** — the `legacy/` baseline
reflects the team's original output; the data-quality pipeline, Python
analysis, SQL analysis, Excel workbook, Power BI specification, and
cross-tool validation work described throughout the rest of the README
are the work being presented in this repository. This document does not
assert an exact percentage split or claim specific file-level authorship
beyond that framing, because no such detail has been confirmed (Section
D explains exactly what is and isn't established).

## D. Current Ownership / Contribution Analysis

**Established by direct repository evidence:**
- `legacy/` = pre-existing team-project baseline, unmodified, still
  present in the repo.
- The data-quality pipeline (`data/generate_data.py`, `clean_data.py`)
  and every downstream analytical layer (notebook, SQL scripts, Excel
  builder, Power BI specification) are distinct from `legacy/` — verified
  by checksum (not the same files) and by content (different logic,
  different structure, described in `README.md` Section 8).

**NOT established by repository evidence — requires the owner's own
recollection, not fabrication:**
- Team size or teammates' names.
- Exact division of labor within the original team project (`legacy/`).
- Specific dates of the team phase vs. the individual extension phase.
- Whether the owner personally contributed to `legacy/` itself, and if
  so, which parts.

None of these were invented in this document or in the public README
edit (Section E). Where an interview question requires this level of
detail, the recommended answers below (Sections F–H) explicitly route to
"I'd need to speak to that specifically" rather than a fabricated
specific.

## E. Public README Decision

**Change made.** The prior wording ("Original team baseline... preserved
unmodified" / "Original team's in-place baseline artifacts... superseded
by the Phase 2+ pipeline") was factually consistent with the now-
confirmed team origin, but left the relationship between `legacy/` and
the rest of the repository ambiguous enough that a recruiter could
reasonably wonder whether the entire repository — not just `legacy/` —
was team-built, or conversely assume the whole project (including
`legacy/`) was solo.

**Smallest truthful fix applied** (public repo, commit `c472bd5`):
1. Added one clarifying paragraph near the top of `README.md`: *"this
   project began as a team/group project. `legacy/` preserves that
   original team baseline... The data pipeline, analysis, and validation
   described throughout the rest of this README are the work presented
   in this repository."*
2. Reworded the two `legacy/`/`dataset/` bullets in the repository-
   structure diagram to point back to this disclosure.
3. Reworded one sentence in `notebooks/README.md` that used
   "independently" in a way that could be misread as an ownership claim
   rather than its intended meaning (the notebook doesn't reuse the
   legacy notebook's logic).

No exaggerated ownership language ("single-handedly," "entirely my own
project," "independently developed every component") was added or
existed before. Verified by direct re-read of the diff (Section L/M
confirms no new AI-signal or ownership-overclaim language was
introduced).

## F. Recommended "Was This a Team Project?" Answer

*(20–30 seconds, natural spoken delivery)*

"Yes, the project originally started as a team project. The repo still
has that original baseline preserved in a `legacy/` folder — the notebook,
dataset, and dashboard image from that phase. What I'm presenting here is
the analytical pipeline I built on top of that: the data-quality process,
the Python, SQL, and Excel analysis, the Power BI specification, and the
cross-tool validation work. I'm happy to go into more detail on the
original team phase specifically if that's useful."

## G. Recommended "Which Parts Did You Personally Work On?"

**Do not fabricate a specific breakdown.** What can be stated from
repository evidence: "The data-cleaning pipeline, the Python notebook,
all ten SQL scripts, the Excel workbook, and the Power BI specification —
everything from the point the clean dataset exists onward — is the
analytical work I'm presenting and can walk you through in detail."

**Safe answer template for the team-phase portion specifically** (where
personal recollection, not this document, must fill in the actual
answer): "For the original team phase itself — [owner fills in their
actual role: e.g., 'I worked on X specifically' or 'I'd want to check my
notes on the exact split before giving you specifics'] — but everything
from the data pipeline onward is my own individual work, which is what
this project primarily demonstrates."

## H. Recommended "Did You Build Everything in This Repository?"

"Not literally everything, no — `legacy/` is a preserved baseline from
when this started as a team project, and I've left it in place rather
than deleting it. Everything else — the data pipeline, the Python, SQL,
and Excel analysis, and the Power BI specification — is my own individual
work, and that's what I'd walk you through."

## I. Interview Red Flags

Must NOT say:
- "I built this entire project myself" (false — `legacy/` is
  team-originated).
- Any specific claim about teammates' names, count, or exact
  responsibilities not actually recalled/confirmed.
- Claiming personal authorship of anything inside `legacy/` without
  being certain that's true.
- Implying the team-phase artifacts were produced by the same rigorous,
  cross-validated process used in the individual analytical work — they
  weren't verified to that standard, and no such claim should be made.
- Inventing dates, semester names, course names, or team size to sound
  more specific than is actually known.
- Getting defensive or evasive if asked directly — the honest, confident
  answer (Section F) is stronger than deflection.

## J. CV Positioning Recommendation

**Recommended description: team-originated project with individual
analytical contribution** — not "individual project" (inaccurate given
the confirmed team origin) and not "team project" alone (understates the
individually-built analytical pipeline, which is the substantive
evidence this project's entire interview-preparation archive is built
on).

Suggested CV phrasing: *"Extended a team-originated sales analytics
project into a full individual Python/SQL/Excel/Power BI analytical
pipeline with cross-tool validation."* This is accurate, doesn't overstate
solo authorship of the original baseline, and correctly foregrounds the
individually verifiable work (which is what CV claim defense in S6
Section 6 already covers).

## K. Final 5-Line Memory Card

PROJECT ORIGIN: Started as a team/group project.
MY ROLE: Extended the team baseline into a full individual analytical pipeline.
LEGACY: `legacy/` preserves the original team baseline, unmodified, not part of the pipeline.
CURRENT WORK: Data cleaning, Python, SQL, Excel, Power BI specification — all individually built and cross-validated.
SAFE OWNERSHIP STATEMENT: "Team-originated project; the analytical work I'm presenting — from the data pipeline onward — is my own."

## L. Public AI-Signal Audit

Re-ran the full banned-term scan (chatgpt, claude, gpt, llm, agent,
prompt engineering, AI assistant, language model, generated by AI,
AI-generated, artificial intelligence, plus the marketing-language list
from S6 Section 2) across the public repository after the README edits.
**Zero hits.** The added wording ("team/group project," "original team
baseline," "work presented in this repository") introduces no new
AI-signal or marketing language.

## M. Public Internal-Workflow Audit

Re-ran the scan for S1–S7, interview archive, mock interview, portfolio
packaging, private repository, internal archive, interview preparation.
**Zero hits.** No internal stage-naming or interview-preparation language
was introduced into the public repository by this or any prior stage.
`reports/` dead-link re-check: zero remaining `reports/` references
anywhere in the public repo (confirms S6's fix in commit `c45ff1e` is
still intact).

## N. Analytical Integrity Verification

Confirmed by checksum immediately before and after the README edits:
`data/clean/sales_data_clean.csv`, `data/raw/sales_data_raw.csv`,
`notebooks/sales_analysis.ipynb`, `excel/sales_business_analysis.xlsx`,
`sql/sales_analysis.db`, and all three `legacy/` files are byte-identical
to their state at the start of this stage. Only `README.md` and
`notebooks/README.md` were modified — both documentation-only changes, no
code, data, or calculated values touched.

## O. Private Repository Verification

`reports/s7_legacy_team_project_ownership_clarification.md` is the only
new file created, only in
`sales-performance-business-analytics-private`. S1–S6 checksums verified
unchanged immediately before this file was written (all six match their
previously recorded values exactly — see Git Status below for the
post-commit re-check).

## P. Public Repository Verification

Verified via `gh repo view`: `sales-performance-business-analytics`
remains PUBLIC, owner `naresh-naik`, default branch `main`. Local HEAD =
`origin/main` after push. README contains the corrected team-project
wording (Section E). `legacy/` remains present (3 files, unmodified by
checksum). No `reports/s*.md` or any other private-archive file is
present in the public repository. No AI-signal or internal-workflow
language present (Sections L/M). All analytical files unchanged (Section
N).

## Q. Git Status

**Public:** commit `c472bd5c9ed1821f66d95cb0775dacbf9f58e61a` — "docs:
clarify team-project origin of legacy/ baseline" — 2 files changed (13
insertions, 6 deletions), local HEAD = origin/main, clean tree.

**Private:** pending this file's commit — see terminal confirmation
following this report for the post-commit HEAD/checksum verification.

## R. Scope Compliance

Only `reports/s7_legacy_team_project_ownership_clarification.md` created
in the private repo. S1–S6 not modified. Public repo received exactly one
justified, minimal, documentation-only commit clarifying already-true
information — no analytical, numerical, or dataset change. Café
repositories not accessed for modification. No team size, teammate names,
dates, file-level ownership, or contribution percentages were invented
anywhere in this document or in the public README.

## S. Final Verdict

## READY

The one open item identified by S6 — the `legacy/` "original team"
narrative having no prepared interview answer — is now resolved: the
public README accurately and minimally discloses the team origin, and
this document provides an honest, non-fabricated spoken answer for every
variant of the "was this a team project" question, including an explicit
template for the one detail (the owner's specific role within the
original team phase) that only the owner can supply. No numerical,
claim-safety, or consistency issue remains open across S1–S7.

---

S7 COMPLETE — LEGACY TEAM-PROJECT HISTORY CLARIFIED, INDIVIDUAL CONTRIBUTION POSITIONING VERIFIED, AND SALES PROJECT INTERVIEW PACKAGE FINALIZED.
