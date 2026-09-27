---
name: images-and-ocr
description: Download every image from web pages or a list of image links (skipping icons and tracking pixels, optionally as a ZIP), and read the text in images and scanned pages with OCR, with word positions when needed. Use when the user wants to save, collect or archive images from a site, or extract text from screenshots, scans, receipts, labels or photos of documents at a URL.
---

# Download images and read text in images

## Download images: `humble-echidna/bulk-image-downloader`

- `urls`: web pages (every image on the page is taken, at the largest size in `srcset`, plus the page's preview image) or direct image links.
- Skip small images with `minWidth` / `minHeight` (default 100 px) and `minFileSizeKb` (default 1). Skipped images are not charged.
- `maxImagesPerPage` and `maxResults` keep a run small.
- `createZip: true` also packs everything into `images-001.zip`, `images-002.zip`, ... in the run's key-value store.

Each result lists the image's source page, URL, size and where it was saved. Give the user the image links and, for a ZIP, the key-value store record (read it with `get-key-value-store-record`, or point the user to the run's storage in Apify Console). Remind the user that images belong to their owners; downloading them does not grant a right to reuse them.

## Read text in images: `humble-echidna/image-ocr`

- `urls`: direct links to PNG, JPEG, WebP, TIFF, GIF or BMP files, or one-page PDF scans. For multi-page PDFs and Office files use `document-to-text` (the `site-to-markdown` skill).
- `languages`: Tesseract codes, up to 4, for example `["eng", "deu"]` (default English).
- `pageSegmentation`: `auto` for pages and documents, `singleBlock` for a receipt or paragraph, `singleLine` for one line, `sparse` for scattered labels, `autoWithOrientation` for sideways text.
- `includeLines` / `includeWords: true` add bounding boxes and confidence for each line or word.

Quote the text, and flag low-confidence parts instead of guessing.

`image-ocr` is new; if it is missing from the connector's tool list, it is not published yet: for scans, `document-to-text` with `ocr: true` also reads image files.

## Combined

To read the text in every image on a page, run `bulk-image-downloader` first, then pass the saved image URLs to `image-ocr`.

## Cost

Charged on the user's own Apify account: image downloads $7 per 1,000 page or image URLs given; OCR $4 per 1,000 images.
