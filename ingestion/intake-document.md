---
name: intake-document
category: ingestion
description: >
  Formally incorporates an external document — sent by client, partner,
  or stakeholder — into the project record. Triggers on "intake document
  [filename]", "client sent a document", or when sync-comms flags an
  attachment. Date-stamps, assesses authority level, checks for conflicts
  with existing Tier 1 documents, updates the index, and prompts PM to
  decide if it should be promoted to reference/. A document does not
  become governing just because it was shared — PM must explicitly promote it.
---

# Skill: intake-document

---

## Trigger

- `"intake document [filename]"`
- `"client sent a document"`
- `"process this attachment"`
- Flagged by sync-comms
- File dropped in `comms/attachments/`

---

## Pre-read

1. `reference/sow.md` — does this supersede anything?
2. `shared/PROJECT_INDEX.md` — current document map
3. `shared/DECISIONS.md` — any relevant locked decisions

---

## Steps

### Step 1 — Date-stamp and save

Save to `comms/attachments/YYYY-MM-DD-[filename]` immediately.
If already there — confirm it is date-stamped correctly.

### Step 2 — Assess the document

Read the document and determine:
- What type is it? (spec, proposal, feedback, contract, research, etc.)
- Does it supersede any existing document?
- What authority level does it claim or imply?
- Does it conflict with any Tier 1 document?

### Step 3 — Present assessment

```
# Document Intake — [filename]
Received: [date]
Saved: comms/attachments/YYYY-MM-DD-[filename]

## Assessment
Type: [spec / proposal / feedback / contract / research]
Supersedes: [existing file / nothing]
Conflicts with: [Tier 1 file / none]
Claimed authority: [what the document implies about its own status]

## Recommendation
[ ] Promote to reference/ as Tier 1 Canonical
[ ] Keep in comms/attachments/ as Tier 3 Archive
[ ] Needs further review before decision

## If it supersedes something
The superseded document would be moved to:
comms/attachments/superseded/YYYY-MM-DD-[old-filename]

What would you like to do?
```

### Step 4 — Wait for PM decision

PM decides:
- Promote to `reference/` → becomes Tier 1, locked
- Keep as attachment → Tier 3, lineage only
- Flag as conflict → write to `shared/CONFLICTS.md`

### Step 5 — Execute PM decision

**If promoted to reference/:**
- Move to `reference/[filename].md`
- Add Tier 1 authority header
- Move superseded document to `comms/attachments/superseded/`
- Update `shared/PROJECT_INDEX.md`
- Log in `shared/DECISIONS.md`: `DEC-00N — [document] promoted to Tier 1`

**If kept as attachment:**
- Add Tier 3 authority header
- Update `shared/PROJECT_INDEX.md`

**If flagged as conflict:**
- Write to `shared/CONFLICTS.md`
- Do not act further until PM resolves

### Step 6 — Commit

`comms: document intake [filename] [date]`

---

## Never

- Never promote a document to Tier 1 without explicit PM instruction
- Never treat a shared document as governing until formally incorporated
- Never delete a superseded document — move to superseded/ folder
