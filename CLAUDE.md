# linkedin-fresh-jobs

A single-file HTML tool that builds LinkedIn job search URLs filtered by post age (15 min / 1 hour / 24 hours / custom) and sorted newest-first, so you see postings before they're flooded with applicants.

Check docs/WORKLOG.md for the current task list and recent session notes before starting work.

## What this is
Plain HTML/CSS/JS, no framework, no build step, no dependencies. Deployed as a static site on Vercel (linkedin-fresh-jobs.vercel.app) so it's reachable from any device including mobile, installable to iOS home screen. v1.1 built and shipped: live URL preview, time-window and workplace-type filters, saved-search chips with cross-device share link, dark/light theme.

## Key decisions
- [2026-07-23] Time-window and workplace chips stay same size when selected; selection is shown by color fill only, not font weight, to avoid layout shift.
- [2026-07-23] Saved searches live in localStorage per-device (no backend sync); a "Share chips" button generates a URL carrying the chip data for manual cross-device import.
- [2026-07-23] Single static HTML file, no Tailwind/Next.js/build tooling, per spec constraints — keeps it dependency-free and easy to open locally or deploy as-is.
- [2026-07-23] Visually matches the separate `fresh-jobs` GUI project (chartreuse/citron OKLCH palette, Geist font, flat/rounded style) via hand-copied CSS values in `BRANDING.md`, but shares no code with it — this stays a standalone project.
