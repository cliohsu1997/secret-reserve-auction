---
name: literature-review
description: Guides how to write and format literature review entries for the RSI project. Use when summarizing papers, writing literature reviews, or when the user asks about review format, paper summaries, or review.tex.
---

# Literature Review Skill

When writing or updating literature review entries (e.g., in `draft/review.tex`), follow this structure and format.

## Structure

Each paper entry is a **subsection** with this order:

1. **Title and author** (subsection heading)
2. **Short summary** (background, setting, problem, methodology, perspective)
3. **Key results and main intuition** (more detail)
4. **Managerial implication** (optional, one bullet)

## 1. Subsection Heading

- Start with the **paper title** in full, then **(Author1, Author2, \& Author3, Year)**.
- Optionally append a short descriptor in parentheses (e.g., ``(online fashion retailer; DiD study, policy change on Nov 1, 2017)'').

Example:
```latex
\subsection{Price Markdowns to Induce Customers to Opt Out of Free Returns (Najafi, Duenyas, \& Singla, 2025)}
```

## 2. Short Summary

Use **bullet points** to cover, in order:

- **Background**: Why the question matters; prior evidence or context.
- **Setting**: Who are the agents (firm, consumers, regulator), what is exogenous (e.g., price, coverage), what is endogenous.
- **Problem**: The research question or decision (e.g., when to offer FO, how to set markdown).
- **Methodology**: Model type (theory, structural, reduced form), data if empirical (sample, period, key variables), identification/estimation in one line if relevant.
- **Perspective**: Whose objective is evaluated (e.g., seller profit vs.\ consumer surplus vs.\ social welfare). State explicitly (e.g., ``The paper approaches the problem from the \textit{seller's} perspective, evaluating \textit{profit} rather than consumer surplus or social welfare.'').

Keep the short summary concise (one or two sentences per bullet where possible).

## 3. Key Results and Main Intuition

- List **key results** (propositions, main findings) as bold or numbered items.
- For each result, give the **main intuition** in more detail: why the result holds, what trade-offs or mechanisms drive it, and how it depends on parameters (e.g., uncertainty, salvage value, expected valuation).
- Use nested `\begin{itemize} ... \end{itemize}` when a result has multiple sub-points or when intuition has several steps.

Example pattern:
```latex
\item Main results and intuition:
  \begin{itemize}
    \item \textbf{Result (Proposition X):} Statement. Intuition: ...
    \item \textbf{Result (Proposition Y):} Statement. Intuition: ...
  \end{itemize}
```

## 4. Managerial Implication (optional)

- One bullet summarizing what managers or policy makers should take away (e.g., when to use a policy, which products or markets it fits).

## LaTeX Format (review.tex)

- Wrap each entry in `\begin{itemize} ... \end{itemize}`.
- Use `\textit{...}` for emphasis (e.g., key terms like ex-ante, seller's perspective).
- Use `\textbf{...}` for result labels (e.g., Proposition numbers) and for **Perspective**.
- Use ``...'' for quoted terms (e.g., ``opt-out of free return'').
- Keep notation consistent with the paper (e.g., FR, FO, $s$, $\theta^h$).

## ⚠️ DELETE ALL AUXILIARY FILES (CRITICAL)

**When working with `draft/review.tex` or any LaTeX in `draft/`, you MUST delete all generated auxiliary files when done with edits or before committing.**

- **Delete ALL** of the following in `draft/`: `.aux`, `.log`, `.bbl`, `.blg`, `.out`, `.toc`, `.fls`, `.fdb_latexmk`, `.synctex.gz` (and optionally `.lof`, `.lot`).
- Do **not** delete source files (`.tex`, `.bib`) or the PDF unless the user requests it.
- This applies **every time** you finish editing `review.tex` or other draft LaTeX, not only when the user explicitly asks to clean.

## Extract intro and conclusion (`extract_intro_conclusion.py`)

When drafting entries from **introduction and conclusion sections** of each paper (not the full paper or abstracts):

- **Script:** `python/code/extract_intro_conclusion.py`. Extracts the **introduction (first 4 pages)** and **conclusion (last 4 pages before references/appendix)** from each PDF in `draft/papers` and writes one `.txt` per PDF to `draft/papers_intro_conclusion/`.
- **Extraction details:**
  - **Introduction**: First 4 pages of each PDF
  - **Conclusion**: Last 4 pages before references/appendix section (includes references page if found)
  - References detection requires both "reference(s)" header AND citation patterns
  - If references not found, extracts last 4 pages from the end
- **Source of papers:** `draft/papers` (Zotero RSI links). Run `doc/how_to_link_zotero_to_cursor/link_zotero_collection.py` if needed.
- **Run with Poetry** (virtual env in `python/virtual env`):
  1. From repo root: `cd python`, then `python -m venv "virtual env"`.
  2. `poetry env use "virtual env/Scripts/python"` (Windows) or `poetry env use "virtual env/bin/python"` (macOS/Linux).
  3. `poetry install`.
  4. `poetry run python code/extract_intro_conclusion.py`.
- **One-liner** (after setup): from `python/`, run `poetry run python code/extract_intro_conclusion.py`.
- See `python/README.md` for full setup and run instructions.

Use the extracted `.txt` files in `draft/papers_intro_conclusion/` (introduction and conclusion sections per paper) to draft or revise entries in `draft/review.tex` (background, setting, problem, methodology, perspective, key results, managerial implication).

## Workflow

1. (Optional) Run `extract_intro_conclusion.py` via Poetry (see above) to refresh `draft/papers_intro_conclusion/`.
2. Identify paper title, authors, year (from `draft/papers` PDFs or extracted `.txt`).
3. Draft short summary (background, setting, problem, methodology, perspective), using **introduction and conclusion sections** text when available.
4. List key results; for each, add a short paragraph of intuition.
5. Add managerial implication if relevant.
6. Ensure the entry matches the format of existing entries in `draft/review.tex`.
7. **Delete all auxiliary files in `draft/`** (see above). Do this always when done with edits.

## Examples

See [examples.md](examples.md) for full-entry examples following this standard.
