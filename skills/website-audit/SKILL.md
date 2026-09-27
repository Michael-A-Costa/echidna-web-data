---
name: website-audit
description: Audit a website for SEO problems, broken links and redirects, and the technologies it runs on, then report prioritized fixes. Use when the user asks to audit, review, or health-check a site, find broken links, check SEO, or find out what a site is built with.
---

# Website audit

Combine three tools from the `echidna-web-data` connector, then write one prioritized report.

1. **SEO**: `humble-echidna/seo-audit` with `startUrls: ["<site>"]`. Keep `maxPages` small at first (the default is 10; 25–50 covers most small sites). It returns a 0–100 score per page and for the site, plus the issues behind each score. It also checks links and images unless `checkLinks` / `checkImages` are false.
2. **Tech stack**: `humble-echidna/tech-stack-detector` with `urls: ["<site>"]`. It returns technologies grouped by category (CMS, analytics, CDN, frameworks, payment, and so on), with versions where the page shows them.
3. **Redirects and status codes** (only when the user cares about URL hygiene or a migration): `humble-echidna/url-checker` with `mode: "sitemap"` and `urls: ["<site>"]`. This checks every URL in the sitemap for its status code, redirect chain and canonical URL.

## Report

- Start with the site score and the three to five fixes that would move it most. Group by issue, not by page ("12 pages have no meta description"), and name example URLs.
- Then list broken links (the page they are on, the target, the status).
- Then the tech stack in one short table.
- Say what was not checked (for example, pages past `maxPages`).

## Cost

Each tool runs on the user's own Apify account and charges per result: SEO audit $10 per 1,000 pages, tech stack $2 per 1,000 sites, URL checks $1 per 1,000 URLs. A 25-page audit costs about $0.25. Tell the user before running an audit larger than 200 pages.

If a run is still going when the tool returns, fetch the results later with `get-actor-run` and `get-dataset-items`.
