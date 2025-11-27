# module2_section_loop.md

## Purpose
Iterate through each section, extract text span, summarize within constraints, and emit per-section outputs and signals.

## Inputs
- **Normalized sections** from Module 1.
- **Paper text** with boundaries.
- **Runtime config** (audience, length caps).

## Outputs
- **Per-section summary** (≤300 words).
- **Flag:** {missing | short | ok}.
- **Signals:** Presence of equations, citations, URLs.

## Steps
1. **Extract span**
   - Use start/end markers to slice text.
   - If invalid indices or empty slice → flag as **missing**, summary = “Section missing or empty.”

2. **Summarize**
   - Focus on: objectives, approach, core results, limitations, key takeaways.
   - Anchor to explicit phrases, numbers, named entities found in the span.
   - Enforce ≤300 words; trim if needed without altering meaning.

3. **Constraint checks**
   - If span <50 words → flag **short**; produce minimal factual summary and defer to guardrails.
   - Ensure terminology consistency and topic progression.

4. **Signals collection**
   - Detect math indicators (LaTeX markers, inline symbols).
   - Detect URLs/DOIs/arXiv/PubMed IDs.
   - Detect bracketed references (e.g., “[Smith, 2021]”).

5. **Emit outputs**
   - Per-section consolidated object:
     - {section_name, summary, flag, signals: {math, urls, ids, refs}}
