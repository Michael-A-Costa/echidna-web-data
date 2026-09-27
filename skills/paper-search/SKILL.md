---
name: paper-search
description: Search scholarly papers and preprints in OpenAlex (including arXiv) and Crossref by keywords, author, date range and open access, look up works by DOI or arXiv ID, and set up alerts for new papers. Use when the user asks for research papers, a literature search, citations, the most-cited work on a topic, or recent publications by an author.
---

# Research paper search

Use `humble-echidna/academic-papers`.

- `queries`: one per line. Keywords run a search; a DOI (`10.1038/nmat1849`) or an arXiv ID (`2010.11929`) looks up that one work.
- `sort`: `relevance` (default), `newest`, or `mostCited`.
- `maxResultsPerQuery` (default 20) and `maxResults` for the total.
- Filters: `author`, `publishedFrom` / `publishedTo` (a year, `2020-06`, or a date), `openAccessOnly`, `searchIn: "title"` for stricter matches.
- `sources`: `["openalex", "crossref"]` by default; works found in both are merged.
- `onlyNew: true` with `sort: "newest"` for a repeat search that returns only works not seen before (a paper alert).
- Without the user's own `openalexApiKey`, OpenAlex allows a small free daily budget (about 100 searches); a large literature sweep may need the user's free key.

Report each work with its title, authors, year, venue, citation count, DOI link, and an open-access link when there is one. Do not describe a paper's findings from the title alone; read the abstract when it is returned, or offer to fetch the open-access PDF with `document-to-text`.

`academic-papers` is new; if it is missing from the connector's tool list, it is not published yet: say so.

## Cost

$1 per 1,000 works returned, on the user's own Apify account.
