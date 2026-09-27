# Echidna Web Data

A Claude plugin for everyday web-data jobs:

- Audit a website's SEO, broken links and tech stack.
- Enrich a list of businesses, such as a Google Maps export, with which websites are dead, what each site is built with, and an SEO score.
- Turn web pages, whole documentation sites, blog articles, PDFs and Word or Excel files into clean Markdown for reading or RAG.
- Research which companies are hiring and for what, straight from their career pages, and turn it into hiring signals: new roles for a skill, hiring surges, and website stack changes.
- Search EU and UK public tenders, French and global company registers, and research papers.
- Transcribe audio and video, download the images from a page, and read the text in images.
- Watch any of these for changes.

## How it works

The plugin adds one connector, **echidna-web-data**. It is Apify's hosted MCP server (`https://mcp.apify.com`), limited to eighteen Apify Actors published by [humble-echidna](https://apify.com/humble-echidna). It also includes four helpers for long runs: `get-actor-run`, `get-dataset-items` and `get-key-value-store-record` read a run's status and results, and `abort-actor-run` stops a run. The plugin also adds ten skills that tell Claude when and how to use each tool.

| Skill | Tools |
|---|---|
| website-audit | seo-audit, tech-stack-detector, url-checker |
| leads-enrichment | url-checker, tech-stack-detector, seo-audit, dataset-transform |
| site-to-markdown | page-to-markdown, document-to-text, article-extractor, sitemap-urls |
| hiring-research | ats-jobs, hiring-signals, remote-jobs |
| tender-search | eu-ted-tenders |
| company-lookup | company-registers |
| paper-search | academic-papers |
| transcribe-media | audio-transcriber |
| images-and-ocr | bulk-image-downloader, image-ocr |
| watch-for-changes | the tools above that have an "only new" or "changes since last run" option, and rss-feed-reader |

Newly published Actors appear in the connector as soon as they are live in the Apify Store. Until then, the skills tell Claude to say that the tool isn't available yet.

## Setup

1. Install the plugin.
2. The first time Claude uses a tool, you sign in to **your own Apify account** (free to create) through Apify's OAuth page.
3. Ask for what you need. For example, "audit example.com and tell me the top fixes", "which of these 20 companies started hiring Rust engineers this month?", or "check the websites in my Google Maps dataset and find the businesses with dead or weak sites".

## Pricing

The plugin is free. Each Actor charges per result on your Apify account, and Apify's free plan includes monthly credit. Prices at 2026-09-27, per 1,000 results:

| Actor | Price |
|---|---|
| seo-audit | $10 per 1,000 pages ($1 per 1,000 unchanged pages in "changes" mode) |
| tech-stack-detector | $2 per 1,000 sites ($0.40 per 1,000 unchanged sites) |
| url-checker, page-to-markdown, article-extractor, rss-feed-reader, academic-papers, dataset-transform | $1 per 1,000 (URLs, pages, articles, feed items, papers, rows) |
| document-to-text | $5 per 1,000 documents, plus $10 per 1,000 OCR pages and $0.30 per 1,000 table pages |
| sitemap-urls | $0.30 per 1,000 URLs |
| ats-jobs | $1.50 per 1,000 jobs |
| remote-jobs | $2 per 1,000 jobs |
| hiring-signals | $20 per 1,000 companies with a signal (quiet companies are free) |
| eu-ted-tenders | $2 per 1,000 notices |
| company-registers | $3 per 1,000 companies |
| audio-transcriber | $6 per 1,000 audio minutes (base model), $15 per 1,000 (small model) |
| bulk-image-downloader | $7 per 1,000 page or image URLs |
| image-ocr | $4 per 1,000 images |

Each run also costs $0.00005 to start. Current prices are on each Actor's page at https://apify.com/humble-echidna. The skills tell Claude to confirm with you before large or costly runs.

## Privacy and data handling

- The plugin contains no code that runs on your computer. It only declares the remote connector and the skills.
- When Claude calls a tool, the tool input goes to Apify's MCP server and runs on your Apify account. The input can be URLs, company names, search terms, or the ID of one of your Apify datasets. Results are stored in your Apify account's storage under Apify's data retention rules and are returned to Claude.
- The Actors fetch only public web pages, files, feeds and public APIs. They respect robots.txt and do not log in to any site. Reading one of your datasets uses your own account's access, read-only.
- The plugin's author does not receive your inputs, results, or Apify credentials. As the Actors' developer, the author can see aggregate usage statistics that Apify provides to all developers.
- The author keeps no data from your use of the plugin, so there is nothing to retain or delete on our side. Apify's retention rules apply to your Apify storage.
- Apify's privacy policy: https://apify.com/privacy-policy.
- Full privacy policy for this plugin: [PRIVACY.md](PRIVACY.md).

## Support

Open an issue on the Actor's page in the Apify Store (the **Issues** tab at https://apify.com/humble-echidna), or an issue in this repository.

## License

MIT
