# T2L: Efficient Zero-Shot Action Recognition with Temporal Token Learning
[![Paper](https://img.shields.io/badge/TMLR-2025-blue)](https://openreview.net/forum?id=WvgoxpGpuU)

<p align="center">
  <img src="teasure.png" alt="T2L Teaser" width="800"/>
</p>

> 📢 This is the official PyTorch implementation of our **TMLR 2025** accepted paper:  
> **T2L: Efficient Zero-Shot Action Recognition with Temporal Token Learning**  
> [[OpenReview]](https://openreview.net/forum?id=WvgoxpGpuU)

---

## 🔥 News
- **April 2025:** Our paper **T2L** has been accepted to **TMLR 2025**! 🎉  
- This repo supersedes our previous work **EZ-CLIP** [[EZ-CLIP GitHub]](https://github.com/Shahzadnit/EZ-CLIP.git), which was the earlier version on arXiv.

---

## 🌟 Highlights
- ⚡️ *Only 5.2M learnable parameters* with **25x fewer** tunables than prior works.
- 🧠 Introduces **Temporal Token Learning (TTL)** to model motion across video frames.
- 📈 Achieves *state-of-the-art performance* in zero-shot and base-to-novel generalization.
- 💡 Proposes **Temporal Feature Diversity Loss (TFD)** for learning temporal variations.
- 🧊 Keeps the core CLIP backbone frozen for maximum efficiency and generalization.

---

## 🧠 Introduction

<p align="center">
  <img src="T2L.jpg" alt="T2L Architecture" width="800"/>
</p>

Temporal adaptation of vision-language models like CLIP is essential for video understanding, but existing approaches often suffer from high compute cost and overfitting. We propose **T2L**, a simple yet effective extension to CLIP that introduces:

- **Temporal Token Learning (TTL):** Injects temporal tokens into each transformer layer to capture cross-frame relations.
- **Temporal Feature Diversity (TFD) Loss:** Encourages variation in temporal embeddings to highlight motion cues.

Our method maintains **frozen CLIP weights** and only trains adapters and tokens—achieving strong performance in **zero-shot**, **few-shot**, and **base-to-novel generalization** benchmarks.

---

## 📄 Paper
**T2L: Efficient Zero-Shot Action Recognition with Temporal Token Learning**  
Shahzad Ahmad, Sukalpa Chanda, Yogesh S. Rawat  
Published in Transactions on Machine Learning Research (TMLR), April 2025  
[[OpenReview]](https://openreview.net/forum?id=WvgoxpGpuU)

---

## 📁 Contents
- [Requirements](#requirements)
- [Model Zoo](#model-zoo)
- [Data Preparation](#data-preparation)
- [Training](#training)
- [Testing](#testing)
- [Citation](#citation)
- [Acknowledgments](#acknowledgments)

---

## ⚙️ Requirements

We provide the conda requirements.txt to help you install these libraries. You can initialize environment by using `pip install -r requirements.txt`.


## 🧪 Model Zoo

> 📝 All experiments utilize the publicly available **CLIP ViT/B-16** as the base visual encoder.

### 🔍 Zero-Shot Evaluation

All models below are trained on **Kinetics-400** and directly evaluated on downstream datasets without any fine-tuning.

| **Model**      | **Input** | **HMDB-51** | **UCF-101** | **Kinetics-600** | **Model Download** |
|----------------|:---------:|:-----------:|:-----------:|:----------------:|:-------------------:|
| **T2L (ViT-16)** | 8×224     | **52.9**     | **79.1**     | **70.1**           | [📥 Link](https://drive.google.com/file/d/19QNGgaZjPyq0yz7XJGFccS7MV09KMY_K/view?usp=drive_link) |

---

### 🔀 Base-to-Novel Generalization

In this setting, each dataset is split into **base** and **novel** classes. The model is trained only on base classes and evaluated on both.

| **Dataset** | **Input** | **Base Acc.** | **Novel Acc.** | **Harmonic Mean (HM)** | **Model Download** |
|-------------|:---------:|:-------------:|:---------------:|:-----------------------:|:-------------------:|
| **Kinetics-400** | 8×224 | 73.1 | 60.6 | **66.3** | [📥 Link](https://drive.google.com/file/d/1q8rBkL0QKNTeJJihWkNUwm1eAGH_OY0U/view?usp=sharing) |
| **HMDB-51**      | 8×224 | 77.0 | 58.2 | **66.3** | [📥 Link](https://drive.google.com/file/d/1hW2i6agAhpyFvoRgPcOki3coQHx-6oWN/view?usp=sharing) |
| **UCF-101**      | 8×224 | 94.4 | 77.9 | **85.4** | [📥 Link](https://drive.google.com/file/d/16HTxwbqfi1N8BPVjfrvL6F_A4xLNt-zc/view?usp=sharing) |
| **SSV2**         | 8×224 | 16.6 | 13.3 | **14.8** | [📥 Link](https://drive.google.com/file/d/1EtpET-s634JnHK7n57vrvqNpE7qH_dHq/view?usp=sharing) |

---

## 🗂️ Data Preparation

To enable fast training and evaluation, we recommend pre-extracting video frames using our scripts in `Dataset_creation_scripts`.

We've verified compatibility and successful training on:
- 🎞️ [Kinetics](https://deepmind.com/research/open-source/open-source-datasets/kinetics/)
- 📺 [UCF101](http://crcv.ucf.edu/data/UCF101.php)
- 🎬 [HMDB51](http://serre-lab.clps.brown.edu/resource/hmdb-a-large-human-motion-database/)

---





## 🏋️‍♂️ Training
```
# Train
python train.py --config configs/K-400/k400_train.yaml

```

## 🧪 Testing
```
# Test 
python test.py --config configs/ucf101/UCF_zero_shot_testing.yaml

```

## 📖 Citation
If you find the code and pre-trained models useful for your research, please consider citing our paper:

```
@article{ahmad2025t2l,
  title={T2L: Efficient Zero-Shot Action Recognition with Temporal Token Learning},
  author={Ahmad, Shahzad and Chanda, Sukalpa and Rawat, Yogesh S},
  journal={Transactions on Machine Learning Research (TMLR)},
  year={2025},
  url={https://openreview.net/forum?id=WvgoxpGpuU}
}
```


## 🙏 Acknowledgments

This repository is built upon the excellent foundation of [ActionCLIP](https://github.com/sallymmx/ActionCLIP?tab=readme-ov-file).  
Special thanks to the open-source community for tools and datasets that made this work possible.



