# SHQC³F — Scalable Hybrid Quantum-Classical Frameworks for Carbon Cycle Prediction

[![CI](https://github.com/<your-username>/SHQC3F-Carbon-Cycle/actions/workflows/ci.yml/badge.svg)](https://github.com/<your-username>/SHQC3F-Carbon-Cycle/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/code%20license-MIT-blue.svg)](LICENSE)
[![Python 3.11](https://img.shields.io/badge/python-3.11-blue.svg)](environment.yml)

Manuscript, code, and the publication-figure suite for **SHQC³F**: a hybrid
quantum-classical modeling framework for the global carbon cycle, built on a
Quantum Biogeochemical Lindblad Master Equation (QBLME), a data
re-uploading variational quantum circuit (VQC), and a quantum-natural-gradient
VQE, benchmarked against NOAA Mauna Loa CO₂ observations and a CMIP6
SSP1-1.9 temperature-anomaly trajectory.

> **Status:** manuscript in preparation / under review. See
> [`manuscript/README.md`](manuscript/README.md) for licensing details on the
> paper text (separate from the MIT-licensed code below).

---

## Repository structure

```
SHQC3F-Carbon-Cycle/
├── manuscript/          LaTeX source for the paper (main.tex)
├── notebooks/           SHQC3F_CO2_figure_suite.ipynb — the Jupyter notebook version
├── src/                 shqc3f_co2_figures.py — the same pipeline as a plain script
├── figures/              16 publication-ready vector PDFs + combined report
├── results/              Every numeric value behind every figure (CSV + master .txt)
├── data/                 README only — see below, raw data is not committed
├── docs/                 (reserved for supplementary documentation)
└── .github/workflows/    CI smoke test
```

## What's in the pipeline

Every quantum object is built **directly from the manuscript's own
equations** — not hand-drawn — and every figure prints and saves the exact
numbers it plots. The physics core (`src/shqc3f_co2_figures.py`, Parts 0–2)
implements:

- the three-reservoir (atmosphere / land / ocean) carbon-cycle Hamiltonian `H_carb`,
- the Quantum Biogeochemical Lindblad Master Equation (QBLME) and its Gibbs steady state,
- an exact Pauli (Walsh–Hadamard) decomposition of `H_carb`,
- a data re-uploading variational quantum circuit (VQC) and its Fourier-expansion theorem,
- a VQE with a quantum-natural-gradient optimizer, and quantum Fisher information,
- zero-noise extrapolation (ZNE) and NISQ circuit-resource scaling,
- a classical Ensemble Kalman Filter for data assimilation, and
- the Quantum Carbon Advantage Theorem's analytic error bounds.

Figure 13 — the centerpiece — trains the VQC (+ a small classical residual
layer) on the **first 75% of the real Mauna Loa monthly record** and
evaluates it **out of sample** on the rest, against classical baselines,
with every RMSE computed fresh from data (never copied from the manuscript).

See [`figures/README.md`](figures/README.md) for the full figure-by-figure
mapping to manuscript equation/theorem labels.

## Quickstart

```bash
git clone https://github.com/<your-username>/SHQC3F-Carbon-Cycle.git
cd SHQC3F-Carbon-Cycle

# Option A: conda
conda env create -f environment.yml
conda activate shqc3f-carbon-cycle

# Option B: pip
pip install -r requirements.txt
```

### 1. Point the pipeline at your data

Download the four source files (see [`data/README.md`](data/README.md)) and
edit the `Config` dataclass at the top of `src/shqc3f_co2_figures.py` (same
cell in the notebook, under "Part 0") with your local paths.

If a file is missing, the pipeline falls back to a clearly-labelled synthetic
placeholder so it still runs end to end — but regenerate before submitting
any figure built on a placeholder.

### 2. Run it

**As a script:**
```bash
python src/shqc3f_co2_figures.py
```

**As a notebook:**
```bash
jupyter notebook notebooks/SHQC3F_CO2_figure_suite.ipynb
# Kernel → Restart & Run All
```

Either way, runtime is ~1.5–2 minutes on a normal laptop and produces:
- `SHQC3F_figures/fig01..fig16*.pdf` — one vector PDF per figure
- `SHQC3F_figures/SHQC3F_all_figures_report.pdf` — all figures, one document
- `SHQC3F_figures/numerics/*.csv` + `SHQC3F_figures/ALL_NUMERICAL_VALUES.txt` — every plotted number

Copy the regenerated `SHQC3F_figures/` contents into `figures/` and
`results/` in this repo before committing a new version.

## Building the manuscript PDF

```bash
cd manuscript
latexmk -pdf main.tex
```

## Citation

See [`CITATION.cff`](CITATION.cff) (GitHub renders a "Cite this repository"
button automatically once this file is present on the default branch).

## License

Code (`src/`, `notebooks/`) is MIT-licensed — see [`LICENSE`](LICENSE). The
manuscript text in `manuscript/main.tex` is **not** covered by that licence
(all rights reserved pending submission) — see
[`manuscript/README.md`](manuscript/README.md).

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md).

---

### Before you make this repository public

- [ ] Replace `<your-username>` in this README and in `CITATION.cff` with your actual GitHub handle
- [ ] Fill in your full name / ORCID in `CITATION.cff` and the copyright line in `LICENSE`
- [ ] Confirm your institution/journal allows a public preprint + code repo before the paper is accepted
- [ ] Re-run the pipeline on your **real** downloaded datasets and replace the contents of `figures/` and `results/` (do not submit synthetic-placeholder figures)
- [ ] Double-check `manuscript/main.tex` does not contain any `#TODO`/private notes before pushing
