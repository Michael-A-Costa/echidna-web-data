---
name: tender-search
description: Search public procurement notices from the EU's TED and the UK's Find a Tender service by keyword, CPV code, country, buyer, and dates. Use when the user asks about government tenders, public contracts, RFPs in Europe or the UK, or bid opportunities.
---

# EU and UK public tenders

Use `humble-echidna/eu-ted-tenders`.

## Input

- `sources`: `["ted"]` for the EU, `["uk"]` for Find a Tender, or both.
- `queries`: keywords, for example `["cybersecurity", "cloud hosting"]`. Each query is a separate search.
- `cpvCodes`: CPV codes when the user names a category (for example `"72000000"` for IT services).
- `countries`: buyer countries as two- or three-letter codes (`DE`, `FRA`), `buyerName`, `publishedFrom` / `publishedTo` (YYYY-MM-DD).
- `noticeTypes`: `["competition"]` (the default) for open calls; add `"award"` when the user asks who won (also `"prior"`, `"modification"`).
- `openOnly: true` keeps only tenders still accepting bids.
- `maxResultsPerQuery` (default 20).

## Report

List each notice with the buyer, title, country, estimated value if stated, deadline, and the notice URL. Sort open tenders by deadline. Point out any that close within 14 days.

## Cost

$2 per 1,000 notices returned, on the user's own Apify account.
