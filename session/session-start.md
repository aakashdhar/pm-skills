---
name: session-start
category: session
description: >
  Mandatory session opening routine. Triggers on "start session",
  "good morning", or any first message when opening a project folder
  in Cowork. Reads the governing layer in order, runs drift detection
  against Tier 1 documents, checks vocabulary consistency, reports
  anything new since last session, and briefs the PM before any work
  begins. Never skips this routine. The PM should never have to
  re-explain context — session-start is what guarantees that.
---

# Skill: session-start

---

## Trigger

- `"start session"`
- `"morning"` / `"good morning"`
- First message after opening project folder in Cowork
- `"what's the status?"`
- `"catch me up"`

---

## Reading order — mandatory, always in this sequence

1. `shared/PROJECT_INDEX.md` — current project state
2. `shared/DECISIONS.md` — what is locked
3. `shared/HOTSHEET.md` — what is blocking or urgent
4. `shared/CONFLICTS.md` — any unresolved conflicts
5. `shared/VOCABULARY.md` — canonical terms
6. `workspaces/aakash/session-log.md` — last session entry
7. `comms/todos.md` — overdue action items

---

## Steps

### Step 1 — Read everything in order

Read all seven files fully before generating anything.

### Step 2 — Run drift detection

Scan all Tier 2 documents against Tier 1:

**Check every `requirements/REQ-*.md` against `reference/sow.md`:**
- Does any requirement contradict the original SOW?
- Has anything been added without a corresponding change-log entry?

**Check every `deliverables/DEL-*.md` against its linked requirement:**
- Does the deliverable spec match what the requirement describes?

**Check `shared/PROJECT_STRATEGY.md` against `reference/sow.md`:**
- Has strategy drifted from the original agreement?

**Check recent `change-log/` entries against `shared/DECISIONS.md`:**
- Do any changes contradict locked decisions?

Collect all drift findings for the briefing.

### Step 3 — Run vocabulary check

Scan the last 3 `change-log/` entries and last meeting summary against `shared/VOCABULARY.md`:
- Are canonical terms being used correctly?
- Any drift in naming or terminology?

### Step 4 — Generate session briefing

```
# Session Briefing — [[PROJECT_NAME]]
Date: [today] | PM: [[PM_NAME]]

---

## Last Session
[Date] — [one line summary from session-log.md last entry]
Reasoning: [why decisions were made — from Reasoning field]

## Status
[🟢/🟡/🔴] [RAG] — [one line reason]
Phase: [phase] | Days to delivery: [N]

## Since Last Session
- New decisions: DEC-00N [title] / None
- New conflicts: CONFLICT-00N / None
- Items resolved: [X] / None

## ⚠ Drift Detected
[List each drift finding:]
- REQ-003 may conflict with sow.md clause B.4 — [detail]
- [or: No drift detected ✓]

## ⚠ Vocabulary Issues
- [term used] in [file] — canonical term is [correct term]
- [or: No vocabulary issues ✓]

## Blocking Right Now
[From HOTSHEET 🔴 — or "Nothing blocking"]

## Needs Attention
[From HOTSHEET 🟡 — or "Nothing pending"]

## Overdue Action Items
[From comms/todos.md — or "None overdue"]

## Open Conflicts
[From CONFLICTS.md — or "No open conflicts"]

## Pending Workspace Proposals
[From proposed-decisions.md + proposed-risks.md — or "None pending"]

---
Ready. What would you like to work on?
```

### Step 5 — Wait for PM instruction

Do not proceed with any work until PM responds.
If drift was detected — suggest: `"resolve drift"` or `"add to conflicts"` before starting other work.

---

## Never

- Never skip this routine even for quick tasks
- Never skip drift detection — it runs every session
- Never assume context from a previous session without reading
- Never start work before completing the briefing
