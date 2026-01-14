# Coral Reef Image Classification (Environmental Impact)

This project builds an image classification system to support **coral reef monitoring** by automatically classifying reef images into key categories. Manual reef assessment is time-consuming and requires expert knowledge; a CNN-based classifier can help scale monitoring efforts for conservation and environmental decision-making.

---

## Project Goals
- Classify coral reef images into **3 classes**:
  - `crustose_coralline_algae`
  - `porites`
  - `sand`
- Implement and compare **two CNN approaches**:
  1) **Custom Lightweight CNN** (built from scratch)
  2) **Transfer Learning (VGG19)** using ImageNet pretrained weights
- Evaluate using:
  - Accuracy
  - Precision / Recall / F1-score
  - Confusion Matrix
- Provide a **demo** showing predictions + confidence scores on unseen images.

---

## Dataset
- Source: Kaggle dataset `jxwleong/coral-reef-dataset`
- Annotation file used: `combined_annotations_remapped.csv`

The dataset contains point annotations. For image-level classification, annotations are aggregated per image (majority label per image). A cleaning step is applied to:
- remove junk columns (e.g., `Unnamed`)
- normalize label strings (strip/lowercase)
- keep only selected classes
- map `filename -> filepath`
- drop images without valid file matches
- (optional) remove uncertain images where the majority label ratio is below a threshold.

---

## Approach Overview

### 1) Custom Lightweight CNN
A compact CNN (Conv → BN → MaxPool blocks + GAP + Dense) trained end-to-end for fast training and baseline comparison.

### 2) Transfer Learning (VGG19)
VGG19 pretrained on ImageNet is used as a feature extractor with a custom classification head. (Optional fine-tuning can be applied with a smaller learning rate.)

---

## Results (Example)
Your exact results may vary depending on class balancing, split seed, and training settings.

- Test Accuracy: ~0.90
- Macro F1-score: ~0.82
- Confusion matrix shows most errors occur between visually similar reef textures (e.g., `porites` vs `crustose_coralline_algae`).

---

## Demo
The demo displays predictions on unseen images in a grid:
- True label
- Predicted label
- Confidence score

Example format:
> `True: porites`  
> `Pred: porites (0.98)`

---

## Installation

### 1) Create and activate a virtual environment
**Windows (PowerShell)**
```bash
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt