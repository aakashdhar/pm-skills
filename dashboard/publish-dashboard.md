---
name: publish-dashboard
category: dashboard
description: >
  Publishes dashboard.html to GitHub Pages. Archives the current version,
  regenerates the version history index, commits, and pushes to gh-pages.
  Triggers on "publish dashboard" or "share the dashboard". Requires
  dashboard.html to exist — run refresh-dashboard first. Every published
  version is permanently accessible. Version history linked from footer.
---

# Skill: publish-dashboard

---

## Trigger

- `"publish dashboard"`
- `"push the dashboard"`
- `"share the dashboard"`
- `"go live with the dashboard"`

---

## Pre-read

1. `dashboard.html` — must exist
2. `dashboard-versions/` — for version number

---

## Steps

### Step 1 — Verify dashboard.html exists

If missing: `⚠ Run "refresh dashboard" first.` Stop.

### Step 2 — Determine version

Count files in `dashboard-versions/` (exclude index.html). Version = count + 1.

### Step 3 — Archive

Copy `dashboard.html` → `dashboard-versions/YYYY-MM-DD-v[N].html`

### Step 4 — Regenerate index

Rebuild `dashboard-versions/index.html` with new version at top.

### Step 5 — Commit and push

```
git add dashboard.html dashboard-versions/
git commit -m "dash: v[N] published [date]"
git push origin main

git checkout gh-pages
cp dashboard.html index.html
cp -r dashboard-versions/ .
git add . && git commit -m "dash: v[N] published [date]"
git push origin gh-pages
git checkout main
```

### Step 6 — Report

```
✓ Archived: dashboard-versions/[date]-v[N].html
✓ Version index updated
✓ Committed: dash: v[N] published [date]
✓ Pushed to GitHub Pages

Dashboard URL: https://betacraft.github.io/pm-[project-slug]
Version history: [url]/dashboard-versions/

Share with [[CLIENT_NAME]]: [url]
```
