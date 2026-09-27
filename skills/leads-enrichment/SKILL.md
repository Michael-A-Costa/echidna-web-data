---
name: leads-enrichment
description: Enrich a list of businesses with website data - which sites are dead or broken, what each site is built with (CMS, analytics, ads, e-commerce), and an SEO score with its top problems - from a Google Maps scraper dataset, a CSV, or a plain list of websites. Use for lead qualification, agency prospecting (find businesses with bad or outdated websites), or cleaning a lead list before outreach.
---

# Enrich business leads with website data

The goal is one table, one row per business: name, website, whether the site works, its main technologies, and an SEO score with the two or three problems a salesperson could mention.

## 1. Get the list of websites

- **A plain list** of websites or domains from the user: use it as is.
- **A Google Maps scraper dataset** (or any Apify dataset of businesses) on the user's account: the websites are usually in a `website` field.
  - Small dataset (up to a few hundred items): read it with `get-dataset-items`, keep the business name, website, phone and address, and drop items without a website.
  - Large or messy dataset: clean it first with `humble-echidna/dataset-transform`: `datasetId: "<id>"`, `filters: ["website is not empty"]`, `dedupeBy: ["website"]`, `fields: ["title", "website", "phone", "address"]`. The cleaned rows are the new run's dataset.
- **A CSV or JSON file at a URL**: `humble-echidna/dataset-transform` with `fileUrl` does the same cleaning.

`dataset-transform` is new; if it is missing from the connector's tool list, it is not published yet: use `get-dataset-items` and do the cleaning yourself.

Businesses with no website are a result too: list them separately ("no website: 14 businesses"), because for an agency they are leads.

Tell the user how many websites will be checked and the estimated cost (below) before running step 2 on more than 200 sites.

## 2. Check the websites

Run these on the same list. They are independent, so run them in parallel.

1. **Dead or broken sites**: `humble-echidna/url-checker`, `mode: "urls"`, `urls: [<websites>]`. `outcome` says what happened: `ok`, `broken` (4xx/5xx), `dns-error` (domain doesn't resolve), `error` (timeout, TLS), `refused` (the site blocks automated checks; not the same as dead). `finalUrl` shows where a redirect ended, which catches domains parked or moved to another business.
2. **Tech stack**: `humble-echidna/tech-stack-detector`, `urls: [<websites>]`. Report the CMS or site builder (WordPress, Wix, Shopify, Squarespace...), analytics, ad pixels, booking or e-commerce tools, and anything visibly outdated.
3. **SEO score**: `humble-echidna/seo-audit`, `startUrls: [<websites>]`, `maxDepth: 0` (home page only), `maxPages` equal to the number of websites, `checkExternalLinks: false`. Link checks share one budget per run (`maxLinkChecks`, default 500), so for more than about 50 sites either raise it or set `checkLinks: false` and `checkImages: false` for a faster, score-only pass. Each result has a 0-100 `score` and its `issues` (missing title or meta description, no H1, images without alt text, broken links, slow response).

Skip step 1 for sites that steps 2 and 3 already reached, if the user wants to save a little.

**Dataset input, when available.** Newer versions of `url-checker`, `tech-stack-detector` and `seo-audit` accept `datasetId` (plus an optional `datasetUrlField`, found automatically when empty) instead of a URL list, and copy each business's name into their results (`sourceTitle`). If the tool's input schema has `datasetId`, pass the Google Maps dataset directly and skip step 1's extraction. If it does not, use the URL list; everything else works the same.

## 3. Join and report

Join the three results on the website's domain. Then:

- A table: business, website, status (working / dead / broken / redirects elsewhere / no website), CMS or builder, key tools, SEO score, top issues.
- Sort by what the user is looking for. For an agency pitch, put dead sites, builder sites with low scores, and sites with no analytics first.
- Summarize: how many work, how many are dead, the most common platforms, the average score, and the most common SEO problems.
- Offer the table as CSV. If the user wants a file, `dataset-transform` with `exportFormat: "csv"` saves one in the run's key-value store (read it with `get-key-value-store-record`).

## Cost

Charged per result on the user's own Apify account: URL checks $1 per 1,000, tech stack $2 per 1,000 sites, SEO audit $10 per 1,000 pages, dataset cleaning $1 per 1,000 rows. All three checks together come to about $0.013 per business, or $13 per 1,000 businesses. SEO is the largest part; drop it if the user only needs status and stack ($3 per 1,000).
