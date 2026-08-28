# An Uncertainty-Aware Machine Learning Emulator for the Reionization kSZ Power Spectrum

*In preparation for Publications of the Astronomical Society of Australia (PASA)*

This repository holds the paper-specific workflow (notebooks, scripts, and records) for the manuscript above. The reusable Python package is maintained separately at [reionemu/reionemu](https://github.com/reionemu/reionemu), with documentation at [reionemu.org](https://reionemu.org/).

---

## Requirements

Python 3.10 or newer. The emulator itself is installed from PyPI and pinned in `requirements.txt`.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

---

## Repository Layout

- **[notebooks/publication_results/](notebooks/publication_results/)**  
    Numbered notebooks 00–07 that produce every manuscript figure and record. Shared paths, constants, and plotting settings are defined in [config.py](notebooks/publication_results/config.py).

- **[notebooks/](notebooks/)**  
    Earlier exploratory notebooks covering parameter-space coverage, raw and processed data inspection, and proof-of-concept models.

- **[scripts/](scripts/)**  
    Parameter sampling, HPC simulation runs, dataset assembly, and hyperparameter tuning. These are environment-specific.

- **[datasets/](datasets/)**  
    Parameter sample files and simulation logs are tracked. Raw and processed HDF5 data are not.

- **[results/](results/)**  
    Figures and JSON records. The manuscript run is tracked and other runs are ignored.

- **[artifacts/](artifacts/)**  
    Self-contained experiment artifacts written by notebook 07. The manuscript artifact is tracked and other experiments are ignored.

- **checkpoints/**  
    Trained weights, normalizers, and the saved MCMC chain. Written by 02 and 04, read by 03 onward. Not tracked.

---

## Data and Artifacts

The processed dataset is archived separately. The figures, records, and experiment artifact for the manuscript run are tracked in this repository.

Archive DOI: TBA

Download the processed dataset to: `datasets/processed/publication_condensed_v6.h5`

---

## Workflow

Run the publication notebooks in this order:

1. [00_dataset_build.ipynb](notebooks/publication_results/00_dataset_build.ipynb)
2. [01_background_figures.ipynb](notebooks/publication_results/01_background_figures.ipynb)
3. [02_training_and_cv.ipynb](notebooks/publication_results/02_training_and_cv.ipynb)
4. [03_emulator_accuracy.ipynb](notebooks/publication_results/03_emulator_accuracy.ipynb)
5. [04_mcmc_single_case.ipynb](notebooks/publication_results/04_mcmc_single_case.ipynb)
6. [05_physical_validation.ipynb](notebooks/publication_results/05_physical_validation.ipynb)
7. [06_mcmc_batch_cases.ipynb](notebooks/publication_results/06_mcmc_batch_cases.ipynb)
8. [07_assemble_artifact.ipynb](notebooks/publication_results/07_assemble_artifact.ipynb)

Notebook 00 builds the processed HDF5 dataset from raw simulation output, which is not distributed. Starting from the archived processed dataset, the run begins at 01.

---

## Outputs

Each run writes to `results/pearce_2026_reionemu_mc_dropout/<experiment>/`. The manuscript run, `n_mc_201_epochs_1000_early_stop_150`, is tracked here, so its figures and records can be read without re-running anything.

Publication figures are saved under `results/` and numerical results are written alongside them under `records/`, one JSON or NPZ file per stage, so every quantity quoted in the manuscript can be traced back to the run that produced it:

- `dataset_build.json` - dataset provenance and build settings
- `heldout_indices.npy` - indices of the held-out test simulations
- `train_results.json` - training history and final losses
- `kfold_summary.json` - cross-validation summary across folds
- `heldout_metrics.json` - held-out accuracy and uncertainty-coverage metrics
- `heldout_predictions.npz` - held-out predictions and predictive spreads
- `physical_validation.json` - ionization-history and optical-depth checks
- `mcmc_batch_cases.json` - batch MCMC recovery across held-out cases

Notebook 07 collects those records into a self-contained artifact at
`artifacts/pearce_2026_reionemu_mc_dropout/mc_dropout_experiment_<experiment>/`:

- `info.json` - manifest, dataset summary and fingerprint, description
- `configs.json` - every config used, from dataset build through training
- `results.json` - summary, metrics, training history, and prep stats
- `model.pt` - trained weights and architecture
- `normalizers.npz` - input normalizer
