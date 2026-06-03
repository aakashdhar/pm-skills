---
name: merge-review
category: maintenance
description: >
  Reviews proposed changes from workspaces/ against shared/ documents,
  shows diffs, flags conflicts, and promotes approved items to the
  governing layer. Triggers on "merge review", "review my proposals",
  or "what have I proposed". Shows exactly what changed, what conflicts
  with existing shared documents, and waits for PM approval before
  promoting anything. The owner is the only one who can approve a merge.
  Nothing in workspaces/ becomes governing until promoted via this skill.
---

# Skill: merge-review

---

## Trigger

- `"merge review"`
- `"review my proposals"`
- `"what have I proposed?"`
- `"promote my decisions"`
- `"merge proposed risks"`
- `"what's in my workspace?"`

---

## Pre-read

1. `workspaces/aakash/proposed-decisions.md` — pending proposals
2. `workspaces/aakash/proposed-risks.md` — pending risk proposals
3. `shared/DECISIONS.md` — current governing decisions
4. `shared/HOTSHEET.md` — current governing open items
5. `shared/CONFLICTS.md` — existing conflicts
6. `shared/VOCABULARY.md` — check proposals use canonical terms

---

## Steps

### Step 1 — Read all pending proposals

Read both proposal files. Identify items with status `Ready for review` or `Draft`.
If nothing pending:
```
No pending proposals in your workspace.
workspaces/aakash/proposed-decisions.md — empty
workspaces/aakash/proposed-risks.md — empty
```

### Step 2 — Diff each proposal against shared/

For each pending proposal — compare against the current shared document:

**For proposed decisions:**
- Does a similar decision already exist in `shared/DECISIONS.md`?
- Does this contradict any existing decision?
- Does this conflict with any Tier 1 document?
- Does it use canonical vocabulary from `shared/VOCABULARY.md`?

**For proposed risks:**
- Is this already in `shared/HOTSHEET.md`?
- Is this consistent with current project status?
- Does the severity classification seem right?

### Step 3 — Present merge review

```
# Merge Review — [[PROJECT_NAME]]
Date: [today] | Reviewer: [[PM_NAME]]

---

## Proposed Decisions ([N] pending)

### PROP-DEC-001 — [Title]
**Proposed:** [date]
**Type:** [type]

**Diff against shared/DECISIONS.md:**
  No existing decision on this topic — clean addition

**Conflict check:**
  ✓ No conflict with existing decisions
  ✓ No conflict with Tier 1 documents
  ⚠ Vocabulary: uses "[term]" — canonical term is "[canonical]"

**Proposed DEC number if approved:** DEC-00N

ACTION: Approve / Edit / Reject / Hold

---

### PROP-DEC-002 — [Title]
**Proposed:** [date]

**Diff against shared/DECISIONS.md:**
  Conflicts with DEC-003: "[existing decision text]"
  This proposal says: "[proposed text]"

**Conflict check:**
  ⚠ Contradicts DEC-003 — requires PM resolution

ACTION: Approve (overrides DEC-003) / Reject / Add to CONFLICTS.md

---

## Proposed Risks ([N] pending)

### PROP-RISK-001 — [Title]
**Proposed:** [date]
**Type:** 🟡 Needs Attention

**Diff against shared/HOTSHEET.md:**
  Not currently in HOTSHEET — clean addition

**Conflict check:**
  ✓ No conflicts

ACTION: Approve / Edit / Reject

---

## Summary
Ready to promote: [N]
Conflicts to resolve: [N]
Vocabulary issues: [N]

Tell me which to approve, edit, or reject.
```

### Step 4 — Wait for PM decisions

Accept per-item decisions:
- `"approve PROP-DEC-001"` → promote to shared/DECISIONS.md
- `"reject PROP-RISK-001"` → mark rejected in proposed-risks.md
- `"edit PROP-DEC-002 — change the rationale to [X]"` → update proposal
- `"hold PROP-DEC-001 — not ready yet"` → leave in Draft
- `"approve all clean ones"` → promote all with no conflicts

### Step 5 — Execute approved promotions

**For approved decisions:**
- Assign next DEC number
- Append to `shared/DECISIONS.md`
- Mark as Promoted in `workspaces/aakash/proposed-decisions.md`
- Fix vocabulary issues before promoting

**For approved risks:**
- Add to appropriate section in `shared/HOTSHEET.md`
- Mark as Promoted in `workspaces/aakash/proposed-risks.md`

**For conflicts:**
- Write to `shared/CONFLICTS.md` with full context
- Do not promote until PM resolves

### Step 6 — Commit

```
dec: DEC-00N [title] promoted from workspace
evt: HOTSHEET updated — [N] risks promoted
```

### Step 7 — Report

```
✓ Promoted: [N] decisions → shared/DECISIONS.md
✓ Promoted: [N] risks → shared/HOTSHEET.md
✓ Conflicts logged: [N] → shared/CONFLICTS.md
✓ Vocabulary fixed: [N] terms corrected
✓ Committed
```

---

## Never

- Never promote without explicit PM approval per item
- Never silently fix vocabulary — show the correction and confirm
- Never overwrite an existing DEC entry — always add as new
- Never promote a decision that conflicts with Tier 1 without PM explicitly overriding
