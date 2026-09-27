# Privacy policy: Echidna Web Data

Last updated: 2026-09-27

Echidna Web Data is a Claude plugin. It is made of text files only: a manifest, a connector declaration (`.mcp.json`) and skill instructions. It contains no code that runs on your computer and no server run by the plugin's author.

## What the plugin sends, and where

- **One destination: Apify's hosted MCP server, `https://mcp.apify.com`.** When Claude uses one of the plugin's tools, the tool input you or Claude provide (web addresses, company names, search terms, job keywords, feed URLs, dataset IDs) is sent there and runs as an Apify Actor on **your own Apify account**, which you sign in to through Apify's OAuth page.
- The Actors then fetch the public web pages, files, feeds and public APIs named in that input. They do not log in to any site, and they follow robots.txt.
- Results are saved in your Apify account's storage (datasets and key-value stores) and returned to Claude.
- The plugin sends nothing anywhere else. It does not read files on your computer, your environment variables, or your conversation beyond the tool inputs above.

## What the author receives

- The author does **not** receive your inputs, your results, your Apify credentials, or your conversations.
- As the developer of the Actors, the author sees the aggregate statistics Apify gives every Actor developer (for example, number of runs and users, and run status).
- The author keeps no data from your use of the plugin, so there is nothing to retain, export or delete on the author's side.

## Retention and deletion

Data kept in your Apify account follows Apify's retention rules and your plan; you can delete runs, datasets and key-value stores in Apify Console at any time. Some Actors remember what they returned before (for "only new" and "changes since last run" options); that state is stored in your own Apify account, in a key-value store you can delete.

## Personal data

The Actors are built to read public business and web information (web pages, job postings, public tenders, company registers, research papers). Some of it can include names of people (for example, a company officer in a public register or an author of a paper). Use the results in line with the laws that apply to you, such as the GDPR.

## Children

The plugin is not intended for people under 18.

## Third parties

- Apify privacy policy: https://apify.com/privacy-policy
- Anthropic's privacy policy covers how Claude handles your conversations: https://www.anthropic.com/legal/privacy

## Contact

Questions about this policy or a security concern: open an issue at https://github.com/Michael-A-Costa/echidna-web-data/issues, or on the Issues tab of the Actor's page at https://apify.com/humble-echidna.
