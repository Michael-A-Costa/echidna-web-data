# Echidna Web Data

A Claude plugin for everyday web-data jobs: audit a website's SEO, broken links and tech stack; turn web pages, whole documentation sites, PDFs and Office documents into clean Markdown for reading or RAG; research which companies are hiring and for what, straight from their career pages; search EU and UK public tenders; look up companies in the French and global LEI registers; transcribe audio and video; and watch any of these for changes.

## How it works

The plugin adds one connector, **echidna-web-data**, which is the Apify MCP server (`https://mcp.apify.com`) limited to eleven Apify Actors published by [humble-echidna](https://apify.com/humble-echidna), plus two read-only helpers for fetching the results of long runs. It also adds seven skills that tell Claude when and how to use each tool.

| Skill | Tools |
|---|---|
| website-audit | seo-audit, tech-stack-detector, url-checker |
| site-to-markdown | page-to-markdown, document-to-text, sitemap-urls |
| hiring-research | ats-jobs |
| tender-search | eu-ted-tenders |
| company-lookup | company-registers |
| transcribe-media | audio-transcriber |
| watch-for-changes | all of the above, in "only changes" mode |

## Setup

1. Install the plugin.
2. The first time Claude uses a tool, you sign in to **your own Apify account** (free to create) through Apify's OAuth page.
3. Ask for what you need, for example "audit example.com and tell me the top fixes" or "which of these 20 companies are hiring Rust engineers?"

## Pricing

The plugin is free. Each Actor charges per result on your Apify account, and Apify's free plan includes monthly credit. Prices at release: SEO audit $10 per 1,000 pages; tech stack $2 per 1,000 sites; URL checks, pages to Markdown, RSS items $1 per 1,000; documents $5 per 1,000; sitemap URLs $0.30 per 1,000; jobs $1.50 per 1,000; tenders $2 per 1,000; companies $3 per 1,000; transcription $6 per 1,000 audio minutes (base model). Each run also costs $0.00005 to start. Current prices are on each Actor's page at https://apify.com/humble-echidna.

## Privacy and data handling

- The plugin contains no code that runs on your computer. It only declares the remote connector and the skills.
- When Claude calls a tool, the tool input (URLs, company names, search terms) goes to Apify's MCP server and runs on your Apify account. Results are stored in your Apify account's storage under Apify's data retention rules and are returned to Claude.
- The Actors fetch only public web pages and public APIs, respect robots.txt, and do not log in to any site.
- The plugin's author does not receive your inputs, results, or Apify credentials. As the Actors' developer, the author can see aggregate usage statistics that Apify provides to all developers.
- The author keeps no data from your use of the plugin, so there is nothing to retain or delete on our side. Apify's retention rules apply to your Apify storage.
- Apify's privacy policy: https://apify.com/privacy-policy.

## Support

Open an issue on the Actor's page in the Apify Store (the **Issues** tab at https://apify.com/humble-echidna), or an issue in this repository.

## License

MIT
