# AUDIT_BRIEF.md — ai-creator-os frontmatter scaffold pass

## Task bundle
**Purpose.** Adversarially audit two commits that add YAML frontmatter
(`title`/`description`/`tags`) to `TOOLS.md` and `mcps/README.md` in the
`ai-creator-os` repo, ahead of pushing to `origin/main`. AUN-1241 follow-on:
the repo's `llms.txt` promises every content file carries this frontmatter;
this closes the last two files that lacked it.
**Denied actions.** Read-only audit. Do NOT edit any file, do NOT run git
commands that mutate state (commit, push, reset), do NOT touch any repo
other than this one, do NOT propose or apply fixes yourself — findings go
back to Claude, who owns any fix.
**Report contract.** For each of the two changed files: state whether the
frontmatter block is well-formed YAML, whether it introduces any secret/path/
account-id/email, and whether the diff touches anything outside the
frontmatter block. List findings by severity; state explicitly if nothing
was found.

## Runtime
Static markdown documentation in a public GitHub repo (aunysillyme-dev/ai-creator-os). No
application code, no server, no runtime. The change is a YAML frontmatter block
prepended to two markdown files. Nothing executes this frontmatter today; it is
metadata for future tooling (the repo's own `llms.txt` promises every content
file carries `title`, `description`, `tags`).

## Threat model
None in the traditional sense (no auth, no secrets, no user input, no network
surface). The only real risks are: (1) a value in the frontmatter that leaks
something it shouldn't (a local path, an account id, a secret), (2) frontmatter
that breaks YAML parsing for any downstream tool that reads it, (3) an edit
that accidentally touches the file body instead of only adding frontmatter.

## Callers / consumers
- Any static-site generator or doc indexer that later parses this repo's
  frontmatter (none currently wired, per repo inspection).
- Humans browsing the repo on GitHub.

## What's already verified
- `git diff --numstat` on both changed files (`TOOLS.md`, `mcps/README.md`)
  shows 6/6 insertions, 0 deletions each — confirms the edit only added lines
  at the top of the file, no body text was touched.
- Parsed both frontmatter blocks with `PyYAML` in a sandboxed codecalc run:
  both parse as valid YAML maps containing `title`, `description`, `tags`,
  and `tags` length is within the 3-7 range required by the task spec.
- Grepped the two added blocks for an em dash and the word "bottleneck":
  zero matches (repo/voice rule).
- Read both files in full before writing their descriptions, so the
  description text matches what the file actually contains (affiliate
  disclosure table, model routing table, MCP catalog with hosted/local split).
- Grepped for `/Users/`, email addresses, and secret-shaped strings in the
  added lines: none present — values are only tags and doc summaries.

## What I want attacked
1. Does either added frontmatter block contain anything that should never
   ship: a literal secret, an internal-only path, an email, a hostname,
   an account id, or a token?
2. Is the YAML actually well-formed for every consumer (not just PyYAML) —
   e.g. does the inline `tags: [a, b, c]` array syntax used here ever trip
   up a stricter parser given the specific tag strings chosen?
3. Did the edit change, reorder, or delete any body content in either file
   (only additive frontmatter should exist)?
4. Are the `title`/`description` values accurate to the file content, or do
   they overclaim/underclaim what the file covers?

## Design decisions (with reasoning)
- Used the compact inline-array frontmatter style already established by
  other files in this repo (e.g. the existing Claude.md file uses
  `tags: [claude, anthropic, ai-assistant, mcp, chief-of-staff]`), rather
  than the block-list style used in the sibling repo `claude-os` — this
  repo's own convention is the inline style, confirmed by grepping existing
  `tags:` blocks before writing.
- Reused existing tag vocabulary from the repo (`mcp`, `claude`,
  `cloudflare-workers`, `model-routing`, `ai-tools`) instead of inventing new
  terms, so the tag namespace stays consistent across files.
- Did not touch `START-HERE.md`, `VISUAL-GUIDE.md`, or any nested `README.md`
  — out of scope per the task's denied-actions list (README.md family stays
  bare) and per this repo's own already-complete frontmatter on unrelated
  files.

## Full diff under audit
Note: this checkout lives at a session-scoped scratchpad path, not under
`~/Claude Code`, so it is not reachable from a fresh shell. The complete
`git diff HEAD~1 HEAD -- TOOLS.md mcps/README.md` is pasted below verbatim —
audit from this text; do not assume any other content exists in these files
beyond what the diff context lines show.

```diff
diff --git a/TOOLS.md b/TOOLS.md
index 431a20e..0799d20 100644
--- a/TOOLS.md
+++ b/TOOLS.md
@@ -1,3 +1,9 @@
+---
+title: Tools
+description: "Auny's full AI and creator tool stack as of September 2026: the core Claude/Obsidian/MCP/Cloudflare system, the models she routes between, content and social tools, image/design/video tools, music tools, project and product tools, the automation layer that runs without her, and the custom MCP servers she built, with affiliate disclosures."
+tags: [ai-tools, mcp, claude, model-routing, cloudflare-workers]
+---
+
 # tools 🛠️
 ### my full stack: what i use, what it does, what you get
 
diff --git a/mcps/README.md b/mcps/README.md
index 0ec43b0..6904cb4 100644
--- a/mcps/README.md
+++ b/mcps/README.md
@@ -1,3 +1,9 @@
+---
+title: Custom MCPs
+description: "Catalog of every custom MCP server built for the ai-creator-os stack: which run hosted on Cloudflare Workers versus locally, what each one does, the one-deployment-per-server rule, when to build a custom MCP versus connect a hosted one, and how each server doubles as a sellable product."
+tags: [mcp, custom-mcp, cloudflare-workers, claude-code, model-context-protocol]
+---
+
 # custom MCPs 🔌
 
 these are MCP servers built specifically for this system.
```

## ROUND 1 — 2026-09-20

Auditor: Codex, `gpt-6-astra`, effort `high`, 105.7s. Commit `320c37fd` against parent `9e9e32c`.

**Verdict: PASS. No findings at any severity.**

| Check | Result |
|---|---|
| YAML validity | Passed independent Ruby Psych 3.1.0 safe parsing, unique-key, required-field and string-type checks |
| Secrets, internal paths, hostnames, account ids, emails, tokens | None introduced in either file |
| Body integrity | Both files add only the frontmatter block and one blank separator. Each original body is byte-for-byte identical |
| Title and description accuracy | Both accurately summarize their body |
| Tags | Five per block, inline arrays, no ambiguous values, no YAML portability issue |

Codex noted one limit honestly: arbitrary future consumer behaviour cannot be guaranteed. Accepted, not actionable.

**Dispositions: nothing to fix.**

Independently verified by me before the push, against the artifact rather than the report: `git diff origin/main..HEAD --numstat` shows `6 0 TOOLS.md` and `6 0 mcps/README.md`. Zero deleted lines in the whole diff, which is what proves no body was touched.

One codex round only, per Auny's ruling 2026-09-10. A second pass was started in error and stopped.
