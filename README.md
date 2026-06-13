# 🧠 Brain Tumor Classification & Segmentation

> A comprehensive deep learning project for brain tumor analysis using MRI scans. Features 10+ classification models, U-Net segmentation, GradCAM explainability, and a premium web application.

---

## 📚 Deep Dive Documentation
I have created 4 detailed guides to help you understand every part of this project:
- **[Part 1: Data Processing & Preparation](docs/01_data_processing.md)**
- **[Part 2: Multi-Model Classification](docs/02_classification.md)**
- **[Part 3: Segmentation & AI Explainability](docs/03_segmentation_and_explainability.md)**
- **[Part 4: Web Integration (Backend & Frontend)](docs/04_web_integration.md)**
- **[Part 5: In-Depth EDA & Advanced Processing](docs/05_eda_and_advanced_processing.md)**

---

## 📊 Dataset

**Merged Multi-Source Dataset (~15,000+ images)** created by combining 3 Kaggle datasets:

| Dataset | Source | Images |
|---------|--------|--------|
| Dataset 1 | `sartajbhuvaji/brain-tumor-classification-mri` | ~3,264 |
| Dataset 2 | `masoudnickparvar/brain-tumor-mri-dataset` | ~7,153 |
| Dataset 3 | `ahmedhamada0/brain-tumor-detection` (Br35H) | ~3,060 |

**Classes:** Glioma, Meningioma, No Tumor, Pituitary

**Segmentation:** 3,064 MRI + binary mask pairs (`nikhilroxtomar/brain-tumor-segmentation`)

### Deduplication
Images are deduplicated using **perceptual hashing** to remove near-identical images across datasets.

---

## 🏗️ Project Structure

```
brain-tumor-project/
├── data/
│   ├── raw/                       # Raw downloads from Kaggle
│   ├── classification/            # Merged & deduplicated
│   └── segmentation/              # Images + masks
├── notebooks/
│   ├── 00_dataset_merge.ipynb     # Download, merge & dedup
│   ├── 01_eda.ipynb               # Exploratory Data Analysis
│   ├── 02_custom_cnn.ipynb        # Custom CNN
│   ├── 03_vgg16.ipynb             # VGG16
│   ├── 04_vgg19.ipynb             # VGG19
│   ├── 05_resnet50.ipynb          # ResNet50
│   ├── 06_resnet101.ipynb         # ResNet101
│   ├── 07_inceptionv3.ipynb       # InceptionV3
│   ├── 08_densenet121.ipynb       # DenseNet121
│   ├── 09_mobilenetv2.ipynb       # MobileNetV2
│   ├── 10_efficientnetb0.ipynb    # EfficientNetB0
│   ├── 11_xception.ipynb          # Xception
│   ├── 12_model_comparison.ipynb  # Comparison & Paper Results
│   ├── 13_unet_segmentation.ipynb # U-Net Segmentation
│   └── 14_gradcam.ipynb           # GradCAM Visualization
├── models/                        # Saved .h5 model weights
├── results/                       # JSON results & LaTeX tables
├── webapp/                        # Flask web application
│   ├── app.py
│   ├── templates/index.html
│   └── static/{css,js}/
├── utils/
│   ├── preprocessing.py           # Data loading & augmentation
│   ├── gradcam.py                 # GradCAM utilities
│   └── model_loader.py            # Model architectures
├── requirements.txt
└── README.md
```

---

## 🚀 Getting Started

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Download & Merge Datasets
```bash
# Option A: Using Kaggle CLI (requires API key in ~/.kaggle/kaggle.json)
cd notebooks
jupyter notebook 00_dataset_merge.ipynb

# Option B: Manual download from Kaggle, then run the merge notebook
```

### 3. Run EDA
```bash
jupyter notebook notebooks/01_eda.ipynb
```

