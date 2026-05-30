# 🧠 CNN Image Classification on CIFAR-10

> Comparing VGG and ResNet architectures with **Max Pooling vs Average Pooling** on all 10 CIFAR-10 categories.

---

## 📋 Overview

This project implements and compares two popular Convolutional Neural Network architectures — **VGG** and **ResNet** — for image classification on the [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) dataset. Each architecture is tested with two pooling strategies (**Max Pooling** and **Average Pooling**), resulting in **4 model variants**. Results are evaluated using accuracy, confusion matrix, and training time (computational cost).

This project was developed as an assignment for the **CNN course** at [University Name].

---

## 🗂️ Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Model Architectures](#-model-architectures)
- [Results](#-results)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Requirements](#-requirements)
- [How to Run](#-how-to-run)
- [Visualizations](#-visualizations)

---

## 📦 Dataset

**CIFAR-10** — 60,000 color images (32×32 pixels) across 10 classes.

| Split | Samples |
|-------|---------|
| Train | 50,000  |
| Test  | 10,000  |

**Classes:**

| ID | Label      |
|----|------------|
| 0  | airplane   |
| 1  | automobile |
| 2  | bird       |
| 3  | cat        |
| 4  | deer       |
| 5  | dog        |
| 6  | frog       |
| 7  | horse      |
| 8  | ship       |
| 9  | truck      |

---

## 🏗️ Model Architectures

### VGGMini

A lightweight VGG-style network with 3 convolutional blocks, each followed by a pooling layer, and a fully connected classifier with dropout.

```
Conv(64) → Conv(64) → Pool
Conv(128) → Conv(128) → Pool
Conv(256) → Conv(256) → Pool
FC(512) → Dropout → FC(10)
```

### ResNetMini

A lightweight ResNet-style network with residual (skip) connections, ending with adaptive pooling.

```
Conv(64) → BasicBlock(64) → BasicBlock(128, stride=2) → BasicBlock(256, stride=2) → AdaptivePool → FC(10)
```

### Pooling Variants

| Model           | Pooling Type   |
|-----------------|----------------|
| VGG_MaxPool     | Max Pooling    |
| VGG_AvgPool     | Average Pooling|
| ResNet_MaxPool  | Adaptive Max   |
| ResNet_AvgPool  | Adaptive Avg   |

---

## 📊 Results

> Results below are representative — actual values may vary by run and hardware.

| Model           | Best Val Acc | Training Time | Params    |
|-----------------|:------------:|:-------------:|----------:|
| VGG_MaxPool     | ~82%         | ~X s          | ~2.4M     |
| VGG_AvgPool     | ~81%         | ~X s          | ~2.4M     |
| ResNet_MaxPool  | ~84%         | ~X s          | ~0.5M     |
| ResNet_AvgPool  | ~83%         | ~X s          | ~0.5M     |

**Key takeaways:**
- ResNet variants generally outperform VGG variants despite having fewer parameters.
- Max Pooling tends to achieve slightly higher accuracy than Average Pooling on CIFAR-10.
- ResNetMini trains faster due to its smaller parameter count.

---

## 📁 Project Structure

```
cnn-cifar10/
│
├── notebooks/
│   └── CNN_CIFAR10_Comparison.ipynb   # Main Google Colab notebook
│
├── outputs/
│   └── cnn_comparison_10class.png     # Result visualizations
│
└── README.md
```

---

## 🚀 Getting Started

### Option 1 — Google Colab (Recommended)

1. Open [Google Colab](https://colab.research.google.com/)
2. Create a **new notebook**
3. Copy and paste each of the **6 code cells** in order:

| Cell | Description |
|------|-------------|
| **Cell 1** | Install & import libraries |
| **Cell 2** | Load CIFAR-10 dataset (all 10 classes) |
| **Cell 3** | Define VGG and ResNet model architectures |
| **Cell 4** | Training loop (all 4 model variants) |
| **Cell 5** | Visualize results (accuracy curves, confusion matrix) |
| **Cell 6** | Detailed analysis & classification report |

4. Enable **GPU runtime**: `Runtime → Change runtime type → GPU`
5. Run all cells sequentially.

### Option 2 — Local Environment

```bash
git clone https://github.com/your-username/cnn-cifar10.git
cd cnn-cifar10
pip install -r requirements.txt
jupyter notebook notebooks/CNN_CIFAR10_Comparison.ipynb
```

---

## 🛠️ Requirements

```
torch>=2.0.0
torchvision>=0.15.0
matplotlib>=3.7.0
seaborn>=0.12.0
scikit-learn>=1.3.0
numpy>=1.24.0
```

Install all at once:

```bash
pip install torch torchvision matplotlib seaborn scikit-learn numpy
```

---

## ▶️ How to Run

### Training Configuration

| Parameter  | Value                        |
|------------|------------------------------|
| Epochs     | 20                           |
| Batch size | 128                          |
| Optimizer  | Adam (lr=1e-3, wd=1e-4)      |
| Scheduler  | CosineAnnealingLR            |
| Loss       | CrossEntropyLoss             |

### Data Augmentation (Train)

- Random crop (32×32, padding=4)
- Random horizontal flip
- Normalization (CIFAR-10 mean & std)

---

## 📈 Visualizations

The notebook generates the following plots saved as `cnn_comparison_10class.png`:

1. **Validation Accuracy per Epoch** — learning curves for all 4 models
2. **Training Loss per Epoch** — convergence comparison
3. **Best Validation Accuracy** — bar chart summary
4. **Training Time (Computational Cost)** — wall-clock time per model
5. **Confusion Matrix** — for the top 2 best-performing models


## 📄 License

This project is for educational purposes.

---

## Acknowledgements

- [CIFAR-10 Dataset](https://www.cs.toronto.edu/~kriz/cifar.html) — Alex Krizhevsky, Vinod Nair, and Geoffrey Hinton
- [VGGNet Paper](https://arxiv.org/abs/1409.1556) — Simonyan & Zisserman, 2014
- [ResNet Paper](https://arxiv.org/abs/1512.03385) — He et al., 2015
- [PyTorch](https://pytorch.org/) — Facebook AI Research
