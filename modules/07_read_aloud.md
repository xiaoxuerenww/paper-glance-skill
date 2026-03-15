# Module 7: 🔊 Read Aloud

Read the current module's generated output aloud using the edge-tts MCP. This is distinct from the podcast module:
- **Module 5 (Podcast)**: rewrites the paper into a narrative script, then generates audio
- **Module 7 (Read Aloud)**: reads the actual generated output as-is, no rewriting

---

## Step 0: Detect edge-tts MCP Availability

Try calling `edge-tts:list_voices` (no parameters):

- ✅ **Call succeeds** → MCP connected; proceed to Step 1
- ❌ **Call fails** → Show setup instructions (same as Module 5); **do not continue**

### When edge-tts MCP is not connected

> ⚠️ **edge-tts MCP not detected — read-aloud is unavailable.**
>
> To enable this feature, install the edge-tts MCP:
>
> **Step 1: Confirm `uvx` is installed**
> ```bash
> which uvx
> ```
> No output? Run:
> ```bash
> curl -LsSf https://astral.sh/uv/install.sh | sh
> ```
>
> **Step 2: Add to your Claude Desktop config file**
>
> Config file location:
> - macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
> - Windows: `%APPDATA%\Claude\claude_desktop_config.json`
>
> ```json
> "edge-tts": {
>   "command": "/replace-with-full-uvx-path/uvx",
>   "args": ["better-tts-mcp"]
> }
> ```
> 💡 Replace the path with the output of `which uvx`. Restart Claude Desktop to take effect.

---

## Step 1: Confirm Content and Voice Settings

Ask the user:

> "What would you like me to read aloud?
> 1. Summary / key conclusions only (approx. 1–2 min)
> 2. Full output (read everything generated, in order)
>
> Voice preference?
> - A) 🧑 Male voice (en-US-GuyNeural, natural and energetic)
> - B) 👩 Female voice (en-US-JennyNeural, calm and clear)
>
> Where should the audio be saved? (Default: `/tmp` — provide a full absolute path)"

If not specified, default to: full content + female voice (en-US-JennyNeural) + save to `/tmp`.

---

## Step 2: Pre-process Text for Speech

Apply the following transformations to make the audio sound natural:

| Original content type | Treatment |
|----------------------|-----------|
| Markdown headings (`###`) | Convert to a spoken pause: "--- [Section Name] ---" |
| Tables | Convert to row-by-row spoken descriptions, e.g. "Method one: XXX. Strength: YYY." |
| Mermaid code blocks | Replace with: "(Mind map diagram — skipped for audio)" |
| Other code blocks | Replace with: "(Code block — skipped for audio)" |
| Bold `**text**` | Strip markdown symbols, keep the text |
| URLs / links | Replace with: "(link omitted)" |
| Numbered lists | Read as: "First, … Second, …" |

After processing, estimate the reading time (at ~130 words/minute) and tell the user:
> "Ready to read aloud — estimated length: X minutes. Saving to [path]. Confirm?"

---

## Step 3: Generate Audio

Call `edge-tts:text_to_speech`:

```
voice:      user-selected voice (default: en-US-JennyNeural)
rate:       +0% (normal speed — reports should not be rushed)
text:       processed text from Step 2
output_dir: user-specified path (default: /tmp)
```

Filename: `readout_[module-number]_[paper-short-title]_[date].mp3`

Example: `readout_01_attention_20240315.mp3`

---

## Step 4: After Generation

> "🔊 Read-aloud audio generated: [file path]
>
> Would you also like:
> - 🔄 Re-read (different voice or content range)
> - 📤 Export full document (Module 6)
> - 🎙️ Podcast version (Module 5 — rewrites content into a conversational narrative)"

---

## Quality Requirements

- Mermaid and code blocks **must be skipped** — never read raw symbols aloud
- Tables must be converted to spoken sentences — never read `|` characters
- Keep reading speed at normal pace (`+0%`) — faster rates make reports hard to follow
- **Always show estimated duration** before generating; require confirmation for content > 5 minutes
