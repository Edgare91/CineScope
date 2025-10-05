# CineScope

Lightweight repo for exploratory analysis of a movie dataset (canonical CSV: `data/raw/imdb_top_1000.csv`). This project is notebook-first: primary work lives in `notebooks/` and reusable code should go into `src/`.

Important files
- `notebooks/edgar.ipynb` — example analysis using pandas.
- `notebooks/catlyn.ipynb` — reserved for additional analysis.
- `data/raw/imdb_top_1000.csv` — canonical dataset (large; `data/raw/*` is gitignored).
- `.github/copilot-instructions.md` — instructions for coding agents and contributors.
- `.gitignore` — currently ignores `data/raw/*` and `data/working/*` (do not commit raw/working data).

Conda-first quick start (recommended for collaborators)

1. Create the environment (if `environment.yml` exists):

```bash
conda env create -f environment.yml
conda activate cinescope
```

2. Or create/install manually:

```bash
conda create -n cinescope python=3.11 -y
conda activate cinescope
conda install -c conda-forge pandas numpy jupyter ipykernel matplotlib seaborn pytest -y
```

3. Register an IPython kernel so VS Code / Jupyter uses the correct interpreter:

```bash
python -m ipykernel install --user --name cinescope --display-name "CineScope (conda)"
```

4. Open the notebooks in VS Code or run the notebook server:

```bash
jupyter notebook notebooks/
```

Pip / virtualenv alternative

If you prefer pip/venv, create and activate a virtualenv then install the minimal packages:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install pandas numpy jupyter ipykernel matplotlib seaborn pytest
python -m ipykernel install --user --name cinescope-venv --display-name "CineScope (.venv)"
```

Smoke test (quick check that environment and data load work)

```bash
python -c "import pandas as pd; print(pd.read_csv('data/raw/imdb_top_1000.csv', nrows=3).head())"
```

Collaboration & data rules
- Do NOT commit raw or large working data. `data/raw/*` and `data/working/*` are ignored by `.gitignore`.
- Commit only small, reproducible outputs to `data/processed/`. If a dataset is too large to commit, include a download script and document how to obtain it in `CONTRIBUTING.md`.
- When exploratory code becomes reusable, move it to `src/` as small functions with clear inputs/outputs.

Project structure (recommended)

- `notebooks/` — exploratory notebooks (analysis + visualizations).
- `data/raw/` — original datasets (ignored).
- `data/processed/` — small processed outputs safe to commit.
- `src/` — reusable modules (e.g., `src/data/load.py`, `src/data/clean.py`).
- `tests/` — unit tests (pytest).

Testing & CI
- Add small pytest tests for any logic extracted to `src/` (e.g., `clean()` helpers). CI can install the conda env or use the pip `requirements.txt` if provided.

Extras and next steps
- Consider committing an `environment.yml` (conda) and optionally a `requirements.txt` for CI/pip users.
- Add a short `CONTRIBUTING.md` describing how to obtain the dataset and run analyses.

Questions? If you want, I can:
- create an `environment.yml` and a short `README` update, or
- generate starter modules under `src/` plus a tiny pytest test suite.
