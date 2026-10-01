# Security policy

This repository is documentation only: markdown files describing a creator's AI operating system built on Obsidian, Claude, and MCP. It has no runtime, no server, no package to install, and no dependencies of its own.

If a doc here recommends a practice that turns out unsafe (a credential-handling pattern, an insecure MCP setup step), report it the same way as a security issue. A vulnerability in a custom MCP this repo documents (see `mcps/`) belongs on that MCP's own repository, for example [grok-mcp-server](https://github.com/aunysillyme-dev/grok-mcp-server). A vulnerability in a third-party SaaS tool this repo documents (Suno, DistroKid, Beehiiv, Typefully, and similar) belongs with that vendor's own security-reporting channel, not with this org.

## Reporting a vulnerability

Use GitHub's private vulnerability reporting on this repository (Security tab, "Report a vulnerability"). That opens a private advisory rather than a public issue.

You will get an acknowledgement within 7 days.

## Scope

In scope: the accuracy and safety of the documentation itself. Out of scope: any tool, MCP server, or third-party service this documentation describes; report those to their own repositories.
