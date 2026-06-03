---
name: promise-check
category: verification
description: >
  Compares the original SOW (Tier 1) against current requirements and
  deliverables. Shows what was promised, what was added post-SOW, what
  was delivered, and what is outstanding. Triggers on "promise check"
  or "what did we promise vs deliver". The definitive accountability
  check. Read-only. reference/sow.md is ground truth — never substitute.
---

# Skill: promise-check

---

## Trigger

- `"promise check"`
- `"what did we promise vs deliver?"`
- `"SOW vs delivery"`
- `"accountability check"`

---

## Pre-read

1. `reference/sow.md` — Tier 1 ground truth
2. `requirements/_baseline.md` — Tier 1 original requirements
3. All `requirements/REQ-*.md`
4. All `deliverables/DEL-*.md`
5. `change-log/`

---

## Output

```
# Promise Check — [[PROJECT_NAME]]
SOW Date: [date] | Report: [today]

## Scope Summary
Original SOW: [N] | Added post-SOW: [N] | Removed: [N] | Total: [N]

## Full Accountability Table
| REQ | Title | Origin | Status | Delivered | Evidence |
|---|---|---|---|---|---|
| REQ-001 | [Title] | ✓ Original | ✓ Delivered | [date] | [link] |
| REQ-005 | [Title] | + Added [date] | ⟳ In Progress | — | — |

## Original SOW Delivery Status
Of [N] originally agreed: ✓ [N] delivered | ⟳ [N] in progress | ✗ [N] not started

## Assessment
[Are we on track? Scope expansion risks? Key gaps?]
```

---

## Read-only. reference/sow.md is the only truth. No commits.
