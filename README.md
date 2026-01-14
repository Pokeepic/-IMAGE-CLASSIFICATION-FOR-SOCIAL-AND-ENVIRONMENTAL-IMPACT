# Coral Reef Image Classification (Environmental Impact)

This project builds an image classification system to support **coral reef monitoring** by automatically classifying reef images into reef-related categories. Manual monitoring is slow and requires expert knowledge; a CNN-based classifier can scale analysis for conservation and environmental decision-making.

---

## Project Goals
- Classify coral reef images into **3 classes**:
  - `crustose_coralline_algae`
  - `porites`
  - `sand`
- Implement and compare **two CNN approaches**:
  1) **Custom Lightweight CNN** (built from scratch)
  2) **Transfer Learning (VGG19)** (pretrained ImageNet backbone)
- Evaluate using:
  - Accuracy
  - Precision / Recall / F1-score (per class)
  - Confusion Matrix
- Provide a **demo** showing prediction outputs with confidence scores.

---

## Dataset
- Source: Kaggle dataset `jxwleong/coral-reef-dataset`
- Annotation file: `combined_annotations_remapped.csv`

The dataset contains **point-level annotations**. For image-level classification, annotations were aggregated per image (majority label per image). Data preparation includes:
- removing junk columns (e.g., `Unnamed`)
- standardizing label text (strip/lowercase)
- selecting only the target classes
- mapping `filename -> filepath`
- dropping entries with missing/unmatched images
- (optional) filtering “uncertain” images using a majority-threshold strategy

---

## Pipeline Summary
1. **Load & clean CSV annotations**
2. **Select 3 target classes**
3. **Create image-level labels** (majority vote per image)
4. **Stratified Train/Validation/Test split**
5. **Preprocessing**: resize to 224×224 and normalize
6. **Train 2 models**: Custom CNN and VGG19 transfer learning
7. **Evaluate** using classification report + confusion matrix
8. **Demo**: show predicted label + confidence on unseen images

---

## Models

### 1) Custom Lightweight CNN (from scratch)
A compact CNN (Conv → BatchNorm → MaxPool blocks + GAP + Dense head).
This model trains quickly but requires careful balancing and preprocessing consistency.

**Observed behaviour (current run):**
- Training accuracy increased, but validation accuracy remained very low.
- The model collapsed to predicting a single class (`sand`) for most/all samples.
- Confusion matrix confirms near-all predictions were `sand`.

This indicates poor generalization under class imbalance and limited feature learning from scratch.

### 2) Transfer Learning (VGG19)
VGG19 pretrained on ImageNet is used as a feature extractor with a custom classification head.
This approach achieved strong generalization and significantly better per-class performance.

---

## Results (Current Run)

### Custom CNN (from scratch)
- Validation accuracy: ~0.10–0.15 (low)
- Test accuracy: ~0.15
- Confusion matrix: model predicts mostly `sand`
- Per-class F1-score: near 0.00 for `crustose_coralline_algae` and `porites`

### VGG19 Transfer Learning
- Validation accuracy improved steadily during training
- Test performance is significantly better across classes
- Confusion matrix shows most samples are correctly classified
- Much higher macro and weighted F1 compared to Custom CNN

> Note: Results can vary depending on random seed, class balancing strategy, and train/val/test split.

---

## Demo
The demo shows predictions on unseen images with confidence scores in the format:
- `True: <label>`
- `Pred: <label> (<confidence>)`

Example:
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
