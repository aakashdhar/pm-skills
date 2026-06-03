---
name: check-alignment
category: verification
description: >
  Scans all requirements against the codebase and reports implementation
  status per requirement. Also flags undocumented features — scope creep
  signals. Triggers on "check alignment". Read-only. Never modifies the
  codebase. Run before demos, delivery milestones, or client calls.
---

# Skill: check-alignment

---

## Trigger

- `"check alignment"`
- `"are all requirements implemented?"`
- `"pre-delivery alignment check"`
- `"does the code match the requirements?"`

---

## Pre-read

1. All `requirements/REQ-*.md`
2. Code repo — read-only, path from `project.md`
3. `reference/sow.md`

---

## Output

```
# Alignment Report — [[PROJECT_NAME]]
[today] | Codebase: [path] | Branch: [branch]

## Summary
Checked: [N] | ✓ Implemented: [N] | ⚠ Partial: [N] | ✗ Not found: [N]
Undocumented features: [N]

## Per-Requirement Status
### REQ-001 — [Title]
Status in docs: Delivered
Status in code: ✓ Confirmed
Evidence: [file:line]

### REQ-003 — [Title]
Status in code: ⚠ Partial
Missing: [what criteria not met]

## Undocumented Features
| Feature | Location | Notes |
|---|---|---|

## Overall Assessment
[Plain language — gaps to address before delivery]
```

---

## Read-only. No commits.
