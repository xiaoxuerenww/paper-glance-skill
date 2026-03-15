# 模块 6：📤 导出到 Google Docs

将本次对话中生成的内容（分析报告、思维导图、审稿意见、宣传脚本、播客脚本等）整理后导出为 Google Docs 文档。

---

## 第零步：检测 Google Docs MCP 是否可用

尝试调用 `gdrive_create_document` 或 `google_docs_create` 工具（无参数测试调用）：

- ✅ **调用成功** → MCP 已连接，进入第一步，告知用户"📤 Google Docs MCP 已就绪，可以直接导出"
- ❌ **调用失败 / 工具不存在** → MCP 未连接，输出以下提示后**降级为 Markdown 导出模式**：

---

### MCP 未连接时的提示内容

> ⚠️ **未检测到 Google Docs MCP，将导出为 Markdown 格式。**
>
> 如需直接导出到 Google Docs，请按以下步骤安装：
>
> **第一步：确认 Google Drive MCP 配置**
>
> 在 Claude Desktop 配置文件中添加：
>
> 配置文件路径：
> - macOS：`~/Library/Application Support/Claude/claude_desktop_config.json`
> - Windows：`%APPDATA%\Claude\claude_desktop_config.json`
>
> 在 `mcpServers` 中添加：
> ```json
> "gdrive": {
>   "command": "npx",
>   "args": ["-y", "@modelcontextprotocol/server-gdrive"]
> }
> ```
>
> **第二步：授权 Google 账号**
>
> 重启 Claude Desktop 后，首次使用时会弹出 Google OAuth 授权窗口，授权后即可使用。
>
> **第三步：重启 Claude Desktop，重新运行导出即可。**
>
> ---
> 现在继续为你生成 Markdown 文档，可复制后粘贴到任意文档工具 👇

---

## 第一步：确认导出内容

询问用户：

> "需要导出哪些内容？（可多选）
> 1. 📊 深度分析报告
> 2. 🧠 思维导图（Mermaid 代码）
> 3. 🔍 审稿意见
> 4. 📢 宣传脚本
> 5. 🎙️ 播客脚本
> 0. 全部已生成的内容
>
> 文档标题？（默认：《[PAPER_CORE.title]》分析报告）"

若用户未指定，默认导出本次对话中已生成的全部内容，标题使用默认格式。

---

## 第二步：整理文档内容

将所选内容整理为结构化文档，格式如下：

```
# 《[PAPER_CORE.title]》（[PAPER_CORE.year]）

> [PAPER_CORE.one_liner]

**作者**：[PAPER_CORE.authors]
**发表**：[PAPER_CORE.venue]
**导出时间**：[当前日期]

---

[所选模块的完整内容，按 1→2→3→4→5 顺序排列]
```

**思维导图处理**：Mermaid 代码在 Google Docs 中无法渲染，改为保留代码块并附注：
> 💡 *请将以下 Mermaid 代码粘贴到 [mermaid.live](https://mermaid.live) 查看思维导图*

---

## 第三步A：Google Docs 导出（MCP 可用时）

1. 调用 MCP 工具创建文档：
   - 工具：`gdrive_create_document` 或 `google_docs_create`
   - 参数：`title`（文档标题）、`content`（第二步整理的内容）

2. 获取文档链接后，告知用户：
   > "📄 Google Docs 文档已创建：[文档链接]
   > 点击链接即可查看和编辑。"

3. 若 MCP 支持设置权限，默认设为"任何人可评论"，并告知用户可在 Google Docs 中调整。

---

## 第三步B：Markdown 降级导出（MCP 不可用时）

直接在对话中输出完整 Markdown 文档，并提示：

> "📋 以下是完整文档内容（Markdown 格式）。
>
> **导入到 Google Docs 的方法：**
> 1. 复制下方全部内容
> 2. 打开 [Google Docs](https://docs.google.com) → 新建文档
> 3. 粘贴内容（格式会自动适配）
>
> 或者直接将内容保存为 `.md` 文件后用 Pandoc 转换：
> ```bash
> pandoc 论文报告.md -o 论文报告.docx
> ```"

---

## 质量要求

- 导出内容保持原模块的完整性，不删减
- 文档顶部必须包含论文基本信息（title、year、venue、authors、one_liner）
- 如果某模块本次对话中未生成，注明"（本次未生成，如需可返回主菜单选择）"
- Mermaid 代码必须保留完整，附 mermaid.live 链接提示
