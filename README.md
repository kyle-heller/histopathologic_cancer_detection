# 🧬 Histopathologic Cancer Detection (Kaggle Project)

This repo contains my work for the [Histopathologic Cancer Detection Kaggle competition](https://www.kaggle.com/competitions/histopathologic-cancer-detection).  
The goal is binary image classification: determine if a given 96x96 pathology image patch contains metastatic cancer.

---

## 📂 Project Structure
- `notebooks/` → Jupyter notebooks with EDA, model training, and results  
- `submission.csv` → Kaggle submission file  
- `histopathologic-cancer-detection/` → dataset folder  
  - `train/` → 220k+ labeled `.tif` images  
  - `test/` → 57k unlabeled `.tif` images  
  - `train_labels.csv` → file with `id,label` (0 = no cancer, 1 = cancer)  

---

## ⚡ Approach
### 1. Data Prep
- Train/validation split (80/20).  
- Keras `ImageDataGenerator` for normalization + augmentations (flips, rotations).  
- Labels cast to strings (needed for binary generators).  
- Careful fix: `.tif` extensions added to filenames to avoid invalid image issues.  

### 2. Baseline Model
- Simple CNN with 3 Conv2D → MaxPooling → Dense layers.  
- Accuracy ~0.88 on validation after 5 epochs.  

### 3. ResNet50 Model
- Transfer learning using pretrained ResNet50 (ImageNet weights).  
- Input resized to 96x96, final layers replaced with binary classifier.  
- Much stronger generalization than the baseline CNN.  

### 4. Results
- Validation accuracy: ~0.90 (baseline CNN) → higher with ResNet50.  
- Submission file generated (`submission.csv`).  

---

## 📊 Results Snapshot
Baseline CNN training (5 epochs):

| Epoch | Train Acc | Val Acc | Val Loss |
|-------|-----------|---------|----------|
| 1     | 0.72      | 0.74    | 0.58     |
| 2     | 0.80      | 0.84    | 0.36     |
| 3     | 0.87      | 0.88    | 0.29     |
| 4     | 0.88      | 0.86    | 0.35     |
| 5     | 0.89      | 0.88    | 0.28     |

---

## 🚀 How to Run
1. Clone this repo:
   ```bash
   git clone https://github.com/your-username/histopathologic-cancer-detection.git
   cd histopathologic-cancer-detection
