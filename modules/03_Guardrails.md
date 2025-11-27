 # module3_guardrails.md

## Purpose
Apply safeguards: handle missing/empty and short sections, prevent hallucinations, manage long-paper chunking, and enforce coherence.

## Inputs
- **Section outputs** from Module 2.
- **Chunk plan** and flags from Module 1.

## Outputs
- **Warnings list** for “Checks & Warnings.”
- **Validated summaries** (no invented content).
- **Chunking notes** if truncation occurred.

## Policies and steps
1. **Missing/empty sections**
   - If flag = missing: add warning “Section '<name>' missing or empty.”
   - Do not infer content or quantitative claims.

2. **<50-word sections**
   - If flag = short: add warning “Section '<name>' under 50 words; details may be insufficient.”
   - Keep minimal summary acknowledging limited detail.

3. **Hallucination mitigation**
   - Use only content present in section span.
   - If cross-section references are necessary, cite the section name rather than inventing details.
   - Mark uncertainties explicitly in warnings; never extend beyond textual evidence.

4. **Long-paper chunking (PS2 context-window strategies)**
   - Summarize per chunk; merge via constrained synthesis respecting original headings.
   - If any section was truncated due to chunking, add warning “Possible truncation due to context limits.”

5. **Coherence enforcement**
   - Ensure narrative flow: motivation → methods → results → limitations → implications.
   - Harmonize terminology; prefer glossary terms to resolve synonyms.

6. **Emit outputs**
   - Clean summaries, aggregated warnings list, chunking notes for final rendering.
