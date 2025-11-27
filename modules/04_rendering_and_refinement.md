## Purpose
Render the final structured output, ensure consistent formatting, produce expert/lay variants, assemble glossary, and compile checks & warnings.

## Inputs
- **Validated per-section summaries** and flags.
- **Warnings list** and chunking notes.
- **Audience mode** from Module 1.

## Outputs
- **Paper summary** (≤300 words).
- **Section-by-section table** with flags.
- **Expert summary** (≤300 words).
- **Lay summary** (≤300 words).
- **Mini-glossary** (5–12 terms).
- **Checks & Warnings** consolidated.
- **Equation explainer (conditional placeholder)** if math detected.

## Steps
1. **Paper summary**
   - Synthesize across sections: problem, method, results, limitations, implications.
   - Keep ≤300 words; ensure neutrality and factual fidelity.

2. **Section-by-section table**
   - Columns: Section | Summary (≤300 words) | Flag.
   - One table only; no citations inside cells.

3. **Expert vs lay variants**
   - **Expert:** Preserve technical terminology, metrics, method details.
   - **Lay:** Translate jargon to plain language, emphasize significance and practical meaning, minimize non-essential numbers.

4. **Mini-glossary**
   - Extract 5–12 high-value terms/acronyms from summaries.
   - Provide concise, audience-appropriate definitions.

5. **Checks & Warnings**
   - Collate from guardrails: missing/short sections, ambiguities, truncation/chunking notes.
   - Present as labeled bullet list.

6. **Formatting**
   - Use exact headings: “Paper summary”, “Section-by-section table”, “Expert summary”, “Lay summary”, “Mini-glossary”, “Checks & Warnings”, “External Resources & references”, “Equation explainer”.
   - Short paragraphs and labeled bullets. No extra sections.
