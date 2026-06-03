---
name: status-report
category: delivery
description: >
  Generates a RAG-focused status report for upper management. Covers
  overall status, promises vs delivery, changes since last report, risks,
  next milestones. No operational noise. Triggers on "status report".
  Read-only. Audience is upper management — concise and decision-relevant.
---

# Skill: status-report

---

## Trigger

- `"status report"`
- `"mgmt update"`
- `"generate status report"`
- `"executive summary"`

---

## Pre-read

1. `shared/PROJECT_INDEX.md`
2. `project.md`
3. `requirements/` and `deliverables/`
4. `change-log/` since last report
5. `shared/HOTSHEET.md`
6. `reference/sow.md`

---

## Output

```
# Status Report — [[PROJECT_NAME]]
Prepared by: [[PM_NAME]] | Date: [today]
Client: [[CLIENT_NAME]] | Phase: [phase]

## Overall Status
[🟢/🟡/🔴]
Reason: [one sentence]

## Summary
[2–3 sentences — progress vs original plan]

## Promises vs Delivery
| Requirement | In SOW | Status | Target / Delivered |
|---|---|---|---|

Original scope: [N] | Added post-SOW: [N] | Delivered: [N] of [total]

## Changes Since Last Report
| Date | Change | Impact |
|---|---|---|

## Risks
| Risk | Severity | Status |
|---|---|---|

## Next Milestones
| Milestone | Target | Status |
|---|---|---|
```

---

## Read-only. No commits.
