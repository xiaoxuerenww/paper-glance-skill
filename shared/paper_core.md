# Paper Core — Shared Extraction Layer

All modules depend on content extracted here. After reading the paper, the entry point (SKILL.md) populates the following structure. Subsequent modules reuse it directly — **do not re-read the paper**.

## Extraction Framework

After reading the paper, internally build the following "Paper Core Card" (not shown directly to the user — it is the raw material for all downstream modules):

```
PAPER_CORE = {

  # ── Basic Info ─────────────────────────────────────────
  title:        Paper title (original English)
  year:         Publication year
  venue:        Journal or conference (e.g. NeurIPS 2024, Nature, CVPR 2023)
  authors:      Author list (abbreviated, e.g. "Zhang et al." or first three)
  paper_type:   Type (Methods paper / Analysis paper / Survey / Application paper / Dataset paper)
  open_source:  Is code/data open-sourced? (Yes / No / Partial), with link if available
  arxiv:        arXiv link or DOI (if available)

  # ── Core Content ───────────────────────────────────────
  one_liner:    Core idea in one sentence, ≤15 words, no jargon
                Example: "Small models learn reasoning from large models via distillation"

  problem:      What problem does this paper solve? (2–3 sentences, plain language,
                explain why the problem is hard)
  prior_work:   What are the dominant existing methods? What are their core limitations?
                (2–4 sentences, name specific methods)
  hypothesis:   What is the paper's core assumption? (1–2 sentences, i.e. "We believe… therefore…")
  insight:      Core insights / innovations (2–4 items, one sentence each, specific not vague)
  contributions:Contributions as explicitly stated in the paper (taken directly from Introduction,
                listed verbatim)

  # ── Method ─────────────────────────────────────────────
  method:       Method pipeline overview (4–6 steps, one sentence each, with key technical details)
  key_modules:  List of core modules/components, one sentence per module explaining its role
                Example: ["Cross-Attention: fuses multimodal features",
                          "Dynamic routing: adaptively selects path based on input"]
  datasets:     Datasets used (name + scale + purpose, e.g. train / val / test)
  metrics:      Evaluation metrics (name + meaning, e.g. "BLEU-4: measures n-gram overlap
                between generated and reference text")

  # ── Experimental Results ────────────────────────────────
  result:       Most important experimental findings (3–5 items, each with specific numbers
                and comparison baseline)
                Example: "Achieves 87.3% Top-1 accuracy on ImageNet, +2.1% over ViT-L"
  ablation:     Key findings from ablation study (which module/design matters most?
                how much does performance drop without it?)
  failure_case: Cases where the method performs poorly (if failure analysis is included)

  # ── Assessment & Outlook ───────────────────────────────
  significance: Why does it matter? Who benefits? What impact might it have?
  limitation:   Main limitations (honest, including both author-acknowledged and reader-visible)
  future_work:  Future directions proposed by the authors (from Conclusion / Future Work)
  prerequisites:Background knowledge needed to understand the paper (list 2–4 key concepts)

  # ── Creative Modules ────────────────────────────────────
  fun_fact:     Counter-intuitive findings, unexpected failures, interesting ablation results
                (great material for podcasts; can be left null if none found)
  key_concepts: [term1, term2, ...]  # Key technical terms in the paper with brief explanations
  analogy:      A real-world analogy that helps non-experts understand the core method
                Example: "Like compressing a thick textbook into a one-page mind map,
                          but retaining the most important reasoning logic"
}
```

## Extraction Principles

- `one_liner` and `analogy` are the foundation of all creative modules — write them carefully, never be vague
- All numbers must come from the paper; do not estimate or fabricate
- `contributions` should be taken verbatim from the Introduction — do not paraphrase or substitute
- For `fun_fact`, prioritize: counter-intuitive results, unexpected failures, surprising ablation findings, things the authors themselves found surprising
- `ablation` is key for understanding design motivation — fill it whenever possible
- For **survey papers**: replace `method` with "main research directions covered", replace `key_modules` with "main sub-fields"
- For **dataset papers**: focus on `datasets` and `metrics`; `method` describes the data collection / annotation process
- If a field cannot be found, fill with `null` — never fabricate content
