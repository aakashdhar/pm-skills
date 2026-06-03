---
name: log-decision
category: ingestion
description: >
  Logs a technical or strategic decision to shared/DECISIONS.md with a
  sequential DEC number, date, participants, decision, and rationale.
  Triggers on "log this decision", "record that we decided to [X]",
  or "add this to the decision log". Confirms details before writing.
  Append-only — never edits existing entries. Also runs automatically
  as part of process-transcript when decisions are extracted from calls.
---

# Skill: log-decision

---

## Trigger

- `"log this decision"`
- `"log a decision"`
- `"record that we decided to [X]"`
- `"add this to the decision log"`
- `"document the decision about [X]"`
- Auto-triggered by process-transcript for decisions extracted from calls

---

## Pre-read

1. `shared/DECISIONS.md` — determine next DEC number
2. `requirements/` — which requirement this affects (if any)

---

## Steps

### Step 1 — Determine next DEC number

Count existing DEC entries in `shared/DECISIONS.md`. Next = count + 1.

### Step 2 — Confirm details

```
Before logging DEC-00N, confirm:

Title: [what Cowork understood — correct?]
Type: Technical / Strategic / Commercial / Operational?
Participants: [[PM_NAME]] + [who else?]
Decision: [what was decided]
Rationale: [why this over alternatives]
Affects: [REQ-00N / deliverable / architecture / N/A]
```

Wait for PM to confirm or correct.

### Step 3 — Append to shared/DECISIONS.md

```markdown
## DEC-00N
**Date:** [today]
**Type:** [Technical / Strategic / Commercial / Operational]
**Participants:** [[PM_NAME]], [others]
**Decision:** [what was decided — one clear sentence]
**Rationale:** [why — key reason]
**Affects:** [REQ-00N / area / N/A]
**Evidence:** [research file or transcript ref if applicable]
```

**Append only. Never edit above this entry.**

### Step 4 — Update architecture/ if significant

For architecture or technology decisions — create a detailed entry:

```markdown
# DEC-00N: [Title]
[Full context, alternatives considered, implications]
```

Save to `architecture/technical/` or `architecture/strategic/`.

### Step 5 — Commit

`dec: DEC-00N [title]`

---

## Never

- Never edit an existing DEC entry
- Never reuse a DEC number
- Never log a decision without PM confirmation of the details
- Never delete any entry from DECISIONS.md
