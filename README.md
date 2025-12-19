# Infrared-image-enhancement-

🔥 Infrared Image Enhancement using UNet-Res-CBAM
📌 Overview

Infrared (IR) images often suffer from low contrast, blur, noise, and poor structural visibility due to sensor limitations and environmental factors.
This project proposes a deep learning–based infrared image enhancement pipeline using a Residual UNet architecture augmented with CBAM attention to improve clarity while preserving thermal structure.

The entire pipeline is implemented as a single, modular script supporting dataset preparation, training, checkpoint recovery, and evaluation.

🧠 Key Highlights

Residual UNet architecture for stable training and feature preservation

CBAM (Channel + Spatial Attention) for adaptive feature enhancement

Synthetic degradation pipeline for supervised learning

Fully reproducible end-to-end workflow

Google Drive–safe checkpoints and outputs

🏗️ Model Architecture
🔹 Backbone

UNet encoder–decoder structure

Skip connections for spatial detail preservation

Residual convolution blocks for improved gradient flow

🔹 Attention Mechanism (CBAM)

Channel Attention → emphasizes informative feature maps

Spatial Attention → focuses on salient regions in IR images

Applied at multiple decoder stages

🔹 Final Output

3-channel enhanced IR image

Sigmoid activation for stable intensity mapping

Input IR → Encoder → Bottleneck → Decoder + CBAM → Enhanced IR

📂 Project Structure
IR_Project/
│
├── original_images/
│   └── sober/                 # Clean infrared images
│
├── degraded_images/           # Synthetic degraded IR images
│
├── patches/
│   ├── input/                 # Degraded patches (patch_XXXXXX.png)
│   └── gt/                    # Ground-truth patches
│
├── checkpoints/
│   └── best.pth               # Best validation model
│
├── results/
│   └── *_grid.png              # Input | Output | GT comparisons
│
├── final_pipeline.py           # End-to-end pipeline
└── README.md

🧪 Dataset Preparation

Since large paired IR datasets are scarce, the project uses synthetic degradation:

Degradation operations

Downsampling & upsampling

Gaussian noise

Gaussian blur

Contrast compression

Patch extraction

Patch size: 384 × 384

Patches per image: 6

Automatically paired as patch_000001.png

⚙️ Pipeline Modes

The pipeline is controlled via a single variable:

MODE = "prepare"   # prepare | repair | train | eval

🔹 Prepare Dataset
MODE = "prepare"


Generates degraded images

Extracts aligned input–GT patches

🔹 Train Model
MODE = "train"


Automatically resumes from best checkpoint

Saves best model to Google Drive

Loss function:

0.7 × L1 + 0.3 × MSE + 0.1 × (1 − SSIM)

🔹 Evaluate
MODE = "eval"


Saves side-by-side grids:

[Input | Enhanced | Ground Truth]

📊 Image Quality Metrics
Metric	Value
PSNR	30.38 dB
SSIM	0.968
Entropy (Input)	6.42
Entropy (Output)	6.61
🔍 Interpretation

High PSNR → strong reconstruction accuracy

SSIM ≈ 0.97 → excellent structural preservation

Entropy increase → richer texture and information content

🖼️ Sample Results
Degraded Input	Enhanced Output	Ground Truth

		

(Replace with your generated grids)

🛠️ Technologies Used

Language: Python

Deep Learning: PyTorch

Vision: OpenCV, PIL

Training: AdamW optimizer

Environment: Google Colab + Google Drive

🎯 Applications

Night-vision enhancement

Thermal surveillance

Autonomous navigation

Industrial inspection

Defense & security imaging

🚀 Future Improvements

Transformer-based IR enhancement

Real-time inference optimization

Multi-spectral fusion (IR + RGB)

Human perceptual evaluation studies
