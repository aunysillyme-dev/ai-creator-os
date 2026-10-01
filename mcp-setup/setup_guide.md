---
title: MCP Setup Guide
description: "How to connect tools to Claude via MCP. Covers both the custom MCPs built for ai-creator-os (auny-vault, grok, codex, remotion) and the hosted MCP integrations available in Claude Desktop."
tags: [mcp, setup-guide, claude-desktop, configuration]
---

# MCP setup guide
### connecting your tools to Claude

MCP (Model Context Protocol) is what turns Claude from a chat
interface into an operating system. this guide covers two things:
connecting the custom MCPs built for this system, and connecting
the hosted MCP integrations available through Claude Desktop.

---

## custom MCPs (built for this system)

these are MCP servers built specifically for ai-creator-os.
each one lives in the `/mcps` folder with its own setup guide.

| MCP | what it does | setup |
|-----|-------------|-------|
| [auny-vault](../mcps/auny-vault.md) | read + write your Obsidian vault | [setup →](../mcps/auny-vault.md) |
| [grok](../mcps/grok.md) | X search + web research mid-session | [setup →](../mcps/grok.md) |
| [codex](../mcps/codex.md) | code review + Codex chat | [setup →](../mcps/codex.md) |
| [remotion](../mcps/remotion.md) | programmatic video generation | [setup →](../mcps/remotion.md) |

start with **auny-vault** — it's the one that makes everything
else in this system work.

---

## what you'll need for all custom MCPs

- Claude Desktop ([download](https://claude.ai/download))
- Node.js ([nodejs.org](https://nodejs.org))
- this repo cloned locally:

```bash
git clone https://github.com/aunysillyme-dev/ai-creator-os.git
```

---

## how Claude Desktop MCP config works

all custom MCPs are added to the same config file in
Claude Desktop:

**mac:** `~/Library/Application Support/Claude/claude_desktop_config.json`
**windows:** `%APPDATA%\Claude\claude_desktop_config.json`

the config follows this pattern:

```json
{
  "mcpServers": {
    "server-name": {
      "command": "node",
      "args": ["/absolute/path/to/server/index.js"],
      "env": {
        "API_KEY": "your-key-if-needed"
      }
    }
  }
}
```

add each MCP as a new entry under `mcpServers`. restart Claude
Desktop after every config change.

---

## hosted MCP integrations (no code required)

for tools that have official MCP connectors, connect them
through Claude Desktop settings — no code needed.

**Claude Desktop → Settings → Integrations**

available hosted connectors include:
- Linear (project management)
- Typefully (social scheduling)
- Beehiiv (newsletter)
- Google Drive
- Gmail
- Google Calendar
- Calendly
- Canva
- Vercel
- Stripe
- and more — full list at [claude.ai/integrations](https://claude.ai/integrations)

---

## testing a connection

once an MCP is added and Claude Desktop is restarted, test it:

> "list the files in my vault root"
(for auny-vault)

> "search X for what's trending in AI tools right now"
(for grok)

if it returns real data, it's working.

---

## mobile access (iPhone)

Claude on iPhone can connect to hosted MCP servers — remote
servers with a public URL. the auny-vault-hosted server
(a Cloudflare Worker backed by a GitHub-synced vault) is how
vault access works on iPhone in this system.

to set up your own hosted vault server, you'll need:
- a Cloudflare account (free tier works)
- a private GitHub repo that your vault syncs to
- a Worker that reads from that repo and exposes the vault tools

the architecture is documented in [mcps/auny-vault.md](../mcps/auny-vault.md).
