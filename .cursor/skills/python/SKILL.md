---
name: python
description: Python code standards and project layout for the RSI project. Use when writing Python, running scripts via Poetry, or when the user asks about python/, virtual env, or extract_intro_conclusion.
---

# Python Skill

Follow these rules for Python code and the `python/` project layout. Style aligns with R coding conventions (line breaks, argument formatting) where applicable.

## ⚠️ IMPORTANT: All Python Code Must Be in `python/` Folder

**ALL Python scripts and code MUST be located in the `python/` folder and run through Poetry.** Do not create Python files in other locations (e.g., root directory, `extract_intro_conclusion/`). Legacy Python files outside `python/` should be deleted or moved to `python/code/`.

## Folder Layout

```
python/
├── virtual env/          → Virtual environment (python -m venv "virtual env"). Gitignored.
├── code/                 → ALL Python scripts (e.g. extract_intro_conclusion.py)
├── pyproject.toml        → Poetry config and dependencies
├── README.md             → Setup and run instructions
└── RUN.md                → Run task: how to execute scripts via Poetry
```

- **`virtual env`**: Create with `python -m venv "virtual env"`. Point Poetry at it with `poetry env use "virtual env/Scripts/python"` (Windows) or `"virtual env/bin/python"` (macOS/Linux). Do not track; `python/virtual env/` is in `.gitignore`.
- **`code`**: **ALL Python scripts MUST live here.** Paths in scripts use the RSI project root (parent of `python/`). No Python files should exist outside this folder.

## Code Style (R-like)

- **Function definitions**: One argument per line; trailing comma on last arg.
- **Loops**: Break lines for loop variable and iterable; keep body readable.
- **Imports**: Group stdlib, then third-party, then local. One per line or aligned.

Example:

```python
def process_pdf(
    path: Path,
    intro_pages: int = 3,
    concl_pages: int = 2,
) -> None:
    for i in range(intro_pages):
        # ...
```

## Running Scripts (Poetry + virtual env)

1. **Setup** (first time): `cd python`, then `python -m venv "virtual env"`, `poetry env use "virtual env/Scripts/python"`, `poetry install`.
2. **Run**: From `python/`, `poetry run python code/<script>.py`.

Example (extract intro+conclusion):

```bash
cd python
poetry run python code/extract_intro_conclusion.py
```

Output goes to `draft/papers_intro_conclusion/` (gitignored). See `python/RUN.md` and the **literature-review** skill for full usage.

## Examples

See [examples.md](examples.md) for examples.
