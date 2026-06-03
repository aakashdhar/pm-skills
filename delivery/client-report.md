---
name: client-report
category: delivery
description: >
  Generates a professional client-facing progress update. Transparent,
  sourced, no internal jargon. Triggers on "client report" or "draft
  client update". Every claim sourced. Never cite Tier 3 documents.
  Read-only — output in chat, PM sends manually.
---

# Skill: client-report

---

## Trigger

- `"client report"`
- `"draft client update"`
- `"write the monthly update"`
- `"client-facing summary"`

---

## Pre-read

1. `reference/sow.md` — Tier 1 baseline
2. `project.md`
3. `requirements/` and `deliverables/`
4. `change-log/` since last report
5. `comms/summary.md`
6. `client.md` — communication preferences

---

## Authority rule

Only cite Tier 1 and Tier 2 documents in client reports.
Never cite Tier 3 (change-log, comms, research) directly in client output.

---

## Output

```
# Project Update — [[PROJECT_NAME]]
[Date] | Prepared by [[PM_NAME]], BetaCraft

## Where We Stand
[🟢 On Track / 🟡 Attention Needed / 🔴 Action Required]
[2–3 plain-language sentences]

## What We've Delivered
| Item | Delivered | Verified |
|---|---|---|

## What We're Working On
| Item | Target | Status |
|---|---|---|

## What Changed Since We Last Spoke
- [Date] — [what changed and why — plain language]

## What We Need From You
- [Action] — needed by [date] — blocks [what]

## What's Coming Next
| Item | Target Date |
|---|---|

[Closing line]
[[PM_NAME]]
Project Manager, BetaCraft
[[PM_EMAIL]]
```

---

## Tone rules

- Professional and warm
- No internal jargon — no REQ-003, HOTSHEET, sprint
- Every claim in source documents — never invent progress
- Problems framed transparently — not hidden
- No emojis in body

## Read-only. No commits.
