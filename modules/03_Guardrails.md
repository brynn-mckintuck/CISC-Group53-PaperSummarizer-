> Module 03 (Guardrails) handles missing, short, and hallucination checks.


> **Change Log (2025-11-27):**  
> Added `evidence_mode = "strict"` option for stronger fact verification.  
> Added standardized warning messages for missing/empty and very short sections.

## Purpose
Apply safeguards: handle missing/empty and short sections, prevent hallucinations, manage long-paper chunking, and enforce coherence.

## Inputs
- **Section outputs** from Module 2.
- **Chunk plan** and flags from Module 1.
- **evidence_mode** = "default" | "strict" (NEW)

### Strict Evidence Mode (NEW)
When `evidence_mode = "strict"`:
- The summarizer must **only include claims, results, and equations** that appear explicitly in the provided text.  
- If it cannot find sufficient information to support a section, it must output this standardized warning:
  > “The source text does not provide enough detail to summarize this section in strict evidence mode.”
- The system should then:
  - Omit or blank the unsupported summary.
  - Tag the section with a flag such as `insufficient_evidence`.


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
