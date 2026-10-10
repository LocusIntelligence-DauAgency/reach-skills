---
name: multi-location-report
description: Read-only multi-location report for agencies and chains on Google Business Profile (GMB, Google My Business) with the Reach MCP server. Compares every connected location over the same date range in one fixed table, adds review stats and rank summary, the top 3 movers and the locations that need attention. Never changes anything. Use when someone asks for a report across all locations, a client or branch comparison, or which locations need work.
license: MIT
---

# Multi-location report

One table for every location, the same shape each time. This skill only reads.

## Setup

This skill needs the Reach MCP server connected in your AI client:

- Server URL: `https://reach.locus-intelligence.com/api/mcp` (remote, Streamable HTTP, OAuth sign-in, no API key)
- Setup for Claude, ChatGPT, Claude Code, Codex, Cursor, VS Code and others: [Reach setup guide](https://reach.locus-intelligence.com/google-business-profile-mcp)

Performance and review data need each Google Business Profile connected in Reach.

## Steps

1. **List locations.** Call `get_account` with `include: ["locations", "connection"]`. Take each entry in `locations.locations`, and read its `connectionStatus` from `connection`.
2. **Skip what cannot be read.** A location whose `connectionStatus` is not `active`, or that is paused, gets a row "skipped: <status>" and a note to reconnect Google in Reach. Public listings (`locations.listings`) have no Google data: list them as "listing only".
3. **Dates.** Default: the 7 days ending yesterday against the 7 days before. Use the range the owner gives instead. State both ranges in the report and use the same ones for every location.
4. **Per location, one at a time** (not in parallel, to respect rate limits):
   - `get_performance` for each range.
   - `get_listing` with `sections: ["reviews"]` and `reviewFilter: { startDate, endDate }` for the current range. Count unanswered reviews.
   - `get_visibility` with `sections: ["summary"]` for tracked keyword rank.
5. **On `rate_limited`,** tell the owner `retryAfterSeconds`, stop, and report the locations done so far. With many locations, offer to continue in batches of 5.
6. **Report** in the shape below, using only returned numbers.

## Report shape

```text
<Account name>: <start> to <end> (compared with <start> to <end>)

| Location | Views | Calls | Directions | Website clicks | New reviews (avg) | Unanswered | Best tracked rank |
| <name> | <n> (<+/-n>) | ... | ... | ... | <n> (<rating>) | <n> | <rank or "none tracked"> |

Top 3 movers: <location, metric, change>, ...
Needs attention: <disconnected, unanswered reviews, no tracked keywords>
Skipped: <location and reason>
Data notes: <each limitations message with its link>
```

Pick movers by the largest absolute change in views. Show a percent only when the earlier number is not zero. Write "not available" for a missing metric.

## Safety

- Read-only. Never edit, reply or publish from this skill.
- Read `limitations` per location before saying there is no data; relay each message and link.
- On `listing_only`, record the location as "listing only" and continue.
- Never estimate, project or invent figures.
- If the owner asks for something Reach cannot do (white-label PDF, scheduled reports), offer to send it with `request_feature`.
