# 安装、更新与卸载

## 先让 Agent 帮你安装

优先使用 [README 中的一条消息安装方式](../README.zh-CN.md)。将仓库地址交给 Agent，让它读取项目说明，按当前工具支持的位置安装，并配置每轮规则。需要指定默认翻译语言时，同时说明目标语言、解释语言和正式回答语言。

这是一条交给 Agent 执行的请求，不是项目自带的一键安装程序。网络、文件权限或配置入口受限时，Agent 应说明剩余手动步骤；完成后报告安装位置、生效范围和重载方式。以下命令供需要手动安装、检查或维护时使用。

以下 shell 命令适用于 macOS/Linux。Windows 可将完整项目文件夹放到对应用户技能目录，例如 `%USERPROFILE%\.agents\skills\contextual-translate`。各工具实际支持的位置见[兼容性表](compatibility.md)。

## 个人安装

适用于当前官方文档支持共享个人目录的 Codex、Cursor、VS Code Copilot 和 OpenCode。首次安装需要 Git：

```sh
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/YOUR_GITHUB_NAME/contextual-translate.git \
  "$HOME/.agents/skills/contextual-translate"
```

替换 `YOUR_GITHUB_NAME` 为实际所有者；仓库改名时也修改 URL。目标目录必须不存在，已有安装按更新章节处理。安装后应能看到 `~/.agents/skills/contextual-translate/SKILL.md`。

Claude Code 使用其官方个人技能目录：

```sh
mkdir -p "$HOME/.claude/skills"
git clone https://github.com/YOUR_GITHUB_NAME/contextual-translate.git \
  "$HOME/.claude/skills/contextual-translate"
```

只有选择 Claude Code 安装方式时才执行后一组。同一工具可能发现多个兼容目录，不要在它同时扫描的位置重复安装同名技能。

不使用 Git 时，可下载仓库 ZIP、解压后把完整项目文件夹改名为 `contextual-translate`，放入对应目录。不要额外嵌套一层 `contextual-translate-main`。

## 项目安装

个人安装对本机多个项目可见，项目安装便于团队随业务项目共享。已完成上述共享个人安装时，可在目标业务项目根目录执行以下首次复制命令：

```sh
mkdir -p .agents/skills/contextual-translate/agents
cp "$HOME/.agents/skills/contextual-translate/SKILL.md" \
  .agents/skills/contextual-translate/SKILL.md
cp "$HOME/.agents/skills/contextual-translate/LICENSE" \
  .agents/skills/contextual-translate/LICENSE
cp "$HOME/.agents/skills/contextual-translate/agents/openai.yaml" \
  .agents/skills/contextual-translate/agents/openai.yaml
```

先确认目标位置没有自己的修改。复制只包含运行规则、Codex 元数据与许可证，不带嵌套 `.git`。若准备长期采用项目安装，验证后移出个人副本，避免同名重复发现。

Claude Code 可按同样结构复制到 `.claude/skills/contextual-translate/`；其他位置见兼容性表。Windows 用户可手动完成相同复制。

## 每轮配置

安装、允许自动选择、要求每轮使用是不同步骤。`agents/openai.yaml` 允许 Codex 自动选择，但其他工具不一定读取它，自动选择也不保证每轮执行。

| 工具 | 配置方式 | 示例 |
| --- | --- | --- |
| Codex | 追加到有效的全局或项目 `AGENTS.md` | [个人安装示例](../examples/codex-global.md) |
| Claude Code | 追加到 `~/.claude/CLAUDE.md` | [个人安装示例](../examples/claude-global.md) |
| Cursor | 保存为项目 `.cursor/rules/contextual-translate.mdc`；全局可把等价指令加入 User Rules | [项目规则](../examples/cursor-project.mdc) |
| VS Code Copilot | 追加到项目 `.github/copilot-instructions.md` | [项目规则](../examples/copilot-project.md) |
| OpenCode | 追加到 `~/.config/opencode/AGENTS.md` | [个人安装示例](../examples/opencode-global.md) |

