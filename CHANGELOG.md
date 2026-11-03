# Changelog

Changes to the hosted Reach MCP server at `https://reach.locus-intelligence.com/api/mcp`. Each tool also carries its own version number, returned with every result.

## Unreleased

- `send_feedback`, `request_feature` and `report_issue` (each emails the Reach team) and `update_recommendation_status` (overwrites a recommendation's status) are now marked `destructiveHint: true`.
- `get_account` and `setup_reach` read the account without side effects.
- `setup_reach` (version 2) and the `set_up_reach` prompt are opt-in: the assistant offers setup once when it looks incomplete, runs `setup_reach` only after a yes, and adds only the skills and scheduled reports the owner agrees to.
- Every tool declares `readOnlyHint`, `destructiveHint`, `idempotentHint` and `openWorldHint` as explicit booleans, from one source in the server. `report_issue` is no longer marked idempotent; `get_visibility` is marked open world (it returns other public Google businesses).
- An account limit now returns `reason: limit_reached` (or `monthly_quota_exhausted`) with the numbers, a plain message and `manageUrl`. Results, prompts and skills no longer show prices, name a plan to buy, promote upgrades or link to a plans page, and `get_account` no longer returns billing term or currency.
- Every tool that returns a list is paged: pass `cursor` and `limit`, and each result carries a `paging` block with the next cursor and a "more available" line. Walk a location's full reviews, customers, booking requests, scheduled posts, photos, tasks, rank history and search terms page by page. Long review, reply, post and note text is cut per item with a marker.
- New `setup_reach` tool and `set_up_reach` prompt: recommended Reach skills, a weekly report and a daily review check for your assistant. It never uses up a monthly call.
- `gbp-weekly-report` ends with one post idea for the week.
- Agent-readable setup steps at `/mcp.txt`.
- The server introduces itself as "Reach: Google Business Profile MCP server", with a website link, an icon and short instructions for the assistant.
- Setup notes for AI agents describe sign-in by dynamic client registration only.
- This public repository: README, `server.json` for the official MCP Registry, `glama.json`, `tools.json` and `llms-install.md`.
- Six skills (`reply-to-google-reviews`, `optimize-google-business-profile`, `write-gbp-post`, `gbp-weekly-report`, `local-rank-audit`, `competitor-watch`), installable with the skills CLI, as a Claude Code plugin and as a Codex plugin.

## 2026-09-25

- Reach runs its own OAuth 2.1 authorization server for MCP clients, with PKCE and dynamic client registration. No API key, client ID or secret is needed.

## 2026-09-21

- Setup guide at `/guides/connect-ai` and agent-readable setup at `/llms.txt`.

## 1.0.0 (2026-09-21)

- First release of the Reach MCP server: 14 tools for a Google Business Profile (reviews, replies, posts, profile edits, photos, local rankings, performance, leads and recommendations) and 3 prompts (`optimise_my_profile`, `review_my_visibility`, `handle_my_reviews`).
