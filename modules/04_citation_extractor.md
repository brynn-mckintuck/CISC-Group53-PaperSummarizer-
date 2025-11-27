## Purpose
Scan completed content and input text for URLs and embedded citations; list unique external resources.

## Inputs
- **Original paper text** (full).
- **Per-section signals** (URLs, IDs, refs).
- **Rendered summaries** (to ensure no missed links).

## Outputs
- **External Resources & references** section with unique items.

## Steps
1. **Scan sources**
   - Regex detect: http/https URLs.
   - Identify DOIs (10.\d{4,9}/[^\s]+), arXiv IDs (arXiv:\d{4}\.\d{4,5}), PubMed IDs (PMID:\d+).
   - Collect bracketed citations (e.g., “[Smith, 2021]”) but list only if they include a resolvable identifier or URL.

2. **Normalize and deduplicate**
   - Lowercase domains; strip trailing punctuation and tracking params.
   - Maintain a set of unique resources.

3. **Render output**
   - Create “External Resources & references” section.
   - List one resource per line; do not invent or expand beyond input.
   - If none found, state “No external resources detected in the input.”
