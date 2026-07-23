---
date: 2026-07-23
type: spec
tags:
  - KnowledgeNote
---
# Spec: LinkedIn Fresh Jobs Link Generator

## What it is
A single-file HTML tool that generates LinkedIn job search URLs filtered by post age, sorted newest-first. Deployed as a static site on Vercel via a git repo, so it's reachable from any device (including mobile) at a live URL.

## Why
LinkedIn's default search sorts by relevance, not recency. Adding `f_TPR` (age in seconds) and `sortBy=DD` params surfaces jobs before they get flooded with applicants. Building that URL by hand every time is tedious.

## Inputs (form fields)
- **Keywords** — text input (e.g. "product designer")
- **Location** — text input, optional
- **Time window** — dropdown with presets:
  - 15 min → `r900`
  - 1 hour → `r3600`
  - 24 hours → `r86400`
  - Custom → number input (minutes), converted to seconds
- **Saved searches** — optional: a small set of preset keyword buttons/chips the user can click to auto-fill (e.g. their 3-4 most common searches)

## Output
- Generated URL displayed in a readonly text field
- "Copy" button (clipboard)
- "Open" button (opens URL in new tab)

## URL format
```
https://www.linkedin.com/jobs/search/?keywords={urlencoded_keywords}&location={urlencoded_location}&f_TPR=r{seconds}&sortBy=DD
```
Omit `location` param entirely if left blank.

## Constraints
- Single HTML file, inline CSS/JS, no dependencies, no build step
- No API calls, no scraping, no auth — pure client-side string building
- Works offline (it's just URL construction)
- Should also work fine opened locally (double-click) if git/Vercel isn't set up yet

## Deployment
- Init a git repo (`git init`), commit the HTML file (+ optional `vercel.json` if needed for static routing)
- Create the GitHub repo using the GitHub CLI (`gh repo create`, requires `gh auth login` if not already authenticated), push to it
- Connect the repo to Vercel (import project in Vercel dashboard, or `vercel` CLI) so it auto-deploys on every push to main
- No environment variables or backend needed, it's a static site
- Resulting Vercel URL works on mobile browsers same as desktop

## Nice-to-haves (skip if out of scope)
- Remember last-used keyword/location/window in localStorage
- Keyboard shortcut (Enter) to generate + open
- Mobile-friendly/responsive layout (important since this will be used on phone)
- `manifest.json` + meta tags so it can be "Added to Home Screen" on mobile for app-like access
