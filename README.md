# Takotsubo Syndrome Detection from CT Scans

This repository contains code for a third-year university project focused on detecting Takotsubo Syndrome in patient CT scans using a deep learning approach. The system consists of two main components:

- **`ML.ipynb`**: A Jupyter notebook containing the machine learning pipeline used to train and evaluate a 3D convolutional neural network (CNN).
- **`app.py`**: A Gradio-based web app interface for deploying the trained model and making predictions on new patient scan data.

---

## 📂 Project Folder Structure

The repository is organized as follows:

```
Takotsubo-Syndrome/
├── code_app/               # Code and resources for the app
│   ├── checkpoints/        # Directory for storing model checkpoints
|   |      └── epoch=32-step=957.ckpt
│   ├── app.py              # Gradio-based web application for predictions
│   ├── model.py            # Model definition and loading utilities
│   └── preprocess.py       # Preprocessing functions for input data
├── code_misc_scripts/      # Miscellaneous scripts and Jupyter notebooks
│   ├── dataset_analysis.ipynb       # Notebook for analyzing the dataset
│   ├── generate_metadata_csv.ipynb # Script for generating metadata CSV files
│   └── preprocessing.ipynb         # Notebook for initial testing on preprocessing data
├── code_model/             # Code and resources for model training
│   ├── ML.ipynb            # Jupyter notebook for training and evaluating the CNN model
│   ├── figures/            # Directory for storing generated figures
│   ├── missing_metadata_ids.txt     # List of missing metadata IDs
│   ├── normal_cases_metadata.csv    # Metadata for normal cases
│   └── takotsubo_cases_metadata.csv # Metadata for Takotsubo cases
├── data/                   # Directory for storing datasets (not included in the repo)
│   ├── normal_cases        # Direcotory for storing normal case dicom folders
│   └── takotsubo_cases     # Direcotory for storing takotsubo case dicom folders
├── .env                    # Environment variables file
├── .gitignore              # Git ignore file
├── README.md               # Project documentation
├── requirements_mac.txt    # Dependencies for macOS
├── requirements_general.txt # General dependencies
└── requirements_app.txt    # Dependencies for running the app
```

This structure ensures a clear separation of concerns, making it easier to navigate and maintain the project.

---

## 🧪 Environment Setup

You must use **Python 3.9.6**. Three separate `requirements.txt` files are provided:

- `requirements_mac.txt`: Tested on macOS
- `requirements_general.txt`: General list (doesn't include the special torch version included in the mac versio )
- `requirements_app.txt`: Tested for the app specifically

Choose the one appropriate for your setup:

### macOS setup
```bash
python3.9 -m venv venv
source venv/bin/activate
pip install -r requirements_mac.txt
```

### General setup
```bash
python3.9 -m venv venv
source venv/bin/activate
pip install -r requirements_general.txt
```

### App setup
```bash
python3.9 -m venv venv
source venv/bin/activate
pip install -r requirements_app.txt
```

# Running the Application
Make sure you have your trained model checkpoint saved at:
`./code_app/checkpoints/epoch=32-step=957.ckpt`

Then launch the app:
```bash
cd code_app
python app.py
```
This will start a Gradio interface in your browser, where you can:
- Upload a ZIP file containing the required DICOM folder structure.
- Enter the patient's age and gender in the provided fields.
- Receive a prediction with associated probability and timing details.


## 📦 Folder Upload Format

To run predictions using the GUI (`app.py`), the input must be a **ZIP file** containing a **single folder**, which in turn contains a subfolder called `DICOM/` with the DICOM images. Inside `DICOM/`, there should be another folder with the actual files (usually named like `EX00000`, but the name doesn't matter).

✅ Example structure:
```
EX12345678.zip
└── EX12345678/
    └── DICOM/
        └── EX00000/  # actual DICOM slices here
            ├── 1.dcm
            ├── 2.dcm
            ├── ...
```

❗️The outer folder can be named anything (ideally the Patient ID), but this internal format is required for the app to work.

# 📊 Model Performance

The 3D CNN model was trained on segmented heart volumes with age and gender metadata. Below are the key evaluation metrics:

### 📊 Model Performance Metrics

- **Recall (Sensitivity):** 100%
- **Specificity:** 92.9%
- **F1-Score:** 96.0%
- **AUC-ROC:** 0.96

Evaluation was conducted on a held-out test set with a class-balanced distribution.

Evaluation was conducted on a held-out test set with a class-balanced distribution.

# 🧾 Citation
If you use this work in your research or publication, please cite:

Awab Akram. Identifying Takotsubo syndrome in CT scans, BSc Final Year Project, University of Manchester, 2025.