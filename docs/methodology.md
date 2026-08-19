# Methodology overview

The thesis formulates mucus-plug grading as patient-level regression from chest CT. A patient-level target is available for each CT examination, while the learning pipeline processes selected axial slices without slice-level labels.

The main workflow is:

1. Convert selected CT series to HU-like volumes and construct a dataset index in an authorised environment.
2. Restrict each volume to central slices, remove low-value candidates using QC heuristics, reserve informative slices, and fill the selection through PCA-assisted MiniBatchKMeans diversity sampling.
3. Create lung-window and mediastinal-window inputs; the main model adds a lung-window high-pass channel with lung-mask suppression.
4. Train a pretrained CNN with weak slice-level supervision, then aggregate slice estimates to patient-level predictions.
5. Evaluate patient-level predictions in five-fold cross-validation.

The main reported internal configuration combines a ResNet18 backbone with ORB descriptors encoded through a bag-of-visual-words vocabulary and concatenated feature fusion. DCT, other high-frequency representations, DenseNet121, and alternative settings are retained as comparison experiments.

MosMed experiments investigate transfer between different CT prediction targets. They are not external validation of the mucus-burden task.
