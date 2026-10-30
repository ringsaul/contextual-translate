# 兼容性与官方依据

核对日期：2026-10-30。此页区分“官方支持加载这种结构”和“本项目实际运行测试”。版本、所选 agent/harness、权限与企业策略可能改变可用性。

## 兼容性表

各技能路径后都需包含 `contextual-translate/SKILL.md`。

| 工具 | 个人技能位置 | 项目技能位置 | 调用与每轮规则 | 本项目验证 |
| --- | --- | --- | --- | --- |
| Codex | `~/.agents/skills/` | `.agents/skills/` | `$contextual-translate`；有效的全局或项目 `AGENTS.md` | 当前本机 Codex 会话已验证 |
| Claude Code | `~/.claude/skills/` | `.claude/skills/` | `/contextual-translate`；个人 `~/.claude/CLAUDE.md` 或项目 `CLAUDE.md` | 官方结构支持，尚未实测 |
| Cursor | `~/.agents/skills/` 或 `~/.cursor/skills/` | `.agents/skills/` 或 `.cursor/skills/` | `/contextual-translate`；项目 `alwaysApply: true` 的 `.mdc`，个人 User Rules | 官方结构支持，尚未实测 |
| VS Code Copilot Agent | `~/.agents/skills/` 或 `~/.copilot/skills/` | `.agents/skills/` 或 `.github/skills/` | `/contextual-translate`；项目 `.github/copilot-instructions.md`，需所选 harness 支持 | 官方结构支持，尚未实测 |
| OpenCode | `~/.agents/skills/` 或 `~/.config/opencode/skills/` | `.agents/skills/` 或 `.opencode/skills/` | 在对话中要求使用，由 agent 加载；全局或项目 `AGENTS.md` | 官方结构支持，尚未实测 |

避免在同一工具扫描的多个位置重复安装。工具只扫描某个目录时，也不会因为另一工具已安装就自动拥有它。

## 差异与边界

可移植核心是 `SKILL.md` 的 `name`、`description` 与 Markdown 正文。本项目没有绑定某个工具的必需脚本、SDK 或权限配置。MIT 许可允许按工具需要修改分发。

`agents/openai.yaml` 属于 Codex 元数据，不应假定其他工具读取其策略。各工具的发现、自动选择和每轮规则需要分别设置。

技能可按需选择不保证每轮调用。常驻规则能明确要求，但不等于确定执行的程序钩子；翻译、纠错和格式遵循也受模型能力影响。

Cursor 官方文档说明，本机个人技能不会自动复制到云端 agent、远程 SSH 会话或自托管 worker。其他工具的远程执行环境也需单独确认，不能将本机效果当作云端验收。

## 非原生工具

若工具允许自定义系统指令或长期规则，可将 `SKILL.md` frontmatter 后的正文复制到它实际支持的入口。只把文件放在工作目录不一定生效。

这种方式是手动迁移，不提供技能发现、调用命令或每轮使用保证，需按[测试用例](testing.md)验证，不能标记为原生支持。

## 官方依据

以下为本次实际查阅的官方页面。兼容性会随版本变化，发布新版本前建议重新核对。

- OpenAI Docs：[Codex Skills](https://developers.openai.com/codex/skills/)、[AGENTS.md](https://developers.openai.com/codex/guides/agents-md/)。
- Anthropic：[Claude Code Skills](https://code.claude.com/docs/en/skills)、[CLAUDE.md 与指令加载](https://code.claude.com/docs/en/memory)。
- Cursor：[Skills](https://cursor.com/docs/context/skills)、[Rules](https://cursor.com/docs/context/rules)。
- VS Code：[Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills)、[Custom Instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)。
- OpenCode：[Skills](https://opencode.ai/docs/skills/)、[Rules](https://opencode.ai/docs/rules/)。
