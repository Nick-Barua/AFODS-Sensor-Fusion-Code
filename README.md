# AFODS Sensor Fusion Code (vehicles-3989222)

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue?style=flat-square)](https://opensource.org/licenses/Apache-2.0)
[![DOI: MDPI](https://img.shields.io/badge/DOI-10.3390%2Fvehicles7040149-blue?style=flat-square)](https://doi.org/10.3390/vehicles7040149)
[![Zenodo Figures](https://img.shields.io/badge/Zenodo-Figures-orange?style=flat-square)](https://doi.org/10.5281/zenodo.17621800)
[![Zenodo Video](https://img.shields.io/badge/Zenodo-Video_Demo-orange?style=flat-square)](https://doi.org/10.5281/zenodo.17460755)
[![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-CUDA-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![ORCID](https://img.shields.io/badge/ORCID-0000--0003--4641--0112-A6CE39?style=flat-square&logo=orcid&logoColor=white)](https://orcid.org/0000-0003-4641-0112)

> **Authors:** Dr. Nick Barua · Prof. Masahito Hitosugi
> AN Holdings Co., Nishinomiya City, Hyogo, Japan · Shiga University of Medical Science
> **Published:** *Vehicles*, MDPI, 2025, 7(4), 149
> **DOI:** [10.3390/vehicles7040149](https://doi.org/10.3390/vehicles7040149)

---

## 📌 Overview

This repository contains the complete implementation scripts, configuration files, and core logic for the **Advanced Falling Object Detection System (AFODS)**, supporting the peer-reviewed manuscript:

> **Advanced Multi-Modal Sensor Fusion System for Detecting Falling Humans: Quantitative Evaluation for Enhanced Vehicle Safety**
> *Vehicles*, MDPI, 2025, 7(4), 149 · DOI: [10.3390/vehicles7040149](https://doi.org/10.3390/vehicles7040149)

The codebase enables full replication of the methodology, benchmarks, and results presented in the paper.

---

## 🚀 Key Features & Models

| Component | Implementation | Details |
| :--- | :--- | :--- |
| **Detection Model** | YOLOv7-Tiny | PyTorch · Cross-Entropy Loss · mAP@0.5: 91.3% |
| **Prediction Model** | GRU (Gated Recurrent Unit) | Proactive fall assessment via pose sequences |
| **Fusion Logic** | Confidence-weighted pipeline | Integrates LWIR · NIR Stereo · Ultrasonic |
| **Acoustic Verification** | MFCC Classifier | Fall signature vs. road noise discrimination |
| **Explainability** | SHAP Values | Forensic audit trail for post-incident reconstruction |
| **Safety Standard** | ISO 26262 ASIL C-D | S3 / E3 / C0 hazard classification |

---

## 📊 Performance Benchmarks

| Condition | TPR (%) | FPR (%) | mAP@0.5 (%) | Latency (ms) |
| :--- | :---: | :---: | :---: | :---: |
| **Daytime, Clear** | 98.2 | 1.8 | 91.3 | 38 |
| **Night, Dry Road** | 95.6 | 3.1 | 88.7 | 42 |
| **Night, Rain** | 89.4 | 5.2 | 83.1 | 51 |
| *Baseline (Monocular, Night)* | *21.4* | *N/A* | *N/A* | *N/A* |

---

## 🛠️ Setup and Installation

### Requirements
- Python 3.x
- NVIDIA CUDA support (recommended for optimal performance)

### 1. Clone the Repository
```bash
git clone https://github.com/Nick-Barua/AFODS-Sensor-Fusion-Code.git
cd AFODS-Sensor-Fusion-Code
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

Core dependencies include:
```txt
torch>=2.0.0
torchvision>=0.15.0
opencv-python>=4.8.0
numpy>=1.24.0
filterpy>=1.4.5
librosa>=0.10.0
shap>=0.42.0
scikit-learn>=1.3.0
pandas>=2.0.0
matplotlib>=3.7.0
pyyaml>=6.0
onnx>=1.14.0
onnxruntime>=1.15.0
```

---

## 📊 Usage: Reproducing Metrics

To reproduce the TPR, FPR, and Latency metrics from **Section 4** of the manuscript:

### Step 1 — Fetch Validation Data
Download validation data logs from the Zenodo archive:
- **Figures & Methodology:** [10.5281/zenodo.17621800](https://doi.org/10.5281/zenodo.17621800)
- **Operational Sequence Video:** [10.5281/zenodo.17460755](https://doi.org/10.5281/zenodo.17460755)

### Step 2 — Run Detection Validation
```bash
# Reproduce night condition metrics
python validation_scripts/calculate_detection_metrics.py \
  --condition night \
  --model afods

# Reproduce daytime condition metrics
python validation_scripts/calculate_detection_metrics.py \
  --condition daytime \
  --model afods

# Compare against monocular baseline
python validation_scripts/calculate_detection_metrics.py \
  --condition night \
  --model baseline_monocular
```

### Step 3 — Run SHAP Explainability
```bash
python explainability/shap_audit_trail.py --input validation_logs/
```

---

## 📂 Repository Structure

| File / Folder | Description |
| :--- | :--- |
| `models/` | YOLOv7-Tiny and GRU model definitions |
| `fusion/` | Confidence-weighted multi-modal fusion logic |
| `validation_scripts/` | TPR · FPR · Latency metric reproduction |
| `explainability/` | SHAP forensic audit trail generation |
| `acoustic/` | MFCC fall signature classifier |
| `config/` | YAML configuration files |
| `requirements.txt` | Python dependencies |
| `CITATION.cff` | Machine-readable citation file |
| `README.md` | Project documentation |

---

## 🔗 Archival Resources

| Resource | DOI | Purpose |
| :--- | :--- | :--- |
| **Published Paper** | [10.3390/vehicles7040149](https://doi.org/10.3390/vehicles7040149) | Full peer-reviewed methodology |
| **Figures & Methodology** | [10.5281/zenodo.17621800](https://doi.org/10.5281/zenodo.17621800) | All key diagrams and results charts |
| **Operational Sequence Video** | [10.5281/zenodo.17460755](https://doi.org/10.5281/zenodo.17460755) | Real-time system performance demo |

---

## 🔗 Related Publications

This repository is **Part 1** of a unified 4-paper road safety research program:

| # | Title | Venue | Role |
| :---: | :--- | :---: | :--- |
| **1** | **Advanced Multi-Modal Sensor Fusion System** *(this repo)* | MDPI Vehicles | Technical foundation & benchmarks |
| 2 | [From Post-Mortem to Prevention: Redefining "Invisible" Pedestrians through ISO 26262 and Multi-Modal AI](https://doi.org/10.2139/ssrn.6305618) | SSRN | Problem framing & ISO 26262 compliance |
| 3 | [Integrated Safety Architectures: Leveraging Multi-Modal AI and ISO 26262 to Protect Vulnerable Road Users](https://ssrn.com/abstract=6112086) | SSRN | System-level VRU architecture |
| 4 | Sudden Incapacitation or Death at the Wheel: Unravelling the Predictors of Catastrophic Multi-Vehicle Collisions | SSRN *(pending)* | Epidemiological evidence for ADAS mandate |

---

## 📂 Related Repositories

- **[sensor-fusion-fall-detection](https://github.com/Nick-Barua/sensor-fusion-fall-detection)** — AFODS framework documentation *(MDPI Vehicles, 2025)*
- **[AFODS-Operational-Sequence](https://github.com/Nick-Barua/AFODS-Operational-Sequence)** — Five-stage pipeline diagrams and graphical abstract
- **[From-Post-Mortem-to-Prevention-AFODS](https://github.com/Nick-Barua/From-Post-Mortem-to-Prevention-AFODS)** — ISO 26262-aligned conceptual framework

---

## 📝 Citation
```bibtex
@article{vehicles7040149,
  author    = {Barua, Nick and Hitosugi, Masahito},
  title     = {Advanced Multi-Modal Sensor Fusion System for Detecting Falling Humans:
               Quantitative Evaluation for Enhanced Vehicle Safety},
  journal   = {Vehicles},
  volume    = {7},
  number    = {4},
  pages     = {149},
  year      = {2025},
  doi       = {10.3390/vehicles7040149},
  url       = {https://doi.org/10.3390/vehicles7040149}
}
```

---

## 📜 License

This project is licensed under the **Apache 2.0 License** — see the [LICENSE](LICENSE) file for details.
