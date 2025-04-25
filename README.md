# T2L: Efficient Zero-Shot Action Recognition with Temporal Token Learning

![Teaser Figure](T2L.jpg)

> **T2L** is an efficient and scalable adaptation of CLIP for zero-shot video action recognition. It introduces **Temporal Token Learning (TTL)** and a novel **Temporal Feature Diversity (TFD)** loss to capture motion without modifying the frozen CLIP backbone. With only 5.2M tunable parameters, T2L achieves state-of-the-art performance on multiple benchmarks while maintaining high throughput and low computational cost.

---

## 🔍 Overview

Recent vision-language models such as CLIP exhibit powerful generalization capabilities in zero-shot image classification. However, extending such models to videos introduces challenges related to temporal modeling and computational complexity. 

**T2L** addresses these challenges by introducing a lightweight **Temporal Token Learning (TTL)** module, along with a **Temporal Feature Diversity (TFD)** loss that enhances motion representation. This design enables T2L to:

- Efficiently model motion across frames with **frozen CLIP** encoders.
- Scale to real-world video benchmarks like UCF-101, HMDB-51, and SSv2.
- Outperform prior video-CLIP adaptations in both accuracy and throughput.

---

![Main Architecture](Screenshot from 2025-04-25 10-13-24.png)

---

## 🆕 Updates

- 🧠 Accepted at **TMLR 2025**
- 📦 Pretrained models available: [Google Drive](https://drive.google.com/drive/folders/1OPt5cXSx-1u_hRXSpst94gMJ5P-c7uBS?usp=sharing)

---

## 📦 Contents

- [Prerequisites](#prerequisites)
- [Model Zoo](#model-zoo)
- [Data Preparation](#data-preparation)
- [Training](#training)
- [Testing](#testing)
- [Citation](#citation)
- [Acknowledgments](#acknowledgments)

---

## 📋 Prerequisites

Install dependencies using:

```bash
pip install -r requirements.txt




## Model Zoo
NOTE: All models in our experiments below uses publicly available ViT/B-16 based CLIP model.

### Zero-shot results
All models are trained on Kinetics-400 and then evaluated directly on downstream datasets.

| Model                                                           | Input  | HMDB-51 | UCF-101 | Kinetics-600 |                                                                    Model                                                                     |
|---------------------------------------------------------------------------|:------:|:-------:|:-------:|:------------:|:--------------------------------------------------------------------------------------------------------------------------------------------:|
| EZ-CLIP(ViT-16) | 8x224 |  52.9   |  79.1   |     70.1     |  [link](https://drive.google.com/file/d/19QNGgaZjPyq0yz7XJGFccS7MV09KMY_K/view?usp=drive_link)  |


### Base-to-novel generalization results
Here, we divide each dataset into base and novel classes.
All models are trained on base classes and evaluated on both base and novel classes.

| Dataset                                                | Input  | Base Acc. | Novel Acc. |  HM  |                                                                                                                                                                                                                   Model                                                                                                                                                                                                                   |
|----------------------------------------------------------------|:------:|:---------:|:----------:|:----:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| K-400 | 8x224 |  73.1 | 60.6 | 66.3| [link](https://drive.google.com/file/d/1q8rBkL0QKNTeJJihWkNUwm1eAGH_OY0U/view?usp=sharing) |
| HMDB-51 | 8x224 | 77.0 | 58.2  |66.3 | [link](https://drive.google.com/file/d/1hW2i6agAhpyFvoRgPcOki3coQHx-6oWN/view?usp=sharing) |
| UCF-101 | 8x224 |    94.4 | 77.9 | 85.4 | [link](https://drive.google.com/file/d/16HTxwbqfi1N8BPVjfrvL6F_A4xLNt-zc/view?usp=sharing) |
| SSV2 | 8x224 |     16.6 | 13.3 | 14.8 | [Link](https://drive.google.com/file/d/1EtpET-s634JnHK7n57vrvqNpE7qH_dHq/view?usp=sharing) |

## Data Preparation
We need to first extract videos into frames for fast reading. Please refer 'Dataset_creation_scripts' data pre-processing.
We have successfully trained on [Kinetics](https://deepmind.com/research/open-source/open-source-datasets/kinetics/), [UCF101](http://crcv.ucf.edu/data/UCF101.php), [HMDB51](http://serre-lab.clps.brown.edu/resource/hmdb-a-large-human-motion-database/),





## Training
```
# Train
python train.py --config configs/K-400/k400_train.yaml

```

## Testing
```
# Test 
python test.py --config configs/ucf101/UCF_zero_shot_testing.yaml

```

## Citation
If you find the code and pre-trained models useful for your research, please consider citing our paper:

```
@article{ez2022clip,
  title={EZ-CLIP: Efficient Zeroshot Video Action Recognition},
  author={Shahzad Ahmad, Sukalpa Chanda, Yogesh S Rawat},
  journal={arXiv preprint arXiv:2312.08010},
  year={2024}
}
```


# Acknowledgments
Our code is based on [ActionCLIP](https://github.com/sallymmx/ActionCLIP?tab=readme-ov-file) 

