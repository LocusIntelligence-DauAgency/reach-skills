---
name: review-insights
description: Analyze the Google reviews on a Google Business Profile (GMB, Google My Business) with the Reach MCP server. Reads the reviews and reports praise themes, complaints, services and staff mentioned, language mix and rating trend, with verbatim quotes, then suggests description lines, services to list and post ideas. Read-only. Use when someone asks what customers say about them, for a review analysis, or for ideas drawn from their reviews.
license: MIT
---

# Review insights

Turn a business's reviews into themes and concrete next steps. This skill never writes.

## Setup

This skill needs the Reach MCP server connected in your AI client:

- Server URL: `https://reach.locus-intelligence.com/api/mcp` (remote, Streamable HTTP, OAuth sign-in, no API key)
- Setup for Claude, ChatGPT, Claude Code, Codex, Cursor, VS Code and others: [Reach setup guide](https://reach.locus-intelligence.com/google-business-profile-mcp)


## Steps

1. **Pick the location.** Call `get_account`. If there is more than one location, ask which one. If its `connectionStatus` is not `active`, tell the owner to reconnect Google in Reach and stop.
2. **Read the reviews.** Call `get_listing` with `sections: ["reviews"]` and `limit: 100`. Read `reviews.stats` for totals and rating distribution. The list covers the last 90 days unless you set `reviewFilter.startDate` and `endDate`; there is no page cursor, so read older reviews by calling again with earlier date windows. `reviewFilter` also takes `sentiment` (`POS`, `NEG`, `NEU`), `replyStatus` and `search` (up to 120 characters). Read `limitations` before saying there is no data.
3. **Find the themes.** Group what reviewers wrote: praise, complaints, services and staff named, and the languages used. Count only what the data shows, and say how many reviews you read and over which dates.
4. **Check the trend.** Compare average rating and volume across two date windows if the data allows. If it does not, say so.
5. **Write the report** in this fixed format:

   ```text
   Scope: <n> reviews, <date range>, rating <avg>
   Praise: <theme> (<count>) - "<verbatim quote>"
   Complaints: <theme> (<count>) - "<verbatim quote>"
   Services and staff mentioned: <list with counts>
   Languages: <language: count>
   Rating trend: <direction, with the numbers>
   Unanswered: <count>
   ```

6. **Suggest next steps**, each tied to a theme: a line for the business description, services to add to the listing, post ideas. Hand off by skill name: `optimize-google-business-profile`, `write-gbp-post`, `reply-to-google-reviews`, `gbp-post-calendar`.

Free tool: [review reply inbox](https://reach.locus-intelligence.com/tools/review-reply-inbox).

## Safety

- Read-only. This skill calls no write tool.
- Quote reviews verbatim only. Never paraphrase inside quote marks, invent a review, or guess a reviewer's name or details.
- Say how many reviews the report covers. Do not generalize beyond them.
- Stop if the location's `connectionStatus` is not `active`.
- Read `limitations` before saying there is no data.
- On `rate_limited`, give `retryAfterSeconds` and do not retry right away. On an upgrade refusal, say what was blocked and which plan (`requiredPlan`) allows it, point to Plans in Reach, and stop. On `listing_only`, relay the message and `connectUrl`, and stop.
- Talk about usage in Credits, never money.
- If the owner asks for something Reach cannot do, offer to send it to the Reach team with `request_feature`: write the request in their words, show it, and send only after they confirm the wording.
