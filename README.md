# linkedin-fresh-jobs

## What this is
A single HTML page that builds a LinkedIn job search link filtered to show only recent postings (15 min, 1 hour, 24 hours, or a custom window), sorted newest-first. LinkedIn's default search sorts by relevance, so fresh postings get buried under ones with 50-100+ applicants already; this tool builds the URL that fixes that.

## How to run it
No install needed. Open `index.html` directly in a browser (double-click it), or once deployed, visit the live Vercel URL. There's no server, no build step, and no dependencies.

## How to test or preview
Open `index.html` in a browser and try generating a link with different keywords and time windows. Confirm the "Copy" and "Open" buttons work and the generated URL matches the format in `fresh-jobs-link-generator-spec.md`.

## Key configuration
None. No environment variables, no API keys, no backend. Everything happens client-side by building a URL string.

## Project structure
- `index.html` — the tool itself (all HTML/CSS/JS in one file)
- `manifest.json` + `icon.svg` — lets the page install like an app from a phone browser ("Add to Home Screen")
- `fresh-jobs-link-generator-spec.md` — full spec (inputs, URL format, deployment plan)
- `BRANDING.md` — colors/fonts/style to match the related `fresh-jobs` GUI project
- `how-to-find-guide.md` — background on why the `f_TPR` URL parameter works
- `docs/WORKLOG.md` — current task list and session notes
