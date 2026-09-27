---
name: hiring-research
description: Research who is hiring and for what, straight from company career pages (Greenhouse, Lever, Ashby, Recruitee, Personio, Teamtailor) and remote job boards, and turn it into hiring signals - companies opening roles that match keywords, hiring surges, and website tech stack changes. Use when the user asks who is hiring, what roles a company has open, hiring trends or salary ranges, wants remote job leads, or wants sales or investment signals from hiring.
---

# Hiring research and hiring signals

Pick the tool by the question:

| The user wants | Tool |
|---|---|
| The open jobs at named companies (lists, counts, salaries) | `humble-echidna/ats-jobs` |
| Which of these companies show a buying or growth signal: new roles for a skill, a hiring surge, a stack change | `humble-echidna/hiring-signals` |
| Remote jobs across the web, without naming companies | `humble-echidna/remote-jobs` |

`hiring-signals` and `remote-jobs` are new. If either is missing from the connector's tool list, it is not published yet: say so, and use `ats-jobs` for the companies the user named.

## Jobs at named companies: `ats-jobs`

It reads jobs directly from each company's applicant tracking system, so postings are current and complete for that company. It does not search job boards; you need the company names or career-page URLs.

- `companies`: company names (for example `"Linear"`), a careers page (for example `"https://linear.app/careers"`), or a job-board URL (for example `"https://boards.greenhouse.io/stripe"` or the short form `"greenhouse:stripe"`). Board URLs are the most reliable.
- Filters are applied before charging: `keywords` (title words), `excludeKeywords`, `locations`, `remoteOnly`, `postedWithinDays`, `departments`, `employmentTypes`, and `minSalary` with `minSalaryCurrency` / `minSalaryPeriod`.
- `includeDescription: false` when the user only needs titles and links (smaller output).
- `onlyNewJobs: true` on repeat runs returns only jobs added since the last run with the same input.

Summarize by company: open role count, departments, locations or remote, and salary ranges where the posting states them. For trend questions, compare `postedAt` dates. Quote job titles and link each job's URL.

## Hiring signals: `hiring-signals`

One result per company that has a signal; quiet companies are not returned and not charged. Use it for account research, sales prospecting ("companies that started hiring Kafka engineers") and investor or competitor tracking.

- `companies`: one per line, same forms as `ats-jobs`. Add the company's domain after a `|` so its website stack can be checked, for example `"https://boards.greenhouse.io/gitlab | gitlab.com"` or `"Linear | linear.app"`.
- `signalKeywords`: the skills or roles that count, for example `["Rust", "Kafka", "data engineer"]`. Prefer specific terms; `matchIn: "title"` gives fewer, stronger matches.
- `departments`, `locations`: narrow both the matching roles and the role counts used for surges.
- `lookbackDays` (default 30): how recent a posting must be to count as new.
- `detectTechStack` (default on): lists the company website's technologies; `stackTechnologies` limits stack signals to named tools such as `HubSpot` or `Segment`.
- `sinceLastRun: true` turns it into a monitor: each later run with the same input returns only what is new since the previous run, including hiring surges (`surgePercent`, `surgeMinRoles`, `surgeWindowDays`) and technologies added or dropped. The first run is the baseline. Surges need at least two runs.
- `maxResults` caps the number of companies with a signal.

Report each company with its signals in plain words ("opened 4 Rust roles in the last 14 days", "open roles up 35% in 30 days", "added Segment"), the matching job titles with links, and the stack. Rank companies by signal strength.

## Remote jobs: `remote-jobs`

Reads We Work Remotely, Remote OK and Python.org Jobs (`sources`), deduplicated across boards.

- Filters: `keywords` (title or tags), `excludeKeywords`, `locations` (where candidates may live, for example `["USA", "Europe"]`; worldwide jobs always match), `categories`, `postedWithinDays`.
- `maxResults` (default 100): keep it small for a quick answer.
- `onlyNewJobs: true` for a repeat search that returns only jobs not seen before.

## Cost

Charged per result on the user's own Apify account: jobs from company boards $1.50 per 1,000, remote-board jobs $2 per 1,000, hiring signals $20 per 1,000 companies with a signal (2 cents each; quiet companies are free). A 20-company job check is typically a few cents. Confirm before a signal run over more than 500 companies.
