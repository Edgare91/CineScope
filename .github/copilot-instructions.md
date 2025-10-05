## Purpose
Short, actionable guidance for AI coding agents working in this repository (CineScope).

## Quick context
- Primary work is exploratory data analysis in Jupyter notebooks under `notebooks/` (examples: `notebooks/edgar.ipynb`, `notebooks/catlyn.ipynb`).
- Raw data lives in `data/raw/` (example: `data/raw/imdb_top_1000.csv`).
- There is a `data/processed/` folder intended for outputs; `data/working/` is used for intermediate files.
- `src/` is currently empty — canonical place to add reusable Python modules or CLI scripts.

## Rules & constraints an agent should follow
- Do not add or commit large raw or working data files. The repository `.gitignore` explicitly ignores `data/raw/*` and `data/working/*` (Spanish note: "No subir datos crudos ni working"). Prefer writing code that reads from `data/raw/` but assume raw files are large and may be excluded from Git history.
- Prefer producing reproducible, small artifacts in `data/processed/` that can be checked in. If outputs are large, ask the human about using git-lfs or a remote storage location.
- Keep notebooks focused on exploration; when logic becomes reusable or testable, extract it to `src/` with a small public API (functions that accept filepaths / DataFrame and return DataFrame/results).

## Typical patterns and examples (do these exactly)
- Loading the main CSV (use pandas):

  Example: `df = pd.read_csv('data/raw/imdb_top_1000.csv')`

- Notebook authors have used inline cleaning and pandas transformations. When refactoring, create functions like `load_raw(path) -> pd.DataFrame`, `clean(df) -> pd.DataFrame`, and `save_processed(df, path)` in `src/`.
- Example module layout (recommended):

  - `src/data/load.py`  # load_raw
  - `src/data/clean.py` # cleaning helpers
  - `src/analysis/run.py` # orchestration scripts

## Environment & developer workflows (how to run/test)
- There is no project-wide `requirements.txt` or test runner in the repo. Minimal reproducible environment commands an engineer will likely run locally:

  - Create a venv and install essentials (if no `requirements.txt` exists):

    python -m venv .venv
    source .venv/bin/activate
    pip install --upgrade pip
    pip install pandas jupyter notebook

  - Start a notebook server and open the notebooks:

    jupyter notebook notebooks/

- When you add reusable code to `src/`, add a `requirements.txt` and simple tests (pytest). Prefer small, fast unit tests under a `tests/` folder.

## Integration points & external dependencies
- Current observable external dependency is the CSV dataset `data/raw/imdb_top_1000.csv`. No APIs or services were detected.
- If you add external data sources or services, document them in a top-level `README.md` and add credentials handling notes. Do not commit credentials.

## Suggested behaviors for AI edits
- Make minimal, incremental changes. Prefer creating small, well-named modules in `src/` and export small functions.
- When modifying notebooks, prefer adding new code cells instead of rewriting existing narrative cells unless requested.
- Before creating or modifying files that will change repository behavior (CI, packaging), ask a human when the repo lacks tests or a README.

## Files to reference when making changes
- `notebooks/edgar.ipynb` — example analysis cells using `pandas` and cleaning steps.
- `notebooks/catlyn.ipynb` — currently empty but reserved for more analysis.
- `data/raw/imdb_top_1000.csv` — canonical dataset used by notebooks.
- `.gitignore` — enforces not committing raw and working data.

If anything here is unclear or you'd like the instructions tuned to prefer a different structure (for example, a CLI-first layout or adding CI/tests), tell me what to change and I will update this file.
