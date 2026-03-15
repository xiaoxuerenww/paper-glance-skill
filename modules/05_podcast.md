# Module 5: 🎙️ Podcast Script + Audio Generation

Transform the paper into ready-to-air podcast content, and optionally generate an MP3 using the edge-tts MCP. **Output entirely in English.**

---

## Step 0: Detect edge-tts MCP Availability

**Complete this check before asking about podcast format.**

Try calling `edge-tts:list_voices` (no parameters):

- ✅ **Call succeeds** → MCP connected; proceed to Step 1 and tell the user: "🎙️ edge-tts is ready — audio can be generated directly"
- ❌ **Call fails / tool not found** → MCP not connected; show setup instructions below, then **continue in text-script-only mode**

---

### When edge-tts MCP is not connected

> ⚠️ **edge-tts MCP not detected — text script only for this session.**
>
> To generate MP3 audio, follow these steps:
>
> **Step 1: Confirm `uvx` is installed**
> ```bash
> which uvx
> ```
> No output? Install it:
> ```bash
> curl -LsSf https://astral.sh/uv/install.sh | sh
> ```
>
> **Step 2: Add the following to your Claude Desktop config file**
>
> Config file location:
> - macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
> - Windows: `%APPDATA%\Claude\claude_desktop_config.json`
>
> Add to `mcpServers`:
> ```json
> "edge-tts": {
>   "command": "/replace-with-full-uvx-path/uvx",
>   "args": ["better-tts-mcp"]
> }
> ```
> 💡 Replace the path with the output of `which uvx`, e.g. `/Users/yourname/.local/bin/uvx`
>
> **Step 3: Restart Claude Desktop and reopen this conversation.**
>
> ---
> Continuing with text script now — once installed, re-run to generate audio directly 👇

---

## Step 1: Ask for Podcast Format and Output Directory

> "Which podcast format would you like?
> A) 🎤 Solo narration (single host, science-explainer style)
> B) 🎭 Two-host dialogue (host × expert, Q&A format, more engaging)
>
> Length preference?
> - Short (approx. 5 min, 800–1000 word script)
> - Long (approx. 12 min, 2000–2500 word script)
>
> Where should the audio be saved? Provide a full absolute path, e.g. `/Users/yourname/Desktop`. Default is `/tmp`."

If not specified: default to two-host dialogue + short version.
If no directory given: default to `/tmp` (provide a `cp` command after generation).

---

## Step 2: Build the Podcast Content Skeleton

The podcast must cover the following dimensions, drawn from PAPER_CORE in priority order:

| Segment | Source fields | Priority |
|---------|--------------|----------|
| Opening hook | `fun_fact` / `one_liner` | ⭐⭐⭐ must be punchy |
| Problem background | `problem` + `prior_work` | ⭐⭐⭐ audience needs to feel the pain first |
| Core insight | `insight` + `hypothesis` + `analogy` | ⭐⭐⭐ the soul of the episode |
| Method walkthrough | `method` + `key_modules` | ⭐⭐ conversational, no formulas |
| Key results | `result` + `ablation` | ⭐⭐⭐ numbers need comparison context |
| Significance & outlook | `significance` + `future_work` | ⭐⭐ leave the listener thinking |
| Limitations | `limitation` + `failure_case` | ⭐ builds credibility, don't skip |

> ⚠️ Podcast writing rules:
> - **No formulas** — convert all math to conversational analogies
> - **No list-reading** — use natural transition sentences
> - Every number needs comparison context: "3% better than the previous best — that's like…"
> - `analogy` is the core weapon — always use it
> - Lead with `fun_fact`; if null, find the most counter-intuitive result in `result`

---

## Step 3: Generate Script

Based on the user's choice in Step 1:

### Format A: Solo Narration Script

```
[Intro music cue: 3 seconds]

[Opening - 30 sec]
Welcome back. Today we're looking at a paper that caught my attention —
[PAPER_CORE.one_liner rephrased conversationally]
[PAPER_CORE.fun_fact or most counter-intuitive finding, to build suspense]

[Problem background - 60 sec]
Before we get into the paper, let's set the scene — what problem is this solving?
[PAPER_CORE.problem expanded conversationally]
[PAPER_CORE.prior_work limitations, 1–2 sentences]
So — is there a better way? This paper offers a pretty interesting answer.

[Core method - 90 sec]
Here's the key idea behind their approach —
[PAPER_CORE.analogy fully expanded, analogy first then technical detail]
Specifically, [PAPER_CORE.method as conversational steps, 3–4 steps, one sentence each]
The most critical design choice is [most important item from PAPER_CORE.key_modules, plain language]

[Results - 60 sec]
So how well does it work?
[PAPER_CORE.result top 1–2 findings, with numbers and comparison context]
They also ran an interesting experiment: [PAPER_CORE.ablation rephrased conversationally]

[Significance & limitations - 40 sec]
Why does this matter? [PAPER_CORE.significance]
That said, it's not without limits: [PAPER_CORE.limitation, 1 sentence, honest]

[Outro - 20 sec]
That's it for today. One sentence to sum up this paper:
[PAPER_CORE.one_liner]
If you want to dig deeper, search for [PAPER_CORE.title]. See you next time.

[Outro music cue: 3 seconds]
```

