## Purpose
When mathematical notation is detected, identify important equations and explain them in plain English, clarifying variables and relationships.

## Activation criterion
- Trigger if any LaTeX blocks, inline math (e.g., \( ... \), 

\[ ... \]

), or symbolic formulas appear in any section.

## Inputs
- **Section texts** and **per-section signals** indicating math presence.

## Outputs
- **Equation explainer** section:
  - Each important equation.
  - A concise explanation of components, variables, units, and intuition.

## Steps
1. **Equation detection**
   - Parse LaTeX delimiters (\( \), 

\[ \]

, $$ $$) and common math symbols (=, Σ, ∂, ∇).
   - Extract candidate equations; filter to those central to objectives, models, transformations, or evaluation metrics.

2. **Variable and structure analysis**
   - Tokenize variables; map to definitions using nearby text.
   - Note relationships (proportionality, optimization targets, constraints, assumptions).

3. **Plain-English breakdown**
   - For each equation:
     - Show the equation verbatim.
     - Explain what it calculates or optimizes.
     - Define variables and units where available.
     - Provide the intuition and how it supports the paper’s goals.

4. **Formatting constraints**
   - Keep each explanation concise (preferably ≤200 words).
   - Use short paragraphs and labeled bullets.
   - Do not introduce new math not present in the source.
