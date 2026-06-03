---
name: update-hotsheet
category: maintenance
description: >
  Rewrites shared/HOTSHEET.md — removes resolved items, adds new ones
  with source references, maintains priority order. Triggers on
  "update hotsheet" or runs automatically after process-transcript
  and sync-comms. When running in a chain — no PM confirmation needed,
  just run and report. Commits automatically.
---

# Skill: update-hotsheet

---

## Trigger

- `"update hotsheet"`
- `"refresh hotsheet"`
- Auto after `process-transcript` and `sync-comms`

---

## Steps

### Step 1 — Identify changes from session

**Resolve:** anything completed, delivered, or answered this session
**Add:** new blockers, risks, action items needing PM attention
**Reclassify:** watching items that escalated, blocking items partially resolved

### Step 2 — Rewrite shared/HOTSHEET.md

Maintain exact structure. Priority: 🔴 Blocking → 🟡 Needs Attention → 🔵 Watching → ✅ Resolved.

Every item must have:
- Description
- Since date (when it first appeared — not today)
- Source reference (file path or comms date)

Resolved items move to ✅ section — never deleted.

### Step 3 — Commit

`evt: HOTSHEET updated [date]`

---

## In chain

No PM confirmation needed. Run silently. Report:
`✓ HOTSHEET.md — [N] added, [N] resolved`
