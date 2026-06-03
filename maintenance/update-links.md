---
name: update-links
category: maintenance
description: >
  Maintains wikilinks and frontmatter across all project documents so
  the Obsidian knowledge graph stays accurate and traversable. Triggers
  on "update links" or runs automatically after any skill that creates
  or renames files. Adds missing frontmatter, adds missing wikilinks,
  fixes broken links. A broken link is a gap in the knowledge graph —
  this skill ensures the graph is always complete. Commits automatically.
---

# Skill: update-links

---

## Trigger

- `"update links"`
- `"fix links"`
- `"refresh knowledge graph"`
- Auto after any skill that creates or renames files

---

## Pre-read

Scan all project files. No specific pre-read needed.

---

## Frontmatter standard

Every document must have frontmatter. Add if missing:

**Requirements:**
```yaml
---
type: requirement
id: REQ-003
title: Stripe payment integration
status: in-progress
authority: tier-2
client: [[CLIENT_NAME]]
date-created: YYYY-MM-DD
date-modified: YYYY-MM-DD
linked-sow: [[reference/sow.md]]
tags: [requirement, stripe, payments]
---
```

**Deliverables:**
```yaml
---
type: deliverable
id: DEL-003
title: Stripe production integration
requirement: [[requirements/REQ-003-stripe-integration]]
status: in-progress
authority: tier-2
date-due: YYYY-MM-DD
date-delivered:
tags: [deliverable, stripe]
---
```

**Change events:**
```yaml
---
type: change-event
requirement: [[requirements/REQ-003-stripe-integration]]
date: YYYY-MM-DD
source: transcript/email/slack
approved-by: [[PM_NAME]]
authority: tier-3
tags: [change, REQ-003]
---
```

**Meeting transcripts:**
```yaml
---
type: transcript
date: YYYY-MM-DD
participants: [[[CLIENT_NAME]], [[PM_NAME]]]
authority: tier-3
tags: [meeting, transcript]
---
```

**Meeting summaries:**
```yaml
---
type: meeting-summary
date: YYYY-MM-DD
transcript: [[comms/meetings/YYYY-MM-DD-[name]-transcript]]
authority: tier-3
tags: [meeting, summary]
---
```

**Decisions:**
```yaml
---
type: decision
id: DEC-004
title: Stripe chosen over Paddle
date: YYYY-MM-DD
authority: tier-2
tags: [decision, stripe, technical]
---
```

---

## Wikilink standard

Add a Related section at the bottom of every document if missing:

**Requirements — link to:**
```markdown
---
*Related: [[reference/sow.md]] · [[requirements/_baseline]] · [[shared/DECISIONS]]*
*Change events: [[change-log/YYYY-MM-DD-title]]*
*Deliverables: [[deliverables/DEL-00N-title]]*
*Transcripts: [[comms/meetings/YYYY-MM-DD-transcript]]*
```

**Deliverables — link to:**
```markdown
---
*Requirement: [[requirements/REQ-00N-title]]*
*Decision: [[shared/DECISIONS#DEC-00N]]*
```

**Change events — link to:**
```markdown
---
*Requirement: [[requirements/REQ-00N-title]]*
*Source: [[comms/meetings/YYYY-MM-DD-transcript]]*
*Decision: [[shared/DECISIONS#DEC-00N]] (if applicable)*
```

**Decisions — link to:**
```markdown
---
*Affects: [[requirements/REQ-00N-title]]*
*Evidence: [[research/technical/YYYY-MM-DD-topic]] (if applicable)*
*Source: [[comms/meetings/YYYY-MM-DD-transcript]]*
```

---

## Steps

### Step 1 — Scan all files

Walk every .md file in the project. For each file:
- Check for frontmatter — add if missing
- Check for Related section — add if missing
- Check all existing wikilinks — flag broken ones

### Step 2 — Resolve broken links

A broken link is a wikilink pointing to a file that doesn't exist.
For each broken link:
- Check if file was renamed — update to new name
- Check if file was moved — update path
- If file genuinely missing — flag in report but don't delete the link

### Step 3 — Report

```
✓ Frontmatter added: [N] files
✓ Wikilinks added: [N] files
✓ Broken links fixed: [N]
⚠ Broken links unfixable: [N] — [list]
```

### Step 4 — Commit

`evt: links updated [date]`

---

## In chain

Run silently after file creation. Report at end:
`✓ Links updated — [N] files`
