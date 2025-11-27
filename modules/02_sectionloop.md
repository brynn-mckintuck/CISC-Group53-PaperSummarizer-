> **Change Log (2025-11-27):**  
> Added `summary_level` modes ("short" | "detailed") with conditional summary behavior.

## Purpose
Iterate through each section, extract text span, summarize within constraints, and emit per-section outputs and signals.

## Inputs
- **Normalized sections** from Module 1.
- **Paper text** with boundaries.
- **Runtime config** (audience, length caps).
- **summary_level** = "short" | "detailed" (NEW)

## Outputs
- **Per-section summary** (≤300 words).
- **Flag:** {missing | short | ok}.
- **Signals:** Presence of equations, citations, URLs.

## Steps
1. **Extract span**
   - Use start/end markers to slice text.
   - If invalid indices or empty slice → flag as **missing**, summary = “Section missing or empty.”

2. **Summarize (by summary level)**
   - **If `summary_level = "short"`:**
     - Produce a 1–2 sentence summary focusing on objectives and key results.
     - No bullet points or expansion.
   - **If `summary_level = "detailed"`:**
     - Produce a short paragraph (~150–200 words) capturing objectives, methods, results, and limitations.
     - Append 3–5 bullet key points summarizing specific facts or findings.
   - Anchor content to explicit phrases, numbers, and named entities found in the span.
   - Enforce ≤300 words total; trim without altering meaning.


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

> Default `summary_level` = "short" if not specified.

### Notes
- Default `summary_level` = "short" if unspecified.  
- Module 03 (Guardrails) handles length violations and evidence validation.  
- Keep all summaries fact-bound to source text per strict evidence rules.
