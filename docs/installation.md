# Installation, updates, and removal

## Ask your agent to install it

Start with the [one-message installation request in the README](../README.md). Give your agent the repository URL and ask it to follow the project instructions, install into a supported location, and configure use on every turn. Specify the target language, learning-note language, and answer language separately.

This is a request for your agent to carry out, not a bundled installer. If network access, file permissions, or settings prevent completion, the agent should explain the remaining manual steps. It should report the installation path, scope, and reload requirements.

The shell commands below are for macOS/Linux. On Windows, place the full project folder in the appropriate user skill directory, for example `%USERPROFILE%\.agents\skills\contextual-translate`. See the [compatibility guide](compatibility.md) for each tool's supported locations.

## Personal installation

For tools with documented support for the shared personal skills directory, including Codex, Cursor, VS Code Copilot, and OpenCode, install with Git:

```sh
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/ringsaul/contextual-translate.git \
  "$HOME/.agents/skills/contextual-translate"
```

The destination must not already exist. For an existing installation, follow the update instructions below. After installation, check that `~/.agents/skills/contextual-translate/SKILL.md` exists.

For Claude Code, use its personal skills directory instead:

```sh
mkdir -p "$HOME/.claude/skills"
git clone https://github.com/ringsaul/contextual-translate.git \
  "$HOME/.claude/skills/contextual-translate"
```

Choose the installation appropriate to your tool. Do not install the same skill into multiple directories scanned by that tool.

Without Git, download and extract the repository ZIP, rename the extracted project folder to `contextual-translate`, and place it in the appropriate directory. Avoid an extra nested `contextual-translate-main` folder.

## Project installation

A personal installation is visible across local projects. A project installation can be shared with a team through its working repository. If you already have the shared personal installation above, run these commands from the destination project's root:

```sh
mkdir -p .agents/skills/contextual-translate/agents
cp "$HOME/.agents/skills/contextual-translate/SKILL.md" \
  .agents/skills/contextual-translate/SKILL.md
cp "$HOME/.agents/skills/contextual-translate/LICENSE" \
  .agents/skills/contextual-translate/LICENSE
cp "$HOME/.agents/skills/contextual-translate/agents/openai.yaml" \
  .agents/skills/contextual-translate/agents/openai.yaml
```

Check the destination for your own changes before copying. This copies only the skill instructions, Codex metadata, and license, without an embedded `.git` directory. If you plan to use only the project installation, move the personal copy out of discovery after verifying the project copy, to avoid duplicate discovery.

For Claude Code, use the same structure under `.claude/skills/contextual-translate/`. See the compatibility guide for other locations. Windows users can copy these files manually.

## Configure use on every turn

Installation, automatic selection, and a requirement to use the skill on every turn are separate steps. `agents/openai.yaml` allows implicit invocation in Codex; other tools may not read it, and automatic selection does not guarantee use on every turn.

| Tool | Where to add the rule | Example |
| --- | --- | --- |
| Codex | Effective personal or project `AGENTS.md` | [Personal rule](../examples/codex-global.md) |
| Claude Code | `~/.claude/CLAUDE.md` | [Personal rule](../examples/claude-global.md) |
| Cursor | Project `.cursor/rules/contextual-translate.mdc`; use equivalent User Rules for personal scope | [Project rule](../examples/cursor-project.mdc) |
| VS Code Copilot | Project `.github/copilot-instructions.md` | [Project rule](../examples/copilot-project.md) |
| OpenCode | `~/.config/opencode/AGENTS.md` | [Personal rule](../examples/opencode-global.md) |

Each example assumes a particular installation location. Adjust its `SKILL.md` path if you choose another location. Use relative paths for project copies rather than committing a local user directory.

The files in `examples/` are templates: leaving them in this repository does not activate them. Append only the marked block to an existing rule file; do not replace the whole file or add the same block twice.

For Codex, the default global configuration directory is `~/.codex`; use the configured directory when `CODEX_HOME` is customized. A nonempty `AGENTS.override.md` takes precedence over `AGENTS.md` in the same directory. Update the file that is actually loaded, and keep the skill's block outside sections managed by other tools.

Specify your preferred languages in the same effective rule block. For example, ask your agent to add: “Translate my requests into Spanish; keep learning notes and answers in English.” The skill's fallback for notes and answers is Simplified Chinese unless overridden.

Reload skills and rules. Existing conversations may need a restart before testing. Per-turn instructions still yield to explicit user requests, strict output formats, and tool permissions.

## Updates

For a Git installation, inspect local changes before updating:

```sh
git -C "$HOME/.agents/skills/contextual-translate" status --short
git -C "$HOME/.agents/skills/contextual-translate" pull --ff-only
```

Adjust the path for other installation locations. Preserve local changes and resolve conflicts rather than using a forced reset. Reload the skill afterward.

ZIP and copied installations have no `.git` directory, so `git pull` does not apply. Back up the old directory, replace it with the updated files, and preserve your customizations. Project copies need their own update; updating a personal installation does not synchronize copies automatically.

A rule block that only references the skill usually needs no change for routine updates. If a new version changes configuration, compare its examples with your own marked block.

## Pause

To skip one turn, say “Skip translation this time.” To pause later turns, say “Pause translation from now on.” Explicitly ask to resume when needed.

For a persistent pause or removal, move the skill out of discovery and remove its rule block. Removing only the rule still allows the model to select the skill; removing only the skill leaves a rule pointing to a missing file.

## Uninstall

Remove both the skill and its rules. This example moves the skill out of discovery while retaining a backup:

```sh
skill_path="$HOME/.agents/skills/contextual-translate"
disabled_path="$HOME/.agents/skills-disabled/contextual-translate-$(date +%Y%m%d-%H%M%S)"
mkdir -p "$HOME/.agents/skills-disabled"
mv "$skill_path" "$disabled_path"
```

Adjust `skill_path` for the actual tool or project installation. Handle each copy separately. A shared personal installation may be used by multiple tools, all of which will lose access to that copy when it is moved.

Edit the `AGENTS.md`, `CLAUDE.md`, Cursor User Rules, or Copilot instructions where you added the rule. Remove only the skill's block, including these markers:

```text
<!-- contextual-translate-every-turn:start -->
<!-- contextual-translate-every-turn:end -->
```

If Cursor uses a dedicated `.cursor/rules/contextual-translate.mdc`, move that file out of `.cursor/rules/` too. Preserve unrelated settings.

Restart or open a new conversation and send an ordinary question. The skill should no longer add Q/N automatically. Existing conversations may retain earlier user preferences; explicitly cancel them if needed.

Delete the backup only when you no longer need it; deletion permanently removes local customizations. To restore, first check that the original destination has no new installation, then move the backup back and restore the rule block.

## Troubleshooting

**Skill not found:** Check the directory nesting, `SKILL.md` filename, frontmatter name, and supported locations, then reload the skill list. The skill name should be `contextual-translate`.

**Explicit invocation works, but not every turn:** Check whether the persistent rule is actually loaded, its path is valid, and no closer rule or explicit user instruction overrides it.

**Duplicate skills:** Check personal and project installations, including multiple compatible directories scanned by the tool.

**Works locally, but not remotely:** Personal skills do not necessarily transfer to another machine. Share a project copy with the team or synchronize it using the tool's supported mechanism.
