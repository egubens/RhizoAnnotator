# 🌱 RhizoAnnotator

**Automated root segmentation from minirhizotron images using deep learning, enabling scalable and reproducible root analysis.**

🔗 Repository: [RhizoAnnotator](https://github.com/egubens/RhizoAnnotator)

---

## 🔬 Overview

**RhizoAnnotator** is a deep learning–based tool for segmenting roots from minirhizotron images.

⚠️ **This repository is intended for inference/segmentation only. It does NOT include training pipelines.**

It generates **binary masks** where:

- **Roots = black (0)**
- **Background = white (255)**

The tool is designed for:

- Rapid annotation of large image datasets  
- Downstream quantitative analysis (root length, density, distribution)  
- Reproducible workflows in soil and plant sciences  

---

## 🚀 Intended Use

This tool is **primarily designed to run in Google Colab with GPU acceleration** for ease of use and accessibility.

---

## 🚀 Quick Start (Google Colab)

### 1. Open the notebook in Google Colab
Click here: [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/egubens/RhizoAnnotator/blob/main/inference_colab.ipynb)

### 2. Enable GPU
In Colab:
Runtime → Change runtime type → GPU

A GPU is strongly recommended for faster inference, especially when processing large image datasets.

### 3. Run the notebook

The notebook will:
- Mount Google Drive automatically  
- Prompt you to set image paths  
- Download model weights  
- Run segmentation  
- Save masks  

👉 **Important:** Follow the instructions printed inside the notebook cells.

---

## 🖥️ Running in JupyterLab / Local Environment

RhizoAnnotator can also be run locally using JupyterLab or a Python script.

### Requirements
- Python ≥ 3.9  
- torch  
- torchvision  
- pillow  
- matplotlib  
- tqdm  
- gdown  

### Installation
```bash
pip install torch torchvision pillow matplotlib tqdm gdown
```

### Steps
1. Set local paths:
```python
IMG_DIR = "/path/to/your/images"
WEIGHTS_PATH = "rhizoannotator_v1.pt"
```

2. Run the notebook or script.

### Notes
- GPU is optional but **strongly recommended**  
- CPU execution is significantly slower  
- Google Drive mounting is **not required** outside Colab  

---

## 📥 Model Weights

Model weights are hosted in the GitHub Releases and are **automatically downloaded by the notebook at runtime**.

This ensures:
- No manual setup
- Consistent versioning
- Reproducible inference

Direct download (optional):  
[Download model weights (v1.0.0)](https://github.com/egubens/RhizoAnnotator/releases/download/V1.0.0/rhizoannotator_v1.pt)

---

## 📂 Input Requirements

- Supported formats: `.png`, `.jpg`, `.jpeg`, `.tif`
- RGB images only
- Recommended resolution: ≥1000 px per side

---

## ⚙️ Key Parameters

```python
IMG_SIZE = (1024, 1152)
BATCH_SIZE = 4
THRESHOLD = 0.5
NUM_PREVIEW = 10
```

---

## 📤 Output

- Masks saved as: `originalname-mask.png`
- Format: PNG (lossless)
- Values:
  - 0 → root  
  - 255 → background  

---
## 📊 Model Performance

The model was trained and validated using the PRMI (Public Root Minirhizotron Image) dataset, consisting of over 15,000 annotated images.

### Dataset
- Training images: 11,284  
- Validation images: 3,947  
- Image size: 256 × 256 (resized during training)

### Evaluation Metrics
Performance was evaluated using:
- Dice coefficient  
- Intersection over Union (IoU)  
- Accuracy  

### Results (Validation Set)
- Accuracy: **98.2%**  
- Dice coefficient: **0.22**  
- IoU: **0.34**

### Interpretation

- The model achieves **high overall accuracy**, primarily due to the strong imbalance between background and root pixels in minirhizotron images.  
- It performs reliably in identifying **dominant root structures** and separating them from complex soil backgrounds, including visually similar materials such as biochar.  
- Performance is more limited for **fine root structures**, which are inherently difficult to capture due to their small size and low contrast.  

### Practical Performance

Despite moderate Dice and IoU values, the model provides:
- Consistent detection of root presence across images  
- Robust separation of roots from noisy backgrounds  
- A scalable alternative to manual annotation and traditional threshold-based methods  

---

## ⚠️ Limitations

- Reduced sensitivity to very fine roots  
- Performance may vary with:
  - Soil type  
  - Imaging conditions  
- Images are resized prior to inference, which may reduce fine-scale detail
  
## 📊 Example Results

<table align="center">
  <tr>
    <td align="center">
      <img src="examples/img1.jpg" width="300"/><br>
      <sub>Image 1</sub>
    </td>
    <td align="center">
      <img src="examples/img1-mask.png" width="300"/><br>
      <sub>Mask 1</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="examples/img2.jpg" width="300"/><br>
      <sub>Image 2</sub>
    </td>
    <td align="center">
      <img src="examples/img2-mask.png" width="300"/><br>
      <sub>Mask 2</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="examples/img3.jpg" width="300"/><br>
      <sub>Image 3</sub>
    </td>
    <td align="center">
      <img src="examples/img3-mask.png" width="300"/><br>
      <sub>Mask 3</sub>
    </td>
  </tr>
</table>

---

## ⚠️ Important Notes

- Images are resized before inference  
- If GPU memory errors occur, set `BATCH_SIZE = 1`  
- CPU execution is slower  

---

## 🧪 Limitations

- Model performance depends on similarity to training data  
- No patch-based inference yet  

---

## 📖 Citation

If you use this tool, please cite:

```
Gutiérrez Benites, E. D. (2026).
RhizoAnnotator: Automated root segmentation from minirhizotron images using deep learning.
GitHub repository. https://github.com/egubens/RhizoAnnotator
```

---

## 📜 License

MIT License

---

## 🔮 Future Work

- Patch-based inference  
- Root trait extraction  
- Improved generalization  

---

## 🤝 Contributing

Open an issue for suggestions or bugs.
