# 🍅 Tomato Leaf Disease Classification

> **EDGE Project — Applied Machine Learning | DUET, Gazipur**
> Automatically detects 10 tomato leaf conditions from a photo and recommends treatment.

---

## 📋 Project Overview

Tomato crop losses due to leaf diseases cost farmers billions of dollars annually. This project builds a **multi-class CNN classifier** that identifies 10 tomato leaf conditions (9 diseases + healthy) from smartphone photographs, and delivers the diagnosis through a simple **upload-and-classify GUI**.

| Field | Detail |
|-------|--------|
| **Project** | Project 05 — Tomato Leaf Disease Classification |
| **Course** | Applied Machine Learning — EDGE Series |
| **Institution** | DUET, Gazipur |
| **Domain** | Agriculture / Precision Farming |
| **Model** | MobileNetV2 (Transfer Learning) |
| **Final Accuracy** | ~91% Validation Accuracy |
| **GUI** | Gradio (shareable web link) |

---

## 🎯 Disease Classes (10)

| # | Class | Images |
|---|-------|--------|
| 1 | Tomato Bacterial Spot | ~2,100 |
| 2 | Tomato Early Blight | ~1,000 |
| 3 | Tomato Late Blight | ~1,900 |
| 4 | Tomato Leaf Mold | ~950 |
| 5 | Tomato Septoria Leaf Spot | ~1,770 |
| 6 | Tomato Spider Mites (Two-Spotted) | ~1,670 |
| 7 | Tomato Target Spot | ~1,400 |
| 8 | Tomato Yellow Leaf Curl Virus | ~3,200 |
| 9 | Tomato Mosaic Virus | ~370 |
| 10 | Tomato Healthy | ~1,590 |

---

## 📊 Results

| Metric | Value |
|--------|-------|
| Validation Accuracy | ~91% |
| Validation Loss | ~0.28 |
| Macro-avg F1-Score | ~0.68 |
| Weighted-avg F1-Score | ~0.72 |

---

## 🗂️ Repository Structure

```
tomato-disease-classification/
│
├── Tomato_Disease_Detection.ipynb   # Main notebook (EDA → Training → Evaluation → GUI)
├── tomato_disease_model.h5          # Trained MobileNetV2 model weights
├── README.md                        # This file
│
└── images/
    ├── class_distribution.png
    ├── sample_images.png
    ├── training_curves.png
    └── confusion_matrix.png
```

---

## 🚀 How to Run

### Option 1 — Google Colab (Recommended)

1. Open the notebook in Google Colab

2. Enable GPU: **Runtime → Change runtime type → T4 GPU**

3. Run all cells top to bottom

4. The final cell launches the **Gradio GUI** with a public shareable link

### Option 2 — Local Setup

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/tomato-disease-classification.git
cd tomato-disease-classification

# Install dependencies
pip install tensorflow gradio scikit-learn matplotlib seaborn pillow kaggle

# Download the dataset
kaggle datasets download -d emmarex/plantdisease
unzip plantdisease.zip -d ./plantdisease

# Open the notebook
jupyter notebook Tomato_Disease_Detection.ipynb
```

---

## 🧠 Model Architecture

```
Input (224×224×3)
        ↓
MobileNetV2 Base (ImageNet weights)
   Phase 1: Base frozen — train head only
   Phase 2: Unfreeze last 30 layers (fine-tuning)
        ↓
GlobalAveragePooling2D
        ↓
Dense(256, ReLU)
        ↓
Dropout(0.4)
        ↓
Dense(10, Softmax)  →  10 disease classes
```

**Training Strategy:**
- Phase 1: Adam (lr=1e-4), 15 epochs, frozen base
- Phase 2: Adam (lr=1e-5), 10 epochs, unfreeze last 30 layers
- Callbacks: EarlyStopping, ReduceLROnPlateau, ModelCheckpoint

**Augmentation:**
Horizontal/vertical flip · Rotation ±30° · Brightness [0.7–1.3] · Zoom ±20%

---

## 🖥️ GUI — Gradio Interface

The Gradio GUI accepts a tomato leaf photograph and returns:
- ✅ Predicted disease name
- 📊 Confidence percentage
- 📋 Top-3 predictions with probabilities
- 💊 Treatment recommendation

**Treatment dictionary covers all 10 classes** with evidence-based agricultural advice including fungicide selection, cultural practices, and resistant variety suggestions.

---

## 📦 Dependencies

```
tensorflow>=2.10
gradio>=3.0
scikit-learn
matplotlib
seaborn
pillow
numpy
kaggle
```

---

## ⚠️ Disclaimer

This tool is intended for educational and guidance purposes only. Always consult a qualified agricultural expert or extension officer for severe disease outbreaks or before applying any pesticide.

---

## 📚 References

1. Hughes, D. P., & Salathé, M. (2015). An open access repository of images on plant health. *arXiv:1511.08060*
2. Sandler, M. et al. (2018). MobileNetV2: Inverted Residuals and Linear Bottlenecks. *CVPR 2018*
3. Mohanty, S. P. et al. (2016). Using deep learning for image-based plant disease detection. *Frontiers in Plant Science, 7, 1419*
4. [PlantVillage Dataset — Kaggle](https://www.kaggle.com/datasets/emmarex/plantdisease)

---

## 👨‍💻 Author

**Md. Khalid Hasan Milu**  
EDGE Digital Skills for Students Program  
Institute of ICT, DUET Gazipur  
Instructors: Prof. Dr. Fazlul Hasan Siddiqui & Md. Rahad Khan
