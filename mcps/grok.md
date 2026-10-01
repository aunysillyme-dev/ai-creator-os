---
title: grok MCP
description: "Custom MCP that gives Claude native access to X search and Grok's web search mid-session. Solves the X-link-reading problem most third-party tools fail at because X blocks scraping."
tags: [mcp, grok, x-search, custom-mcp, web-search]
---

# grok MCP 🔍

the grok MCP gives Claude native access to X search and Grok's
web search mid-session. when a trending post, topic, or X link
comes up, Claude searches or reads it directly without leaving
the conversation — no tab switching, no copy-pasting results back in.

**repo:** [aunysillyme-dev/ai-creator-os](https://github.com/aunysillyme-dev/ai-creator-os)

---

## tools

| tool | what it does |
|------|-------------|
| `x_search` | searches X natively — returns recent posts, engagement, authors |
| `grok_web_search` | web search via Grok — current information with sources |
| `grok_chat` | Grok chat for second-model opinion or large context |

---

## reading X links

one of the most practical uses of this MCP is reading X posts
by URL. X actively blocks scraping and most third-party tools
can't reliably fetch post content from an x.com link.

`x_search` works around this — because Grok is native to X,
it can surface post content, thread text, and engagement data
that other tools can't access. when you drop an x.com link
mid-session, Claude uses `x_search` to read it directly.

this is the reason a dedicated "link reader" MCP isn't needed
for X content — the grok MCP already handles it.

---

## setup

```bash
cd ai-creator-os/mcps/grok
npm install
```

you'll need a Grok API key. add it to your environment:

```bash
export GROK_API_KEY=your_key_here
```

then add to Claude Desktop config:

```json
"grok": {
  "command": "node",
  "args": ["/path/to/ai-creator-os/mcps/grok/index.js"],
  "env": {
    "GROK_API_KEY": "your_key_here"
  }
}
```

---

## how it's used in this system

every content session includes a research pass across active
content pillars. Claude uses `x_search` to find what's trending
in AI, X strategy, personal branding, and human psychology —
then filters results against voice and pillars before writing
anything.

`grok_web_search` handles deeper research — stats, articles,
and context for factual grounding when writing educational content.

`grok_chat` is used when a second model perspective is useful
or when a document is too large for the current context.

the pillar filter rule: trending ≠ relevant.
Claude only surfaces results that map to active content pillars.
