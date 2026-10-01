---
title: auny-vault MCP
description: "Custom MCP that connects Claude directly to an Obsidian vault. Claude reads, writes, searches, and updates vault files mid-session. The core infrastructure that makes ai-creator-os work."
tags: [mcp, obsidian, vault, custom-mcp, ai-creator-os]
---

# auny-vault MCP 🗂️

the auny-vault MCP connects Claude directly to your Obsidian
vault. Claude can read, write, search, and update vault files
mid-session — no copy-pasting, no leaving the conversation.

this is the core infrastructure that makes ai-creator-os work.
every session protocol, every domain routing decision, every
output written back to the vault — it all runs through this MCP.

**repo:** [aunysillyme-dev/ai-creator-os](https://github.com/aunysillyme-dev/ai-creator-os)

---

## tools

| tool | what it does |
|------|-------------|
| `read_file` | reads the full contents of any vault file |
| `write_file` | creates or overwrites a file |
| `append_to_file` | adds content to the end of a file |
| `patch_file` | find and replace within a file |
| `list_files` | lists files in a folder |
| `search_files` | semantic search across the vault |
| `delete_file` | deletes a file |

---

## two versions

**local (Mac / Windows)**
runs as a Node.js server on your machine. reads your vault
directly from the filesystem. fastest option. works offline.
use this as your primary setup on desktop.

**hosted (remote server)**
the same 7 tools, deployed as a remote server.
vault syncs automatically to a remote source so the hosted
version stays current.
use this on iPhone or any device without local filesystem access.

---

## setup

see [mcp-setup/setup_guide.md](../mcp-setup/setup_guide.md) for full installation steps.

quick version:

```bash
git clone https://github.com/aunysillyme-dev/ai-creator-os.git
cd ai-creator-os/mcps/auny-vault
npm install
```

then add to Claude Desktop config:

```json
"auny-vault": {
  "command": "node",
  "args": ["/path/to/ai-creator-os/mcps/auny-vault/index.js"]
}
```

---

## how it's used in this system

Claude reads these files at the start of every session:
- session log → what changed recently
- master index → full vault map
- domain files → whatever's relevant to the current task

Claude writes to the vault:
- session logs after every session
- new idea cards when an idea surfaces
- workflow docs when a workflow is built
- updated files when something changes

the vault is only useful as a memory layer if Claude can
write back to it. read-only access is half the system.
