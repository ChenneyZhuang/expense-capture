# Compatibility / 兼容性

One SKILL.md, no scripts, no dependencies beyond what the agent already has. 安装即用，无脚本依赖。

| Agent | Install | Notes |
|---|---|---|
| Claude Code | `npx skills add ChenneyZhuang/expense-capture` or clone to `~/.claude/skills/expense-capture/` | model-invoked via description triggers; verified against the skills CLI |
| Codex CLI | `npx skills add ChenneyZhuang/expense-capture` | same SKILL.md, no changes needed |
| Cursor | `npx skills add ChenneyZhuang/expense-capture` | loads as project rules/skill per CLI mapping |
| OpenCode / Windsurf / Gemini CLI / Cline / AMP / GitHub Copilot | `npx skills add ChenneyZhuang/expense-capture` | 75+ agents supported by the skills CLI |
| DSH | clone repo, `dsh plugin --profile <name> add link:<repo>` | `dsh.bundle` manifest included |
| Hermes | `cp -r` into `~/.hermes/profiles/<profile>/skills/expense-capture/` | loads via description; verify with `hermes skills` |

What the skill needs from the agent runtime: file read/write access and (where noted) web search or shell. Every capability degrades honestly — if the runtime lacks a tool, the skill's integrity rules require labeling the result `unverified` rather than guessing.

对 agent 运行时的要求：文件读写，部分场景需搜索或 shell。运行时缺工具时，skill 的诚信规则要求如实标注 `unverified` 而不是猜。


