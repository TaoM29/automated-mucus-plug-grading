# Automated Grading of Mucus Plugs in Lung CT Scans

Research code and experiment notebooks developed for a 2026 Master's thesis in Data Science at the Norwegian University of Life Sciences (NMBU). The thesis received grade A.

## Overview

This repository documents a weakly supervised, slice-based approach to predicting a patient-level mucus plugging score from chest CT. It preserves the notebook-centric research workflow used in the thesis rather than presenting a production clinical system.

The clinical dataset is **not distributed**. This repository contains no CT volumes, DICOM files, patient identifiers, annotations, labels, fold assignments, trained checkpoints, or patient-level predictions.

## Research problem

The task is patient-level regression from chest CT examinations where only one mucus-burden target is available per examination. The models operate on selected axial slices and do not use slice-level mucus annotations.

## Methodology

```text
Chest CT
  -> HU preprocessing
  -> representative slice selection
  -> lung and mediastinal CT windows
  -> high-frequency third channel
  -> ResNet18 feature extraction
  -> ORB-BoVW features
  -> CNN and handcrafted feature fusion
  -> weak slice-level predictions
  -> patient-level aggregation
  -> mucus plugging score
```

The final internal configuration uses representative sampling, a three-channel high-pass CT representation, ResNet18, ORB bag-of-visual-words features, feature fusion, and patient-level aggregation. Five-fold patient-level cross-validation was used for internal evaluation. MosMed experiments study transfer and domain shift only; they are not external validation for mucus-burden prediction.

## Repository structure

```text
notebooks/main/      Main thesis experiments
notebooks/archive/   Earlier and alternative thesis experiments
configs/             Configuration guidance; no real paths or credentials
data/                Synthetic manifest schema and access guidance only
results/             Publication-safe aggregate results only
docs/                Methodology, data access, and reproducibility notes
thesis/              LaTeX thesis source and bibliography
```

## Notebook guide

| Notebook | Purpose |
| --- | --- |
| `01_data_preparation_and_baseline.ipynb` | DICOM/HU preparation logic and two-window baseline experiments. |
| `02_three_channel_dct_experiment.ipynb` | DCT-bandpass third-channel comparison. |
| `03_final_resnet18_orb_bovw.ipynb` | Final internal ResNet18 three-channel ORB-BoVW fusion configuration. |
| `04_mosmed_transfer_learning.ipynb` | Mucus-to-MosMed transfer and adaptation experiments. |
| `05_reverse_transfer_mosmed_to_mucus.ipynb` | MosMed-to-mucus transfer and adaptation experiments. |

Archived notebooks preserve legitimate development history and alternative experiments, but are not the recommended starting point.

## Main results

The aggregate five-fold internal results below are reproduced from the submitted thesis. Metrics are reported as mean +/- standard deviation across patient-level validation folds; error metrics are on the raw mucus-score scale.

| Experiment | MAE | RMSE | R2 | Spearman |
| --- | ---: | ---: | ---: | ---: |
| ResNet18, two-window input | 1.451 +/- 0.395 | 1.858 +/- 0.434 | 0.126 +/- 0.161 | 0.363 +/- 0.239 |
| ResNet18, three-channel input | 1.386 +/- 0.456 | 1.826 +/- 0.394 | 0.186 +/- 0.394 | 0.387 +/- 0.256 |
| ResNet18-3CH+BoVW | **1.244 +/- 0.297** | **1.712 +/- 0.505** | **0.236 +/- 0.295** | **0.498 +/- 0.346** |

These findings are exploratory and limited by the small internal cohort, weak supervision, and lack of external validation with a comparable mucus-burden target.

## Dataset availability

Clinical data and derived data are restricted and are not included. See [data/README.md](data/README.md). The example manifest contains only synthetic records.

## Reproducibility

Install the unpinned research dependencies with:

```bash
python -m pip install -r requirements.txt
```

Then configure paths to authorised data in the configuration cell near the beginning of the relevant notebook. Exact package versions, hardware details, and fully deterministic CUDA execution were not preserved in the original thesis snapshot; see [docs/reproducibility.md](docs/reproducibility.md).

## Thesis

The LaTeX source and bibliography are provided in `thesis/`. The final PDF is intentionally not bundled here; add the official publication URL when available.

## Citation

Please cite the associated thesis. Citation metadata is available in [CITATION.cff](CITATION.cff).

## Acknowledgements

The author thanks the thesis supervisor and collaborators who supported the research. Clinical data are not made available through this repository.

## License

No licence has yet been selected. See [LICENSE_PLACEHOLDER.md](LICENSE_PLACEHOLDER.md).
