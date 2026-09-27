---
name: company-lookup
description: Look up companies in the French business register (SIREN/SIRET, INSEE) and the global LEI register, by name or by identifier, or list newly registered French companies by activity and region. Use for company verification, KYB, supplier checks, or prospect lists in France.
---

# Company register lookup

Use `humble-echidna/company-registers`.

- **By name**: `mode: "search"`, `searchTerms: ["<name>"]`, `registers: ["france", "lei"]`. Narrow with `status: "active"`, `departments`, `regions`, `activityCodes` (NAF/APE), `sizeCategories`, `revenueMin` / `revenueMax`.
- **By identifier**: put SIREN, SIRET, VAT or LEI numbers in `identifiers`.
- **New French companies**: `mode: "newCompanies"` with `sinceDays` (default 3) and activity or region filters. This reads the official BODACC announcements.
- `crossLink: true` (the default) adds each French company's LEI when it has one.

Report the legal name, identifiers, status, address, activity, size, and when found, the LEI and parent. Say which register each fact came from.

$3 per 1,000 companies returned, on the user's own Apify account.
