# Contributing

This repository accompanies a manuscript under preparation/review. Until the
paper is accepted, please open an **Issue** before submitting a pull request
so changes to the physics model, figures, or numerics can be reviewed against
the manuscript text.

## Reporting a problem

Please include:
1. Which figure / notebook cell / script function is affected.
2. The exact command or cell you ran.
3. The full traceback (if a crash) or the numeric discrepancy (if a wrong
   value), ideally with a reference to the manuscript equation it should match.

## Development setup

```bash
git clone https://github.com/<your-username>/SHQC3F-Carbon-Cycle.git
cd SHQC3F-Carbon-Cycle
conda env create -f environment.yml
conda activate shqc3f-carbon-cycle
# or: pip install -r requirements.txt
```

## Code style

- Keep every quantum object traceable to a manuscript equation label
  (`eq:...`, `thm:...`, `def:...`) in its docstring — see `src/shqc3f_co2_figures.py`
  for the convention used throughout.
- Any new figure should also log its underlying numbers via the `NumLog`
  utility (`NUM.add(...)`) so results stay auditable in
  `results/ALL_NUMERICAL_VALUES.txt`.
- Run `jupyter nbconvert --to notebook --execute --inplace notebooks/SHQC3F_CO2_figure_suite.ipynb`
  before opening a PR touching the notebook, and confirm no cell raises an error.
