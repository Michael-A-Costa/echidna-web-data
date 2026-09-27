# Directory submission package: Echidna Web Data

Everything needed to submit this plugin to Anthropic's Claude directory. Prepared 2026-09-27 for plugin version 1.1.0. Sources are listed at the end; anything not confirmed from them is marked **unverified**.

## How the listing is built

The developer portal builds the listing from the repository itself. The docs say: "The **Listing details** step shows how the plugin appears in the directory, read from `plugin.json` and the README. To change a field before you submit, edit `plugin.json` or the README in the repository and validate again." The directory also "shows your README as the listing's description."

So the name, one-liner and long description below are already in `plugin.json` and `README.md`. This file shows them in one place and covers the answers the form asks for.

## Listing text

**Name** (`plugin.json` `name` / `displayName`): `echidna-web-data` / **Echidna Web Data**

**Publisher** (`author.name`): humble-echidna

**One-liner** (`plugin.json` `description`):

> Audit websites (SEO, broken links, tech stack), enrich business leads, turn pages, articles and documents into Markdown, track company hiring signals, search EU/UK tenders, company registers and research papers, transcribe audio, and download or OCR images. Runs on your own Apify account.

**Long description:** `README.md` (the portal uses it as is). Its opening, for any field that wants a short paragraph:

> Everyday web-data jobs inside Claude, run on your own Apify account. Audit a site's SEO, broken links and tech stack. Qualify a Google Maps lead list by dead sites, platform and SEO score. Turn pages, whole docs sites, articles, PDFs and Office files into clean Markdown for RAG. Find which companies are hiring for a skill, and catch hiring surges and stack changes. Search EU and UK tenders, French and LEI company registers, and research papers. Transcribe audio, download a page's images, and OCR text in images. Every check can be re-run to return only what changed. Pay per result on Apify: about $0.25 for a 25-page SEO audit, and 2 cents per company with a hiring signal.

**Categories:** the plugin submission docs do not describe a category field (**unverified** whether the form has one; the connector form may). If asked, pick in this order: Data and research, Marketing and SEO, Sales, Developer tools. The `keywords` in `plugin.json` are the tags: seo, web-scraping, markdown, rag, lead-enrichment, jobs, hiring-signals, tenders, research-papers, transcription, ocr, apify.

## Example prompts

These work with the skills as written. Each one names the skill it triggers.

1. "Audit example.com: give me the SEO score, the five fixes that matter most, and what the site is built with." (website-audit)
2. "Here's my Google Maps dataset of dentists in Austin (dataset ID abc123). Which ones have dead websites, which run on Wix or Squarespace, and which score under 50 for SEO?" (leads-enrichment)
3. "Which of these 30 companies opened Rust or Kafka roles in the last two weeks? Include their website stack." (hiring-research, hiring-signals)
4. "Turn the docs section of docs.example.com into chunked Markdown I can load into a vector store." (site-to-markdown)
5. "Find open EU tenders for cybersecurity services in Germany and France that close in the next 30 days." (tender-search)
6. "Look up SIREN 552 081 317: legal name, status, address and LEI." (company-lookup)
7. "Find the 20 most-cited open-access papers on CRISPR base editing since 2022." (paper-search)
8. "Transcribe this podcast episode and give me a summary with timestamps: <URL>." (transcribe-media)
9. "Download every product image on this page, skip the icons, and zip them." (images-and-ocr)
10. "Every Monday, tell me which of these competitors changed their tech stack or posted new sales roles." (watch-for-changes)

## Screenshots

The plugin docs don't list a screenshot upload for a plugin bundle (**unverified**; the form may ask). The directory accepts PNG, JPEG, GIF and WebP images in the plugin folder and shows them when the README uses Markdown image syntax. Keep each under 5 MiB. The checklist holds files over 256 KiB that aren't images or fonts for a reviewer, but images are exempt.

Take these in claude.ai with the plugin installed, on a light theme, with no personal account details visible:

