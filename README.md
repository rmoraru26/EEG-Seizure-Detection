# EEG-Seizure-Detection
A patient-wise machine-learning pipeline for detecting epileptic seizure
activity in scalp EEG recordings from the CHB-MIT dataset.
This project investigates whether temporal and spectral EEG features can
distinguish normal interictal activity from ictal seizure activity.

The pipeline performs:

- automatic EEG download from PhysioNet;
- band-pass filtering between 0.5 and 40 Hz;
- segmentation into two-second windows;
- time-domain and frequency-domain feature extraction;
- comparison of three machine-learning classifiers;
- Leave-One-Patient-Out Cross-Validation;
- ROC, confusion-matrix, and feature-contribution analysis.

## Dataset

The project uses selected recordings from the
[CHB-MIT Scalp EEG Database](https://physionet.org/content/chbmit/1.0.0/).

The database contains long-term scalp EEG recordings from pediatric
patients with annotated seizure intervals. Signals were sampled at 256 Hz.

This experiment uses selected recordings from five patients:

- `chb01`
- `chb02`
- `chb03`
- `chb05`
- `chb08`

The EDF recordings are downloaded temporarily when the notebook is run.
They are not stored in this repository.

## EEG processing

Five bipolar EEG channels are included:

- FP1-F7
- F7-T7
- T7-P7
- P7-O1
- FP1-F3

Signals are filtered between 0.5 and 40 Hz and divided into non-overlapping
two-second windows.

## Extracted features

### Frequency-domain features

Relative spectral power is calculated for:

- Delta: 0.5–4 Hz
- Theta: 4–8 Hz
- Alpha: 8–13 Hz
- Beta: 13–30 Hz
- Gamma: 30–40 Hz

### Time-domain features

- Mean absolute amplitude
- Standard deviation
- Root mean square amplitude
- Line length

## Machine-learning models

The following classifiers are compared:

- Logistic Regression
- Random Forest
- Support Vector Machine

Feature scaling is performed inside each training fold where required.

## Patient-wise evaluation

The models are evaluated using Leave-One-Patient-Out Cross-Validation.

During each fold, all EEG windows from one patient are held out for
testing, while the remaining patients are used for training. This prevents
windows belonging to the same patient from appearing in both the training
and test sets.

## Results

Logistic Regression achieved the strongest overall performance:

| Metric | Mean score |
|---|---:|
| Accuracy | 76.9% |
| Sensitivity | 71.1% |
| Specificity | 82.7% |
| F1-score | 73.5% |
| ROC-AUC | 89.9% |

Performance varied across patients, demonstrating the difficulty of
generalizing EEG seizure-detection models to unseen individuals.

## Repository structure

```text
EEG-Seizure-Detection/
├── notebooks/
│   └── EEG_Seizure_Detection.ipynb
├── results/
│   ├── logistic_regression_evaluation.png
│   └── feature_contributions.png
├── .gitignore
├── LICENSE
└── README.md


