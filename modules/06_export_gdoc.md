# Module 6: 📤 Export to Google Docs

Compile and export content generated in this conversation (analysis report, mind map, peer review, promo scripts, podcast script, etc.) to a Google Docs document.

---

## Step 0: Detect Google Docs MCP Availability

Try calling `gdrive_create_document` or `google_docs_create` (test call, no parameters):

- ✅ **Call succeeds** → MCP connected; proceed to Step 1 and notify the user: "📤 Google Docs MCP is ready — exporting directly"
- ❌ **Call fails / tool not found** → MCP not connected; show setup instructions below, then **fall back to Markdown export mode**

---

### When Google Docs MCP is not connected

> ⚠️ **Google Docs MCP not detected — exporting as Markdown instead.**
>
> To export directly to Google Docs, follow these steps:
>
> **Step 1: Configure Google Drive MCP**
>
> Add the following to your Claude Desktop config file:
>
> Config file location:
> - macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
> - Windows: `%APPDATA%\Claude\claude_desktop_config.json`
>
> Add to `mcpServers`:
> ```json
> "gdrive": {
>   "command": "npx",
>   "args": ["-y", "@modelcontextprotocol/server-gdrive"]
> }
> ```
>
> **Step 2: Authorize your Google account**
>
> After restarting Claude Desktop, a Google OAuth window will appear on first use. Authorize it and you're ready.
>
> **Step 3: Restart Claude Desktop and re-run the export.**
>
> ---
> Continuing with Markdown export now — you can paste it into any document tool 👇

---

## Step 1: Confirm Export Content

Ask the user:

> "Which content would you like to export? (You can pick multiple)
> 1. 📊 Deep Analysis Report
> 2. 🧠 Mind Map (Mermaid code)
> 3. 🔍 Peer Review
> 4. 📢 Promotional Scripts
> 5. 🎙️ Podcast Script
> 0. All content generated in this session
>
> Document title? (Default: *[PAPER_CORE.title]* — Analysis Report)"

If not specified, default to all content generated in this session, using the default title.

---

## Step 2: Compile Document Content

Organize the selected content into a structured document:

```
# [PAPER_CORE.title] ([PAPER_CORE.year])

> [PAPER_CORE.one_liner]

**Authors**: [PAPER_CORE.authors]
**Venue**: [PAPER_CORE.venue]
**Exported**: [current date]

---

[Selected module content, arranged in order: 1 → 2 → 3 → 4 → 5]
```

**Mermaid diagrams**: Mermaid code cannot render in Google Docs — keep the code block and add a note:
> 💡 *Paste the Mermaid code below into [mermaid.live](https://mermaid.live) to view the diagram*

---

## Step 3A: Google Docs Export (when MCP is available)

1. Call the MCP tool to create the document:
   - Tool: `gdrive_create_document` or `google_docs_create`
   - Parameters: `title` (document title), `content` (compiled content from Step 2)

2. After getting the document link, tell the user:
   > "📄 Google Doc created: [document link]
   > Click the link to view and edit."

3. If the MCP supports permission settings, default to "Anyone with the link can comment" and inform the user they can adjust this in Google Docs.

---

## Step 3B: Markdown Fallback Export (when MCP is not available)

Output the full Markdown document in the conversation and prompt:

> "📋 Here is the full document content (Markdown format).
>
> **To import into Google Docs:**
> 1. Copy all the content below
> 2. Go to [Google Docs](https://docs.google.com) → create a new document
> 3. Paste the content (formatting will adapt automatically)
>
> Or save as a `.md` file and convert with Pandoc:
> ```bash
> pandoc paper_report.md -o paper_report.docx
> ```"

---

## Quality Requirements

- Export content must be complete — do not truncate any module
- The document header must include paper metadata (title, year, venue, authors, one_liner)
- If a module was not generated in this session, note "(not generated this session — return to main menu to generate)"
- Mermaid code must be preserved in full, with the mermaid.live link notice
