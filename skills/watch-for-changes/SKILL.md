---
name: watch-for-changes
description: Set up repeatable checks that report only what changed since the last run - new jobs at companies, new pages in a sitemap, tech stack changes, new or broken URLs, new RSS items, new tenders. Use when the user wants to monitor, track, or get alerts about changes to websites, feeds, or hiring.
---

# Watch for changes

Several tools remember the previous run with the same input and can return only the difference. Run the same input again later (or on an Apify schedule) to get just the changes.

| To watch | Tool | Setting |
|---|---|---|
| New jobs at companies | `humble-echidna/ats-jobs` | `onlyNewJobs: true` (`includeClosedAndChanged: true` also reports closed and edited jobs) |
| New or removed pages on a site | `humble-echidna/sitemap-urls` | `onlyNewAndRemovedUrls: true` |
| Tech stack changes | `humble-echidna/tech-stack-detector` | `onlyStackChanges: true` |
| Changed pages as Markdown | `humble-echidna/page-to-markdown` | `onlyChangedPages: true` |
| URLs whose status or redirect changed | `humble-echidna/url-checker` | `onlyChanged: true` |
| SEO regressions | `humble-echidna/seo-audit` | `compareWithPreviousAudit: true` |
| New blog or news posts | `humble-echidna/rss-feed-reader` | `feeds: [...]`, `onlyNewItems: true`, optional `keywords` |
| New tenders | `humble-echidna/eu-ted-tenders` | `onlyNew: true` |

The first run returns everything and sets the baseline; tell the user so. Keep the input identical between runs, because the remembered state is tied to it.

For a recurring watch, suggest an Apify schedule on the user's account (Apify Console → Schedules) so the check runs without Claude, and the user can come back and ask for a summary of the latest results.

Each tool charges per result on the user's own Apify account; "only changes" runs are cheap because unchanged items are not returned (the tech stack and SEO tools charge a small fee for unchanged sites and pages).
