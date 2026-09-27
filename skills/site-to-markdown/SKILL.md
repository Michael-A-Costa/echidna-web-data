---
name: site-to-markdown
description: Convert web pages, whole documentation sites, blog and news articles, PDFs, Word documents, spreadsheets and images of text into clean Markdown or text, optionally chunked for RAG. Use when the user wants to read, ingest, summarize, or build a knowledge base from web pages, articles, or documents at a URL, or pull the latest posts from a blog.
---

# Pages and documents to Markdown

## Web pages: `humble-echidna/page-to-markdown`

- One or a few pages: `urls: [...]`.
- A whole site or docs section: `urls: ["<start url>"]`, `crawlWholeSite: true`, and a `maxPagesPerSite` that fits the request (the default is 100). Narrow it with `includeUrlPatterns` / `excludeUrlPatterns` (for example `["/docs/"]`).
- For RAG, set `chunkMarkdown: true` and `maxChunkChars` (the default is 2000). Each chunk keeps its page URL and heading path.
- The output is the main content only: navigation, cookie banners and footers are removed.

## Documents: `humble-echidna/document-to-text`

- `urls: [...]` pointing at PDF, Word (.docx) or Excel (.xlsx) files, or images of text.
- Scanned PDFs are read with OCR (`ocr: true` is the default; set `languages` for non-English text).
- `extractTables: true` returns PDF tables as structured rows.
- `pages: "1-5"` reads only part of a long PDF.

## Blog and news articles: `humble-echidna/article-extractor`

Use it when the user wants articles (title, author, date, body) rather than whole pages, or "the latest posts" from a blog without knowing their URLs.

- `sites: ["https://blog.example.com/"]`: finds the site's feed or sitemap and extracts the newest `maxArticlesPerSite` (default 3). `urlPatterns` (for example `["/blog/"]`) keeps only matching articles.
- `articleUrls: [...]` extracts specific article pages. Set `sites: []` when you only pass `articleUrls`, or the default site is added.
- `onlyNewArticles: true` on repeat runs returns only articles not returned before.

`article-extractor` is new; if it is missing from the connector's tool list, it is not published yet: use `page-to-markdown` on the article URLs instead.

## Text in images

For screenshots, scanned images or photos of documents (PNG, JPEG, WebP, TIFF), use `humble-echidna/image-ocr`; the `images-and-ocr` skill covers it.

## Finding the URLs first

If the user names a site but not its pages, list them with `humble-echidna/sitemap-urls` (`sites: ["example.com"]`, optional `includeUrlPatterns`) and pick the relevant ones before converting.

## Cost

Charged per result on the user's own Apify account: pages $1 per 1,000, articles $1 per 1,000, documents $5 per 1,000 (plus $10 per 1,000 scanned pages read with OCR and $0.30 per 1,000 pages with extracted tables), sitemap URLs $0.30 per 1,000. Confirm before crawling more than 500 pages.
