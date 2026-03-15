# Module 6: 📤 Export to DOCX

Compile content generated in this conversation into a `.docx` file saved to the user's `Downloads/` folder.

---

## Step 1: Confirm Export Content

Ask the user:

> "Which content would you like to export? (You can pick multiple)
> 1. 📊 Deep Analysis Report
> 2. 🧠 Mind Map (Mermaid code, with view link)
> 3. 🔍 Peer Review
> 4. 📢 Promotional Scripts
> 5. 🎙️ Podcast Script
> 0. All content generated in this session
>
> Document title? (Default: `[paper-short-title]_report`)"

If not specified, default to all content generated in this session.

---

## Step 2: Compile Document Content

Assemble the selected content into a single Markdown string with this structure:

```
# [PAPER_CORE.title] ([PAPER_CORE.year])

> [PAPER_CORE.one_liner]

**Authors**: [PAPER_CORE.authors]
**Venue**: [PAPER_CORE.venue]
**Exported**: [current date]

---

[Selected module content in order: 1 → 2 → 3 → 4 → 5]
```

**Mermaid diagrams**: cannot render in DOCX — keep the code block and add:
> 💡 *Paste the Mermaid code below into [mermaid.live](https://mermaid.live) to view the diagram*

---

## Step 3: Determine Downloads Path

Resolve the user's Downloads folder:

| OS | Default path |
|----|-------------|
| macOS | `/Users/[username]/Downloads/` |
| Windows | `C:\Users\[username]\Downloads\` |
| Linux | `/home/[username]/Downloads/` |

If the username is unknown, ask:
> "What is your system username? (Used to build the Downloads path, e.g. `/Users/yourname/Downloads/`)"

Output filename: `[document-title].md` (intermediate) and `[document-title].docx` (final).
Example: `attention_report.docx`

---

## Step 4: Write and Convert

### 4a. Write the Markdown file

Use the `write_file` tool (or equivalent filesystem tool) to save the compiled Markdown to:
```
/Users/[username]/Downloads/[document-title].md
```

### 4b. Convert to DOCX using Pandoc

Run the following shell command:
```bash
pandoc "/Users/[username]/Downloads/[document-title].md" \
  -o "/Users/[username]/Downloads/[document-title].docx"
```

- ✅ **Conversion succeeds** → notify the user (see Step 5)
- ❌ **`pandoc` not found** → show installation instructions below, and offer the `.md` file as fallback

---

### When Pandoc is not installed

> ⚠️ **`pandoc` not found — the Markdown file has been saved but could not be converted to DOCX.**
>
> **Option 1: Install Pandoc**
> - macOS: `brew install pandoc`
> - Windows: download from [pandoc.org/installing](https://pandoc.org/installing.html)
> - Linux: `sudo apt install pandoc`
>
> Then run:
> ```bash
> pandoc "~/Downloads/[document-title].md" -o "~/Downloads/[document-title].docx"
> ```
>
> **Option 2: Open the `.md` file directly**
> The Markdown file is already saved at:
> `~/Downloads/[document-title].md`
> You can open it in VS Code, Typora, Obsidian, or any Markdown editor.
>
> **Option 3: Paste into Word / Google Docs manually**
> The full document content is shown below — copy and paste it in.

---

## Step 5: After Successful Export

> "📄 Export complete!
> - **DOCX**: `~/Downloads/[document-title].docx`
> - **Markdown source**: `~/Downloads/[document-title].md`
>
> Would you also like:
> - 🔊 Read the report aloud (Module 7)
> - 🎙️ Generate a podcast version (Module 5)"

---

## Quality Requirements

- Export content must be complete — do not truncate any module
- The document header must include paper metadata (title, year, venue, authors, one_liner)
- If a module was not generated in this session, note: "(not generated this session — return to main menu to generate)"
- Mermaid code blocks must be preserved in full with the mermaid.live notice
- Always clean up the intermediate `.md` file if the `.docx` was created successfully and the user did not ask to keep it
