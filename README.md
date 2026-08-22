# PhD_Progress

A single-file static page tracking manuscripts under review, papers in writing,
and queued work. Deployed with GitHub Pages.

**Live:** https://rakesh2109.github.io/PhD_Progress/

## Updating status

Everything on the page is generated from one array. Open `index.html`, find the
block marked `EDIT HERE`, and edit the entries:

```js
{
  status:"review",          // "review" | "writing" | "backlog"
  venue:"IEEE Internet of Things Journal",
  kind:"Regular Article",
  title:"...",
  id:"IoT-71372-2026",      // manuscript ID (review items)
  submitted:"2026-07-25",   // YYYY-MM-DD — "days in review" is computed from this
  stage:1,                  // 0 submitted · 1 under review · 2 decision
  badge:"Under Review · Submission 2",
  facts:[["Round","2nd submission"]]   // extra key/value rows
}
```

Writing items use `deadline:"YYYY-MM-DD"` and `progress:0-100` instead of
`id`/`submitted`/`stage`. Countdowns, the "days in review" counters, the stat
strip and the deadline timeline all recompute in the browser — no need to touch
any dates other than the ones you enter.

Common edits:

- **Paper accepted** → change `status` to `"review"`, `stage:2`,
  `badge:"Accepted"` (or move it into a new section).
- **Started a draft** → bump `progress`.
- **Backlog item picked up** → change `status` to `"writing"` and add a `deadline`.

## Publishing to GitHub Pages

```bash
cd phd-progress
git init -b main
git add .
git commit -m "Research progress board"
gh repo create <repo-name> --public --source=. --push
```

Then in the repo: **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.
The site is live at `https://rakesh2109.github.io/PhD_Progress/` in about a minute.

To push later updates:

```bash
git add index.html && git commit -m "Update status" && git push
```
