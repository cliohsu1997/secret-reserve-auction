---
name: improve-academic-draft
description: Reviews and improves academic draft text by checking notation definitions, logical flow, tone, and mathematical consistency. Use when reviewing academic papers, LaTeX documents, draft text, or when the user asks to improve, review, or check academic writing.
---

# Improve Academic Draft

When invoked on draft text, perform these checks systematically:

## 1. Notation and Concept Definitions

- List all notations/symbols/technical concepts used
- Verify each is defined at its first appearance
- Flag undefined or late-defined terms

**Output**: Create a table listing all notations/concepts with their definitions and first appearance location.

## 2. Paragraph and Sentence Structure

- Each paragraph has a clear topic/purpose
- Sentences are concise; flag overly complex sentences
- Remove redundancy and fix ambiguous references

**Output**: Bullet list of structure issues with locations (paragraph/sentence numbers or line references).

## 3. Logic Flow

- Arguments progress clearly; conclusions follow from premises
- Identify logical gaps/unexplained jumps; improve transitions

**Output**: Bullet list of logic flow issues with locations and suggested improvements.

## 4. Academic Tone

- Flag informal/colloquial language
- Ensure consistent voice; use appropriate hedging

**Output**: Bullet list of tone issues with locations and suggested academic alternatives.

## 5. Grammar, Spelling, and Punctuation

- Fix spelling/grammar/collocation/punctuation
- **Remove all em dashes (—) and en dashes (–) from main text**
- Replace dashes with parentheses/colons/semicolons or split sentences

**Output**: Bullet list of grammar/spelling/punctuation issues with locations and corrections.

## 6. Mathematical Consistency

- List all equations/formulas
- Verify notation is consistent across math and matches the narrative
- Flag contradictions

**Output**: Table of equations with notation verification and consistency checks.

## 7. Proof Consistency and Validity

For each theorem/lemma/proposition proof:
- Verify logical validity and completeness
- Track assumptions and case coverage
- Verify correct application of definitions/results
- Flag circular reasoning, missing cases, unjustified steps, direction/quantifier errors, ambiguity

**Output**: Bullet list of proof issues with locations and specific problems identified.

## Output Format

Produce:

1. **Notation/Concepts Table**: All notations/symbols with definitions and first appearance
2. **Mathematical Consistency Table**: All equations with notation verification
3. **Structure Issues**: Bullet list with locations (paragraph/sentence references)
4. **Logic Flow Issues**: Bullet list with locations and suggested improvements
5. **Tone Issues**: Bullet list with locations and academic alternatives
6. **Grammar/Spelling/Punctuation Issues**: Bullet list with locations and corrections
7. **Proof Issues**: Bullet list with locations and specific problems
8. **Revised Cleaned Draft**: Complete revised version with all improvements applied

## LaTeX Auxiliary Files

When working with LaTeX drafts (e.g., in `draft/`):

- **Delete automatically generated auxiliary files** after edits or when the user requests a clean state (e.g., before committing, or when listing/cleaning the draft folder).
- Auxiliary file types to delete: `.aux`, `.log`, `.bbl`, `.blg`, `.out`, `.toc`, `.fls`, `.fdb_latexmk`, `.synctex.gz`, and optionally `.lof`, `.lot`.
- Do not delete source files (`.tex`, `.bib`) or output the user keeps (e.g., `.pdf` if they want it tracked).

## Workflow

1. Read the entire draft first
2. Perform checks 1-7 systematically
3. Compile all issues into organized output
4. Create revised draft with all improvements
5. Present both the analysis and the cleaned draft
6. When done with LaTeX drafts: delete auxiliary files as above if the user has asked to clean or commit