示例路径分别对应个人或项目安装，换用另一种方式时改成实际 `SKILL.md` 路径。项目副本优先使用相对路径，不要提交本机用户目录。

这些是待复制的配置示例，仅放在本仓库 `examples/` 中不会自动生效。已有规则文件只追加对应标记区块，不要整文件覆盖或重复添加。

Codex 默认全局目录为 `~/.codex`，自定义 `CODEX_HOME` 时使用对应目录。有非空 `AGENTS.override.md` 时优先读取它，不能只改未被加载的 `AGENTS.md`。新增区块放在其他工具托管区之外。

重新加载技能与规则；已有会话可能需重启后再测。每轮规则仍受用户本轮明确要求、严格格式和工具权限约束。

## 更新

Git 安装先查看本地修改，再更新：

```sh
git -C "$HOME/.agents/skills/contextual-translate" status --short
git -C "$HOME/.agents/skills/contextual-translate" pull --ff-only
```

其他安装方式请替换路径。有本地修改或冲突时先保存改动，不使用强制重置。更新后重新加载技能。

ZIP 或复制安装没有 `.git`，不能 `git pull`；先备份旧目录，再用新的完整文件替换并保留个性化修改。项目级副本也要单独更新，个人安装更新不会自动同步到已复制文件。

常驻规则只引用技能时，通常无需每次改规则。新版改变配置格式时，再核对新示例与自己的标记区块。

## 暂停

临时跳过一轮，直接说“这次跳过翻译”。暂停后续轮次可说“接下来暂停翻译”，恢复时明确要求恢复。

长期暂停或卸载，应移出技能并删除其常驻规则。只移除规则，技能仍可能被模型选中；只移出技能而保留规则，会让规则指向不存在的文件。

## 卸载

卸载同时处理技能与规则。以下示例移出发现目录并保留备份，不立即删除个性化修改：

```sh
skill_path="$HOME/.agents/skills/contextual-translate"
disabled_path="$HOME/.agents/skills-disabled/contextual-translate-$(date +%Y%m%d-%H%M%S)"
mkdir -p "$HOME/.agents/skills-disabled"
mv "$skill_path" "$disabled_path"
```

其他工具或项目安装必须把 `skill_path` 改成实际目录，有多份副本时分别处理。共享个人目录可能被多个工具使用，移出后它们都会失去该副本。

然后编辑曾经配置的 `AGENTS.md`、`CLAUDE.md`、Cursor User Rules 或 Copilot instructions，只删除以下标记之间及标记本身的本技能区块：

```text
<!-- contextual-translate-every-turn:start -->
<!-- contextual-translate-every-turn:end -->
```

Cursor 若使用专用 `.cursor/rules/contextual-translate.mdc`，将该文件一起移出 `.cursor/rules/`。保留其他配置。

重启或新开会话验证：普通问题不应再自动附加本技能 Q/N。已有会话可能仍记得此前用户要求，必要时明确取消偏好。

需要彻底删除时，确认不再需要备份后删除 `disabled_path` 对应文件夹；这会永久删除本地修改，卸载本身不要求立即清理备份。恢复时把备份移回原安装位置，并重新加入规则，先确认原路径没有新安装。

## 常见问题

**找不到技能**：检查目录层级、`SKILL.md` 文件名、frontmatter 名称与工具支持位置，重新加载技能列表。名称应为 `contextual-translate`。

**显式调用有效，每轮不生效**：确认常驻规则确实被读取、路径有效，且未被更近的规则或用户明确要求覆盖。

**重复技能**：检查个人与项目目录是否同时安装，以及工具是否扫描了多个兼容路径。

**本机有效，远程无效**：个人技能通常不会自动传到另一台机器。将项目技能提交到业务仓库，或按工具支持的方式同步到对应环境。
