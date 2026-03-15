# Module 1: 📊 Deep Analysis Report

Based on `PAPER_CORE`, produce a complete academic analysis report. Audience: researchers. Tone: professional and rigorous. **Output entirely in English.**

## Output Structure

Strictly follow these 7 sections in order. Do not skip any.

---

### 0. Abstract

Reproduce or closely paraphrase the paper's abstract. Keep academic language style; do not summarize or shorten.

---

### 1. Motivation

**a) Why this paper?**
What drove the authors to propose this approach? Research background and motivation.

**b) Pain points of prior work**
Specific limitations of existing mainstream methods (be concrete, not vague).

**c) Core hypothesis and intuition**
Summarize the paper's central research assumption in 2–3 sentences.

---

### 2. Method Design

> ⚠️ This is the most critical section — be thorough. The user may not read the original paper.

**a) Pipeline**
Input → each processing step (with technical detail) → output. For each step: what it does, why, and how it's implemented.

**b) Module architecture** (if a model/network structure exists)
Each module's function and how they work together.

**c) Key formulas and algorithms** (if applicable)
Plain-language explanation of each key formula's meaning and role.

---

### 3. Comparison with Prior Work

**a) Fundamental difference**: What is the most essential distinction?

**b) Contributions**: Core contributions as a numbered list

**c) When it works best**: In what settings does this method have the clearest advantage?

**d) Comparison table**

| Method | Core idea | Strengths | Weaknesses | What this paper improves |
|--------|-----------|-----------|------------|--------------------------|
| This paper | | | | |
| Baseline 1 | | | | |
| Baseline 2 | | | | |

---

### 4. Experimental Results

**a) Experimental setup**: datasets, baselines, evaluation metrics, implementation details

**b) Key results**: most representative numbers and conclusions (be specific)

**c) Where it shines**: settings where the advantage is most pronounced

**d) Limitations**: generalization, compute cost, data requirements, scope of applicability

---

### 5. Reproducibility & Applications

**a) Open-source status and reproduction advice**

**b) Implementation details**: hyperparameters, data preprocessing, training tricks

**c) Transfer potential**: can it be applied to other tasks or domains?

---

### 6. Summary

**a) One-liner** (≤15 words, from `PAPER_CORE.one_liner`)

**b) Quick-reference pipeline** (3–5 steps, plain language, no jargon)

Example format:
1. Take raw image, extract multi-scale features
2. Compute attention weights independently per region
3. Fuse features across scales with learned weights
4. Output final classification

---

## Output Rules

- If the paper does not cover a sub-item, write "Not covered in paper" — do not skip the section
- Focus depth on Methodology; avoid over-expanding Introduction and Conclusion
