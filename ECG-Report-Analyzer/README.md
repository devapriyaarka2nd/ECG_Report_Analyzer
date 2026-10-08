# ECG Report Analyzer — CNN Baseline

A Jupyter notebook that trains a convolutional neural network to classify ECG report images into four dataset classes. The implementation operates on images; it does not extract ECG waveforms or generate clinical report text.

## Classes

| Dataset class | Encoded label |
| --- | --- |
| Abnormal heartbeat | 0 |
| History of myocardial infarction | 1 |
| Myocardial infarction | 2 |
| Normal | 3 |

## Repository contents

| File or folder | Purpose |
| --- | --- |
| `ECG_Report_Analyzer_with_CNN.ipynb` | Image loading, CNN training, evaluation, and model export |
| `requirements.txt` | Python dependencies |
| `data/README.md` | Dataset folder requirements |
| `.gitignore` | Excludes local datasets, trained models, environments, and notebook checkpoints |

The dataset and trained weights are not included. This package was prepared from the supplied notebook, not from the inaccessible original ZIP.

## Setup

Create a Python virtual environment and install dependencies:

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Or on macOS/Linux:

```bash
source .venv/bin/activate
```

Then install and launch Jupyter:

```bash
python -m pip install -r requirements.txt
python -m jupyter lab
```

Dependencies are unpinned because the supplied notebook does not record its package versions. A compatible Python/TensorFlow environment must be selected; dependency installation and full training have not been verified for this prepared package.

## Dataset setup

Place your dataset under `data/ecg_report_images/`, following the folder naming rules in `data/README.md`. Alternatively, change `data_path` in the notebook or set `ECG_DATA_DIR` to the directory containing the four class folders.

PowerShell example:

```powershell
$env:ECG_DATA_DIR = "C:\datasets\ecg_report_images"
python -m jupyter lab
```

macOS/Linux example:

```bash
export ECG_DATA_DIR=/path/to/ecg_report_images
python -m jupyter lab
```

For Colab, open the notebook, mount Google Drive using its setup instructions, and point `data_path` to the dataset folder. Run all code cells in order.

The dataset's original source and license were not provided. Add the verified source citation and permitted-use terms before redistributing dataset files.

## Model and preprocessing

- Read images with OpenCV, resize to 240 × 240, and convert BGR to RGB.
- Normalize pixel values to the range 0–1 and one-hot encode labels.
- Apply two convolution/pooling blocks with 32 and 64 filters.
- Flatten features, apply a 128-unit dense layer and dropout of 0.2, and classify with a four-unit softmax layer.
- Train for 25 epochs using Adam and categorical cross-entropy.
- Save the trained model as `model.h5` and archive it as `model.h5.zip`.

The notebook loads all images into memory. `BATCH_SIZE = 32` is declared, but the supplied training call uses Keras's default batch size.

## Evaluation limitations

The baseline makes an 80/20 image-level split with `random_state=19`. It uses the same held-out data for validation during training and final evaluation. The displayed “Test accuracy” should therefore be interpreted as validation accuracy, not a result from an independent test set. No accuracy claim is made in this README.

The split is not stratified. Patient identifiers are not used for splitting, so patient-level separation cannot be established from this notebook. Full reproducibility is also not established: the split seed is fixed, but model initialization and training randomness are not seeded.

Before making research performance claims, use separate training, validation, and test sets, apply patient-level grouping where identifiers are available, and report per-class metrics. This repository contains an experimental image classifier; clinical suitability has not been established.

## Changes made for repository preparation

- Cleared saved cell outputs, execution counts, and Colab-specific cell metadata.
- Replaced the personal Drive path with a configurable dataset path and an explicit missing-directory error.
- Made Google Drive mounting optional and kept Keras imports under `tensorflow.keras`.
- Added notebook section descriptions, setup instructions, and exclusion rules.

The CNN architecture, label mapping, image preprocessing, split, training call, and model export behavior were preserved. Code cells passed syntax checks; training was not rerun because the dataset was not supplied.

## Create a separate GitHub repository

Suggested repository name: `ECG-Report-Analyzer`.

Suggested description: `CNN baseline for four-class ECG report image classification using TensorFlow and OpenCV.`

On GitHub, create an empty repository with that name. Extract this package, open a terminal in the `ECG-Report-Analyzer` folder, and run:

```bash
git init
git add .
git commit -m "Add ECG report classification CNN baseline"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/ECG-Report-Analyzer.git
git push -u origin main
```

Replace `YOUR_USERNAME` with the actual owner. Select public or private visibility when creating the repository. No GitHub repository has been created by this package.

No license has been selected. Add one after confirming your ownership of the code and the relevant dataset permissions.