1. **Website audit report:** prompt 1 above, showing the score, the top fixes and the stack table.
2. **Lead enrichment table:** prompt 2 on a small public-business sample, showing the status, CMS and score columns.
3. **Hiring signals:** prompt 3, showing companies ranked by signal with job links.
4. **Docs to Markdown:** prompt 4, showing a chunk with its URL and heading path.
5. **Connector sign-in:** the plugin's Connectors tab, with the Apify OAuth consent, to show that runs use the user's own account.

Put them in `docs/screenshots/` and add them to the README under a "Screenshots" heading. If they go in the plugin root folder, they ship to every user, which is allowed.

## Privacy and data handling

- **Privacy policy link:** `https://github.com/Michael-A-Costa/echidna-web-data/blob/main/PRIVACY.md`. The Software Directory Policy requires one for software that "connects to a remote service."
- **Answers for the Data handling step.** The step asks four questions:
  - *Does the plugin read or store personal data?* No, not by design. The tools read public web pages and public records. Some records can include people's names, such as a company officer in a register or a paper's authors. Nothing is stored by the plugin or its author. Results are stored in the user's own Apify account.
  - *Does it send data to services other than its declared connectors?* No. The only destination is the declared connector, `https://mcp.apify.com`. The Actors then fetch the public URLs that the user gives them.
  - *How long is data kept?* The author keeps nothing. Apify's retention rules and the user's plan apply to the user's own Apify storage.
  - *Is it intended for people under 18?* No.
- **What the plugin runs:** nothing locally. There are no hooks, scripts, local MCP servers or package launchers, only JSON and Markdown files. This keeps it clear of every "held for a reviewer" rule about executables.

## Support contact

- **Public support channel:** GitHub issues at https://github.com/Michael-A-Costa/echidna-web-data/issues, and the Issues tab on each Actor at https://apify.com/humble-echidna. Both are in the README and PRIVACY.md.
- **Contact email for Anthropic:** `<SUPPORT EMAIL: owner to choose>`. The Compliance step shows the email of the claude.ai account that submits. The Software Directory Policy asks for "verified contact information and support channels for users with product or security concerns." Don't put a personal address in this public repository. If a public support email is wanted, use a dedicated alias.

## Checks already done (2026-09-27)

- `claude plugin validate .` and `claude plugin validate --strict .` pass with Claude Code 2.1.283.
- Every skill's `name` matches its folder, and each `description` is a single string of 250 to 455 characters, under the 1,024 limit.
- The README has more than 40 words, and the `LICENSE` file is MIT.
- The folder holds no symlinks, submodules, LFS files or OS metadata files, and `.gitignore` covers `.DS_Store`.
- `.mcp.json` is valid JSON. It declares one `http` server with an absolute `https://` URL and no credentials.
- A `tools/list` call against the connector URL, made with the owner's Apify token, returned all 18 Actor tools and the 4 helpers. Actors that aren't public yet show up only for their owner. When a filter names an Actor that doesn't exist, the server drops it silently, and the other tools still load. That was tested with a made-up name.

Not done: the portal's own **Validate**, which runs extra checks for the README, license and name conflicts. Also not done: signing in with Apify OAuth from inside claude.ai, and a `claude plugin eval` run.

## Risks a reviewer may raise

1. **The connector isn't ours.** The Software Directory Policy says developers "must verify that they own or control any API endpoint… their Software connects to". It then says: "Plugins are an exception, and may connect to any Connector approved in the Software Directory." Apify's docs say Apify is in Claude's connector directory ("Search for 'Apify' in the Claude Desktop connector directory"). That is **unverified** from inside claude.ai. Our URL is Apify's server with a `?tools=` filter, which is the same server but not the exact directory URL. If the reviewer asks, the answer is that it is Apify's approved connector, filtered to our Actors. Don't submit `mcp.apify.com` as our own MCP connector. The docs' advice to also submit the server applies only when "you run the remote MCP server."
2. **Queued Actors.** As of 2026-09-27, six Actors are private and waiting in the publish queue: article-extractor, remote-jobs, academic-papers, image-ocr, dataset-transform and hiring-signals. Apify allows 5 publications per 24 hours, so they should all be public by about 2026-09-29. The plugin works before then, but a reviewer would not see those tools. **Submit after hiring-signals is public.**
3. **Cost.** Every tool charges the user's Apify account. The README lists each price, and the skills tell Claude to confirm large runs. There is no policy text on cost disclosure (the policy page doesn't address it).

