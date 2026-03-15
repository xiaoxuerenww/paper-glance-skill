# Module 3: 🔍 Peer Review

Produce a structured academic review from the perspective of a top-venue reviewer. **Output entirely in English.**

---

## Output Format

Follow this structure strictly — every section must be complete:

---

### 📋 Paper Review

**Title**: [paper title]
**Venue (if known)**: [conference/journal name, or "Unknown"]
**Overall Score**: [score 1–10 + one-line verdict, e.g. 6/10 — Interesting idea but needs stronger experiments]

---

### 1. Summary

Summarize the paper in 3–5 sentences covering: the core problem, the proposed method, and the main findings. Requirements:
- Objective — no evaluation, just description
- Must include: the specific problem addressed, the method's key idea, and the main experimental conclusion

---

### 2. Strengths

List 3–5 strengths. Format for each:

**[S1]** [Short title]: [1–2 sentences with specific evidence or numbers from the paper]

Evaluation dimensions to consider (pick the most relevant):
- Novelty: novel problem formulation / unique method design
- Empirical rigor: diverse datasets / comprehensive baseline comparisons
- Theoretical grounding: formal proofs or analysis
- Practical value: deployable / open-sourced / easy to reproduce
- Clarity: well-structured writing / intuitive figures

---

### 3. Weaknesses

List 3–5 weaknesses. Format for each:

**[W1]** [Short title]: [1–2 sentences of specific explanation] → **Suggestion**: [concrete improvement]

Evaluation dimensions to consider (pick the most relevant):
- Insufficient experiments: missing a specific comparison / incomplete ablation / single dataset
- Unclear motivation: lack of justification for a design choice
- Questionable scalability: not validated on other settings or scales
- Writing issues: a section is vague / figures are unclear
- Limitations not acknowledged: method's scope of applicability not discussed

---

### 4. Questions for Authors

List 3–5 questions that need clarification. Format:

**[Q1]** [Specific question?]

Questions should focus on:
- Justification for experimental design choices
- Rationale behind specific method decisions
- Reproducibility of results under particular conditions
- Specific differences from closely related work

---

### 5. Minor Comments (optional)

If any of the following exist, list them briefly (omit this section if none):
- Undefined formula symbols
- Reference formatting issues
- Unclear figure captions
- Typos or grammatical errors

---

### 6. Summary Decision

**Recommendation**: [Accept / Weak Accept / Borderline / Weak Reject / Reject]

**Justification** (2–3 sentences): Summarize the main reason for the recommendation, highlighting the 1–2 most critical factors.

---

## Quality Requirements

- Weaknesses must be specific — never write vague comments like "more experiments needed"; always name **exactly which experiment is missing**
- Questions must be genuine open questions, not restatements of weaknesses
- Scoring guide: 8+ = strong accept, 6–7 = accept with conditions, 4–5 = major revision, 1–3 = reject
- All evaluations must be grounded in `PAPER_CORE`; do not fabricate content not in the paper
