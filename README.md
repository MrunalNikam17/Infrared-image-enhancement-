


#  Infrared Image Enhancement
## 📌 Overview
Infrared (IR) images often suffer from low contrast, blur, noise, and poor structural visibility due to sensor and environmental limitations.  
This project implements a **deep learning–based infrared image enhancement pipeline** using a **Residual UNet architecture with CBAM (Channel & Spatial Attention)** to significantly improve image quality while preserving thermal structures.

The entire system is implemented as a **single end-to-end pipeline** supporting dataset preparation, training, checkpoint recovery, and evaluation.

---

## 🧠 Key Features
- Residual UNet architecture for stable training  
- CBAM (Channel + Spatial Attention) for adaptive feature enhancement  
- Synthetic degradation–based supervised learning  
- Automatic patch pairing and normalization  
- Google Drive–safe checkpointing  
- Quantitative & qualitative evaluation  

---

## 🏗️ Model Architecture
- **Backbone**: UNet encoder–decoder  
- **Residual Blocks**: Improve gradient flow and convergence  
- **Attention**: CBAM applied at decoder stages  
- **Output**: 3-channel enhanced IR image (Sigmoid activation)

```

Input IR → Encoder → Bottleneck → Decoder + CBAM → Enhanced IR

```

---

## 📂 Project Structure
```

IR_Project/
│
├── original_images/
│   └── sober/                 # Clean infrared images
│
├── degraded_images/           # Synthetic degraded IR images
│
├── patches/
│   ├── input/                 # Degraded patches
│   └── gt/                    # Ground truth patches
│
├── checkpoints/
│   └── best.pth               # Best validation model
│
├── results/
│   └── *_grid.png              # Input | Output | GT comparisons
│
├── final_pipeline.py           # All-in-one pipeline
└── README.md

````

---

## 🧪 Dataset Preparation
Since large paired IR datasets are scarce, **synthetic degradation** is applied to clean IR images.

### Degradation Techniques
- Downsampling & upsampling  
- Gaussian blur  
- Gaussian noise  
- Contrast compression  

### Patch Extraction
- Patch size: **384 × 384**  
- Patches per image: **6**  
- Naming format: `patch_000001.png`  

---

## ⚙️ Pipeline Modes
Controlled by a single variable inside `final_pipeline.py`:

```python
MODE = "prepare"   # prepare | repair | train | eval
````

### 1️⃣ Prepare Dataset

```python
MODE = "prepare"
```

* Generates degraded images
* Extracts aligned input–GT patches

### 2️⃣ Train Model

```python
MODE = "train"
```

**Loss Function**

```
0.7 × L1 + 0.3 × MSE + 0.1 × (1 − SSIM)
```

### 3️⃣ Evaluate Model

```python
MODE = "eval"
```

Outputs are saved as:

```
[Input | Enhanced | Ground Truth]
```

---

## 📊 Image Quality Metrics

| Metric               | Value        |
| -------------------- | ------------ |
| **PSNR**             | **30.38 dB** |
| **SSIM**             | **0.968**    |
| **Entropy (Input)**  | 6.42         |
| **Entropy (Output)** | 6.61         |

### Interpretation

* High **PSNR** → strong reconstruction fidelity
* **SSIM ≈ 0.97** → excellent structural preservation
* Increased **entropy** → richer texture information

---

## 🖼️ Sample Results

```
Input (Degraded) | Enhanced Output | Ground Truth
```

*(Use images from the `results/` directory)*

---

## 🛠️ Requirements

```
python >= 3.8
torch
torchvision
numpy
opencv-python
Pillow
tqdm
```

---

## 🛠️ Technologies Used

* Python
* PyTorch
* OpenCV, PIL
* NumPy
* Google Colab & Google Drive

---

## 🎯 Applications

* Night-vision enhancement
* Thermal surveillance
* Autonomous navigation
* Industrial inspection
* Defense & security imaging

---

## 🚀 Future Work

* Transformer-based infrared enhancement
* Real-time inference optimization
* Multi-spectral fusion (IR + RGB)
* Human perceptual quality evaluation

---




