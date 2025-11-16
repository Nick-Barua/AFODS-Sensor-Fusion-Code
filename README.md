# AFODS-Sensor-Fusion-Code (vehicles-3989222)

This repository contains the complete implementation scripts, configuration files, and core logic for the **Advanced Falling Object Detection System (AFODS)**, supporting the academic manuscript **"Advanced Multi-Modal Sensor Fusion System for Detecting Falling Humans: Quantitative Evaluation for Enhanced Vehicle Safety."**

## 🚀 Key Features & Models

The codebase allows for the replication of the methodology detailed in the paper, addressing the methodological requirements for reproducibility:

* **Detection Model:** YOLOv7-Tiny (Trained with PyTorch, Cross-Entropy Loss).
* **Prediction Model:** Gated Recurrent Unit (GRU) for proactive fall assessment based on pose sequences.
* **Fusion Logic:** Confidence-weighted pipeline integrating LWIR, NIR, and Ultrasonic data.
* **Safety Context:** Designed for alignment with ISO 26262 functional safety principles.

## 🛠️ Setup and Installation (Reproducibility)

The system requires Python 3.x and NVIDA CUDA support for optimal performance.

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Nick-Barua/AFODS-Sensor-Fusion-Code.git](https://github.com/Nick-Barua/AFODS-Sensor-Fusion-Code.git)
    cd AFODS-Sensor-Fusion-Code
    ```
2.  **Install Dependencies:**
    You must first create the required `requirements.txt` file (listing PyTorch, OpenCV, etc.). Then install:
    ```bash
    pip install -r requirements.txt
    ```

## 📊 Usage Example (Reproducing Metrics)

To reproduce the True Positive Rate (TPR), False Positive Rate (FPR), and Latency metrics presented in **Section 4** of the manuscript:

1.  **Get Data:** Validation data logs must be fetched from the associated Zenodo archive (linked below).
2.  **Run Core Validation Script:** (Assuming data logs are in the correct directory)
    ```bash
    python validation_scripts/calculate_detection_metrics.py --condition night --model afods
    ```

## 🔗 Archival and Citation

Please cite our published article when using this code. All documentation, figures, and video data are permanently archived.

* **Final Figures & Methodology:** [10.5281/zenodo.17621800]
* **Operational Sequence Video:** [10.5281/zenodo.17460755]
