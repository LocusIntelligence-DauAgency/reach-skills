# Reach: Google Business Profile MCP server

Reach is a hosted Google Business Profile MCP server for local businesses and the people who manage them. Connect it once with OAuth and your AI assistant can read your profile, reviews, performance, local search rankings, nearby competitors and leads, then, with your explicit approval, reply to reviews, publish Google posts, edit profile fields and manage photos. Every public change is previewed or shown in full before it is made, write tools carry MCP destructive annotations, and Google writes are rate limited per business. Works with Claude, ChatGPT, Claude Code, Cursor, VS Code, Codex, Windsurf, Cline and any client that supports remote MCP servers. Free plan available.

- **Endpoint:** `https://reach.locus-intelligence.com/api/mcp`
- **Transport:** Streamable HTTP. No SSE, no local install, nothing to run.
- **Auth:** OAuth 2.1 with PKCE and dynamic client registration. No API key, client ID or secret. You sign in with your own Reach account in the browser.
- **Website:** [reach.locus-intelligence.com/google-business-profile-mcp](https://reach.locus-intelligence.com/google-business-profile-mcp?utm_source=github-readme&utm_medium=mcp_directory&utm_campaign=reach_mcp)

This repository holds the public documentation, registry metadata (`server.json`, `glama.json`), the tool list (`tools.json`), install notes, [skills](#skills) and Claude Code and Codex plugin packaging for the hosted server. The server itself runs at the endpoint above; there is no code to install.

You need a Reach account ([sign up free](https://reach.locus-intelligence.com/?utm_source=github-readme&utm_medium=mcp_directory&utm_campaign=reach_mcp)). The assistant sees full data after you connect your Google Business Profile in Reach; before that it can read your public listing only.

## Report a tool problem

When a Reach tool fails, follow its recovery instructions. Use `report_issue` to save a bounded
account of the goal, expected and actual behavior, steps and retries for the Reach team. Remove
people and business names, addresses, identifiers and customer content first. Never include raw
arguments, transcripts, headers, tokens or attachments. Reach scrubs common sensitive patterns
before storage and email; it cannot guarantee that arbitrary prose is anonymous.

Reports are stored for 90 days with a pseudonymous account key. The tool separately confirms
`saved` and `email_sent`: a saved report remains available to the team if mail fails or its outcome
is unknown. Retry with the same idempotency key; an existing report is never emailed again automatically.

## Install

### Claude (claude.ai, Claude Desktop, Claude mobile)

1. Open **Customize**, then **Connectors**.
2. Click **+**, then **Add custom connector**.
3. Name: `Reach`. URL: `https://reach.locus-intelligence.com/api/mcp`. Leave Advanced settings empty and click **Add**.
4. Click **Connect** next to Reach and sign in with your Reach account.
5. In a chat, click **+**, open **Connectors** and turn on Reach.

Custom connectors are available to every Claude user. On Team and Enterprise, an owner adds the connector in Organization settings, then each member clicks Connect.

### ChatGPT

1. In ChatGPT on the web, open **Settings**, then **Apps**, then **Advanced settings**, and turn on **Developer mode**.
2. Go back to **Apps** and click **Create**.
3. Name: `Reach`. URL: `https://reach.locus-intelligence.com/api/mcp`. Authentication: **OAuth**.
4. Sign in with your Reach account when asked, then click **Create**.
5. In a chat, choose Reach from the tools menu or mention it by name.

Developer mode is a ChatGPT setting; a workspace admin may need to allow it first.

### Claude Code

```sh
claude mcp add --transport http reach https://reach.locus-intelligence.com/api/mcp
```

Add `--scope user` before `reach` to use it in every project. Then type `/mcp` in Claude Code, select `reach` and sign in in the browser window that opens. `claude mcp list` shows `reach` as connected when sign-in is done.

### Codex

```sh
codex mcp add reach --url https://reach.locus-intelligence.com/api/mcp
codex mcp login reach
```

### Cursor

Add this to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project), merged with any existing `mcpServers`:

```json
{ "mcpServers": { "reach": { "url": "https://reach.locus-intelligence.com/api/mcp" } } }
```

Or open this install link in a browser on a machine with Cursor installed:

```text
cursor://anysphere.cursor-deeplink/mcp/install?name=reach&config=eyJ1cmwiOiJodHRwczovL3JlYWNoLmxvY3VzLWludGVsbGlnZW5jZS5jb20vYXBpL21jcCJ9
```

Restart Cursor, open **Customize**, then **MCPs**, and follow the sign-in prompt for `reach`. With the Cursor CLI: `agent mcp login reach`.

### VS Code (GitHub Copilot agent mode)

[Install in VS Code](https://insiders.vscode.dev/redirect/mcp/install?name=reach&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Freach.locus-intelligence.com%2Fapi%2Fmcp%22%7D) or [Install in VS Code Insiders](https://insiders.vscode.dev/redirect/mcp/install?name=reach&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Freach.locus-intelligence.com%2Fapi%2Fmcp%22%7D&quality=insiders), or run:

```sh
code --add-mcp '{"name":"reach","type":"http","url":"https://reach.locus-intelligence.com/api/mcp"}'
```

Start the server from the MCP view and sign in when VS Code opens the browser.

### Cline

1. Open the MCP Servers panel, then the **Remote Servers** tab.
2. Server name: `reach`. Server URL: `https://reach.locus-intelligence.com/api/mcp`. Transport type: **Streamable HTTP**. Click **Add Server**.
3. Follow the sign-in prompt and sign in with your Reach account.

Or add it to Cline's MCP settings JSON:

```json
{ "mcpServers": { "reach": { "type": "streamableHttp", "url": "https://reach.locus-intelligence.com/api/mcp" } } }
```

### Windsurf (Devin Desktop)

Add this to `~/.config/devin/mcp_config.json` (older installs: `~/.codeium/windsurf/mcp_config.json`). Windsurf reads `serverUrl`, not `url`:

```json
{ "mcpServers": { "reach": { "serverUrl": "https://reach.locus-intelligence.com/api/mcp" } } }
```

Refresh the MCP servers list and sign in with your Reach account when prompted.

### Google Antigravity

Add this to `~/.gemini/config/mcp_config.json` (or `.agents/mcp_config.json` in a workspace). Antigravity reads `serverUrl`, not `url`:

```json
{ "mcpServers": { "reach": { "serverUrl": "https://reach.locus-intelligence.com/api/mcp" } } }
```

Open **Agent Settings**, then **Customizations**, click **Authenticate** next to `reach`, sign in, then paste the code Antigravity shows back into the settings panel and click **Submit**.

### Any other MCP client

Configure a remote (Streamable HTTP) server named `reach` with the URL `https://reach.locus-intelligence.com/api/mcp` and no headers or API key. The client finds the sign-in server from the 401 response and registers itself.

```json
{ "mcpServers": { "reach": { "type": "http", "url": "https://reach.locus-intelligence.com/api/mcp" } } }
```

AI agents setting Reach up on a user's behalf can follow [`llms-install.md`](llms-install.md).

### Smithery

Reach is listed on Smithery by its URL; there is no Smithery config file in this repository.

## Skills

Eighteen [Agent Skills](https://agentskills.io) in [`skills/`](skills) turn the server into repeatable jobs. Each one calls only the Reach tools listed below, and each one that changes Google shows the exact change and waits for your yes.

| Skill | What it does | Changes Google |
| --- | --- | --- |
| [`reply-to-google-reviews`](skills/reply-to-google-reviews/SKILL.md) | Finds unanswered reviews, drafts replies in the reviewer's language, posts the ones you approve. | After your yes |
| [`optimize-google-business-profile`](skills/optimize-google-business-profile/SKILL.md) | Finds what the profile is missing and fixes it one previewed change at a time. | After your yes |
| [`write-gbp-post`](skills/write-gbp-post/SKILL.md) | Turns a brief into a Google post, offer or event and publishes or schedules it. | After your yes |
| [`gbp-weekly-report`](skills/gbp-weekly-report/SKILL.md) | This week against last week: views, calls, directions, website clicks, reviews and rank. | Never (read-only) |
| [`local-rank-audit`](skills/local-rank-audit/SKILL.md) | Rankings, the local search grid and who ranks above you, with the gaps the data shows. | Never; tracking a new keyword uses a keyword slot, after your yes |
| [`competitor-watch`](skills/competitor-watch/SKILL.md) | Nearby competitors and a rival's 12-month rating and photo history. | Never (read-only) |
| [`review-insights`](skills/review-insights/SKILL.md) | Praise themes, complaints, and the services and staff named across your reviews. | Never (read-only) |
| [`review-request-kit`](skills/review-request-kit/SKILL.md) | A real review link and short request messages you can send customers. | Never (read-only) |
| [`gbp-post-calendar`](skills/gbp-post-calendar/SKILL.md) | Plans a month of posts from your services, offers and events, and schedules the ones you approve. | After your yes |
| [`gbp-photo-refresh`](skills/gbp-photo-refresh/SKILL.md) | Checks photo counts and recency against nearby competitors, then uploads the photos you approve. | After your yes |
| [`holiday-hours`](skills/holiday-hours/SKILL.md) | Sets special opening hours for upcoming public holidays, one approved change at a time. | After your yes |
| [`categories-and-service-area`](skills/categories-and-service-area/SKILL.md) | Previews and updates additional categories and the service area. | After your yes |
| [`keyword-picker`](skills/keyword-picker/SKILL.md) | Picks which local keywords to track from the search terms people really used. | Never; tracking a keyword uses a keyword slot, after your yes |
| [`growth-plan`](skills/growth-plan/SKILL.md) | Walks through your open growth tasks, each explained with its data. | Never; marks tasks done in Reach after your yes |
| [`lead-follow-up`](skills/lead-follow-up/SKILL.md) | Lists new leads and booking requests and drafts a reply you can send. | Never (read-only) |
| [`multi-location-report`](skills/multi-location-report/SKILL.md) | Compares every connected location over the same dates. | Never (read-only) |
| [`not-showing-on-maps`](skills/not-showing-on-maps/SKILL.md) | Diagnoses why the business is missing from Google Maps or Search. | Never (read-only) |
| [`add-local-business-schema`](skills/add-local-business-schema/SKILL.md) | Builds LocalBusiness schema for your website from the listing. | Never (changes your website code after your yes) |

The skills need the Reach MCP server connected (see Install above). The plugins below bundle both.

With the [skills CLI](https://skills.sh) (Claude Code, Codex, Cursor and other agents):

```sh
npx skills add LocusIntelligence-DauAgency/reach-skills
```

As a Claude Code plugin (the `reach` MCP server plus all eighteen skills):

```text
/plugin marketplace add LocusIntelligence-DauAgency/reach-skills
/plugin install reach@google-business-profile-mcp
```

As a Codex plugin (the `reach` MCP server plus all eighteen skills):

```sh
codex plugin marketplace add LocusIntelligence-DauAgency/reach-skills
codex plugin add reach@google-business-profile-mcp
codex mcp login reach
```

## Tools

<!-- tools:start -->
<!-- Generated from the Reach server by mcp:public. Do not edit by hand. -->

| Tool | What it does | Read or public change | Cost |
| --- | --- | --- | --- |
| `get_account` | Your plan, locations, Google connection state and which Reach features you have. | Read | None |
| `get_listing` | One listing's profile, reviews, posts and photos. | Read | None |
| `get_visibility` | Search rankings for tracked keywords, nearby competitors and the local search grid. | Read | None |
| `get_performance` | Profile views, customer actions and search terms for a date range your plan covers. | Read | None |
| `get_customers` | Leads and booking requests from your Reach pages. | Read | None |
| `get_recommendations` | What your profile is missing, and which items the assistant can fix for you. | Read | None |
| `update_listing` | Change profile details (hours, description, phone, links, services) and service area, after a preview you approve. | Public change on Google, after your approval | None |
| `manage_media` | Add or remove photos and videos, after a preview you approve. | Public change on Google, after your approval (cannot be undone through Reach) | None |
| `publish_post` | Publish or schedule a Google post you have approved word for word. | Public change on Google, after your approval (cannot be undone through Reach) | None |
| `reply_to_review` | Post the review reply you approved. Calling again replaces it. | Public change on Google, after your approval (cannot be undone through Reach) | None |
| `draft_review_reply` | Draft reply options for a review. Nothing is posted. | Changes Reach only | 2 Credits per draft |
| `track_keywords` | Start or stop tracking keywords on a location: a list rank and a weekly map scan for each. | Changes Reach only | 1 plan keyword per tracked keyword; untracking frees it |
| `request_feature` | Deprecated: use send_feedback. Sends the Reach team a feature request. | Changes Reach only | None |
| `send_feedback` | Send the Reach team an idea, a problem or praise in your own words. Asks for no contact details and never uses up a call. | Changes Reach only | None |
| `report_issue` | Save sanitized diagnostics about a failed MCP operation for the Reach team. | Changes Reach only | None |
| `update_recommendation_status` | Mark a recommendation done or dismissed in Reach. | Changes Reach only | None |
| `setup_reach` | Recommended setup for your assistant: the Reach skills, a weekly report and a daily review check. Your assistant adds only what you agree to. Never uses up a call. | Read | None |

Changes to Google are limited to 20 per business per hour through AI assistants. A limited call says how many seconds to wait; it is never queued or retried.

Prompts:

- `set_up_reach`: See the recommended Reach setup for this assistant (skills, a weekly report, a daily review check) and choose what to add.
- `optimise_my_profile`: Find what the listing is missing and fix it one confirmed change at a time.
- `review_my_visibility`: An honest read on search rank, competitors and profile traffic.
- `handle_my_reviews`: Find unanswered reviews, draft replies, and post the ones I approve.

Full input schemas and annotations: [`tools.json`](tools.json).
<!-- tools:end -->

## Safety and consent

- **Preview first.** Tools that change your Google profile default to a preview that shows the before and after without writing anything.
- **Explicit yes.** The assistant is told never to change anything on Google without your yes to the exact change. Review replies and posts are shown word for word before they are published.
- **Annotations.** Every tool declares MCP annotations (`readOnlyHint`, `destructiveHint`, `idempotentHint`, `openWorldHint`), so clients that ask before destructive calls will ask.
- **Your access, nothing more.** The assistant acts as you, with exactly your locations, plan and permissions in Reach.
- **Rate limited.** Changes to Google are limited per business (see the note under Tools).
- **Block any assistant.** In Reach, **Settings → AI Connectors** lists every assistant that has used your account. Block one or all of them; a block applies from the next request and is checked again right before any Google change.

## Limits

- Account limits apply exactly as in the Reach app. When a limit stops a call, the tool result says what happened and where you manage your account in Reach, and the assistant stops.
- A result that is empty or partial says why under `limitations` (public listing only, a feature your plan does not include, Google not synced yet, or no connected location), with a link to fix it. An empty `limitations` means nothing was hidden.
- Reading costs nothing. Drafting a review reply uses Credits; tracking a keyword uses a keyword slot. The Cost column above has the exact numbers.

## Data and privacy

- Tool results go to the AI assistant you connected, under that assistant's own data terms.
- Customer phone numbers in leads are masked to their last 4 digits.
- Reach logs each tool call (tool, time, outcome) for your activity log under AI Connectors. Results of read tools are not stored.
- Full details: [Reach Privacy Policy](https://reach.locus-intelligence.com/privacy?utm_source=github-readme&utm_medium=mcp_directory&utm_campaign=reach_mcp), section on AI connectors.

## Example prompts

- "Which of my Google reviews have no reply yet?"
- "Draft a reply to my latest 3-star review." (Nothing is posted until you approve a draft.)
- "How am I ranking for my main keyword near me, and who ranks above me?"
- "What is missing from my Google Business Profile? Fix the simple things after showing me each change."
- "Summarise my profile views, calls and direction requests for the last 28 days."

## FAQ

**Do I need an API key?** No. You sign in with your Reach account through OAuth; the client registers itself.

**Can the assistant post or change things without asking?** It is instructed not to, every change tool shows the exact change first, and write tools are annotated as destructive so your client can ask before running them. You can block any assistant in Reach at any time.

**Does it work without connecting Google?** Yes, for your public listing. Connect your Google Business Profile in Reach for reviews management, posts, performance data and edits.

**Which clients are supported?** Any MCP client that supports remote Streamable HTTP servers with OAuth. Setup for the common ones is above.

**Is the server open source?** No. This repository documents the hosted server; the server runs at the endpoint above.

**Where do I report a problem?** Open an issue here, or email [hello@locus-intelligence.com](mailto:hello@locus-intelligence.com). Security issues: see [SECURITY.md](SECURITY.md).

## Links

- [Reach Google Business Profile MCP server](https://reach.locus-intelligence.com/google-business-profile-mcp?utm_source=github-readme&utm_medium=mcp_directory&utm_campaign=reach_mcp)
- [Setup guide: connect Reach to Claude, ChatGPT and Claude Code](https://reach.locus-intelligence.com/google-business-profile-mcp/setup?utm_source=github-readme&utm_medium=mcp_directory&utm_campaign=reach_mcp)
- [llms.txt](https://reach.locus-intelligence.com/llms.txt)
- [Privacy Policy](https://reach.locus-intelligence.com/privacy?utm_source=github-readme&utm_medium=mcp_directory&utm_campaign=reach_mcp)
- [Terms & Conditions](https://reach.locus-intelligence.com/terms?utm_source=github-readme&utm_medium=mcp_directory&utm_campaign=reach_mcp)
- [Changelog](CHANGELOG.md)

Reach by Locus is built by Growthnomics Technologies Private Limited. Documentation in this repository is MIT licensed.
