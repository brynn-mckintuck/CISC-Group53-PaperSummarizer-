# module1_intake_and_setup.md

## Purpose
Normalize section metadata, ingest input text, detect missing/short sections, set audience and constraints, and plan chunking for long papers.

## Inputs
- **Paper text:** Extracted text from PDF with reliable section boundaries.
- **Section list:** Ordered sections with start/end markers.
- **Audience:** {expert | lay} (default: expert).

## Outputs
- **Normalized sections:** Canonical names, order, start/end markers.
- **Detection report:** Missing or short (<50 words) sections.
- **Chunk plan:** Mapping of sections to chunk IDs for long papers.
- **Runtime config:** Word-limit caps and coherence checks enabled.

## Steps
1. **Validate inputs**
   - Require non-empty paper text and a non-empty ordered section list with valid boundaries.
   - If invalid, record errors for “Checks & Warnings” and continue with available sections.

2. **Normalize sections**
   - Canonicalize names (e.g., “Intro” → “Introduction”, “Methods” → “Methodology” where appropriate).
   - Ensure uniqueness and strict order; trim whitespace; collapse duplicate headers.
   - Result: sections[i] = {name, order, start, end}.

3. **Span extraction test**
   - For each section, compute span length; if 0 → **missing**; if <50 words → **short**.
   - Record flags for downstream guardrails.

4. **Audience and constraints**
   - Set audience mode (expert or lay); default expert.
   - Enforce per-section summary cap ≤300 words; coherence checks = enabled.

5. **Chunk planning (PS2 context-window strategies)**
   - If total text length exceeds operational context, segment by section boundaries.
   - Build chunk index: section_id → [chunk_ids].
   - Prioritize core sections (Abstract, Introduction, Methods, Results, Discussion, Conclusion) in first pass.

6. **Emit outputs**
   - Normalized section list, flags, chunk plan, runtime config to subsequent modules.
