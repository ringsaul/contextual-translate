# Compatibility and official sources

Documentation checked: 2026-10-30. This page distinguishes documented support for a skill layout from actual testing of this project. Availability may vary by version, agent or harness, permissions, and organization policy.

## Compatibility table

Each directory below must contain `contextual-translate/SKILL.md`.

| Tool | Personal skill locations | Project skill locations | Invocation and per-turn rules | Project verification |
| --- | --- | --- | --- | --- |
| Codex | `~/.agents/skills/` | `.agents/skills/` | `$contextual-translate`; effective personal or project `AGENTS.md` | Observed in the current local Codex conversation |
| Claude Code | `~/.claude/skills/` | `.claude/skills/` | `/contextual-translate`; personal `~/.claude/CLAUDE.md` or project `CLAUDE.md` | Documented structure; not tested in this project |
| Cursor | `~/.agents/skills/` or `~/.cursor/skills/` | `.agents/skills/` or `.cursor/skills/` | `/contextual-translate`; project `.mdc` with `alwaysApply: true`, or personal User Rules | Documented structure; not tested in this project |
| VS Code Copilot Agent | `~/.agents/skills/` or `~/.copilot/skills/` | `.agents/skills/` or `.github/skills/` | `/contextual-translate`; project `.github/copilot-instructions.md`, subject to harness support | Documented structure; not tested in this project |
| OpenCode | `~/.agents/skills/` or `~/.config/opencode/skills/` | `.agents/skills/` or `.opencode/skills/` | Ask the agent to load the skill; personal or project `AGENTS.md` | Documented structure; not tested in this project |

Avoid duplicate installations in directories scanned by the same tool. Installing for one tool does not automatically make the skill available to a tool that scans different locations.

## Differences and limits

The portable core is the `name`, `description`, and Markdown body in `SKILL.md`. The skill has no required tool-specific script, SDK, or permission configuration. The MIT license permits adapting and redistributing it for other tools.

`agents/openai.yaml` is Codex metadata. Do not assume other tools read its policy. Configure discovery, automatic selection, and per-turn rules for each tool separately.

Availability for automatic selection does not guarantee use on every turn. Persistent rules express the requirement but are not execution hooks. Translation, corrections, and formatting also depend on the model.

Cursor's documentation notes that personal skills are not automatically copied to cloud agents, remote SSH sessions, or self-hosted workers. Check other tools' remote environments separately as well; local behavior does not establish cloud compatibility.

## Tools without native skill support

If a tool accepts custom system instructions or persistent rules, you can manually copy the body of `SKILL.md`, excluding its frontmatter, into a supported configuration entry. Simply placing a file in the working directory may have no effect.

This is a manual adaptation, without native discovery, invocation commands, or a guarantee of per-turn use. Verify it with the [manual test cases](testing.md) rather than claiming native support.

## Official sources

These sources were checked for the documented installation layouts. Compatibility can change with tool versions.

- OpenAI Docs: [Codex Skills](https://developers.openai.com/codex/skills/), [AGENTS.md](https://developers.openai.com/codex/guides/agents-md/).
- Anthropic: [Claude Code Skills](https://code.claude.com/docs/en/skills), [CLAUDE.md and instruction loading](https://code.claude.com/docs/en/memory).
- Cursor: [Skills](https://cursor.com/docs/context/skills), [Rules](https://cursor.com/docs/context/rules).
- VS Code: [Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills), [Custom Instructions](https://code.visualstudio.com/docs/copilot/customization/custom-instructions).
- OpenCode: [Skills](https://opencode.ai/docs/skills/), [Rules](https://opencode.ai/docs/rules/).
