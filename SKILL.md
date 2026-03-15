---
name: paper-glance
description: All-in-one academic paper processing tool. Must trigger whenever the user uploads a paper PDF, pastes paper text or abstract, uploads an audio file, uses voice input, or mentions "paper", "research", "literature", "arxiv", or "study". Features include deep analysis report, mind map, peer review, promotional scripts, podcast audio, Google Docs export, and read-aloud output. Trigger even if the user simply says "help me read this paper" or uploads a PDF directly.
---

# Paper Glance — All-in-One Paper Processing Tool

## Step 1: Pre-check

Check whether the user has provided paper content:

- ✅ Uploaded a PDF / pasted text / provided an abstract → continue
- ✅ Uploaded an audio file (MP3, M4A, WAV, etc.) → use `view` tool to read `/mnt/skills/user/paper-glance/modules/00_voice_input.md` and run transcription first, then continue
- ✅ Voice input already transcribed by Claude Desktop → continue directly
- ✅ Voiced an action command (e.g. "analyze this", "make a mind map") but no paper provided → read `00_voice_input.md` to identify the command; if `PAPER_CORE` already exists in this conversation, execute the corresponding module directly; otherwise prompt the user to provide a paper
- ❌ Nothing provided → reply: "Please upload a paper PDF, paste the paper content, or speak the abstract aloud — I'll take it from there."

---

## Step 2: Understand the Paper

Use the `view` tool to read `/mnt/skills/user/paper-glance/shared/paper_core.md` and internally build `PAPER_CORE` using the extraction framework defined there.

This step is **done silently — do not show the extraction process to the user.**

**Missing field rules** (when the paper does not provide certain information):
- `title` missing → use "Untitled Paper"
- `year` missing → omit the year parentheses
- `one_liner` missing → write a one-sentence summary yourself, never leave it blank
- Other fields missing → fill with `null`; downstream modules should note "not mentioned in paper" rather than fabricating content

---

## Step 3: Show Menu

Once the paper is understood, output the following fixed-format menu:

---

📄 **Paper loaded:** *[title]* ([year])

> [one_liner]

**What would you like to do with this paper?**

| # | Feature | Description |
|---|---------|-------------|
| 1 | 📊 Deep Analysis | Full academic breakdown: methods, experiments, contributions |
| 2 | 🧠 Mind Map | Mermaid mind map or flowchart, renders instantly — no plugins needed |
| 3 | 🔍 Peer Review | Structured review: Summary / Strengths / Weaknesses / Questions |
| 4 | 📢 Promo Script | Social media posts, blog summary, talk intro, email summary |
| 5 | 🎙️ Podcast | Solo or two-host script, can generate MP3 audio |
| 6 | 📤 Export to Google Docs | Export generated content as a Google Doc |
| 7 | 🔊 Read Aloud | Read the generated output aloud via TTS |
| 0 | All | Generate all features in order: 1 → 2 → 3 → 4 → 5 |

Reply with a number, or say what you want naturally (e.g. "write me a review", "make a podcast").

---

## Step 4: Execute the Corresponding Module

Based on the user's selection, use the `view` tool to read and execute the corresponding module file:

| Selection | File to read (use view tool) |
|-----------|------------------------------|
| Audio file / voice command | `/mnt/skills/user/paper-glance/modules/00_voice_input.md` |
| 1 / analysis | `/mnt/skills/user/paper-glance/modules/01_analysis.md` |
| 2 / mind map | `/mnt/skills/user/paper-glance/modules/02_mindmap.md` |
| 3 / review | `/mnt/skills/user/paper-glance/modules/03_review.md` |
| 4 / promo | `/mnt/skills/user/paper-glance/modules/04_promo.md` |
| 5 / podcast | `/mnt/skills/user/paper-glance/modules/05_podcast.md` |
| 6 / export | `/mnt/skills/user/paper-glance/modules/06_export_gdoc.md` |
| 7 / read aloud | `/mnt/skills/user/paper-glance/modules/07_read_aloud.md` |
| 0 / all | Read modules 01 → 02 → 03 → 04 → 05 in sequence and execute each |

After executing, ask: "Anything else you'd like?" (show remaining options), and append:
> 🔊 Want to hear it read aloud? Reply **7** to listen to the output just generated.
> 📤 Happy with the results? Reply **6** to export everything to Google Docs.

---

- `PAPER_CORE` remains valid throughout the conversation — **do not re-read the paper** when switching modules
- If the user directly says "write me a review", "generate a mind map", "make a podcast", etc. (typed or spoken), skip the menu and execute the corresponding module directly
- If the user uploads a new paper or audio file, re-run Step 2 to update `PAPER_CORE`
- Podcast module (5) requires edge-tts MCP to generate audio; without it, output text script only
- Read-aloud module (7) requires edge-tts MCP; without it, show setup instructions
- Voice input module (00) handles audio transcription and voice command recognition; Claude Desktop's built-in STT requires no extra configuration
- **Always output in English**, regardless of the paper's language
