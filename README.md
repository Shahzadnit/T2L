# T2L: Efficient Zero-Shot Action Recognition with Temporal Token Learning

[![Paper](https://img.shields.io/badge/TMLR-2025-blue)](https://openreview.net/forum?id=WvgoxpGpuU)
[![License](https://img.shields.io/badge/License-MIT-green)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-orange)](https://pytorch.org/)

<p align="center">
  <img src="images/teasure.png" alt="T2L Teaser" width="800"/>
</p>

> 📢 Official PyTorch implementation of the **TMLR 2025** accepted paper:  
> **T2L: Efficient Zero-Shot Action Recognition with Temporal Token Learning**  
> Shahzad Ahmad, Sukalpa Chanda, Yogesh S. Rawat  
> [[OpenReview]](https://openreview.net/forum?id=WvgoxpGpuU) | [[Code]](https://github.com/Shahzadnit/T2L)

---

## 🔥 News
- **April 2025:** T2L accepted to **Transactions on Machine Learning Research (TMLR) 2025**! 🎉
- This repository supersedes our previous work, **EZ-CLIP** [[EZ-CLIP GitHub]](https://github.com/Shahzadnit/EZ-CLIP.git), with enhanced methods and updated code.

---

## 🌟 Highlights
- **Lightweight Design:** Only **5.2M learnable parameters**, 25x fewer than prior approaches, trainable on a single GPU.
- **Temporal Token Learning (TTL):** Captures cross-frame motion dynamics without altering the CLIP architecture.
- **Temporal Feature Diversity (TFD) Loss:** Promotes diverse temporal embeddings for robust action recognition.
- **Top Performance:** Achieves state-of-the-art results in **zero-shot**, **few-shot**, and **base-to-novel generalization** tasks.
- **Frozen CLIP Backbone:** Maintains generalization by keeping pre-trained CLIP weights frozen.

<p align="center">
  <img src="images/efficency.png" alt="Efficiency Comparison" width="800"/>
  <br>
  <em>Comparison of T2L with ActionCLIP, XCLIP, and ViFi-CLIP on tunable parameters, GFLOPs, total parameters, and throughput.</em>
</p>


## 👀 Qualitative Analysis: Attention Maps

<p align="center">
  <img src="images/attension_map.png" alt="T2L Attention Map" width="800"/>
</p>

Above are **temporal attention maps** for various video actions, showing how **T2L learns dynamic regions** crucial for action recognition over time. These maps demonstrate the effectiveness of our **temporal token learning** strategy.


---

## 🧠 Overview

<p align="center">
  <img src="images/T2L.jpg" alt="T2L Architecture" width="800"/>
</p>

**T2L** adapts CLIP for efficient video action recognition by introducing:
- **Temporal Token Learning (TTL):** Lightweight tokens model temporal relations across video frames.
- **Temporal Feature Diversity (TFD) Loss:** Enhances motion cue learning through diverse temporal embeddings.

With minimal computational overhead, T2L excels in **zero-shot**, **few-shot**, and **base-to-novel** settings across multiple benchmarks. For qualitative insights, see attention map visualizations in the [paper](https://openreview.net/pdf?id=WvgoxpGpuU) (Appendix A.7), showcasing T2L's robustness on out-of-distribution scenarios.

---

## 📄 Paper
**T2L: Efficient Zero-Shot Action Recognition with Temporal Token Learning**  
Shahzad Ahmad, Sukalpa Chanda, Yogesh S. Rawat  
*Transactions on Machine Learning Research (TMLR), April 2025*  
[[OpenReview]](https://openreview.net/forum?id=WvgoxpGpuU) | [[PDF]](https://openreview.net/pdf?id=WvgoxpGpuU)

---

## 📑 Table of Contents
- [Installation](#installation)
- [Model Zoo](#model-zoo)
- [Data Preparation](#data-preparation)
- [Training](#training)
- [Evaluation](#evaluation)
- [Citation](#citation)
- [Acknowledgments](#acknowledgments)
- [License](#license)

---

## ⚙️ Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Shahzadnit/T2L.git
   cd T2L
   ```

2. **Create a virtual environment:**
   ```bash
   conda create -n t2l python=3.8
   conda activate t2l
   pip install -r requirements.txt
   ```

3. **Install PyTorch:**
   Install PyTorch following instructions from [PyTorch's official site](https://pytorch.org/).

---

## 🧪 Model Zoo

All models utilize the **CLIP ViT-B/16** backbone and are trained on **Kinetics-400** unless otherwise specified.

### 🔍 Zero-Shot Evaluation
Models are trained on Kinetics-400 and evaluated directly on downstream datasets.

| **Model**      | **Input** | **HMDB-51** | **UCF-101** | **Kinetics-600** | **Model Download** |
|----------------|:---------:|:-----------:|:-----------:|:----------------:|:-------------------:|
| **T2L (ViT-16)** | 8×224     | **52.9**     | **79.1**     | **70.1**           | [📥 Link](https://drive.google.com/file/d/19QNGgaZjPyq0yz7XJGFccS7MV09KMY_K/view?usp=drive_link) |

### 🔀 Base-to-Novel Generalization
Models are trained on base classes and evaluated on both base and novel classes.

| **Dataset** | **Input** | **Base Acc.** | **Novel Acc.** | **Harmonic Mean (HM)** | **Model Download** |
|-------------|:---------:|:-------------:|:---------------:|:-----------------------:|:-------------------:|
| **Kinetics-400** | 8×224 | 73.1 | 60.6 | **66.3** | [📥 Link](https://drive.google.com/file/d/1q8rBkL0QKNTeJJihWkNUwm1eAGH_OY0U/view?usp=sharing) |
| **HMDB-51**      | 8×224 | 77.0 | 58.2 | **66.3** | [📥 Link](https://drive.google.com/file/d/1hW2i6agAhpyFvoRgPcOki3coQHx-6oWN/view?usp=sharing) |
| **UCF-101**      | 8×224 | 94.4 | 77.9 | **85.4** | [📥 Link](https://drive.google.com/file/d/16HTxwbqfi1N8BPVjfrvL6F_A4xLNt-zc/view?usp=sharing) |
| **SSv2**         | 8×224 | 16.6 | 13.3 | **14.8** | [📥 Link](https://drive.google.com/file/d/1EtpET-s634JnHK7n57vrvqNpE7qH_dHq/view?usp=sharing) |

---

## 🗂️ Data Preparation

Pre-extract video frames for efficient training and evaluation using scripts in `Dataset_creation_scripts`.

**Supported Datasets:**
- 🎞️ [Kinetics-400/600](https://deepmind.com/research/open-source/open-source-datasets/kinetics/)
- 📺 [UCF-101](http://crcv.ucf.edu/data/UCF101.php)
- 🎬 [HMDB-51](http://serre-lab.clps.brown.edu/resource/hmdb-a-large-human-motion-database/)
- 🎬 [Something-Something-v2](https://developer.qualcomm.com/software/something-something-video-dataset)

**Steps:**
1. Download datasets from their official websites.
2. Extract frames:
   ```bash
   python Dataset_creation_scripts/extract_frames.py --dataset <dataset_name> --data_path <path_to_videos>
   ```
3. Update dataset paths in configuration files (`configs/<dataset>/*.yaml`).

---

## 🏋️ Training

Train T2L with the provided configuration files:
```bash
python train.py --config configs/K-400/k400_train.yaml
```

**Training Details:**
- **Backbone:** CLIP ViT-B/16
- **Optimizer:** AdamW, learning rate 5e-5
- **Epochs:** 50
- **Batch Size:** 70
- **Hardware:** Single NVIDIA A100 80GB GPU

---

## 🧪 Evaluation

Evaluate pre-trained models:
```bash
python test.py --config configs/ucf101/UCF_zero_shot_testing.yaml
```

**Evaluation Settings:**
- **Zero-Shot:** HMDB-51, UCF-101, Kinetics-600
- **Base-to-Novel:** Base and novel classes
- **Few-Shot:** K={2,4,8,16} shots

---

## 📖 Citation

If you find this work useful, please cite our paper:

```bibtex
@article{
ahmad2025tl,
title={T2L: Efficient Zero-Shot Action Recognition with Temporal Token Learning},
author={Shahzad Ahmad and Sukalpa Chanda and Yogesh S Rawat},
journal={Transactions on Machine Learning Research},
issn={2835-8856},
year={2025},
url={https://openreview.net/forum?id=WvgoxpGpuU},
note={}
}
```

---

## 🙏 Acknowledgments

- Built upon [ActionCLIP](https://github.com/sallymmx/ActionCLIP).
- Gratitude to the open-source community for datasets and tools.
- Supported by Østfold University College and the University of Central Florida.

---

## 📜 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.