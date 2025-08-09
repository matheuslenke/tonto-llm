## Tonto + LLM Guidance Experiment

This repository contains a small experiment used in the paper leveraging "LLM-Based Modeling Assistance for Textual Ontology-Driven Conceptual Modeling". The goal is to compare modeling assistance with and without custom UFO-based guidance texts.

### What this shows
- **Baseline (no guidance)**: The agent struggles with Tonto grammar/keywords and often misapplies UFO concepts (e.g., syntactically incorrect specializations, misuse of labels/descriptions).
- **With guidance**: The agent adheres to UFO and Tonto best practices, correctly using concepts (e.g., `kind`, `role`, `phase`, `category`, `relator`, `mode`, `quality`) and can produce more complex structures (e.g., powertype pattern) with fewer semantic issues.

### Repository layout
- `guidances/`: UFO-based guidance texts to steer the LLM. It contains the same files in the correct format for VS Code (`.github/instructions`) and Cursor (`.cursor/rules`).
- `experiment-with-guidances/`:
  - `university-before/`: input ontology for the guided condition.
  - `university-after/`: generated ontology (agent output) with guidance.
- `experiment-without-guidances/`:
  - `university-before/`: input ontology for the baseline condition.
  - `university-after/`: generated ontology (agent output) without guidance.

### Prerequisites
- Cursor IDE: see `https://cursor.com`.
- [Tonto VS Code extension](https://marketplace.visualstudio.com/items?itemName=Lenke.tonto) installed in Cursor for syntax highlighting and on-the-fly checks
- Access to any modern LLM available in Cursor. In our exploratory runs we observed good initial results with Claude 3.7 Sonnet, Gemini 2.5 Pro, and OpenAI o3; results may vary by model. We used cursor with the "Pro" plan.

### How to run the comparison:

> Important detail: The guidance rules only work if they are at the root of your current open folder in Cursor/ VsCode. Make sure that this is the case, otherwise no rule will be applied.

1) Guided condition
   - Open the workspace in Cursor.
   - Pin or otherwise add the files in `guidances/` (or `.cursor/rules`) as persistent guidance/context for the assistant.
   - Open `experiment-with-guidances/university-before/` in the editor.
   - Ask the agent the following prompt:
   ```
        Your task is to help me check the terminology of my ontology and fix semantic errors.
        Get the errors from @Linter Errors . Take a look at all packages.
        Also, create labels and descriptions in English and French, please.
   ```
   - Observe the agent’s edits and verify with the Tonto extension’s feedback.
   - For reference, compare with `experiment-with-guidances/university-after/`.

2) Baseline (no guidance)
   - Remove/unpin the guidance texts.
   - Open `experiment-without-guidances/university-before/`.
   - Use the same prompt:
   ```
    Your task is to help me check the terminology of my ontology and fix semantic errors.
    Get the errors from @Linter Errors . Take a look at all packages.
    Also, create labels and descriptions in English and French, please.
   ```
   - For reference, compare with `experiment-without-guidances/university-after/` and with the guided condition (grammar use, UFO concept adherence, structural correctness, label/description usage).

### Expected outcomes
- Without guidance, expect more grammar violations, misplaced UFO types, and documentation as code comments rather than proper `label`/`description` attributes.
- With guidance, expect broader and more accurate use of UFO concepts mapped to Tonto keywords, better-formed specializations/associations, and improved documentation.

### Notes
- Tonto is a textual language for UFO-based conceptual modeling, designed to be readable and expressive while enabling integration with text-centric tooling and LLMs.
- Cursor’s agent mode can create and edit files; keep the modeler in the loop and review changes suggested by the assistant.

### Reference
- Project repo: `https://github.com/matheuslenke/tonto-llm`
- Cursor: `https://cursor.com`


