---
name: update-index
category: maintenance
description: >
  Scans all project folders and rewrites shared/PROJECT_INDEX.md with
  a current map of every document — file path, authority tier, and
  one-line description. Triggers on "update index" or automatically
  when new files are created. The master index must always be current.
  Commits automatically. Never modifies any file other than PROJECT_INDEX.md.
---

# Skill: update-index

---

## Trigger

- `"update index"`
- `"refresh project index"`
- Auto after any skill that creates new files

---

## Steps

### Step 1 — Scan all folders

Walk the full project directory. For each file:
- Path (relative to project root)
- Authority tier (from file header or inferred from folder)
- One-line description (from filename and first line)
- Last modified date

### Step 2 — Rewrite shared/PROJECT_INDEX.md

Update all tables. Update `Last Updated` and `Last session` fields.
Every file in the project must appear. Do not list PROJECT_INDEX.md itself.

### Step 3 — Commit

`evt: PROJECT_INDEX updated [date]`

---

## In chain

No PM confirmation. Run silently. Report:
`✓ PROJECT_INDEX.md updated`
