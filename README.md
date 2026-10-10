# Reach by Locus: Google Business Profile skills

Agent Skills for managing Google Business Profile through the Reach remote MCP server.

## Install skills

```sh
npx skills add LocusIntelligence-DauAgency/reach-skills
```

The skills CLI lets you choose your agent. See [official CLI documentation](https://skills.sh/docs/cli). This repository includes instructions and remote client manifests only.

## Connect Reach

- URL: `https://reach.locus-intelligence.com/api/mcp`
- Transport: Streamable HTTP
- Authentication: browser OAuth using your own Reach account; no API key
- Connect your Google Business Profile in Reach for connected account data and profile management. Features depend on account access and connection state.

See [SETUP.md](SETUP.md) and the [Reach MCP setup guide](https://reach.locus-intelligence.com/google-business-profile-mcp).

## Skills

Read-only skills never change anything. Skills that write show the exact change first and act only on the owner's explicit yes.

**Reviews and customers**

- [reply-to-google-reviews](skills/reply-to-google-reviews/SKILL.md): answer unanswered reviews
- [review-insights](skills/review-insights/SKILL.md): themes across all reviews (read-only)
- [review-request-kit](skills/review-request-kit/SKILL.md): review link and request message for customers (sends nothing)
- [lead-follow-up](skills/lead-follow-up/SKILL.md): new leads and booking requests with follow-up drafts (read-only)

**Profile**

- [optimize-google-business-profile](skills/optimize-google-business-profile/SKILL.md): find and fix profile gaps
- [categories-and-service-area](skills/categories-and-service-area/SKILL.md): additional categories and service area
- [holiday-hours](skills/holiday-hours/SKILL.md): special hours for upcoming holidays
- [gbp-photo-refresh](skills/gbp-photo-refresh/SKILL.md): add and retire profile photos
- [add-local-business-schema](skills/add-local-business-schema/SKILL.md): LocalBusiness structured data for your website, from the live profile

**Posts**

- [write-gbp-post](skills/write-gbp-post/SKILL.md): one post, offer or event
- [gbp-post-calendar](skills/gbp-post-calendar/SKILL.md): plan and schedule a month of posts

**Search visibility**

- [local-rank-audit](skills/local-rank-audit/SKILL.md): Google Maps and local search rankings
- [keyword-picker](skills/keyword-picker/SKILL.md): choose which keywords to track
- [not-showing-on-maps](skills/not-showing-on-maps/SKILL.md): diagnose a missing Maps listing (read-only)
- [competitor-watch](skills/competitor-watch/SKILL.md): nearby rivals and how they changed (read-only)

**Reporting and planning**

- [gbp-weekly-report](skills/gbp-weekly-report/SKILL.md): this week against last week (read-only)
- [multi-location-report](skills/multi-location-report/SKILL.md): one table across every location (read-only)
- [growth-plan](skills/growth-plan/SKILL.md): work through Reach's growth recommendations

## Cursor

The root `.cursor-plugin/plugin.json` and `mcp.json` form a Cursor plugin. For a local installation, place the repository in a local Cursor plugin directory according to the [official plugin reference](https://cursor.com/docs/reference/plugins). Authenticate Reach in MCP settings.

## Grok Build

Load this repository with `grok --plugin-dir /absolute/path/to/reach-skills`. The .grok-plugin/plugin.json manifest, skills/ and .mcp.json use Grok Build's documented plugin layout. Open `/mcps` to authenticate Reach. Alternatively merge grok-config.toml.example into your Grok configuration and install the skill folders separately; choose one setup to avoid duplicate servers. See [Grok Build plugin docs](https://docs.x.ai/build/features/skills-plugins-marketplaces) and [MCP docs](https://docs.x.ai/build/features/mcp-servers).

## MCP Registry

server.json describes the hosted remote MCP endpoint. It contains no installable server package or backend source. Registry publication requires separate namespace authentication.

## Approval and evidence

Read data before proposing changes. Publishing review replies, posts or profile updates requires approval of the exact text or before-and-after change. Keyword tracking requires explicit approval too. Respect Reach permissions, tool limitations and Google connection requirements. Never invent performance, rankings, business details or missing data.

## License

[MIT](LICENSE) covers these skills, manifests and setup documentation. The original Growthnomics Technologies Private Limited copyright notice is preserved. The hosted Reach service, backend code, customer data, trademarks and third-party content are outside this distribution license. Reach by Locus is product branding, not a declaration resolving the publisher's legal entity.
