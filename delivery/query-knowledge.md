---
name: query-knowledge
category: delivery
description: >
  Natural language queries against the project knowledge graph via
  Obsidian MCP. Triggers on "query:", "what did the client say about
  [topic]", "full history of [requirement]", "all decisions linked to
  [topic]", or "what changed between [date] and [date]". Uses the
  Obsidian MCP connection to search across all documents by content,
  tags, backlinks, and frontmatter — precise retrieval regardless of
  project size. Completely abstracted — user never needs to know
  Obsidian is involved. Read-only. No files modified.
---

# Skill: query-knowledge

---

## Trigger

- `"query: [anything]"`
- `"what did the client say about [topic]?"`
- `"full history of REQ-00N"`
- `"all decisions linked to [topic]"`
- `"what changed between [date] and [date]"`
- `"find everything about [topic]"`
- `"when did we first discuss [topic]?"`
- `"what was agreed about [topic]?"`

---

## How it works

Uses the Obsidian MCP server (running locally) to query the project vault.
The vault is the project folder — all Markdown files indexed by Obsidian.
Cowork navigates the knowledge graph via backlinks, frontmatter, and
full-text search rather than reading files linearly.

This is what makes retrieval fast and precise as the project grows.

---

## Query types and how to handle each

### Type 1 — Topic query
```
"what did the client say about Stripe?"
```
1. Full-text search vault for "Stripe"
2. Filter to comms/ files (emails, meetings, slack)
3. Navigate backlinks to linked requirements and decisions
4. Return: sourced quotes with file references and dates

### Type 2 — Requirement history
```
"full history of REQ-003"
```
1. Open requirements/REQ-003-*.md via MCP
2. Follow wikilinks to: sow.md, change-log entries, decisions, transcripts, deliverables
3. Build chronological timeline of every event touching this requirement
4. Return: complete history with dates and sources

### Type 3 — Decision trail
```
"all decisions linked to the login flow"
```
1. Search DECISIONS.md frontmatter for login-related tags
2. Navigate backlinks from those decisions to requirements
3. Navigate forward links to change events and transcripts
4. Return: decision list with rationale and source attribution

### Type 4 — Date range query
```
"what changed between March and May?"
```
1. Filter change-log/ by frontmatter date field
2. Filter DECISIONS.md entries by date
3. Filter comms/meetings/ summaries by date
4. Return: chronological summary of everything in range

### Type 5 — Source attribution query
```
"when did we first discuss the free tier?"
```
1. Full-text search for "free tier" across all files
2. Sort results by frontmatter date — oldest first
3. Return: first occurrence with exact quote and file reference

---

## Output format

```
# Knowledge Query — [[PROJECT_NAME]]
Query: "[what was asked]"
Date: [today]

## Answer
[Direct answer in plain language]

## Sources
| Date | File | Relevant excerpt |
|---|---|---|
| [date] | [file path] | "[quote]" |

## Related Documents
- [[file]] — [why relevant]
- [[file]] — [why relevant]

## Graph path taken
[Optional — show the link traversal for complex queries]
```

---

## Read-only. No files modified. No commits.

---

## If Obsidian MCP is not connected

Fall back to linear file reading with a note:
```
⚠ Obsidian MCP not connected — using linear search.
  Run install.sh or migrate.sh to enable knowledge graph queries.
  Results may be slower and less precise for large projects.
```
