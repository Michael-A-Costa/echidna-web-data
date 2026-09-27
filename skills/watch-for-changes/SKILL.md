---
name: watch-for-changes
description: Set up repeatable checks that report only what changed since the last run - new jobs at companies, hiring signals and surges, new pages in a sitemap, tech stack changes, new or broken URLs, new RSS items and blog articles, new tenders, new research papers. Use when the user wants to monitor, track, or get alerts about changes to websites, feeds, or hiring.
---

# Watch for changes

Several tools remember the previous run with the same input and can return only the difference. Run the same input again later (or on an Apify schedule) to get just the changes.

| To watch | Tool | Setting |
|---|---|---|
| New jobs at companies | `humble-echidna/ats-jobs` | `onlyNewJobs: true` (`includeClosedAndChanged: true` also reports closed and edited jobs) |
| Hiring signals: new matching roles, hiring surges, website stack changes | `humble-echidna/hiring-signals` | `sinceLastRun: true` with `signalKeywords` (see the `hiring-research` skill) |
| New remote jobs | `humble-echidna/remote-jobs` | `onlyNewJobs: true` |
| New or removed pages on a site | `humble-echidna/sitemap-urls` | `onlyNewAndRemovedUrls: true` |
| Tech stack changes | `humble-echidna/tech-stack-detector` | `onlyStackChanges: true` |
| Changed pages as Markdown | `humble-echidna/page-to-markdown` | `onlyChangedPages: true` |
| URLs whose status or redirect changed | `humble-echidna/url-checker` | `onlyChanged: true` |
| SEO regressions | `humble-echidna/seo-audit` | `compareWithPreviousAudit: true` |
| New blog or news posts | `humble-echidna/rss-feed-reader` | `feeds: [...]`, `onlyNewItems: true`, optional `keywords` |
| New articles with their full text | `humble-echidna/article-extractor` | `sites: [...]`, `onlyNewArticles: true` |
| New tenders | `humble-echidna/eu-ted-tenders` | `onlyNew: true` |
| New research papers | `humble-echidna/academic-papers` | `onlyNew: true`, `sort: "newest"` |

`hiring-signals`, `remote-jobs`, `article-extractor` and `academic-papers` are new; one that is missing from the connector's tool list is not published yet.

The first run returns everything and sets the baseline; tell the user so. Keep the input identical between runs, because the remembered state is tied to it.

For a recurring watch, suggest an Apify schedule on the user's account (Apify Console → Schedules) so the check runs without Claude, and the user can come back and ask for a summary of the latest results.

Each tool charges per result on the user's own Apify account; "only changes" runs are cheap because unchanged items are not returned (the tech stack and SEO tools charge a small fee for unchanged sites and pages: $0.40 and $1 per 1,000). A hiring-signals monitor charges only for companies with a new signal, $20 per 1,000.
