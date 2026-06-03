---
name: session-end
category: session
description: >
  Mandatory session closing routine. Triggers on "end session", "done
  for today", "wrap up", or "closing". Updates PROJECT_INDEX.md,
  appends session-log.md with work done AND reasoning, checks for
  uncommitted changes and unlogged decisions, then commits and pushes
  everything. The Reasoning field is critical — it records why decisions
  were made so any PM can reconstruct the thinking months later.
  No single person's memory should be the bottleneck.
---

# Skill: session-end

---

## Trigger

- `"end session"`
- `"done for today"`
- `"wrap up"`
- `"closing"`
- `"sign off"`

---

## Steps

### Step 1 — Review what happened this session

Read all files modified during this session. Identify:
- What was created or updated
- What decisions were made (check all are in DECISIONS.md)
- What was committed vs uncommitted
- Any conflicts added to CONFLICTS.md
- Any action items completed
- Any proposals added to workspace

### Step 2 — Update shared/PROJECT_INDEX.md

Update:
- `Last session:` → today
- `Status:` → current RAG
- `Open Questions:` → refresh
- `Decisions (latest 5):` → refresh
- `Blocking Items:` → refresh from HOTSHEET

Commit: `evt: PROJECT_INDEX updated [date]`

### Step 3 — Check for unlogged decisions

If any significant decision was made not in `shared/DECISIONS.md`:
```
⚠ Unlogged decision found:
  "[what was decided]"
  Add to shared/DECISIONS.md or proposed-decisions.md?
```
Wait for PM choice.

### Step 4 — Check for uncommitted changes

Run `git status`. If uncommitted files exist — list and commit them.

### Step 5 — Append session-log.md

Append one entry with the Reasoning field:

```markdown
## [YYYY-MM-DD] — [one line summary]

**Work done:**
- [Specific item — file created/updated]
- [Specific item]

**Reasoning:**
- [Why item 1 was done — the thinking behind the action]
- [Why item 2 was done]

**Drift detected:** [what was flagged / None]
**Decisions logged:** DEC-00N [title] / None
**Proposals added:** PROP-DEC-00N / None
**Files committed:** [N] files
**Open items:** [N] blocking, [N] watching
```

Commit: `session: [date] closed`

### Step 6 — Push

```bash
git push origin main
```

### Step 7 — Final report

```
✓ PROJECT_INDEX.md updated
✓ Session log appended — [date]
✓ [N] files committed
✓ Pushed to GitHub

Session closed.
```

---

## Never

- Never skip the Reasoning field — this is what makes the log useful
- Never leave uncommitted changes without flagging
- Never close without checking for unlogged decisions
