[🇺🇸 English](#english) · [🇨🇳 中文](#chinese)

---

<a name="english"></a>

# antalpha-ai-docs

**Auto-generate and sync Antalpha Skills MCP documentation from source code.**

Every time the MCP server tools change, run this skill to regenerate the technical reference and setup guide — no manual editing required.

## What It Does

| Step | Action |
|------|--------|
| 1 | Scans all `*.tools.ts` source files in the `antalpha-skills` monorepo |
| 2 | Generates `docs/mcp-documentation.md` — full tool reference (params, types, returns) |
| 3 | Regenerates `antalpha-ai-setup/SKILL.md` — user-facing setup guide |
| 4 | Commits and pushes: opens a PR for the team repo, direct push for the setup guide |

> Source code is the single source of truth. Changelogs and human-written docs are never used.

## Install

```bash
openclaw skill install https://github.com/AntalphaAI/antalpha-ai-docs
```

## Usage

Trigger this skill manually after making changes to the `antalpha-skills` repository:

```
Sync the Antalpha MCP documentation
```

```
Regenerate the MCP tool reference from the latest source code
```

```
Update antalpha-ai-setup SKILL.md after today's changes
```

## Output Files

| File | Location | Description |
|------|----------|-------------|
| Technical Reference | `~/antalpha-com/antalpha-skills/docs/mcp-documentation.md` | Full tool reference — parameters, types, returns |
| Setup Guide | `~/.openclaw/workspace/skills/antalpha-ai-setup/SKILL.md` | User-facing MCP connection + setup instructions |

## Requirements

- Access to `~/antalpha-com/antalpha-skills` (local clone)
- Git configured with push access to both repos
- OpenClaw agent runtime

## Notes

- Always syncs from `main` before creating a docs branch
- Shows a diff summary before pushing — no silent commits
- Skips empty tool files gracefully
- Version bump is optional if no meaningful changes are detected

---

<a name="chinese"></a>

# antalpha-ai-docs

**自动从源码生成并同步 Antalpha Skills MCP 文档。**

每次 MCP Server 工具有变更，运行此 Skill 即可自动重新生成技术参考文档和安装指南，无需手动编辑。

## 功能概览

| 步骤 | 操作 |
|------|------|
| 1 | 扫描 `antalpha-skills` monorepo 中所有 `*.tools.ts` 源文件 |
| 2 | 生成 `docs/mcp-documentation.md` — 完整工具参考（参数、类型、返回值） |
| 3 | 重新生成 `antalpha-ai-setup/SKILL.md` — 面向用户的安装配置指南 |
| 4 | 提交推送：团队仓库开 PR，安装指南仓库直接推送 |

> 源代码是唯一权威来源，不使用 Changelog 或人工撰写的文档。

## 安装

```bash
openclaw skill install https://github.com/AntalphaAI/antalpha-ai-docs
```

## 使用方式

在 `antalpha-skills` 仓库有代码变更后，手动触发此 Skill：

```
同步 Antalpha MCP 文档
```

```
从最新源码重新生成 MCP 工具参考文档
```

```
今天的改动已完成，更新 antalpha-ai-setup SKILL.md
```

## 输出文件

| 文件 | 路径 | 说明 |
|------|------|------|
| 技术参考文档 | `~/antalpha-com/antalpha-skills/docs/mcp-documentation.md` | 完整工具参考——参数、类型、返回值 |
| 安装配置指南 | `~/.openclaw/workspace/skills/antalpha-ai-setup/SKILL.md` | 面向用户的 MCP 连接与配置说明 |

## 环境要求

- 本地已克隆 `~/antalpha-com/antalpha-skills`
- Git 已配置两个仓库的推送权限
- OpenClaw Agent 运行时环境

## 注意事项

- 创建 docs 分支前始终从 `main` 同步最新代码
- 推送前展示 diff 摘要，无静默提交
- 空工具文件自动跳过，不中断流程
- 若无实质性变更，版本号可不更新
