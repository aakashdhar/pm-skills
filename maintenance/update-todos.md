---
name: update-todos
category: maintenance
description: >
  Updates comms/todos.md — marks completed action items as done and
  adds new ones with owner, source, and due date. Triggers on
  "update todos" or automatically after process-transcript and sync-comms.
  Todos are communication-level commitments — different from HOTSHEET
  which tracks broader project open items. Commits automatically.
---

# Skill: update-todos

---

## Trigger

- `"update todos"`
- `"refresh action items"`
- Auto after `process-transcript` and `sync-comms`

---

## Steps

### Step 1 — Identify changes

**Complete:** items with completion signals in this session's processed content
**Add:** new commitments — "I will", "we will", "please send", "by [date]"

### Step 2 — Rewrite comms/todos.md

Format:
```markdown
## Open
- [ ] [Action] — [Owner] — Source: [file ref] — Due: [date or —]

## Completed
- [x] [Action] — [Owner] — Completed [date]
```

Most urgent first. Completed items never deleted.

### Step 3 — Commit

`evt: todos updated [date]`

---

## In chain

No PM confirmation. Run silently. Report:
`✓ comms/todos.md — [N] new, [N] completed`
