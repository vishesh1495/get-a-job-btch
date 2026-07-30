# Daily Qualified Jobs Tracker

A single self-contained `index.html` — no build step, no dependencies. Job data lives inline as JSON in the page; status marks (Interested/Applied/Ignored) are saved in the visitor's browser via `localStorage`.

## Host it on GitHub Pages

1. Create a repo (e.g. `job-tracker`) and push `index.html` to the root (or to a `/docs` folder — either works).
2. In the repo, go to **Settings → Pages**.
3. Under **Source**, choose the branch (`main`) and folder (`/` or `/docs`), then **Save**.
4. GitHub gives you a URL like `https://<your-username>.github.io/job-tracker/` within a minute or two.

## Updating the job list

Open `index.html`, find the `<script id="jobs-db" type="application/json">` block near the bottom, and edit the JSON array directly — add a new object for each new posting:

```json
{
  "id": "company-title-location",
  "roleFamily": "Product Manager",
  "title": "Senior Product Manager",
  "company": "Example Corp",
  "location": "Paris, France",
  "score": "High",
  "scoreRank": 1,
  "dateConfidence": "confirmed",
  "sourceUrl": "https://...",
  "rationale": "One sentence on why this is a good fit.",
  "firstSeen": "2026-08-01",
  "lastSeenRun": "2026-08-01"
}
```

- `score` is one of `High`, `Medium-High`, `Medium`, `Low-Medium`, `Low`.
- `scoreRank` controls sort order: High=1, Medium-High=2, Medium=3, Low-Medium=4, Low=5.
- `dateConfidence` is `confirmed` or `unverified`.
- Also update the `<script id="run-meta">` block (`runDate`, `newTodayCount`, `searchesRun`, `confirmedTodayCount`, `note`) so the run-info bar at the top reflects the latest update.

Commit and push — GitHub Pages redeploys automatically within a minute or two.

## Later (not built yet)

If you want this to update itself daily instead of by hand, the natural next step is a GitHub Actions workflow (scheduled on a cron trigger) that runs a script to search for new postings and commit the updated JSON automatically. Say the word when you want that built.
