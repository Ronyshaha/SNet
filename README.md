# YOLO-SNet

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.10.0-red.svg)](https://pytorch.org/)
[![CUDA](https://img.shields.io/badge/CUDA-11.3-green.svg)](https://developer.nvidia.com/cuda-toolkit)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Official repository for **YOLO-SNet: Detection of Distant Smaller Entities from Aerial Surveillance Images Consisting Heterogeneous Objects**.

**Authors:**
Rony Shaha, Kaushik Sarker*, Md Mahibul Hasan, Sayed Jobaer, Foysal Ahmed, MD Ahasan Habib Tushar, and Sumonta Ghosh

*Corresponding author

YOLO-SNet is a lightweight and efficient object detection model designed for detecting small and flat objects from UAV-assisted aerial surveillance images under complex environments, including high-altitude views, low-light conditions, cluttered backgrounds, and heterogeneous object distributions.

The proposed YOLO-SNet introduces a Ghost Backbone, C3k2_gConv module, and C3k2_GDC module to improve detection accuracy while reducing computational complexity for real-time UAV-based aerial object detection.

---

## Code Availability

This repository provides the implementation, configuration files, training and evaluation scripts, pretrained model weights, and representative experimental results for YOLO-SNet.

The repository is intended to support reproducibility of the main results reported in the manuscript, including experiments on:

* **SOD-Dataset**
* **VisDrone2019**

Repository link:

```text
https://github.com/dhuvisionlab/YOLO-SNet
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

## Training

### Train YOLO-SNet on SOD-Dataset

```bash
python tools/train.py \
  --model configs/model/yolo_snet.yaml \
  --data configs/data/sod_dataset.yaml \
  --config configs/train/train_yolo_snet.yaml
```

### Train YOLO-SNet on VisDrone2019

```bash
python tools/train.py \
  --model configs/model/yolo_snet.yaml \
  --data configs/data/visdrone2019.yaml \
  --config configs/train/train_yolo_snet.yaml
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

## Contact

For questions about the code, dataset access, or experimental results, please open an issue in this repository.

Repository:

```text
https://github.com/dhuvisionlab/YOLO-SNet
```
