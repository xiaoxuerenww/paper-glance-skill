# Module 4: 📢 Promotional Scripts

Turn the paper into multiple promotional formats. Use cases: author self-promotion, lab outreach, science communication. **Output entirely in English.**

## Ask for Desired Format

> "Which type of promotional content do you need? (You can pick multiple)
> A) 🐦 Social media thread (Twitter/X style)
> B) 📱 Blog / newsletter summary (500–800 words, for general readers)
> C) 🎤 Conference talk opener (30-second verbal intro for peers)
> D) 📧 Email summary (brief update to advisor or collaborator)
> E) All of the above"

---

## Format A: Social Media Thread (Twitter/X)

```
🧵 [casual title summarizing the paper] (1/N)

[PAPER_CORE.problem rephrased as a relatable everyday observation]

[1–2 high-impact numbers from PAPER_CORE.result]

🔑 Key insight: [distilled version of PAPER_CORE.analogy]

📄 Paper: [title]
🔗 [arxiv link (omit this line if unavailable)]

#MachineLearning #AI #[relevant field tag]
```

Constraints: each tweet ≤ 280 characters; generate 3–5 connected tweets in a thread.

---

## Format B: Blog / Newsletter Summary

500–800 words, structured as follows:

```
**Title**: [engaging headline starting with a question or number, ≤12 words]

**Hook** (50 words):
A scenario or question that resonates with a general reader

**Background** (100 words):
What problem this field is tackling and why it matters

**What this paper does** (200 words):
Use PAPER_CORE.analogy to explain the core method.
Avoid formulas. Use phrases like "essentially", "think of it as", "it's like".

**How well does it work** (100 words):
Key numbers + comparison to prior methods, with context

**Why it matters** (150 words):
PAPER_CORE.significance — potential impact on industry or daily life

**Further reading**:
Paper title, authors, year, venue
```

Writing style: like a knowledgeable friend sharing something interesting — direct, no jargon-dropping, with a point of view.

---

## Format C: Conference Talk Opener

30-second verbal intro for an academic audience — formal but engaging.

```
[Version 1: Conference presentation]
"I'm going to talk about [PAPER_CORE.title].
 The problem we're addressing is [problem, one sentence].
 Our key insight is [insight, use analogy as a hook].
 We show that [result, key number].
 I'll walk you through our approach in the next [X] minutes."

[Version 2: Poster session]
"Hi, this poster is about [topic].
 [problem rephrased as everyday frustration].
 We found that [one_liner].
 If you're interested in [1–2 key concepts], let's chat!"
```

---

## Format D: Email Summary

Brief update to an advisor or collaborator, 100–150 words.

```
Subject: Paper recommendation | [PAPER_CORE.title]

Hi [name],

Wanted to share a paper I came across: "[title]" ([venue] [year]).

Core contribution: [one_liner].

Methodologically, [1–2 sentence overview of method].

Key result: [most important single number from result].

[Optional: one sentence on how this connects to our research direction]

Link: [if available]
```

---

## General Principles

**Numbers need context**: don't say "accuracy improved by 3%"; say "3% better than the previous best method — roughly equivalent to…"

**Use analogies instead of jargon**: for non-expert audiences, every technical term needs a plain-language explanation

**Good headline formulas**:
- Number-led: "Matching GPT-4's performance with 1% of the parameters"
- Question-led: "Why do AI models keep forgetting? This paper has an answer"
- Reversal: "We thought the model was reasoning — turns out it was just memorizing"
