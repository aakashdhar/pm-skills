---
name: update-summary
category: maintenance
description: >
  Reads all communications from the last 30 days and rewrites
  comms/summary.md as a plain-English narrative of the client
  relationship. Not a list — a narrative a new PM could read to
  understand the full relationship history. Triggers on "update
  comms summary" or automatically after sync-comms. Commits automatically.
---

# Skill: update-summary

---

## Trigger

- `"update comms summary"`
- `"refresh the comms summary"`
- Auto after `sync-comms`

---

## Steps

### Step 1 — Read all recent comms

All files in `comms/emails/`, `comms/slack/`, `comms/meetings/` from last 30 days.

### Step 2 — Rewrite comms/summary.md

Write as prose narrative — not bullets. Third person. Under 400 words.
Sections: Relationship Overview, What Has Been Discussed, What Was Agreed, What Is Pending, Client Sentiment, Notable Moments.

Every claim must trace to a comms file. Never invent.

### Step 3 — Commit

`comms: summary updated [date]`

---

## In chain

No PM confirmation. Run silently. Report:
`✓ comms/summary.md updated`
