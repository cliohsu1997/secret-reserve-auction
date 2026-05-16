# Python Skill Examples

## Folder layout

```
python/
├── virtual env/
├── code/
│   └── extract_intro_conclusion.py
├── pyproject.toml
├── README.md
└── RUN.md
```

## Function (R-like argument formatting)

```python
def extract_pages(
    pdf_path: Path,
    intro_n: int = 3,
    concl_n: int = 2,
) -> list[int]:
    indices = list(range(min(intro_n, n))) + list(range(max(0, n - concl_n), n))
    return sorted(set(indices))
```

## Poetry run using virtual env

```bash
cd python
poetry run python code/extract_intro_conclusion.py
```

After setup (`python -m venv "virtual env"`, `poetry env use "virtual env/Scripts/python"`, `poetry install`), this uses the `virtual env` interpreter and installed deps (e.g. pymupdf).
