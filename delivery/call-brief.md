---
name: call-brief
category: delivery
description: >
  Generates a structured PM call brief before a client call. Triggers
  on "call brief", "prepare call brief", or "brief me before the call".
  Reads full project context — status, what changed since last call,
  open items, risks, talking points, outstanding action items.
  Read-only. No files created or modified. Output for PM only.
---

# Skill: call-brief

---

## Trigger

- `"call brief"`
- `"prepare call brief"`
- `"brief me before the call"`
- `"what do I need to know for today's call?"`

---

## Pre-read

1. `shared/PROJECT_INDEX.md`
2. `shared/HOTSHEET.md`
3. `shared/DECISIONS.md` — last 3 entries
4. `shared/CONFLICTS.md` — any open conflicts
5. `requirements/` — all statuses
6. `change-log/` — last 3 entries
7. `comms/summary.md`
8. `comms/meetings/` — last meeting summary
9. `comms/todos.md`
10. `reference/sow.md` — promise baseline

---

## Output

```
# Call Brief — [[PROJECT_NAME]]
Prepared: [today] | Call with: [[CLIENT_NAME]]

## Status
[🟢/🟡/🔴] [RAG] — [one line reason]
Phase: [phase] | Days to delivery: [N]

## Since Last Call ([date])
- [What changed — requirement, deliverable, decision]

## Open Items to Discuss
- [Item] — [what resolution is needed]

## Open Conflicts
- [CONFLICT-00N] — [one line summary] — needs your decision

## Risks to Flag
- [Risk] — [status and mitigation]

## Suggested Talking Points
1. [Point and why]
2. [Point]

## Outstanding Action Items
| Item | Owner | Due | Status |
|---|---|---|---|
| [Item] | [Owner] | [Date] | ✓ Done / ⟳ Pending / ⚠ Overdue |

## Context Notes
[Client sentiment and relationship notes from comms/summary.md]
```

---

## Read-only

No files created. No commits. Output in chat only.
