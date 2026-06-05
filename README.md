# YOLO-SNet

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.10.0-red.svg)](https://pytorch.org/)
[![CUDA](https://img.shields.io/badge/CUDA-11.3-green.svg)](https://developer.nvidia.com/cuda-toolkit)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Official repository for **YOLO-SNet: Detection of Distant Smaller Entities from Aerial Surveillance Images Consisting Heterogeneous Objects**.

**Authors:**
Rony Shaha, Kaushik Sarker*, Md Mahibul Hasan, Sayed Jobaer, Foysal Ahmed, MD Ahasan Habib Tushar, and Sumonta Ghosh

*Corresponding author

YOLO-SNet is a lightweight object detection model designed for detecting small and flat objects from UAV-assisted aerial surveillance images under complex environments, including high-altitude views, low-light conditions, cluttered backgrounds, and heterogeneous object distributions.

The proposed YOLO-SNet integrates a Ghost Backbone, C3k2_gConv module, C3k2_GDC module, and WIoUv3 loss to improve detection accuracy while reducing computational complexity for real-time UAV-based aerial object detection.

---

## Code Availability

This repository provides the source code, model configuration files, training scripts, evaluation scripts, inference scripts, pretrained weights, and representative experimental results used in the YOLO-SNet manuscript.

The repository supports reproducibility of the main experimental results reported on:

* **SOD-Dataset**
* **VisDrone2019**

Repository:

```text
https://github.com/dhuvisionlab/YOLO-SNet
```

---

## Highlights

* Lightweight YOLO-based architecture for UAV-assisted small object detection.
* Ghost Backbone for efficient feature extraction.
* C3k2_gConv module for reducing computational cost in the backbone.
* C3k2_GDC module using Ghost Dynamic Convolution for adaptive feature learning.
* WIoUv3 loss for improved bounding-box regression.
* Evaluated on the custom SOD-Dataset and the public VisDrone2019 dataset.
* Designed for real-time aerial surveillance, small-object detection, and resource-constrained applications.
* Demonstrates strong trade-off among accuracy, FPS, parameters, FLOPs, and model size.

---

## Overall Architecture

YOLO-SNet consists of three major components:

1. **Backbone**
   The backbone adopts GhostConv and C3k2_gConv modules to reduce redundant computation while preserving useful feature representations for small-object detection.

2. **Neck**
   The neck replaces traditional C3k2 modules with the proposed C3k2_GDC module, which combines GhostConv and dynamic convolution for efficient multi-scale feature aggregation.

3. **Head**
   The detection head predicts object classes and bounding boxes from multi-scale features, enabling robust detection of small and flat objects in UAV imagery.

<p align="center">
  <img src="images/Figure-1.png" width="900">
</p>

---

## Proposed Modules

### Ghost Backbone

The Ghost Backbone uses GhostConv-based operations to generate efficient feature maps with reduced computational cost. This helps YOLO-SNet maintain strong detection performance while reducing parameter count and model size.

### C3k2_gConv Module

The C3k2_gConv module improves feature extraction efficiency by replacing conventional convolution operations with GhostConv-based lightweight operations.

### C3k2_GDC Module

The proposed C3k2_GDC module combines GhostConv with dynamic convolution. It dynamically aggregates multiple Ghost convolution kernels using attention weights, allowing the model to adapt to different aerial scenes and object scales.

<p align="center">
  <img src="images/Figure-3.png" width="850">
</p>

### WIoUv3 Loss

WIoUv3 is adopted for bounding-box regression to improve localization performance, especially for small and flat objects in complex UAV-assisted aerial images.

---

## Main Results

### Benchmark Results on SOD-Dataset

| Model            | Params (M) | FLOPs (G) | mAP@50 | mAP@50-95 | Model Size (MB) | FPS |
| ---------------- | ---------: | --------: | -----: | --------: | --------------: | --: |
| YOLOv11s         |        9.4 |      21.3 |   50.2 |      30.6 |            19.2 | 256 |
| YOLO-SNet (Ours) |        7.0 |      15.3 |   53.5 |      32.8 |            14.5 | 322 |

### Benchmark Results on VisDrone2019

| Model            | Params (M) | FLOPs (G) | mAP@50 | mAP@50-95 | Model Size (MB) | FPS |
| ---------------- | ---------: | --------: | -----: | --------: | --------------: | --: |
| YOLOv11s         |        9.4 |      21.3 |   48.6 |      33.2 |            12.2 |  87 |
| YOLO-SNet (Ours) |        7.0 |      15.3 |   49.7 |      34.5 |            12.9 | 294 |

---

## Ablation Study

The ablation study evaluates the contribution of the major components used in YOLO-SNet, including GhostConv, C3k2_gConv, and C3k2_GDC.

| Version      | GhostConv | C3k2_gConv | C3k2_GDC | Mean mAP | Params (M) |
| ------------ | --------- | ---------- | -------- | -------: | ---------: |
| V1           | ✓         | ✓          | -        |     50.7 |       8.04 |
| V2           | ✓         | -          | ✓        |     48.2 |       8.00 |
| V3           | -         | ✓          | ✓        |     48.5 |       7.09 |
| V4 YOLO-SNet | ✓         | ✓          | ✓        |     53.5 |       7.00 |

---

## Qualitative Results

The following visual comparison demonstrates YOLO-SNet and YOLOv11s under different lighting conditions, including morning, noon, evening, and night scenes. YOLO-SNet shows stronger detection capability for small and flat objects in complex UAV-assisted aerial scenes.

<p align="center">
  <img src="images/Figure-7.png" width="950">
</p>

---

## Training Curves

The following curves compare mAP@50, mAP@50-95, precision, and recall across 300 training epochs. YOLO-SNet shows strong convergence and competitive performance compared with other YOLO variants.

<p align="center">
  <img src="images/Figure-10.png" width="950">
</p>

---

## Model Efficiency Analysis

YOLO-SNet is designed to provide a strong trade-off between detection accuracy and computational efficiency. The following figure compares latency, accuracy, throughput, and efficiency gain between YOLO-SNet and YOLOv11 variants.

<p align="center">
  <img src="images/Figure-11.png" width="950">
</p>

### Latency vs Parameters

The following figure shows the speed-size trade-off, where YOLO-SNet achieves low inference time and reduced parameter count.

<p align="center">
  <img src="images/Figure-12.png" width="850">
</p>

---

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/dhuvisionlab/YOLO-SNet.git
cd YOLO-SNet
```

### 2. Create environment

Using Conda:

```bash
conda create -n yolo_snet python=3.8 -y
conda activate yolo_snet
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

Recommended environment:

```text
Ubuntu 20.04
Python >= 3.8
PyTorch 1.10.0
CUDA 11.3
OpenCV
NumPy
PyYAML
tqdm
matplotlib
ultralytics
```

---

## Dataset Preparation

This repository supports two datasets used in the manuscript:

* **SOD-Dataset**
* **VisDrone2019**

### Expected Dataset Structure

```text
datasets/
├── SOD-Dataset/
│   ├── images/
│   │   ├── train/
│   │   ├── val/
│   │   └── test/
│   └── labels/
│       ├── train/
│       ├── val/
│       └── test/
│
└── VisDrone2019/
    ├── images/
    │   ├── train/
    │   ├── val/
    │   └── test/
    └── labels/
        ├── train/
        ├── val/
        └── test/
```

### Data Preprocessing

Raw images and annotations should be organized in YOLO format before training. Each image should have a corresponding `.txt` annotation file with normalized bounding-box coordinates.

YOLO annotation format:

```text
class_id x_center y_center width height
```

Example:

```text
0 0.512 0.431 0.042 0.038
```

### SOD-Dataset

The SOD-Dataset is a custom UAV-assisted small object detection dataset developed for detecting small and flat objects in complex aerial environments.

The dataset contains nine object classes:

```text
Cargo, Person, Car, Electric Bike, Truck, Boat, Bus, Bicycle, Tram
```

The SOD-Dataset can be accessed from the following Google Drive link:

```text
https://drive.google.com/drive/folders/1OuoB48SMy5MPwzQ3Fm6cfGvgRINe07-T?usp=drive_link
```

### VisDrone2019

VisDrone2019 is a public UAV-based object detection dataset used to evaluate the generalization ability of YOLO-SNet on real-world aerial imagery.

The VisDrone2019 dataset can be accessed from the official repository:

```text
https://github.com/VisDrone/VisDrone-Dataset
```

### Dataset YAML Files

Dataset configuration files are provided in:

```text
configs/data/
├── sod_dataset.yaml
└── visdrone2019.yaml
```

---

## Training

### Train on SOD-Dataset

```bash
python tools/train.py \
  --model configs/model/yolo_snet.yaml \
  --data configs/data/sod_dataset.yaml \
  --config configs/train/train_yolo_snet.yaml
```

### Train on VisDrone2019

```bash
python tools/train.py \
  --model configs/model/yolo_snet.yaml \
  --data configs/data/visdrone2019.yaml \
  --config configs/train/train_yolo_snet.yaml
```

### Training Configuration

The main training configuration file is:

```text
configs/train/train_yolo_snet.yaml
```

Default training settings:

```text
image size: 640
batch size: 16
epochs: 300
optimizer: default
initial weights: training from scratch
```

---

## Evaluation

### Evaluate on SOD-Dataset

```bash
python tools/val.py \
  --weights weights/best.pt \
  --data configs/data/sod_dataset.yaml \
  --img 640
```

### Evaluate on VisDrone2019

```bash
python tools/val.py \
  --weights weights/best.pt \
  --data configs/data/visdrone2019.yaml \
  --img 640
```

### Evaluation Metrics

The following metrics are used for evaluation:

* Precision
* Recall
* F1-score
* mAP@50
* mAP@50-95
* Parameters
* FLOPs
* FPS
* Model size

---

## Lighting Condition Evaluation

YOLO-SNet is evaluated under different aerial scene conditions, including morning, noon, evening, and night environments. These experiments demonstrate the model's robustness for detecting small and flat objects under diverse lighting and background conditions.

```bash
python tools/val.py \
  --weights weights/best.pt \
  --data configs/data/sod_dataset.yaml \
  --img 640
```

---

## Inference

### Image Inference

```bash
python tools/infer_image.py \
  --weights weights/best.pt \
  --source assets/demo.jpg \
  --img 640 \
  --conf 0.25
```

### Video Inference

```bash
python tools/infer_video.py \
  --weights weights/best.pt \
  --source assets/demo.mp4 \
  --img 640 \
  --conf 0.25
```

The inference results will be saved in:

```text
runs/inference/
```

---

## Model Profiling

To calculate FLOPs, parameters, inference time, and FPS:

```bash
python tools/profile_model.py \
  --weights weights/best.pt \
  --img 640 \
  --device 0
```

---

## Pretrained Weights

| Model     | Dataset      | Weight                            |
| --------- | ------------ | --------------------------------- |
| YOLO-SNet | SOD-Dataset  | `weights/best.pt`                 |
| YOLO-SNet | VisDrone2019 | Available upon request or release |

If pretrained weights are larger than the GitHub upload limit, they can be provided through GitHub Releases, Google Drive, or another external storage link.

---

## Results Directory

Representative training and validation results are provided in:

```text
results/
├── sod_dataset/
│   ├── results.csv
│   ├── results.png
│   ├── F1_curve.png
│   ├── PR_curve.png
│   ├── P_curve.png
│   └── R_curve.png
│
└── visdrone2019/
```

---

## Repository Structure

```text
YOLO-SNet/
├── assets/
│   └── demo.jpg
│
├── configs/
│   ├── data/
│   │   ├── sod_dataset.yaml
│   │   └── visdrone2019.yaml
│   ├── model/
│   │   └── yolo_snet.yaml
│   └── train/
│       └── train_yolo_snet.yaml
│
├── data/
│   ├── README.md
│   └── sample_data/
│
├── images/
│   ├── Figure-1_architecture.png
│   ├── Figure-3_ghost_dynamic_conv.png
│   ├── Figure-7_efficiency.png
│   ├── Figure-8_sod_comparison.png
│   ├── Figure-11_training_curves.png
│   └── Figure-12_latency_params.png
│
├── results/
│   ├── sod_dataset/
│   │   ├── results.csv
│   │   ├── results.png
│   │   ├── F1_curve.png
│   │   ├── PR_curve.png
│   │   ├── P_curve.png
│   │   └── R_curve.png
│   └── visdrone2019/
│
├── tools/
│   ├── train.py
│   ├── val.py
│   ├── infer_image.py
│   ├── infer_video.py
│   └── profile_model.py
│
├── yolo_snet/
│   ├── models/
│   ├── modules/
│   ├── losses/
│   └── utils/
│
├── weights/
│   └── best.pt
│
├── README.md
├── requirements.txt
├── environment.yml
├── LICENSE
└── CITATION.cff
```

---

## Citation

If this work is useful for your research, please cite our paper:

```bibtex
@article{shaha2025yolosnet,
  title   = {YOLO-SNet: Detection of Distant Smaller Entities from Aerial Surveillance Images Consisting Heterogeneous Objects},
  author  = {Shaha, Rony and Sarker, Kaushik and Hasan, Md Mahibul and Jobaer, Sayed and Ahmed, Foysal and Habib Tushar, MD Ahasan and Ghosh, Sumonta},
  journal = {Image and Vision Computing},
  year    = {2025}
}
```

---

## Acknowledgements

We thank the researchers and contributors working on UAV-assisted aerial image analysis, small object detection, and lightweight YOLO-based object detection methods.

---

## License

This project is released under the MIT License.

---

## Contact

For questions about the code, dataset access, or experimental results, please open an issue in this repository.

Repository:

```text
https://github.com/dhuvisionlab/YOLO-SNet
```
