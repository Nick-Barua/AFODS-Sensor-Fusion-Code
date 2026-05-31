# AFODS Sensor Fusion Code

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue?style=flat-square)](https://opensource.org/licenses/Apache-2.0)
[![DOI: MDPI](https://img.shields.io/badge/DOI-10.3390%2Fvehicles7040149-blue?style=flat-square)](https://doi.org/10.3390/vehicles7040149)
[![Zenodo Figures](https://img.shields.io/badge/Zenodo-Figures-orange?style=flat-square)](https://doi.org/10.5281/zenodo.17621800)
[![Zenodo Video](https://img.shields.io/badge/Zenodo-Video_Demo-orange?style=flat-square)](https://doi.org/10.5281/zenodo.17460755)
[![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-CUDA-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![ISO 26262](https://img.shields.io/badge/Standard-ISO_26262_ASIL_B-red?style=flat-square)](https://www.iso.org/standard/43464.html)
[![Patent](https://img.shields.io/badge/Patent-JP_2025--167440-green?style=flat-square)]()
[![ORCID](https://img.shields.io/badge/ORCID-0000--0003--4641--0112-A6CE39?style=flat-square&logo=orcid&logoColor=white)](https://orcid.org/0000-0003-4641-0112)

> **Authors:** Dr. Nick Barua · Prof. Masahito Hitosugi  
> Department of Legal Medicine, Shiga University of Medical Science, Otsu, Shiga, Japan  
> **Published:** *Vehicles*, MDPI, 2025, 7(4), 149  
> **DOI:** [10.3390/vehicles7040149](https://doi.org/10.3390/vehicles7040149)  
> **Patent Filed:** Japanese Patent Application No. 2025-167440 (Filed: 3 October 2025)

---

## 📌 Overview

This repository contains the complete implementation scripts, configuration files, and core logic for the **Advanced Falling Object Detection System (AFODS)**, supporting the peer-reviewed manuscript:

> **Advanced Multi-Modal Sensor Fusion System for Detecting Falling Humans: Quantitative Evaluation for Enhanced Vehicle Safety**  
> *Vehicles*, MDPI, 2025, 7(4), 149 · DOI: [10.3390/vehicles7040149](https://doi.org/10.3390/vehicles7040149)

The codebase enables full replication of the methodology, benchmarks, and results presented in the paper. Validated across **320 controlled trials**, AFODS achieved **98.2% TPR at night (0 lux)** — a condition where the baseline visible-spectrum system collapsed to 21.4%.

---

## 🚀 Key Features & Models

| Component | Implementation | Details |
| :--- | :--- | :--- |
| **Detection Model** | YOLOv7-Tiny | PyTorch · Cross-Entropy Loss · Adam optimiser · mAP@0.5: 91.3% |
| **Prediction Model** | GRU (Gated Recurrent Unit) | Proactive fall assessment via normalised 2D pose keypoints over 1–2 s window |
| **Fusion Logic** | Confidence-weighted pipeline | Dynamically integrates LWIR · NIR Stereo · Ultrasonic based on environmental conditions |
| **Depth & Motion** | SGM + Lucas–Kanade optical flow | Dense disparity map + vertical motion tracking + lightweight pose estimation |
| **Acoustic Verification** | MFCC Classifier (CNN/RNN) | Fall signature vs. road noise discrimination — corroborating factor only |
| **Safety Standard** | ISO 26262 — target **ASIL B** | Redundant sensor modalities mitigate single-point failures |

---

## 📊 Validated Performance (320 Controlled Trials)

All metrics are drawn directly from the peer-reviewed publication (Tables 1 & 2, Section 4). Each condition was repeated 20 times using standardised ATDs deployed via pneumatic rig at 20 m.

### Detection Accuracy (True Positive Rate)

| Environmental Condition | AFODS TPR (%) | Baseline TPR (%) | p-value |
| :--- | :---: | :---: | :---: |
| **Clear Daylight** | **99.5** | 96.8 | 0.041 |
| **Night (0 lux)** | **98.2** | 21.4 | <0.001 |
| **Rain (50 mm/h)** | **96.4** | 55.7 | <0.001 |
| **Fog (<50 m visibility)** | **95.8** | 32.1 | <0.001 |

### False Positive Rate

| System | Condition | False Positives (per 24 h) | Reduction vs. Baseline |
| :--- | :--- | :---: | :---: |
| Baseline | Daytime | 16.4 | — |
| Baseline | Nighttime | 31.2 | — |
| Baseline | Adverse Weather | 48.9 | — |
| **AFODS** | **Daytime** | **1.1** | **93.3%** |
| **AFODS** | **Nighttime** | **1.5** | **95.2%** |
| **AFODS** | **Adverse Weather** | **2.3** | **95.3%** |
| **AFODS** | **Average** | **1.6** | **95.0%** |

**Mean System Latency:** 46.3 ms (SD = 4.1 ms) across all 320 trials  
**Mean Detection Range:** AFODS 41.5 m (SD = 4.8 m) vs. Baseline 22.3 m (SD = 12.5 m) — *t*(158) = 15.72, *p* < 0.001

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

---

## 📊 Usage: Reproducing Metrics

To reproduce the TPR, FPR, and Latency metrics from **Section 4** of the manuscript:

### Step 1 — Fetch Validation Data

Download validation data logs from the Zenodo archive:

- **Figures & Methodology:** [10.5281/zenodo.17621800](https://doi.org/10.5281/zenodo.17621800)
- **Operational Sequence Video:** [10.5281/zenodo.17460755](https://doi.org/10.5281/zenodo.17460755)

### Step 2 — Run Detection Validation

```bash
# Reproduce night condition metrics (primary novel claim)
python validation_scripts/calculate_detection_metrics.py \
  --condition night \
  --model afods

# Reproduce daytime condition metrics
python validation_scripts/calculate_detection_metrics.py \
  --condition daytime \
  --model afods

# Compare against visible-spectrum baseline
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

This repository is part of a unified research program on sensor fusion and road safety:

| # | Title | Venue | Role |
| :---: | :--- | :---: | :--- |
| **1** | **Advanced Multi-Modal Sensor Fusion System** *(this repo)* | MDPI Vehicles | Technical foundation & benchmarks |
| 2 | [Integrated Safety Architectures: Leveraging Multi-Modal AI and ISO 26262 to Protect Vulnerable Road Users](https://doi.org/10.2139/ssrn.6112086) | SSRN | System-level ISO 26262 safety architecture |
| 3 | [From Post-Mortem to Prevention: Redefining "Invisible" Pedestrians through ISO 26262 and Multi-Modal AI](https://doi.org/10.2139/ssrn.6305618) | SSRN | Problem framing & ISO 26262 compliance |
| 4 | [Sudden Incapacitation or Death at the Wheel: Probabilistic Risk Factors for Catastrophic Multi-Vehicle Collisions](https://doi.org/10.2139/ssrn.6305478) | SSRN | Epidemiological evidence for ADAS mandate |
| 5 | [The Invisible Victims of the Road: Why ADAS Cannot See the Pedestrians Most Likely to Die](https://doi.org/10.20944/preprints202604.0850.v1) | Preprints.org *(under review)* | AFODS forensic injury translation & regulatory advocacy |
| 6 | [A Physics-Grounded Multi-Modal Sensor Fusion Framework for Pedestrian Impact Kinematic Reconstruction Under Uncertainty: Phase 1 Design and Theoretical Evaluation](https://doi.org/10.3390/s26113387) | MDPI Sensors | Forensic reconstruction companion — retrospective kinematic reconstruction from post-impact scene observables |

---

## 📂 Related Repositories

- **[Advanced-Multi-Modal-Sensor-Fusion-System-for-Detecting-Falling-Humans](https://github.com/Nick-Barua/Advanced-Multi-Modal-Sensor-Fusion-System-for-Detecting-Falling-Humans)** — Primary repository with full system documentation and figures
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

The system described in this repository is subject to **Japanese Patent Application No. 2025-167440** (Filed: 3 October 2025).
