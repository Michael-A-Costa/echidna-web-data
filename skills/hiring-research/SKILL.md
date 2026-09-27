---
name: hiring-research
description: Find and analyze open jobs at specific companies straight from their career pages (Greenhouse, Lever, Ashby, Recruitee, Personio and Teamtailor). Use when the user asks who is hiring, what roles a company has open, hiring trends, salary ranges in postings, or wants job leads.
---

# Hiring research from company career pages

Use `humble-echidna/ats-jobs`. It reads jobs directly from each company's applicant tracking system, so postings are current and complete for that company. It does not search job boards; you need the company names or career-page URLs.

## Input

- `companies`: company names (for example `"Linear"`) a careers page (for example `"https://linear.app/careers"`), or a job-board URL (for example `"https://boards.greenhouse.io/stripe"` or the short form `"greenhouse:stripe"`). Board URLs are the most reliable.
- Filters are applied before charging: `keywords` (title words), `excludeKeywords`, `locations`, `remoteOnly`, `postedWithinDays`, `departments`, `employmentTypes`, and `minSalary` with `minSalaryCurrency` / `minSalaryPeriod`.
- `includeDescription: false` when the user only needs titles and links (smaller output).
- `onlyNewJobs: true` on repeat runs returns only jobs added since the last run with the same input.

## Analysis

Summarize by company: open role count, departments, locations or remote, and salary ranges where the posting states them. For trend questions, compare `postedAt` dates. Quote job titles and link each job's URL.

## Cost

$1.50 per 1,000 jobs returned, on the user's own Apify account. A 20-company check is typically a few cents.
