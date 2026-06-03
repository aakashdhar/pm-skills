---
name: change-summary
category: delivery
description: >
  Returns a sourced summary of every requirement change, deliverable,
  and decision since a specified date. Triggers on "what changed since
  [date]" or "changes since [date]". Sources every item to its
  change-event file or DECISIONS.md entry. Read-only.
---

# Skill: change-summary

---

## Trigger

- `"what changed since [date]"`
- `"changes since [date]"`
- `"what happened in [month]"`
- `"summarise the last [N] weeks"`

---

## Pre-read

1. `change-log/` — all files after specified date
2. `shared/DECISIONS.md` — entries in date range
3. `deliverables/` — status changes in date range
4. `comms/meetings/` — meeting summaries in date range

---

## Output

```
# Change Summary — [[PROJECT_NAME]]
Period: [start] to [today]

## Requirements Changed ([N])
### [Date] — [Title]
Requirement: REQ-00N
What changed: [before → after]
Source: "[exact quote]" — [file ref]
Approved by: [[PM_NAME]]

## Delivered ([N])
| Item | Delivered | Evidence |
|---|---|---|

## Decisions Made ([N])
| DEC | Decision | Date |
|---|---|---|
```

If a change happened with no change-log entry:
`⚠ No change-log entry found for [X] — run log-change to document it`

---

## Read-only. No commits.
