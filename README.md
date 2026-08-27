# An Uncertainty-Aware Machine Learning Emulator for the Reionization kSZ Power Spectrum
## Publications of the Astronomical Society of Australia

This repository contains the paper-specific workflow for "An Uncertainty-Aware Machine Learning Emulator for the Reionization kSZ Power Spectrum."

The reusable Python package is maintained separately at [reionemu/reionemu](https://github.com/reionemu/reionemu) and documentation is available at [reionemu.org](https://reionemu.org/).
This repository contains the notebooks, scripts, records, and artifacts used to produce the PASA manuscript figures, tables, and numerical results.

## Installation
```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Data and Artifacts

Large datasets, trained checkpoints, MCMC chains, and generated results are not intended
to be stored directly in Git. They are archived separately.

Archive DOI: TBA

Layout after downloading archived artifacts:

```text
datasets/raw/sims_v6/
datasets/processed/publication_condensed_v6.h5
checkpoints/pearce_2026_reionemu_mc_dropout/mc_dropout_n_mc_201_epochs_1000_early_stop_150/
results/pearce_2026_reionemu_mc_dropout/n_mc_201_epochs_1000_early_stop_150/
```

## Workflow

Run the publication notebooks in this order:

1. `notebooks/publication_results/00_dataset_build.ipynb`
2. `notebooks/publication_results/01_background_figures.ipynb`
3. `notebooks/publication_results/02_training_and_cv.ipynb`
4. `notebooks/publication_results/03_emulator_accuracy.ipynb`
5. `notebooks/publication_results/04_mcmc_single_case.ipynb`
6. `notebooks/publication_results/05_physical_validation.ipynb`
7. `notebooks/publication_results/06_mcmc_batch_cases.ipynb`
8. `notebooks/publication_results/07_assemble_artifact.ipynb`

Shared paths and constants are defined in: `notebooks/publication_results/config.py`

## Expected Headline Results

The final manuscript run can be found in: `pearce_2026_reionemu_mc_dropout/n_mc_201_epochs_1000_early_stop_150`

- Held-out MAPE: 5.12%
- MC-dropout coverage: 67.1%, 89.7%, and 97.1% at 1/2/3 sigma
- Central mock ionization-history error: 2.4%
- Central mock optical-depth error: 1.2%
- Random held-out MCMC mean ionization-history error: 18.0%


## Directory Guide

