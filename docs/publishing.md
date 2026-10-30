# 发布到 GitHub

建议仓库名：`contextual-translate`。作者与 MIT 版权人：wwj。

## 发布内容

上传本项目中的 `SKILL.md`、`agents/`、`README.md`、`README.zh-CN.md`、`README.ja.md`、`docs/`、`examples/`、`LICENSE` 和 `.gitignore`。无需上传工作目录、虚拟环境、个人 `AGENTS.md`、备份、会话记录或本机安装目录。

`README.md` 为英文首页，GitHub 打开仓库时会自动展示，无需另外设置文档语言。中文与日文分别在 `README.zh-CN.md`、`README.ja.md`，三个版本顶部均提供语言切换链接。

项目只有技能规则、示例和文档，没有构建步骤或独立 API 密钥配置。

## 网页发布

1. 在 GitHub 创建 `contextual-translate` 仓库，按分享意图选择公开或私有。
2. 如自动生成过 README 或 LICENSE，与项目文件核对合并，避免两套说明或冲突许可。
3. 上传本项目目录内文件，保留 `agents/`、`docs/`、`examples/` 层级；仓库根目录直接包含 `SKILL.md`。
4. 包含隐藏文件 `.gitignore`。上传页不会把 ZIP 自动展开为源码，使用发布包时先解压。
5. 将 README 与安装文档的 `YOUR_GITHUB_NAME` 替换为实际所有者；仓库改名时也替换名称。
6. 从新仓库安装并按测试文档验证，再创建版本标签。

## Git 发布

在本项目目录初始化并审阅上传内容：

```sh
git init -b main
git add SKILL.md agents README.md README.zh-CN.md README.ja.md docs examples LICENSE .gitignore
git diff --cached --stat
git diff --cached
```

配置真实提交身份，作者署名使用 `wwj`，邮箱用自己的 GitHub 提交邮箱。确认内容后：

```sh
git commit -m "docs: prepare contextual-translate for release"
git remote add origin https://github.com/YOUR_GITHUB_NAME/contextual-translate.git
git push -u origin main
```

替换所有者后执行，需要已有仓库及身份验证。若远端已有初始化提交，先获取并合并，不强制覆盖。

## 首版说明

仓库简介建议：

> 结合上下文的多语言 Q/N 翻译、母语表达与轻量纠错技能，可用于 Codex 及支持 Agent Skills 的工具。

主题标签建议：`agent-skills`、`codex`、`translation`、`language-learning`、`grammar-correction`。

首版可用 `v0.1.0`，实际创建标签后再推荐按该标签安装；建议标签不代表当前已经发布。

说明中应保留验证边界：当前在 Codex 会话观察到预期效果，其他工具已核对官方结构支持但尚未实测。
