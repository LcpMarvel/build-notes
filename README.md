# Build Notes

[English](README.en.md)

这个 Codex 插件用于分享你在 Codex 里的发现、构建过程和发布成果。在有上下文的原任务里说一句「把这个发到 X」，原任务就会开子代理整理真实经历和可公开的事实，交给固定的 X 内容编辑台核对、发布并记录链接。你不需要复制对话或重写 README。

## 工作方式

```text
原任务里的发现、构建记录或发布成果
        ↓  用户说“把这个发到 X”
原任务的子代理整理经历、事实和草稿
        ↓  Codex 跨任务转交
X 内容编辑台核对账号、文案和重复帖子
        ↓
X 帖子链接 + 本地发布记录
```

插件包含两个技能：[`x-handoff`](skills/x-handoff/SKILL.md) 负责在原任务交接上下文；[`x-editor`](skills/x-editor/SKILL.md) 负责在编辑台写稿、发布和记录。技能按受众选择语言，并区分已经验证的事实与尚未验证的说法。

## 安装

本仓库根目录包含插件清单 `plugin.json`、Codex 兼容清单 `.codex-plugin/plugin.json`、技能目录 `skills/`，以及仓库 marketplace 清单 `.agents/plugins/marketplace.json`。当前仓库 [LcpMarvel/build-notes](https://github.com/LcpMarvel/build-notes) 为私有。要试用本地工作区，在这个目录中运行：

```bash
codex plugin marketplace add .
codex plugin add build-notes@build-notes
```

第一条把本地仓库加入插件来源，第二条安装插件；这两条已在当前工作区验证。仓库公开后，远程安装命令是：

```bash
codex plugin marketplace add LcpMarvel/build-notes
codex plugin add build-notes@build-notes
```

安装和刷新流程见 [OpenAI 插件文档](https://developers.openai.com/plugins/build/plugins)。

## 首次设置

1. 在 Codex 创建并置顶一个长期任务，标题使用 **`X 内容编辑台`** 或 **`X Content Desk`**。这一步只做一次。
2. 在编辑台告诉 Codex：目标 X 账号、中文/英文偏好，以及发布记录应放在哪里。可直接说：「这个任务管理我的 @账号；中文项目用中文，面向全球的项目用英文；发布链接记在当前工作区。」
3. 在可用的浏览器里登录目标 X 账号。插件不读取或保存密码、Cookie、API Key。

原任务需要能使用子代理和 Codex 任务工具；发布需要可用的浏览器控制能力。如果这些能力缺失，技能会留下草稿并说明缺少什么。

## 一句话使用

在**有对应上下文的原任务**里发送：

> 把这个发到 X。

这表示请求发布当前这件具体内容，可以是一个发现、一次构建经历或一个完成的项目。原任务会转交相关事实、经历、链接和草稿；编辑台再确认登录账号，发布后回报 X 帖子链接。

只想先看文案时发送：

> 把这个交给 X 内容编辑台做候选帖。

候选帖只生成草稿。任务之间不会自动复制整段对话；子代理负责提炼相关上下文，必要时编辑台会追溯来源。

## 范围与安全

- 只在你从原任务发出指令时运行，不后台扫描其他任务，也不定时发帖。
- 公开发布前核对来源、账号和重复内容；不编造数据、效果或使用体验。
- 遇到浏览器或安全审批要求时按要求停下，不绕过拦截；点击失败不算发布成功。
- 插件没有 X API 集成，也不携带任何账号凭据。

## 仓库文件

| 路径 | 用途 |
| --- | --- |
| [`plugin.json`](plugin.json) | 可移植插件清单 |
| [`.codex-plugin/plugin.json`](.codex-plugin/plugin.json) | Codex 兼容清单与展示信息 |
| [`.agents/plugins/marketplace.json`](.agents/plugins/marketplace.json) | 从本仓库发现插件 |
| [`skills/x-handoff/SKILL.md`](skills/x-handoff/SKILL.md) | 原任务交接流程 |
| [`skills/x-editor/SKILL.md`](skills/x-editor/SKILL.md) | 编辑台发布流程 |

当前版本为 `0.1.0`。清单和技能结构已做本地检查；跨任务到 X 的端到端流程仍需在安装后的新任务中实测。正式公开发布前还需选择许可证。本账号的本地发帖记录保存在被 Git 忽略的 `CONTENT.md`，不会进入插件仓库。
