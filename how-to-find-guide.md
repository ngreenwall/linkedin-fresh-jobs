---
date: 2026-07-22
type: reference
source:
tags:
  - KnowledgeNote
---
# Finding Fresh LinkedIn Jobs (Before the Applicant Flood)

## The Problem

LinkedIn's default job search sorts by "relevance," not recency, so by the time you see a posting it may already have 50-100+ applicants.

## The Fix: URL Parameters

LinkedIn job search URLs accept a `f_TPR` parameter that filters by post age, in seconds.

|Window|Parameter|Best for|
|---|---|---|
|15 min|`f_TPR=r900`|Tightest filter, catches jobs right as they post|
|1 hour|`f_TPR=r3600`|Good balance of freshness and result count|
|24 hours|`f_TPR=r86400`|Wider net, more results, more competition|

Custom windows work too, just do minutes × 60 for the seconds value.

Also add `sortBy=DD` so results sort by date posted (newest first) instead of relevance.

## Example URL

```
https://www.linkedin.com/jobs/search/?keywords=product%20designer&f_TPR=r900&sortBy=DD
```

Swap `product%20designer` for any keyword (spaces become `%20`).

## Recommended Workflow

1. Bookmark the 1-hour version (`r3600`) as your daily driver.
2. Check it every 1-2 hours during business hours, that's when most postings go live.
3. Drop to `r900` (15 min) during peak posting windows if you want to be first in.

## Tradeoffs

- **Narrower window (15 min-1hr):** fewer applicants ahead of you, but fewer total results, needs frequent checking.
- **Wider window (24hr):** more results to browse, but competition builds fast, often already 50+ applicants by the time you see it.

## Notes

- This only affects the job search URL, not the LinkedIn app (app doesn't expose this filter).
- LinkedIn may still show a few weeks-old "reposted" jobs mixed in, that's a LinkedIn quirk, not a filter failure.