**Length control**: Short version = opening + background + method + results + outro; long version = all segments fully expanded.

---

### Format B: Two-Host Dialogue Script

Character setup:
- **Host [H]**: curious tech enthusiast, asks questions on behalf of the audience
- **Expert [E]**: domain specialist, provides in-depth explanations

```
[H] Opening + introduce the topic (use fun_fact or a counter-intuitive question to create suspense)

[E] Pick up the thread, briefly confirm what makes this research interesting

[H] "So before this paper, how were people handling this problem?"

[E] Describe prior_work, point out the core limitations (conversational, specific)

[H] "So what's the new idea here? Explain it like I'm not an expert."

[E] Use analogy to explain, then gradually introduce method (analogy first, then technical)

[H] Raise a question the audience would naturally have (from PAPER_CORE.hypothesis or the hardest-to-grasp key_module)

[E] Answer, optionally adding key_modules detail

[H] "How do the numbers look? Is it actually better than what came before?"

[E] Report result (top 1–2 numbers) with comparison context; mention interesting ablation finding

[H] "Sounds impressive — but are there things it still can't do?"

[E] Honestly describe limitation and failure_case — academic honesty matters

[H] "Last question — what do you think is the most important takeaway from this work?"

[E] Summarize significance + future_work, close with one_liner

[H] Thanks + outro
```

**Two-host dialogue rules**:
- [H]'s questions must be genuine audience questions — never placeholder lines like "can you describe the method?"
- [E]'s responses should stay under 80 words each to maintain conversational rhythm
- Never use "first… second… finally" list-style pacing throughout
- The dialogue should have back-and-forth energy — [H] can push back, show surprise, or add a follow-up

---

## Step 4: Generate Audio (when MCP is available)

> ⚠️ If Step 0 found MCP unavailable, skip this step and output the text script with setup instructions.

### ⚠️ Important: output_dir

The edge-tts MCP runs on the **user's local machine**. File paths must be local filesystem paths —
**not** Claude's cloud container paths (e.g. `/mnt/user-data/outputs` or `/home/claude`).

**Path rules:**
1. **User provides a path** → use it directly (must be an absolute path)
2. **User says "default" or doesn't specify** → use `/tmp`, provide a `cp` command after generation
3. **Never use**: `.` (relative), `~/Desktop` (tilde not expanded by MCP), `/mnt/...`, `/home/claude/...`

### Solo audio (call `edge-tts:text_to_speech`)

```
voice:      en-US-GuyNeural (male, natural) or en-US-JennyNeural (female)
rate:       +5% (slightly faster, podcast pacing)
output_dir: /tmp (default) or user-specified local path
```

Suggested filename: `podcast_[paper-short-title]_[date].mp3`

### Two-host audio (call `edge-tts:text_to_speech_multi_voice`)

Marker format:
```
[en-US-GuyNeural](Host line)
[en-US-JennyNeural](Expert line)
```

Recommended voice pairing:
- Host [H]: `en-US-GuyNeural` (male, energetic)
- Expert [E]: `en-US-JennyNeural` (female, calm and clear)
- Or swap based on user preference

### Confirm before generating

Show the user:
> "Ready to generate audio:
> - Format: [solo / two-host]
> - Estimated length: [X] minutes
> - Save location: [user path or /tmp]
> Confirm?"

---

## Step 5: After Generation

Tell the user:
> "🎙️ Podcast generated: [file path]
> Would you also like:
> - 📝 Transcript (useful for publishing to podcast platforms)
> - 📢 Promo thread (Module 4)
> - 🧠 Companion mind map (Module 2, great for cover art or show notes)"

---

## Quality Checklist

Before generating the script, verify:
- [ ] `analogy` is used (the soul of the episode)
- [ ] `fun_fact` or most counter-intuitive finding leads the opening
- [ ] All numbers have comparison context
- [ ] No formulas, no list-reading
- [ ] `limitation` is honestly mentioned
- [ ] No "first… second… finally" pacing
- [ ] [H]'s questions are genuine audience questions
