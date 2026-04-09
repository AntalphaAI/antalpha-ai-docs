---
name: antalpha-ai-docs
description: >
  Generate and update Antalpha Skills MCP documentation by reading source code.
  Use when you need to sync the MCP tool reference and setup guide after code changes.
version: 1.0.0
author: antalpha
---

# Antalpha AI Docs Generator

Generate and update two documentation files for the Antalpha Skills MCP server by reading the source code directly.

## Workflow

Execute the following steps in order. Do not skip or reorder steps.

---

## Step 1 — Scan Source Code

Read the source files at these locations:

```
~/antalpha-com/antalpha-skills/libs/skills/*/src/tools/*.tools.ts
```

Also read the repository root files for context:

```
~/antalpha-com/antalpha-skills/AGENTS.md
~/antalpha-com/antalpha-skills/README.md
```

For each `*.tools.ts` file, extract:

- Tool name (the `name` field in `registerTool`)
- Parameters (name, type, required, description)
- Return value description
- Category (DEX, Smart Money, Polymarket, Hyperliquid, DeFi, Settlement, Utility)

---

## Step 2 — Generate Technical Reference

Create the technical documentation at:

```
~/antalpha-com/antalpha-skills/docs/mcp-documentation.md
```

**Format reference:** Follow the structure of `/home/admin/antalpha-skills-mcp-documentation.md`.

The document must include these sections:

1. **Overview** — Server description, transport, protocol
2. **Quick Start** — Server URL table, first request prompts
3. **Capabilities** — Category table (DEX Swaps, Smart Money, Polymarket, Hyperliquid, DeFi Analytics, Settlement Intelligence, Multi-Chain Assets)
4. **Getting Started** — Register agent, verify connectivity
5. **Tool Reference** — One section per category, each tool with:
   - Tool name as `####` heading
   - One-line description
   - Parameters table (Parameter, Type, Required, Description)
   - Returns description
   - Notes (if any)
6. **Security & Authentication** — Agent auth, zero custody, rate limiting, error handling
7. **Example Prompts** — Natural language prompt examples

**Critical rule:** Extract parameter types, required flags, and descriptions **directly from the source code**. Do not rely on CHANGELOG, release notes, or human-written summaries.

---

## Step 3 — Generate Setup Guide

Create the setup guide at:

```
/home/admin/.openclaw/workspace/skills/antalpha-ai-setup/SKILL.md
```

**Format reference:** Follow the format of the current `antalpha-ai-setup/SKILL.md`.

The document must include these sections:

1. **Frontmatter** — `name: antalpha-ai-setup`, short description (2 sentences max), version, author, homepage
2. **Overview** — 1-paragraph server description with tool count
3. **Quick Install** — `clawhub install antalpha-ai-setup` command
4. **Prerequisites** — Supported clients list
5. **Step 1 — Add the MCP Server** — Configuration for each client:
   - Claude.ai (web), Claude Code, Codex, Claude Desktop/Cursor/Windsurf, Gemini CLI, OpenCode, OpenClaw
6. **Step 2 — Register Your Agent** — Registration steps + auth mode explanation
7. **Step 3 — Verify** — `test-ping` instruction
8. **Step 4 — Get Your First Result** — Prompt examples table with tool names
9. **Available Tools** — Compact table (Tool | Description), all tools listed
10. **Troubleshooting** — Common issues and solutions

**Critical rules:**
- OpenClaw config must use direct HTTP URL (no npx mcp-remote)
- Description field in frontmatter: max 2 sentences
- Wallet address placeholders: `0x\<your_wallet_address\>` (not bare `0x...`)

---

## Step 4 — Git Commit

After generating both files, commit and push to their respective repositories.

### Technical Reference (antalpha-skills)

```bash
cd ~/antalpha-com/antalpha-skills
git add docs/mcp-documentation.md
git commit -m "docs: auto-update MCP technical reference from source code"
git push origin main
```

### Setup Guide (antalpha-ai-setup)

```bash
cd /home/admin/.openclaw/workspace/skills/antalpha-ai-setup
git add SKILL.md
git commit -m "docs: auto-update setup guide from source code"
git push origin main
```

---

## Important Notes

- **Always read source code.** Do not assume tools are unchanged based on past knowledge. Re-read every `*.tools.ts` file on each run.
- **Do not use changelogs or human-written docs as a source of truth.** Only the source code is authoritative.
- **Preserve the format of the reference documents.** The technical reference and setup guide must follow the exact structure shown in the reference files.
- **Version bump is optional.** If no meaningful changes were found, you may skip the commit or make a minor note.
- **Handle missing files gracefully.** If a tool file is empty or has no registered tools, skip that section in the output.
- **Report before committing.** After scanning and generating, show the diff summary before pushing. If you encounter errors, report them and do not push.

---

## Reference File Locations

| Reference | Path |
|-----------|------|
| Technical doc format | `/home/admin/antalpha-skills-mcp-documentation.md` |
| Setup guide format | `/home/admin/.openclaw/workspace/skills/antalpha-ai-setup/SKILL.md` |
| Source code | `~/antalpha-com/antalpha-skills/libs/skills/*/src/tools/*.tools.ts` |
| Repo context | `~/antalpha-com/antalpha-skills/AGENTS.md` |

---

**Trigger:** Run this skill manually when you want to refresh the documentation after code changes to the antalpha-skills repository.
