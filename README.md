# Data

Raw data files are **not committed** to this repository (see `.gitignore`) —
they are large, third-party, and update periodically at the source. Download
them yourself and point the pipeline at your local copies.

| File | Source | Used for |
|---|---|---|
| `co2_daily_mlo.csv` | [NOAA GML Mauna Loa, daily](https://gml.noaa.gov/ccgg/trends/data.html) | Figure 1 |
| `co2_mm_mlo.csv` | [NOAA GML Mauna Loa, monthly](https://gml.noaa.gov/ccgg/trends/data.html) | Figures 1, 9, 13 |
| `co2_annmean_mlo.csv` | [NOAA GML Mauna Loa, annual mean](https://gml.noaa.gov/ccgg/trends/data.html) | Figures 1, 14 |
| `tas_Global_yearly_ensemble_ssp119_r1i1p1f1_anomaly_2015-2100_mean (1).csv` | CMIP6 SSP1-1.9 global-mean near-surface temperature anomaly ensemble | Figure 2 |

## How to point the pipeline at your files

Edit the `Config` dataclass at the top of `src/shqc3f_co2_figures.py`
(equivalently, the first code cell under "Part 0" in
`notebooks/SHQC3F_CO2_figure_suite.ipynb`):

```python
daily_path:   str = r"/path/to/co2_daily_mlo.csv"
monthly_path: str = r"/path/to/co2_mm_mlo.csv"
annual_path:  str = r"/path/to/co2_annmean_mlo.csv"
tas_path:     str = r"/path/to/tas_Global_yearly_ensemble_ssp119_r1i1p1f1_anomaly_2015-2100_mean (1).csv"
```

If a file is missing or fails to parse, the pipeline substitutes a **clearly
labelled synthetic placeholder** (printed as `[warning] ... substituting a
clearly-labelled synthetic placeholder`) so the rest of the run still
completes — but any figure built on a placeholder must be regenerated from
the real file before it is used in the submitted manuscript. Check
`results/ALL_NUMERICAL_VALUES.txt` for a `[note]` line listing which, if any,
datasets were substituted in a given run.
