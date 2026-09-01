> **⚠️ Proprietary — All Rights Reserved.** © 2026 Sandeep Grover. This repository is licensed to Sandeep Grover and may **not** be used, run, copied, modified, distributed, or used to train models without prior written permission. Public visibility does not grant a license. See [LICENSE](LICENSE).

---

![Python](https://img.shields.io/badge/Python-3.10%2B-blue) ![CV](https://img.shields.io/badge/Computer-Vision-red) ![License](https://img.shields.io/badge/license-CC%20BY--NC%204.0-lightgrey)

# Industrial Component Anomaly Detection

Unsupervised and semi-supervised anomaly detection on industrial surface defects using PatchCore and autoencoder baselines.

---

## Task

**Anomaly Detection (Computer Vision)**

---

## Architecture

```
Normal Images → WideResNet Feature Extraction → Memory Bank → Patch-level Anomaly Score → Heatmap
```

---

## Key Features

- PatchCore (Roth et al. 2022) — nearest-neighbour memory bank on WideResNet features
- Autoencoder reconstruction baseline for comparison
- Pixel-level anomaly segmentation heatmaps
- AUROC and PRO (Per-Region Overlap) evaluation
- No defect labels required at training time (normal images only)

---

## Dataset

[MVTec Anomaly Detection Dataset](https://www.mvtec.com/company/research/datasets/mvtec-ad)

---

## Project Structure

```
├── src/
│   ├── model_baseline.py      # Baseline model
│   └── model_advanced.py      # Advanced model
├── notebooks/
│   └── 01_EDA.ipynb           # Exploratory analysis
├── manuscripts/
│   └── manuscript.md          # IMRaD writeup
├── reports/
│   └── references.md          # Verified references
├── deliverables/
│   └── presentation.html      # Self-contained HTML
├── data/
│   └── README.md              # Dataset download instructions
└── requirements.txt
```

---

## Quick Start

```bash
git clone https://github.com/Sandyyy123/industrial-anomaly-detection.git
cd industrial-anomaly-detection
pip install -r requirements.txt

# See data/README.md for dataset download
jupyter notebook notebooks/01_eda.ipynb
# or run modeling:
jupyter notebook notebooks/03_modeling.ipynb
jupyter notebook notebooks/03_modeling.ipynb  # advanced model (GPU recommended)
```

---

## Tech Stack

`PyTorch · torchvision · PatchCore · scikit-learn · OpenCV`

---

## Author

**Dr. Sandeep Grover** — PhD Data Science, independent ML researcher, Germany.

---

## License

MIT
