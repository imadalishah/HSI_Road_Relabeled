# Extending HSI-Road Dataset: From Binary Labels to Six-Class Surface-Oriented Taxonomy

Official repository for the manuscript: **"HSI-Road Relabeled: Surface-Aware Road-Scene Segmentation"**

> ⚠️ **Release Status:** The manuscript is currently under peer review. Annotation masks, registration code, model configurations, and benchmark evaluation scripts will be made publicly available soon.

---

## 📌 Abstract

The HSI-Road dataset provides paired RGB and 25-channel NIR images with binary masks but no surface-level labels. This repository introduces a manually relabelled six-class taxonomy (**Non-drivable**, **Asphalt**, **Concrete**, **Dirt**, **Water**, and **Grass**) and an RGB-to-NIR registration pipeline with corresponding registered annotations.

Six semantic segmentation models (SSMs) are evaluated across four input modal configurations:
* **$\text{RGB}_{\text{ori}}$**: Original-resolution RGB.
* **$\text{RGB}_{\text{reg}}$**: Registered low-resolution RGB aligned with NIR space.
* **$\text{NIR}$**: 25-channel Near-Infrared images.
* **$\text{RGBN}_{\text{stk}}$**: Channel-stacked $\text{RGB}_{\text{reg}}$–NIR representation.

The benchmark quantifies the combined effect of registration and spatial-resolution reduction on RGB, along with evaluating NIR and $\text{RGBN}_{\text{stk}}$ configurations using per-class/mean IoU and F1 scores.

---

## 🏷️ Relabelled Six-Class Taxonomy

We refine the binary road masks into six detailed surface and off-road categories:

| Class ID | Class Name | Description & Scope |
| :---: | :--- | :--- |
| **0** | **Non-drivable** | Roadside structures, non-navigable terrain, vegetation, pedestrians, and obstacles |
| **1** | **Asphalt** | Paved asphalt roadways |
| **2** | **Concrete** | Concrete paths and road sections |
| **3** | **Dirt** | Unpaved dirt roads, soil tracks, and gravel paths |
| **4** | **Water** | Puddles, water bodies, and open drain/ditches |
| **5** | **Grass** | Road side drivable grassy patches |

---

## ⚙️ Input Configurations & Benchmark

The evaluation pipeline tests 6 SSMs across 4 distinct modal configurations to analyze multimodal surface perception:

```text
                ┌──► RGB_ori  (Original High-Res RGB:       [3, 704, 1280])
                │
HSI-Road Pair ──┼──► RGB_reg  (Registered Low-Res RGB:      [3, 192, 384])
                │
                ├──► NIR      (25-Channel Near-Infrared:    [25, 192, 384])
                │
                └──► RGBN_stk (Channel-stacked RGB_reg+NIR: [28, 192, 384])
```

### Key Dataset Findings

* **$\text{RGB}_{\text{ori}}$** achieves the highest overall performance across SSMs and Class wise metrics.
* **$\text{RGBN}_{\text{stk}}$** consistently improves over both single-modal **$\text{RGB}_{\text{reg}}$** and **$\text{NIR}$** for 5 out of 6 evaluated SSMs.
* **Water** shows the most significant, consistent class-level gain under $\text{RGBN}_{\text{stk}}$, while **Grass** segmentation performance remains heavily configuration-dependent.

---

## 📁 Repository Structure (Updating Soon)

```text
├── annotations/
│   ├── train/                 # 6-class semantic segmentation masks
│   ├── val/
│   └── test/
├── registration/
│   ├── rgb_nir_register.py    # RGB-to-NIR registration pipeline
│   └── registered_masks/      # Co-registered spatial annotations
├── models/                    # Implementation of the 6 evaluated SSMs
├── configs/                   # Experiment configs for RGB_ori, RGB_reg, NIR, RGBN_stk
├── evaluate.py                # Evaluation script (mIoU, F1, Per-class metrics)
├── LICENSE.md                 # CC BY-NC 4.0 License details
└── README.md

```

---

## 📜 License

* The **6-class annotations, registration pipeline, and code** in this repository are licensed under the [Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0)](LICENSE.md).
* The **original raw RGB and 25-channel NIR images** belong to the original [HSI-Road dataset](https://github.com/NUST-Machine-Intelligence-Laboratory/hsi_road).

---

## 📖 Citation

If you use this relabelled dataset, registration pipeline, or benchmark setup in your research, please cite our paper and original dataset authors/contribution:

```bibtex
@inproceedings{shah2026hsiroad6class,
  author={Shah, Imad Ali and Li, Jiarong and Glavin, Martin and Jones, Edward and Ward, Enda and Deegan, Brian},
  title={HSI-Road Relabeled: Surface-Aware Road-Scene Segmentation}, 
  year={2026},
  volume={},
  number={},
  pages={1-5},
  journal={arXiv preprint arXiv:2608.XXXXX},
}

```

Original HSI-Road Dataset:

```bibtex
@inproceedings{lu2020HSI,
  title     = {HSI Road: A Hyper Spectral Image Dataset for Road Segmentation},
  author    = {Jiarou Lu and Huafeng Liu and Yazhou Yao and Shuyin Tao and Zhenmin Tang and Jianfeng Lu},
  booktitle = {IEEE International Conference on Multimedia and Expo (ICME)},
  year      = {2020}
}

```

```

```
