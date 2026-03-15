# Module 2: 🧠 Mind Map

Visualize the paper's core structure as a mind map. Output a Mermaid code block directly — no plugins needed, renders natively in Claude.ai.

---

## Default Output: Mind Map (mindmap)

**Generate the mind map by default**, unless the user explicitly asks for a flowchart.

Output a Mermaid mindmap code block directly:

````mermaid
mindmap
  root((**[Paper Short Title]**))
    **Problem**
      [Pain point of prior work 1]
      [Pain point of prior work 2]
    **Method**
      [Core module 1]
        [Sub-component]
      [Core module 2]
    **Experiments**
      [Dataset name]
      [Key result + specific number]
    **Contributions**
      [Innovation 1]
      [Innovation 2]
    **Limitations**
      [Limitation 1]
````

After generating, ask: "Would you also like a **method pipeline flowchart**?"

---

## Optional: Method Pipeline Flowchart

If the user requests it, also output a Mermaid flowchart code block:

````mermaid
flowchart TD
    Input["📥 Input\n[input data type]"]

    subgraph Method["[Paper method name]"]
        Step1["[Step 1 name]\n[one-sentence description]"]
        Step2["[Step 2 name]\n[one-sentence description]"]
        Step3["[Step 3 name]\n[one-sentence description]"]
    end

    Output["📤 Output\n[output result]"]
    Result["📊 Key Result\n[PAPER_CORE.result key numbers]"]

    Input --> Step1 --> Step2 --> Step3 --> Output --> Result

    style Method fill:#e8f4f8,stroke:#2196F3
    style Result fill:#e8f5e9,stroke:#4CAF50
````

Adjust the number of nodes to match the actual steps in `PAPER_CORE.method`. Use the paper's real module names.

---

## Quality Requirements

- All node text must come from the paper; do not fabricate modules
- Numbers must come from `PAPER_CORE.result`; do not estimate
- Leaf node text should be under 8 words for readability
- Output as a standard Mermaid code block; user can also copy to [mermaid.live](https://mermaid.live) to edit further
