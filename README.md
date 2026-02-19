# Computer Vision for Fabric Defect Detection
### *An Unsupervised Texture Analysis Approach*

This repository contains the documentation and implementation framework for a systematic approach to automated fabric inspection. By leveraging mathematical pixel relationships, the system "visually feels" fabric surfaces to identify anomalies in real-time.

---

## I. Comparative Analysis of Datasets
For unsupervised projects using a **One-Class SVM**, selecting a dataset with high-quality "Normal" samples is critical. Below is a comparison of industry-standard datasets:

| Dataset | Total Images | Defect-Free Images | Resolution | Primary Benefit |
| :--- | :--- | :--- | :--- | :--- |
| **AITEX (AFID)** | 245 | 140 | 4096 × 256 | **Best Match:** High-res images allow for thousands of 32x32 patches from a single "perfect" sample. |
| **MVTec AD** | 5,354 | ~3,600 | Variable | **Industry Standard:** Optimized for anomaly detection; training sets contain only normal images. |
| **Ten Fabrics (TFD)**| 3,000 | 2,257 | 256 × 256 | **Variety:** Includes 27 different defect types to test flagging sensitivity. |
| **TILDA** | 3,200 | Variable | 768 × 512 | **Robustness:** Includes rotations and lighting changes to test feature invariance. |
| **Lusitano (2024)**| 32,000 | 6,000 | 4096 × 1024 | **Scale:** Modern dataset collected under industrial line-camera conditions. |

---

## II. Methodology: The 3-Step Workflow
The system follows a modular pipeline designed for speed and explainability.



### 1. Windowing (The Scanner)
The system employs a **Sliding Window** technique (typically **32×32 pixels**). Instead of processing entire fabric rolls at once, it examines the material patch-by-patch. This ensures:
* Continuous inspection during production.
* Low memory overhead.
* Precise localization of defects.



### 2. Feature Extraction (The Math Engines)
Visual patches are converted into numerical vectors using three specialized algorithms:
* **Local Binary Patterns (LBP):** Efficiently detects surface irregularities like knots and slubs.
* **GLCM (Gray-Level Co-occurrence Matrix):** Measures **Contrast** and **Entropy** to flag sudden changes in smoothness or sheen.
* **Gabor Filters:** Tuned to specific frequencies and angles to identify directional errors in weaves like Twill or Corduroy.



### 3. Anomaly Detection (The Decision)
The engine utilizes an **Unsupervised One-Class SVM**. 
* **Training:** The model learns the "Normal" mathematical boundary using only perfect fabric examples (30–50 images).
* **Inference:** Any patch whose features fall outside this boundary is flagged as a defect.

---

## III. Technical Advantages

### 🚀 Real-Time Speed
Mathematically efficient algorithms (LBP/GLCM) run on standard CPUs or embedded devices, removing the need for expensive GPUs.

### 📉 Small Data Requirement
Unlike Deep Learning, which requires thousands of labeled defect images, this system requires only **30–50 perfect images** to establish a baseline.

### 🔍 Explainable Results
This is not a "black box." When fabric is rejected, the system can provide specific reasons (e.g., *"Contrast exceeded threshold of 0.8"*), making it easier for engineers to troubleshoot production lines.

---

## Getting Started
1. Clone this repository.
2. Ensure your dataset is organized into `/NODefect_images`, `/Defect_images`, and `/Mask_images`.
3. Install dependencies: `pip install opencv-python scikit-image scikit-learn`.

---
*Developed by Bisman Roop Singh & Bhumika Das*
