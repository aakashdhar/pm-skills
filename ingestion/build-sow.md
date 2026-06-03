---
name: build-sow
category: ingestion
description: >
  Builds the complete Statement of Work for a new project by interviewing
  the PM conversationally. Triggers on "build sow", "create the sow",
  or "let's do the sow". Asks one topic at a time — not a form. Generates
  a professionally formatted SOW matching BetaCraft's standard template,
  presents it for review, and on approval locks it as Tier 1 Canonical,
  extracts baseline requirements, updates shared/PROJECT_INDEX.md, and
  commits. This is the first skill run on any new project.
---

# Skill: build-sow

---

## Trigger

- `"build sow"`
- `"create the sow"`
- `"let's do the sow"`
- `"write the statement of work"`
- `"start the sow"`

---

## Pre-read

1. `client.md` — client name, contact, any context already filled
2. `reference/sow.md` — check if already populated (abort if Tier 1 locked)

If `reference/sow.md` is already locked as Tier 1 — stop:
```
⚠ reference/sow.md is already locked as Tier 1 Canonical.
  To make changes, raise a Change Order via the change-log/.
  I cannot overwrite a locked SOW.
```

---

## Interview — one topic at a time

Ask these conversationally. Do not present as a form. Wait for each answer before asking the next.

```
1. "What are we building for [[CLIENT_NAME]]?
    Give me a plain-language description — one paragraph."

2. "What does this build on or relate to?
    Is this a new engagement, a new phase of something existing,
    or a standalone project?"

3. "Walk me through the main objectives —
    what are the key outcomes this project needs to achieve?"

4. "What are the main workstreams or deliverable areas?
    For each one, give me a title and a brief description of what's included."

5. "What is explicitly out of scope?
    Things you want to make sure are not included."

6. "What are the key milestones and target dates?"

7. "What is the fixed fee for this engagement?
    And what is the payment schedule — e.g. 50% on signing, 50% on delivery?"

8. "Is there a variable bucket — time and materials hours
    for out-of-scope uncertainties? If yes, how many hours and what is the max value?"

9. "What is the client responsible for in this engagement?
    What are the key dependencies that could affect delivery?"

10. "Any confidentiality requirements beyond standard?
     Is this part of a larger engagement or MSA?"
```

---

## Steps

### Step 1 — Run the interview

Ask questions one at a time. Take notes after each answer. Confirm understanding where needed.

### Step 2 — Draft the SOW

Generate a complete SOW using BetaCraft's standard structure:

```
[BetaCraft Header]
[Effective Date]
[Project Number]

A. The Project
   - Description
   - Project Objectives
   - Scope Definition

B. Scope of Work
   - Numbered workstream sections
   - Explicit out-of-scope items
   - Deliverables list
   - Outcome statement

C. Time Schedule
   - Milestone table
   - Timeline assumptions and risks

D. Fees & Expenses
   - Fixed fee
   - Payment schedule table
   - Variable bucket (if applicable)
   - Expenses clause

E. Data Responsibility & Audit Ownership
   - Client responsibilities
   - BetaCraft responsibilities
   - Dependency acknowledgements

F. Miscellaneous
   - Additional work clause
   - Confidentiality
   - Phase relationship (if applicable)
   - SOW prevails clause

G. Signatures
   - Client and BetaCraft signature blocks
```

All legal boilerplate is generated automatically. PM only provides the project-specific content.

### Step 3 — Present for review

Show the complete SOW. Say:

```
Here is the complete SOW draft for [[PROJECT_NAME]].
Review each section. Tell me what to change.
When you are happy with everything, say "approved" and I will lock it.
```

### Step 4 — Conversational editing

Accept edits naturally:
- `"Change the fee to $25,000"` → update D
- `"Add webhook implementation to out of scope"` → update B
- `"The milestone dates are wrong — delivery is 8 weeks not 6"` → update C

Show the changed section after each edit. Confirm before moving on.

### Step 5 — Final approval

Wait for PM to say `"approved"`.

### Step 6 — Lock and extract

On approval:

**Lock sow.md:**
```markdown
**Authority:** Tier 1 — Canonical
**Locked:** [today's date]
**Locked by:** [[PM_NAME]]
**Rule:** Never edit. Raise a Change Order for any scope changes.
```

**Extract baseline requirements into `requirements/_baseline.md`:**
- Pull every deliverable and requirement from section B
- Number them REQ-001, REQ-002...
- Add Tier 1 authority header
- Lock with today's date

**Update `shared/PROJECT_INDEX.md`:**
- Add sow.md and _baseline.md to Reference section with locked date
- Update project state summary

**Update `shared/PROJECT_STRATEGY.md`:**
- Populate Vision, Goals, Constraints from SOW objectives and scope

**Update `project.md`:**
- Add target delivery date from SOW
- Add fee summary
- List active requirements from baseline

**First DEC entry in `shared/DECISIONS.md`:**
```markdown
## DEC-001
**Date:** [today]
**Participants:** [[PM_NAME]], [[CLIENT_NAME]]
**Decision:** SOW for [[PROJECT_NAME]] agreed and locked
**Why:** Establishes Tier 1 baseline for the engagement
**Affects:** All requirements and deliverables
```

**Commit:**
```
init: sow.md locked [date]
init: requirements/_baseline.md extracted
init: DEC-001 SOW agreed
```

### Step 7 — Report

```
✓ reference/sow.md — locked as Tier 1 Canonical
✓ requirements/_baseline.md — [N] requirements extracted
✓ shared/PROJECT_INDEX.md — updated
✓ shared/PROJECT_STRATEGY.md — populated
✓ project.md — updated with delivery date and fee
✓ DEC-001 logged — SOW agreed
✓ Committed and pushed

Project is live. Run "start session" to begin work.
```

---

## Never

- Never overwrite a locked sow.md
- Never skip the HITL review — PM must say "approved"
- Never invent project details — only what PM provides
- Never lock without explicit PM approval

---

## Vocabulary Extraction — runs as part of Step 6

After locking sow.md, extract canonical vocabulary into `shared/VOCABULARY.md`:

**Interview addition — ask before Step 5:**
```
"Are there any specific terms, names, or concepts that must be
 used consistently across all documents and calls?
 For example — product names, technical terms, entity names."
```

**Auto-extract from SOW text:**
- Project name and any abbreviations (canonical form only)
- All named entities: systems, services, components
- All role names: how each party is referred to
- All process terms: what each workflow is called
- Technical terms with specific meanings in this project

**Save to `shared/VOCABULARY.md`** with Tier 1 authority header.
**Lock alongside sow.md** — vocabulary is Tier 1 canonical.

**Add to commit:**
`init: shared/VOCABULARY.md locked [date]`
