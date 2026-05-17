# Cardiac-semi-supervised-learning-segmentation
A comparative evaluation of semi-supervised learning methods  for cardiac image segmentation under limited annotation conditions,  conducted as part of my Master's degree at Université Sorbonne Paris Nord.

---

## Overview

Obtaining labeled medical data is expensive and requires clinical expertise.
This project benchmarks four semi-supervised learning strategies against a fully supervised baseline on the ACDC cardiac MRI dataset, analyzing their ability to leverage unlabeled data when annotations are scarce.

**Methods evaluated:**
| Method | Type |
|---|---|
| Fully Supervised (EfficientUNet) | Baseline |
| Mean Teacher | Consistency regularization |
| Cross Pseudo Supervision (CPS) | Mutual learning |
| Adversarial Network (GAN-based) | Adversarial learning |
| DiffRect | Diffusion-based label rectification |

---

## Dataset

**ACDC** (Automated Cardiac Diagnosis Challenge)  
- 100 patients, cardiac cine MRI (end-diastole & end-systole)  
- Structures: Left Ventricle (LV), Right Ventricle (RV), Myocardium (MYO)  
- Split: 80 train / 20 val / 50 test  
- Two low-label regimes tested: **7 labeled patients** and **14 labeled patients**

---

## Key Results

### Dice Score (↑ better)

| Method | 7 labels | 14 labels |
|---|---|---|
| Fully Supervised | 78.50 | 81.35 |
| Mean Teacher | 79.02 | 81.51 |
| CPS | 78.97 | 81.97 |
| GAN | 76.31 | 77.97 |
| **DiffRect** | **81.91** | **86.22** |
| FS (80 labels) | — | 89.62 |


> DiffRect achieves a **+4.87 Dice gain** over the supervised baseline with 
> only 14 labeled patients, approaching full-supervision performance while 
> using 83% less labeled data.

### Observations

- **Consistency-based methods** (Mean Teacher, CPS) yield only marginal 
  improvements, likely due to noisy pseudo-labels in the low-data regime.
- **Adversarial training** is unstable in small-data settings, consistently 
  degrading performance.
- **DiffRect** stands out by rectifying pseudo-labels via a Label Context 
  Correction (LCC) block and aligning latent feature distributions (LFR), 
  making it significantly more robust to annotation scarcity.

---

## Implementation

Training code adapted from:
- [SSL4MIS](https://github.com/HiLab-git/SSL4MIS) — Mean Teacher, CPS, 
  Adversarial, Fully Supervised baselines
- [DiffRect](https://github.com/CUHK-AIM-Group/DiffRect) — diffusion-based 
  label rectification

All methods trained for 10,000 iterations, batch size 8 (4 labeled per batch),
256×256 input resolution, EfficientUNet backbone (except DiffRect: standard UNet).

---

## Report

The full written analysis is available in [`report.pdf`](./Article.pdf).

---
## Predictions
Pre-computed segmentation outputs for all methods are available — 
see [PREDICTIONS.md](./PREDICTIONS.md) for download links and 
visualization instructions.

---
## Skills demonstrated

`PyTorch` · `Medical image segmentation` · `Semi-supervised learning` · 
`Experimental design` · `Quantitative evaluation` · `Scientific writing`

