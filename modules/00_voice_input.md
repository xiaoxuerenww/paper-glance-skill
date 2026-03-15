# Module 0: 🎤 Voice Input Handling

Handles two voice input scenarios:
1. **Voice commands**: the user speaks an action instruction (e.g. "analyze this paper", "make a mind map")
2. **Audio file transcription**: the user uploads an audio file containing a paper abstract or reading, which must be converted to text first

---

## Scenario A: Voice Command Recognition (No MCP required)

Claude Desktop has built-in speech-to-text — when the user speaks, the text automatically appears in the chat.
**No extra configuration needed.** The skill receives the transcribed text and processes it normally.

### Voice Command Mapping

Recognize the following spoken phrases and map them to the corresponding module, **skipping the menu**:

| What the user might say | Execute module |
|------------------------|----------------|
| analyze / deep dive / read this / summarize | Module 1: Deep Analysis |
| mind map / mindmap / visualize / diagram / flowchart | Module 2: Mind Map |
| review / peer review / give feedback / critique | Module 3: Peer Review |
| promote / tweet / blog post / social media / write about it | Module 4: Promo Script |
| podcast / audio / make a podcast | Module 5: Podcast |
| export / google doc / save / download | Module 6: Export to Google Docs |
| read aloud / read it out / speak / listen | Module 7: Read Aloud |
| all / everything / do all / run all | Modules 1 → 5 in sequence |

**Fuzzy matching rule**: speech recognition may produce incomplete words or minor errors — prioritize understanding the user's intent over exact string matching.

---

## Scenario B: Audio File Transcription (Requires Whisper MCP)

The user has uploaded an audio file (MP3, M4A, WAV, etc.) containing a paper abstract or spoken content.

### Step 0: Detect Whisper MCP Availability

Try calling the `whisper_transcribe` or `stt_transcribe` tool:

- ✅ **Call succeeds** → MCP connected, proceed to transcription
- ❌ **Call fails** → Show setup instructions and suggest alternatives

---

### When Whisper MCP is not connected

> ⚠️ **Whisper MCP not detected — cannot process audio files directly.**
>
> **Alternatives (pick one):**
>
> **Option 1: Use Claude Desktop's built-in voice input**
> Click the 🎤 microphone icon next to the chat box and speak the abstract — Claude will transcribe it automatically.
>
> **Option 2: Install Whisper MCP**
>
> Make sure Python and pip are installed, then run:
> ```bash
> pip install openai-whisper
> ```
>
> Add the following to your Claude Desktop config file:
> ```json
> "whisper": {
>   "command": "python",
>   "args": ["-m", "whisper_mcp"]
> }
> ```
>
> **Option 3: Transcribe with another tool first**
> - macOS: Dictation in Notes app
> - Windows: Windows Speech Recognition
> - Online: whisper.ai or similar tools
>
> Once converted to text, paste it directly into the chat.

---

### When Whisper MCP is available

1. Call `whisper_transcribe` with:
   - `file_path`: path to the uploaded audio file
   - `language`: `en` (English) or leave blank for auto-detection

2. After transcription, treat the text as the paper content and **return to SKILL.md Step 2** to continue.

3. Notify the user:
   > "🎤 Transcription complete. Here's what was recognized:
   > [first 100 words of transcript]...
   > Analyzing paper content now — please wait."

4. If the transcript is too short (< 100 words), warn:
   > "The transcription seems incomplete — this may be due to audio quality. Consider pasting the paper text directly for better results."

---

## General Voice Input Principles

- **Fault-tolerant first**: voice recognition may produce typos; prioritize semantic understanding over exact wording
- **Multilingual support**: mixed-language voice commands are accepted
- **Regardless of input method**, all content is passed back to the SKILL.md main flow for processing
