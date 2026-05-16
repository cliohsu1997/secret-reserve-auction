---
name: latex-compilation
description: Handles LaTeX compilation workflow including auxiliary file cleanup and proper citation compilation. Use when compiling LaTeX documents, fixing missing citations, or cleaning up auxiliary files.
---

# LaTeX Compilation Workflow

## Auto-Compile Requirement

**Mandatory:** Whenever any `.tex` file in this repository is modified, compile the affected document **in the same assistant turn**, before ending the response. Do not wait for the user to say “compile it” or “build the PDF.”

When any file under `draft/` is edited (especially `.tex`, `.bib`, or figure files used by LaTeX), compile the affected document before finishing the task. Standalone `.tex` files outside `draft/` follow the same rule: compile that file’s PDF after editing it.

## Automatic rebuild in Cursor / VS Code

This workspace’s **`.vscode/settings.json`** turns on **LaTeX Workshop** auto-build with `"latex-workshop.latex.autoBuild.run": "onFileChange"`. Whenever a `.tex` file is **written to disk** (manual save, auto-save, or another tool saving the file), LaTeX Workshop should rebuild the PDF for the detected root document without a separate “Build LaTeX project” click. Keep the correct root (e.g. open the standalone `.tex` or use a `% !TEX root` magic comment for subfiles).

- If the edited file is a standalone draft (e.g., `draft/multiproduct/oligopoly_simplified.tex`), compile that file directly.
- If the edited file is part of the main manuscript build, compile `draft/main.tex`.
- If references/citations are involved, use the full cycle below.

## Compilation Process for Citations

To ensure all citations and references appear correctly, run the full compilation cycle:

```
pdflatex -interaction=nonstopmode main.tex
bibtex main
pdflatex -interaction=nonstopmode main.tex
pdflatex -interaction=nonstopmode main.tex
```

**Important**: In PowerShell, run these as separate commands (do NOT use `&&` which is not supported).

### When to Use Full Compilation

- After adding new `\cite{}` commands
- After modifying `library.bib`
- When citations show as "?" in the PDF
- After deleting auxiliary files

### Quick Compilation (No Citation Changes)

If no bibliography changes, run pdflatex twice to stabilize cross-references:

```
pdflatex -interaction=nonstopmode main.tex
pdflatex -interaction=nonstopmode main.tex
```

## Auxiliary Files

### Common Auxiliary File Extensions

| Extension | Purpose |
|-----------|---------|
| `.aux` | Cross-references and citations |
| `.log` | Compilation log |
| `.out` | Hyperref bookmarks |
| `.bbl` | Processed bibliography |
| `.blg` | BibTeX log |
| `.toc` | Table of contents |
| `.lof` | List of figures |
| `.lot` | List of tables |
| `.fls` | File list (latexmk) |
| `.fdb_latexmk` | Latexmk database |
| `.synctex.gz` | SyncTeX data |

### Cleaning Auxiliary Files

Before committing or when troubleshooting, delete auxiliary files:

```powershell
# In the draft folder, delete common auxiliary files
Remove-Item main.aux, main.log, main.out, main.bbl, main.blg, main.fls, main.fdb_latexmk -ErrorAction SilentlyContinue
```

Or use the Delete tool to remove each file individually.

### Files to Keep

- `.tex` - Source files
- `.pdf` - Compiled output
- `.bib` - Bibliography database
- `.bst` - Bibliography style

### Files to Delete Before Commit

- All auxiliary files listed above
- Temporary/standalone compilation files (e.g., `*_standalone.tex`, `*_standalone.pdf`)

## Project-Specific Notes

- Main document: `draft/main.tex`
- Bibliography: `draft/library.bib`
- Bibliography style: `draft/ecta.bst` (Econometrica style)
- The estimation section is in `draft/estimation_gmm.tex` (included via `\input{estimation_gmm}`)

## Troubleshooting

### Citations Show as "?"

1. Delete all auxiliary files
2. Run the full compilation cycle (pdflatex -> bibtex -> pdflatex -> pdflatex)

### Undefined References

1. Run pdflatex twice to resolve cross-references
2. Check that all `\label{}` commands are defined before `\ref{}` calls

### BibTeX Errors

1. Check `main.blg` for error messages
2. Verify bibliography entries in `library.bib` are correctly formatted
