# Lung & Colon Cancer Histopathology Classification

[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-orange.svg)](https://pytorch.org/)
[![Dataset: LC25000](https://img.shields.io/badge/Dataset-LC25000-green.svg)](https://www.kaggle.com/datasets/andrewmvd/lung-and-colon-cancer-histopathological-images)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

A PyTorch notebook for comparing **ResNet-50** and **ViT-Base** on five-class lung and colon histopathology image classification with the **LC25000** dataset.

---

## 📌 Project Overview

The project implements a research and education workflow for five image classes:

1. `colon_aca`: Colon Adenocarcinoma (Malignant)
2. `colon_n`: Benign Colon Tissue
3. `lung_aca`: Lung Adenocarcinoma (Malignant)
4. `lung_n`: Benign Lung Tissue
5. `lung_scc`: Lung Squamous Cell Carcinoma (Malignant)

---

## 🧠 Architectures Compared

| Architecture | Paradigm | Total Parameters | Key Characteristic |
| :--- | :--- | :---: | :--- |
| **ResNet-50** | Convolutional Neural Network (CNN) | **23.52 M** | Deep residual bottlenecks with skip connections capturing localized cellular and gland textures. |
| **ViT-Base (`vit_b_16`)** | Self-Attention Transformer | **85.80 M** | $16 \times 16$ patch projection with Multi-Head Self-Attention (MHSA) capturing global spatial tissue dependencies. |

---

## 📊 Dataset & Preprocessing

- **Dataset**: [LC25000 (Lung and Colon Cancer Histopathological Images)](https://www.kaggle.com/datasets/andrewmvd/lung-and-colon-cancer-histopathological-images).
- **Loaded data in the recorded run**: 22,501 images in the train/validation directory and 2,499 in the test directory.
- **Notebook split**: 18,000 training images / 4,501 validation images / 2,499 test images.
- **Preprocessing Pipeline**:
  - Resized to $224 \times 224$ pixels.
  - Data Augmentation: Random horizontal flip, random rotation, color jitter (brightness/contrast adjustment).
  - ImageNet normalization ($\mu = [0.485, 0.456, 0.406]$, $\sigma = [0.229, 0.224, 0.225]$).

---

## 🔬 Evaluation Status

The notebook contains model definitions, data loading, training, checkpointing, and evaluation code for both architectures. The committed execution is incomplete: it stops near the start of ResNet training and contains no executed test metrics for either model. Previous accuracy tables and charts were removed because their values could not be traced to the saved notebook outputs.

### Dataset limitation

LC25000 contains augmented derivatives of a much smaller set of source images. This notebook uses image-level folders and a random validation split, without source-image or patient identifiers. Closely related image variants may therefore occur across splits and inflate performance. Results from this setup must not be interpreted as patient-level generalization or clinical validation.

---

## 📁 Repository Structure

```
Cancer_Histopathology_Classification_ViT_ResNet/
├── cancer_classification_vit_resnet.ipynb  # End-to-end notebook (Pipeline, ResNet-50 & ViT-Base)
├── requirements.txt                        # Python dependencies
├── README.md                               # Project documentation
├── LICENSE                                 # MIT Open-Source License
└── .gitignore                              # Standard PyTorch ignore rules
```

---

## 🚀 Getting Started

### Prerequisites
Install the required libraries:
```bash
python -m venv .venv
source .venv/bin/activate  # Windows PowerShell: .venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### Running the Notebook
Open `cancer_classification_vit_resnet.ipynb` in Jupyter Notebook or Google Colab:
```bash
jupyter notebook cancer_classification_vit_resnet.ipynb
```
Follow the step-by-step cells to:
1. Load and augment the LC25000 dataset.
2. Instantiate ResNet-50 and Vision Transformer backbones.
3. Train or load model checkpoints.
4. Run comparative evaluation and plot performance curves.

Update `data_root` before running. The committed path points to the local machine used for the original experiment. Training both pretrained backbones for the configured 25 epochs is compute intensive.
