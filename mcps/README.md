---
title: Custom MCPs
description: "Catalog of every custom MCP server built for the ai-creator-os stack: which run hosted on Cloudflare Workers versus locally, what each one does, the one-deployment-per-server rule, when to build a custom MCP versus connect a hosted one, and how each server doubles as a sellable product."
tags: [mcp, custom-mcp, cloudflare-workers, claude-code, model-context-protocol]
---

# custom MCPs 🔌

these are MCP servers built specifically for this system.
each one is a self-contained tool that plugs into Claude and
runs mid-session without leaving the conversation.

**updated september 2026.** v1 of this file listed four. two of them were
wrong by the time anyone read it, and the count is now around fifteen. what
follows is what actually runs.

---

## what changed since v1

| v1 said | what is true now |
|---|---|
| `codex` is an MCP | it never stayed one. **Codex is a CLI lane**, not an MCP server. see [codex.md](./codex.md) |
| `remotion` is live | **retired.** superseded by an HTML-to-video pipeline. see [remotion.md](./remotion.md) |
| `auny-vault` is a local server | **hosted on Cloudflare** now, so it answers from every device and from scheduled jobs |
| `grok` is a local server | **hosted**, and it is now the metered fallback. day to day X research goes through the Grok CLI, which costs nothing |

---

## hosted (Cloudflare Workers)

these run as Workers, so they answer from the desktop app, the phone, and
jobs that run on a schedule with nobody watching.

| MCP | what it does |
|-----|-------------|
| [auny-vault](./auny-vault.md) | the vault door. read, write, and hybrid semantic search across every note |
| [grok](./grok.md) | Grok chat, image, and X/web search. metered, so it is the fallback rather than the default |
| x | the X API. posts, DMs, lists, bookmarks, analytics on my own account |
| x-ads | the X Ads API. campaigns and stats |
| google | Drive, Docs and Sheets, full read and write |
| google-tasks | Google Tasks, including recurring ones |
| clients-hub | a second vault, walled off from the first, for client work |
| calc | every number. exact and symbolic maths, percentages, stats, unit conversion |
| mirror | cross-posts Threads to Facebook and Instagram |

## local

| MCP | what it does |
|-----|-------------|
| obsidian-tc | plugin-native vault operations: Dataview, Templater, Excalidraw, OCR, bulk edits |
| codecalc | runs and verifies code in a sandbox across 30-odd languages |
| plur | memory. corrections and preferences that persist across sessions |
| session-relay | message a Claude Code session on another machine and get its reply |

---

## the rule i wish i had known in v1

**one deployment per server.** i once had a local copy and a hosted copy of
the same MCP. i rotated a key in one of them. the other kept running on the
stale key and the failure looked like the vendor's fault for a day.

if a server is hosted, delete the local copy. if it is local, do not deploy it.

---

## when to build a custom MCP vs connect a hosted one

**build a custom MCP when:**
- the tool you need doesn't have an official MCP connector
- you need capability available across every session, not just once
- you want to own the tool surface area completely

**connect a hosted MCP when:**
- the vendor has an official connector (Linear, Typefully, Beehiiv, Stripe, and more)
- the capability is standard enough that a generic connector covers it

the vendor connectors are set up in Claude's settings under Connectors. no
code required.

---

## build them with Claude Code

every server listed above was written in Claude Code. i had no prior coding
background when i started. the loop that works:

1. describe what the tool should do, in plain language
2. let Claude Code write it and deploy it to Cloudflare
3. hand the code to a **different** model for an adversarial audit
4. fix what the audit finds, and keep a test for each fix

step 3 matters more than it sounds. a model reviewing its own work agrees
with itself. one of my public servers shipped with an auth hole for two
months because nobody with fresh eyes read it.

---

## monetization note

each custom MCP is also a sellable product. the code +
a setup guide + a short walkthrough video = a listing.
every MCP built here has that path available.

one of them is already public and deployable in a few commands:
[aunysillyme-dev/grok-mcp-server](https://github.com/aunysillyme-dev/grok-mcp-server).
