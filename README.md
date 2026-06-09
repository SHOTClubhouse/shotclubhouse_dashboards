# shotclubhouse_dashboards

SHOT Clubhouse internal dashboards, research, ADRs &amp; guides — served as **plain static HTML** via GitHub Pages. **No build step.** No Jekyll, no MkDocs, no Docusaurus.

**Live site:** https://shotclubhouse.github.io/shotclubhouse_dashboards/

## How it works

- Every page is a self-contained `.html` file. Drop it into a section folder, add a link to that section's `index.html`, push. That's the whole workflow.
- A `.nojekyll` file at the repo root tells GitHub Pages to serve the HTML and asset folders **verbatim** (no Jekyll processing).
- Shared styling lives in `/assets/style.css` (dark SHOT theme — teal `#1ABC9C`, purple `#6B00DB`, gold `#F7B613`). Link it with a relative path. Brand rule: red `#EF4444` is for **error states only**, never decorative.

## Structure

```
/index.html                                  landing page → links the 4 sections
/.nojekyll                                   serve folders verbatim (no Jekyll)
/assets/style.css                            shared dark SHOT theme
/dashboards/index.html                       lists dashboards
/dashboards/perform-verify/index.html        Perform Verify run archive (table of runs)
/dashboards/perform-verify/runs/<date>/index.html   one self-contained run snapshot
/research/index.html                         research notes & deep-dives (placeholder)
/adrs/index.html                             architecture decision records (placeholder)
/guides/index.html                           how-to guides & runbooks (placeholder)
```

## Adding a new HTML page

1. Author a self-contained `.html` file (inline any data — don't rely on a runtime fetch of a file that won't exist on Pages).
2. Save it into the matching section folder (e.g. `research/my-deep-dive.html`).
3. Link `../assets/style.css` (adjust the relative depth) for consistent styling.
4. Add a link/card to that section's `index.html`.
5. Commit and push to `main` — Pages redeploys automatically (~1 min).

> The `/explain-to-me` skill output drops straight in: save the generated HTML into a section folder and add a link. No conversion needed.

## Adding a new Perform Verify run snapshot

1. Create `dashboards/perform-verify/runs/<YYYY-MM-DD>/index.html`.
2. Make it self-contained — inline the per-area / per-feature results (e.g. from that run's `state.json`) directly into the HTML.
3. Add a row to `dashboards/perform-verify/index.html` linking to the new snapshot (date, environment, branch, result, green count).

## GitHub Pages

Pages is served from the **repo root** on the **`main` branch**. Pushing to `main` redeploys. No GitHub Actions workflow and no build are involved.
