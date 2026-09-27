---
name: site-to-markdown
description: Convert web pages, whole documentation sites, PDFs, Word documents and spreadsheets into clean Markdown or text, optionally chunked for RAG. Use when the user wants to read, ingest, summarize, or build a knowledge base from web pages or documents at a URL.
---

# Pages and documents to Markdown

## Web pages: `humble-echidna/page-to-markdown`

- One or a few pages: `urls: [...]`.
- A whole site or docs section: `urls: ["<start url>"]`, `crawlWholeSite: true`, and a `maxPagesPerSite` that fits the request (the default is 100). Narrow it with `includeUrlPatterns` / `excludeUrlPatterns` (for example `["/docs/"]`).
- For RAG, set `chunkMarkdown: true` and `maxChunkChars` (the default is 2000). Each chunk keeps its page URL and heading path.
- The output is the main content only: navigation, cookie banners and footers are removed.

## Documents: `humble-echidna/document-to-text`

- `urls: [...]` pointing at PDF, DOCX, XLSX, PPTX and similar files.
- Scanned PDFs are read with OCR (`ocr: true` is the default; set `languages` for non-English text).
- `extractTables: true` returns PDF tables as structured rows.
- `pages: "1-5"` reads only part of a long PDF.

## Finding the URLs first

If the user names a site but not its pages, list them with `humble-echidna/sitemap-urls` (`sites: ["example.com"]`, optional `includeUrlPatterns`) and pick the relevant ones before converting.

## Cost

Charged per result on the user's own Apify account: pages $1 per 1,000, documents $5 per 1,000, sitemap URLs $0.30 per 1,000. Confirm before crawling more than 500 pages.