### 4. Train Models
Run each notebook (02-11) individually. **GPU recommended** (Google Colab / Kaggle Notebooks work great):
```bash
jupyter notebook notebooks/02_custom_cnn.ipynb
# ... repeat for 03-11
```

### 5. Compare Models
```bash
jupyter notebook notebooks/12_model_comparison.ipynb
```

### 6. Train Segmentation Model
```bash
jupyter notebook notebooks/13_unet_segmentation.ipynb
```

### 7. GradCAM Visualization
```bash
jupyter notebook notebooks/14_gradcam.ipynb
```

### 8. Launch Web Application
```bash
cd webapp
python app.py
# Visit http://localhost:5000
```

---

## 🧪 Classification Models

| # | Model | Input Size | Architecture |
|---|-------|-----------|--------------|
| 1 | Custom CNN | 224×224 | 4-block CNN from scratch |
| 2 | VGG16 | 224×224 | Transfer Learning (ImageNet) |
| 3 | VGG19 | 224×224 | Transfer Learning (ImageNet) |
| 4 | ResNet50 | 224×224 | Transfer Learning (ImageNet) |
| 5 | ResNet101 | 224×224 | Transfer Learning (ImageNet) |
| 6 | InceptionV3 | 299×299 | Transfer Learning (ImageNet) |
| 7 | DenseNet121 | 224×224 | Transfer Learning (ImageNet) |
| 8 | MobileNetV2 | 224×224 | Transfer Learning (ImageNet) |
| 9 | EfficientNetB0 | 224×224 | Transfer Learning (ImageNet) |
| 10 | Xception | 299×299 | Transfer Learning (ImageNet) |

Each model generates: accuracy, precision, recall, F1-score, confusion matrix, ROC-AUC curves.

---

## 🔬 Segmentation

**Attention U-Net** architecture with pretrained EfficientNetB3 encoder.
- **Attention Gates** (scSE) suppress irrelevant background and focus on tumor regions.
- **Metrics (Validation)**:
  - **IoU Score**: 0.75 (75% overlap accuracy)
  - **F1-Score**: 0.85
  - **Dice Coefficient**: 0.69
  - **Pixel Accuracy**: 99.5%
- Binary segmentation for tumor localization.

### 🧠 How Attention Works (scSE)
The model uses **Concurrent Spatial and Channel Squeeze & Excitation (scSE)** attention:
- **Spatial Attention**: Focuses the model on **WHERE** the tumor is located within the brain slice.
- **Channel Attention**: Learns **WHICH** feature maps (edges, textures) are the most important for identifying tumor tissue.
- **Result**: Significant reduction in "false positives" on healthy brain tissue compared to a standard U-Net.

---

## 🔥 GradCAM Explainability

- Visual explanations for model predictions
- Heatmaps showing regions of interest
- Multi-model comparison
- Combined GradCAM + segmentation overlay

---

## 🌐 Web Application

Premium dark-themed Flask web app with:
- Drag & drop MRI upload
- Real-time classification with confidence scores
- Tumor segmentation overlay
- GradCAM heatmap visualization
- Responsive design with glassmorphism UI

---

## 📝 Citation

If you use this project in your research, please cite the source datasets:

```bibtex
@dataset{sartaj_brain_tumor,
  title={Brain Tumor Classification (MRI)},
  author={Sartaj Bhuvaji et al.},
  year={2020},
  publisher={Kaggle}
}

@dataset{masoud_brain_tumor,
  title={Brain Tumor MRI Dataset},
  author={Masoud Nickparvar},
  year={2021},
  publisher={Kaggle}
}

@dataset{ahmed_br35h,
  title={Br35H :: Brain Tumor Detection 2020},
  author={Ahmed Hamada},
  year={2020},
  publisher={Kaggle}
}
```

---

## ⚠️ Disclaimer

This project is for **research and educational purposes only**. It is NOT intended for clinical diagnosis. Always consult qualified medical professionals for brain tumor diagnosis and treatment.

---

## 📄 License

MIT License