## Exact submission steps

Prerequisites: a Pro, Max, Team or Enterprise Claude plan, since free accounts can't submit. On Pro or Max, you submit from your own account.

1. **Merge this branch.** The directory follows the repository's default branch (`main`) unless you name another. Merge `directory` into `main` and push. Wait until `hiring-signals` shows at https://apify.com/humble-echidna.
2. **Test on your own account first.** In Claude Code, run `claude --plugin-dir <path to this repository>`, try prompts 1 and 3, and complete the Apify OAuth sign-in. Then, in claude.ai, go to **Customize > Plugins > Add > Upload plugin** with a zip of the folder, connect the connector on the plugin's **Connectors** tab, and try one prompt in chat.
3. **Connect GitHub** to claude.ai in the organization you'll submit from. The portal checks that the connected account can push to `Michael-A-Costa/echidna-web-data`. The repository is public, so it doesn't need the Claude GitHub App.
4. Open **https://claude.ai/directory/manage** and select **Submit new**, then **Plugin bundle**.
5. On the **Source** step:
   - **Repository:** `Michael-A-Costa/echidna-web-data`
   - **Plugin path:** leave empty, since the plugin is at the root.
   - **Branch or tag:** leave empty to follow `main`, or use a release tag if you want to publish deliberately.
   - Select **Validate**. Fix anything marked **Blocking**, push, and select **Re-validate**.
6. On **Listing details**, check the name and description. Any change goes in `plugin.json` or the README, then re-validate.
7. On **Data handling**, answer as in the Privacy and data handling section above.
8. On **Compliance**, check the contact email and select all four acknowledgements.
9. On **Review and submit**, keep **GitHub push webhook** (setting it up needs repository admin) and leave **Auto-publish passing versions** off for the first version. Then select **Submit for review**.
10. Follow the review under **Submissions**. When the version passes, select **Publish**. By default, an Anthropic reviewer then publishes it. Later releases work by raising `version` in `plugin.json` and merging to `main`.

Limits: 10 submissions per organization per 24 hours, drafts included, and one submission per repository and folder. If a submission is stuck, the contact is `directory@anthropic.com`.

## Sources read (2026-09-27)

- Anthropic, "Build plugins for Claude with the directory submission portal": https://claude.com/blog/build-plugins-for-claude. It covers the portal URL, the paid-plan requirement, the two submission kinds and auto-validation.
- Publish to the directory: https://claude.com/docs/directory/publish. It covers who can submit, bundle versus connector, and the review process.
- Submit your plugin: https://claude.com/docs/plugins/submit. It covers the Source, Listing details, Data handling, Compliance and Review steps, private repositories, and publish settings.
- Plugin pre-submission checklist: https://claude.com/docs/plugins/pre-submission-checklist. It covers the blocking, held and warning rules, the README (40 words) and license, file limits, and the MCP URL rules.
- Plugin feature support across platforms: https://claude.com/docs/plugins/platform-support. It says a remote http MCP server in chat is "Listed on the plugin's **Connectors** tab; works once you add or connect it there."
- Create custom skills: https://claude.com/docs/skills/how-to. It covers the `name` and `description` frontmatter rules.
- Plugin manifest reference: https://code.claude.com/docs/en/plugins-reference. It covers the `plugin.json` fields, including `displayName`.
- Anthropic Software Directory Policy: https://support.claude.com/en/articles/13145358-anthropic-software-directory-policy. It covers endpoint ownership and the plugin exception, the privacy policy link, and the support contact.
- Apify, Claude Desktop integration: https://docs.apify.com/integrations/claude-desktop. It says Apify is listed in Claude's connector directory.
- Unite.AI news report on the portal opening: https://www.unite.ai/anthropic-opens-directory-submission-portal-for-claude-plugins/. It was seen only as a search-result summary and not opened.

Not read: the Anthropic Software Directory Terms (https://support.claude.com/en/articles/13145338-anthropic-software-directory-terms), and the portal itself, which needs the owner's signed-in paid account.
