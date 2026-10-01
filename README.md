# ai-creator-os 🕷️
### an AI operating system built on Obsidian + Claude + MCP

**v2 — september 2026.** [what changed since v1](./CHANGELOG.md)

by [@AunySillyMe](https://x.com/AunySillyMe) · [aunysillyme.com](https://aunysillyme.com)

---

## what this is

most people use Claude as a chatbot.

this is different.

ai-creator-os is a full operating system for your creative and business life — built inside Obsidian, connected to Claude via MCP, and designed so that every session starts with context and ends with output.

Claude reads your vault before every task. writes to it after. nothing has to be re-explained between sessions. every workflow you build is simultaneously a tool, a content piece, and a product.

i run my entire creator business through this system:
- content strategy and daily batch writing
- music releases and distribution workflows
- consulting, client management, and service delivery
- novel writing (yes, really)
- monetization tracking and product development

this repo documents how i built it and how you can build your own.

**what v2 changed.** v1 was one Claude window reading a local vault. since
then the vault moved behind a server so it reaches every device and every
scheduled job, the custom MCP count went from four to around fifteen, a build
surface got added (Claude Code, which is where all of it was written), and
tasks now route across several models instead of one. two things v1 told you
were wrong within weeks, and both are corrected in place rather than deleted,
because the correction is the useful part.

---

## the core concept

Claude has no memory between sessions by default.

Projects help. Custom instructions help. But neither gives Claude the *full picture.*

your vault does.

```
Obsidian vault  ←→  MCP connection  ←→  Claude
     ↑                                      ↓
  you write                           Claude reads,
  your life                           writes, acts
```

every file in your vault becomes context Claude can read mid-session. every workflow output gets written back. the vault is a living document — it grows with you.

---

## what's in this repo

```
ai-creator-os/
│
├── README.md                    ← you are here
├── TOOLS.md                     ← full stack + affiliate links
│
├── /vault-structure
│   ├── folder-map.md            ← full folder structure
│   └── naming-conventions.md   ← how to name files Claude can find
│
├── /session-protocols
│   ├── 01_session_start.md      ← how every session begins
│   ├── 02_domain_routing.md     ← which files Claude reads for which tasks
│   └── 03_content_session.md   ← content-specific session flow
│
├── /templates
│   ├── idea_card.md             ← capture monetizable ideas fast
│   ├── session_log.md           ← what changed, every session
│   ├── workflow_doc.md          ← document any workflow you build
│   └── monetization_tracker.md ← track every revenue angle
│
├── /mcps
│   ├── README.md                ← every server i run, and what changed
│   ├── auny-vault.md            ← vault read/write MCP
│   ├── grok.md                  ← X search + read X links + web research
│   ├── codex.md                 ← correction: Codex is a CLI lane, not an MCP
│   └── remotion.md              ← retired, and what replaced it
│
├── /content-types
│   ├── written.md               ← posts, threads, newsletters
│   ├── art.md                   ← image generation workflows
│   ├── music.md                 ← music creation + release pipeline
│   └── video.md                 ← music videos, marketing videos
│
├── /workflows
│   ├── music-release.md         ← Suno → master → distribute end to end
│   ├── music-video.md           ← Grok Imagine Agent → full music video
│   └── content-batching.md      ← full day of content in one session
│
├── /stack
│   ├── claude-code.md           ← the build surface (new in v2)
│   ├── cloudflare.md            ← where the servers live (new in v2)
│   ├── model-routing.md         ← which model gets which job (new in v2)
│   └── ...                      ← claude, obsidian, mcp, suno, and the rest
│
├── /mcp-setup
│   └── setup_guide.md           ← connect all MCPs to Claude Desktop
│
└── /content-system
    ├── content_pillars.md       ← how to build a pillar system
    └── formats_reference.md     ← post formats that actually work
```

---

## quick start

**step 1 — install Obsidian**
free. [obsidian.md](https://obsidian.md). mac, windows, ios, android.

**step 2 — clone this repo**
```bash
git clone https://github.com/aunysillyme-dev/ai-creator-os.git
```

**step 3 — set up your vault structure**
copy the folder structure from [vault-structure/folder-map.md](./vault-structure/folder-map.md) into your Obsidian vault.

**step 4 — connect Obsidian to Claude via MCP**
full guide in [mcp-setup/setup_guide.md](./mcp-setup/setup_guide.md)

**step 5 — run your first session**
start with [session-protocols/01_session_start.md](./session-protocols/01_session_start.md) — this is the file Claude reads first, every time.

**step 6 — use it. update it.**
the system only works if you actually use it. update your vault after every session. it gets smarter as you go.

**step 7 — when you outgrow one window**
once the vault is carrying real weight, the next two moves are
[Claude Code](./stack/claude-code.md) to build your own tools and
[hosting them](./stack/cloudflare.md) so they work everywhere. neither is
required to start.

---

## want help setting this up?

i offer a 1-hour **Claude for Creators** call where we build your system together — your vault, your protocols, your workflows.

→ [book a call](https://buymeacoffee.com/aunysillyme/e/531498) · $100 · members get $25 off

---

## tools i use

full stack with links in [TOOLS.md](./TOOLS.md)

---

## license

[MIT](./LICENSE) — use it, fork it, build on it.

---

## follow the build

i document everything i build publicly.

- **X** → [@AunySillyMe](https://x.com/AunySillyMe)
- **newsletter** → [Explained Without Fluff](https://explained-without-fluff.beehiiv.com)
- **music** → [Spotify](https://open.spotify.com/artist/2HSQl7HB2BksGuCU8f39hI)

---

*built in public. learning as i go. sharing it all. 🧡*
