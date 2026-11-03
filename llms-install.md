# Install Reach: Google Business Profile MCP server

<!-- Generated from the Reach server by mcp:public. Do not edit by hand. -->

MCP server URL: https://reach.locus-intelligence.com/api/mcp
Transport: Streamable HTTP (no SSE, no local install, no API key).
Authentication: OAuth 2.1 with PKCE. Clients register themselves automatically; no client ID, secret or API key needs to be configured. The user signs in with their own Reach account in a browser.

## Instructions for AI assistants setting this up

Your user wants to connect Reach. Use the steps for the client you are running in. Never ask the user for a password, token or API key; sign-in always happens on the Reach sign-in page in the user's browser.

The sign-in step opens a browser, so it must run in an interactive terminal. If your shell is non-interactive (no TTY), run the add command yourself, then ask the user to run the login command in their own terminal.

### Claude Code (you can do this yourself)

1. Run: `claude mcp add --transport http reach https://reach.locus-intelligence.com/api/mcp`
   Add `--scope user` before `reach` to make it available in every project.
2. Ask the user to type `/mcp` in Claude Code, select `reach` and sign in with their Reach account in the browser window that opens.
3. `claude mcp list` shows `reach` as connected when sign-in is complete. "Needs authentication" means step 2 is not done.

### Claude (claude.ai web, Claude Desktop, Claude mobile)

You cannot add a connector for the user. Tell them to:
1. Open Customize, then Connectors.
2. Click +, then Add custom connector.
3. Enter the name `Reach` and the URL `https://reach.locus-intelligence.com/api/mcp`. Leave Advanced settings empty. Click Add.
4. Click Connect next to Reach and sign in with their Reach account.
5. In a chat, click +, open Connectors and turn on Reach.
Custom connectors are available to every Claude user. On Team and Enterprise, an owner adds it in Organization settings, then each member clicks Connect.

### ChatGPT

You cannot add an app for the user. Tell them to:
1. In ChatGPT on the web, open Settings, then Apps, then Advanced settings, and turn on Developer mode.
2. Go back to Apps and click Create.
3. Enter the name `Reach`, the URL `https://reach.locus-intelligence.com/api/mcp`, and choose OAuth authentication.
4. Sign in with their Reach account when asked, then click Create.
5. In a chat, choose Reach from the tools menu or mention it by name.
Developer mode is a ChatGPT setting; a workspace admin may need to allow it first.

### Cursor

1. Add this to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project), merging with any existing `mcpServers`:
   `{ "mcpServers": { "reach": { "url": "https://reach.locus-intelligence.com/api/mcp" } } }`
2. Restart Cursor, open Customize, then MCPs, and follow the sign-in prompt for reach. With the Cursor CLI: `agent mcp login reach`.

### Google Antigravity

1. Add this to `~/.gemini/config/mcp_config.json` (or `.agents/mcp_config.json` in a workspace), merging with any existing `mcpServers`. Antigravity reads `serverUrl`, not `url`:
   `{ "mcpServers": { "reach": { "serverUrl": "https://reach.locus-intelligence.com/api/mcp" } } }`
2. Open Agent Settings, then Customizations, click Authenticate next to reach, sign in with their Reach account, then paste the code Antigravity shows back into the settings panel and click Submit.

### VS Code (GitHub Copilot agent mode)

1. Run: `code --add-mcp '{"name":"reach","type":"http","url":"https://reach.locus-intelligence.com/api/mcp"}'`
2. Start the server from the MCP view and sign in when VS Code opens the browser.

### Windsurf

1. In Cascade, open the MCP settings and edit the raw config file (`mcp_config.json`), merging with any existing `mcpServers`. Windsurf reads `serverUrl` for a remote server:
   `{ "mcpServers": { "reach": { "serverUrl": "https://reach.locus-intelligence.com/api/mcp" } } }`
2. Save, refresh the MCP servers, and sign in with their Reach account when Windsurf asks.

### Cline

1. Open the MCP Servers panel, then Remote Servers. Enter the name `reach`, the URL `https://reach.locus-intelligence.com/api/mcp`, choose Streamable HTTP and click Add Server. Or add this to `cline_mcp_settings.json`:
   `{ "mcpServers": { "reach": { "type": "streamableHttp", "url": "https://reach.locus-intelligence.com/api/mcp" } } }`
2. On the Installed tab, click Authenticate under reach and sign in with their Reach account in the browser.

### Codex

1. Run: `codex mcp add reach --url https://reach.locus-intelligence.com/api/mcp`
2. Run: `codex mcp login reach` and sign in in the browser.

### Hermes Agent

1. Run: `hermes mcp add reach --url https://reach.locus-intelligence.com/api/mcp --auth oauth`
2. Run: `hermes mcp login reach` in an interactive terminal and sign in in the browser.
3. Start a new Hermes session so the Reach tools load.

### Other MCP clients

Configure a remote (Streamable HTTP) MCP server named `reach` with the URL `https://reach.locus-intelligence.com/api/mcp` and no headers or API key. The client discovers the sign-in server from the 401 response and registers itself. Example for clients that read an `mcpServers` JSON file:

```json
{ "mcpServers": { "reach": { "type": "http", "url": "https://reach.locus-intelligence.com/api/mcp" } } }
```

### Before you start

The user needs a Reach account (sign up free at https://reach.locus-intelligence.com). The assistant sees full data only after the user connects their Google Business Profile in Reach; otherwise it can read the public listing only. Account limits apply exactly as in the Reach app; when a limit stops a call, the tool result says what happened and where the owner manages their account.
