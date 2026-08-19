# Reproducibility notes

The notebooks were developed in a Google Colab-oriented research environment. Public copies have been sanitised: executed outputs, private Drive mounts, private paths, and stored widget state have been removed.

## Environment

Install the dependencies in `requirements.txt` in a dedicated Python environment. Versions are intentionally unpinned because exact package versions and CUDA details were not retained in the thesis snapshot. The notebooks use Python type-union syntax and should be run with Python 3.10 or newer.

## Data and paths

Set `DATA_ROOT` to a directory containing authorised data and `OUTPUT_ROOT` to a local directory for generated outputs. Do not use the repository `data/` directory for clinical data and do not commit generated outputs.

## Important limitations

- The public notebooks do not run end-to-end without authorised clinical data and any required external dataset access.
- RadImageNet weights were downloaded by the original notebooks; review the upstream licence and access conditions before use.
- Several components use fixed seeds, but the original workflow does not guarantee complete Python, NumPy, PyTorch, or CUDA determinism.
- Results must be interpreted as exploratory research results, not as a clinical deployment system.
