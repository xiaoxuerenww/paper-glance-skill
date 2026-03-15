# 📄 Paper Glance

中文说明（当前页） | English: [README_EN.md](README_EN.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Skill](https://img.shields.io/badge/Claude-Skill-blueviolet?logo=anthropic)](https://claude.ai)
[![Zero MCP Required](https://img.shields.io/badge/MCP-Not_Required-brightgreen)](https://claude.ai)

**Claude Skill：论文全能处理工具**

上传任意学术论文 PDF，Claude 自动帮你生成：深度分析报告、思维导图、专业审稿意见、宣传文案、播客脚本与音频。**核心功能开箱即用，无需额外插件。**

---

## ✨ 功能一览

| # | 功能 | 说明 | 
|---|------|------|
| 1 | 📊 深度分析报告 | 方法、实验、创新点的完整学术解读 |
| 2 | 🧠 思维导图 | Mermaid 思维导图 + 方法流程图，对话内直接渲染 | 
| 3 | 🔍 审稿意见 | Summary / Strengths / Weaknesses / Questions 专业格式 | 
| 4 | 📢 宣传脚本 | 推文、公众号摘要、演讲开场白、邮件摘要 |
| 5 | 🎙️ 播客音频 | 单人/双人播客脚本，可连接 TTS 一键生成 MP3 |
| 6 | 📤 导出 Google Docs | 将已生成内容一键导出为 Google Docs 文档 |

> 1-4 功能无需 MCP；5 号播客在未连接 [TTS MCP](https://github.com/CatVinci-Studio/better-tts-mcp) 时会自动降级为纯文字脚本；6 号导出在未连接 Google Drive MCP 时会自动降级为 Markdown 格式输出。

---

## 🚀 快速开始

### 第一步：安装 Skill

> **什么是 Skill？** Skill 是给 Claude 增加专项能力的指令文件夹，放到指定目录后 Claude 会自动识别和使用。目前支持 **Claude Desktop**（需登录账号）。

1. 点击右上角 `Code → Download ZIP`，或者在Release中下载。
2. 在Claude Code打开`Customize`、 `Skills`中的`Upload a skill`
3. 上传压缩包, Skill安装完成 ✅

### 第二步：开始使用

安装后，上传一篇论文 PDF，发送任意消息：

```
"帮我看这篇论文"
"生成思维导图"
"帮我写审稿意见"
"做一份宣传推文"
```

Claude 会自动读取论文，展示功能菜单：

```
📄 已读取论文：《Attention Is All You Need》（2017）
> 用自注意力机制替代 RNN，奠定现代 Transformer 架构基础

你想用这篇论文做什么？

  1  📊 深度分析报告
  2  🧠 思维导图
  3  🔍 审稿意见
  4  📢 宣传脚本
  5  🎙️ 播客音频
  0  全部生成
```

回复数字或直接说需求即可。

---

## 📦 功能详解

### 1 · 📊 深度分析报告
对论文进行结构化学术解读，涵盖：问题背景与动机、方法设计与核心创新、实验设置与结果分析、局限性与未来方向。

### 2 · 🧠 思维导图
默认生成放射状**思维导图**，展示论文整体结构（问题→方法→实验→贡献→局限）。生成后可选择追加**方法流程图**（Pipeline），展示数据流向。两者均为标准 Mermaid 代码，在 Claude 对话窗口内直接渲染，也可复制到 [mermaid.live](https://mermaid.live) 继续编辑。

### 3 · 🔍 审稿意见
模拟顶会/期刊审稿人视角，输出结构化审稿报告：

| Section | 内容 |
|---------|------|
| **Summary** | 3–5 句客观概括核心问题、方法与结论 |
| **Strengths** | 3–5 条优点，有具体论据 |
| **Weaknesses** | 3–5 条不足，每条附改进建议 |
| **Questions** | 3–5 个给作者的问题 |
| **Minor Comments** | 小问题（可选） |
| **Decision** | Accept / Weak Accept / Borderline / Weak Reject / Reject + 理由 |

支持中英双语输出，适合投稿前自查或组会汇报。

### 4 · 📢 宣传脚本
一键生成多种宣传格式：Twitter/X 推文（含 hashtag）、公众号/知乎摘要、学术演讲开场介绍、邮件摘要。

### 6 · 📤 导出 Google Docs

对结果满意后，回复 **6** 即可将本次对话中已生成的任意内容（可多选）整理导出：

- 若已连接 [Google Drive MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/gdrive)，直接创建 Google Docs 并返回链接
- 若未连接，自动降级为 Markdown 格式输出，并提供粘贴到 Google Docs 的步骤说明

导出文档包含论文基本信息（标题、作者、年份、一句话摘要）和所选内容，思维导图代码块附 [mermaid.live](https://mermaid.live) 渲染链接。

### 5 · 🎙️ 播客脚本 + 音频生成
将论文自动转成可播客化内容，支持两种模式：

- 单人解说（主播独白，科普节奏）
- 双人对话（主持人 x 研究员，问答互动）

若已连接 `better-tts-mcp`，可直接生成 MP3；若未连接则自动降级为文字脚本，不影响使用。

- TTS 项目链接：`https://github.com/CatVinci-Studio/better-tts-mcp`

---

## 📁 文件结构

```
paper-glance-skill/
├── SKILL.md                # 入口：论文理解 + 功能菜单
├── README.md               # 本文件
├── README_EN.md            # 英文说明
├── shared/
│   └── paper_core.md       # 共享论文提取框架
└── modules/
    ├── 01_analysis.md      # 深度分析报告
    ├── 02_mindmap.md       # 思维导图 + 流程图
    ├── 03_review.md        # 审稿意见
    ├── 04_promo.md         # 宣传脚本
    ├── 05_podcast.md       # 播客脚本 + 音频生成
    └── 06_export_gdoc.md   # 导出到 Google Docs
```

---

## ❓ 常见问题

**Q：需要 API Key 或付费插件吗？**
不需要。全部功能基于 Claude 原生能力，无需任何额外配置。

**Q：支持英文论文吗？**
支持。Claude 可处理中英文论文，输出语言默认跟随论文语言，也可以明确指定输出语言。

**Q：思维导图显示不出来？**
确保使用 Claude Desktop 最新版本。Mermaid 渲染依赖客户端支持，也可以将代码复制到 [mermaid.live](https://mermaid.live) 查看。

**Q：可以同时处理多篇论文吗？**
上传新论文后发送消息，Claude 会自动更新到新论文。如需对比多篇，建议开启新对话分别处理。

**Q：播客功能为什么没生成 MP3？**
通常是因为未连接 TTS MCP。此时 Skill 会自动降级为文字脚本模式。按以下项目安装并连接后即可直接生成音频：`https://github.com/CatVinci-Studio/better-tts-mcp`

---

## 📄 License

MIT — 随意使用、修改和分享。欢迎 PR 和 Issue。
