---
name: verify-delivery
category: verification
description: >
  Reads a deliverable spec and its linked requirement, scans the codebase
  read-only, and reports Confirmed / Partial / Not Found with file references.
  Triggers on "verify [deliverable]" or "verify DEL-00N". Use before
  telling a client something is delivered. Never modifies the codebase.
---

# Skill: verify-delivery

---

## Trigger

- `"verify [deliverable]"`
- `"verify DEL-00N"`
- `"is [feature] actually implemented?"`
- `"confirm DEL-00N before the client call"`

---

## Pre-read

1. `deliverables/DEL-00N-[title].md`
2. Linked `requirements/REQ-00N-[title].md`
3. Code repo path from `project.md` — read-only

---

## Output

```
# Delivery Verification — [Title]
DEL-00N | REQ-00N | [today]

Verdict: ✓ Confirmed / ⚠ Partial / ✗ Not Found

## What Was Agreed
[Acceptance criteria from REQ file]

## What Was Found in Code
| Criterion | Found | Location |
|---|---|---|

## Verdict Detail
[Plain language — what matches, what is missing]

## Recommendation
[Should this be marked Delivered? If partial — what's missing?]
```

---

## Read-only. Codebase never modified. No commits.
