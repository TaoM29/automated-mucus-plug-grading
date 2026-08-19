# Restricted data access

The original clinical dataset is not released. This includes DICOM data, converted HU volumes, NIfTI files, annotations, labels, patient identifiers, DICOM UIDs, acquisition metadata, splits, and trained checkpoints.

To reproduce the workflow, an authorised researcher must obtain independent approval for the underlying data and prepare local inputs outside this repository. Use `data/example_manifest.csv` only as a schema example. It contains synthetic records and must not be joined with real study data.

Before sharing any derivative output, confirm that it cannot disclose patient information. In particular, do not publish CT screenshots, notebook outputs, per-patient tables, identifiers, metadata, or predictions without documented approval.
