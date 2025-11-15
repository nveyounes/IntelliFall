# 🚨 IntelliFall: Real-time, Privacy-Preserving Fall Detection Framework

[![GitHub last commit](https://img.shields.io/github/last-commit/nveyounes/IntelliFall?style=for-the-badge&color=2ecc71)](https://github.com/nveyounes/IntelliFall)
[![License](https://img.shields.io/github/license/nveyounes/IntelliFall?style=for-the-badge&color=3498db)](LICENSE)
[![Website Demo](https://img.shields.io/badge/Live%20Demo-Visit%20Website-important?style=for-the-badge&logo=github&color=e74c3c)](https://nveyounes.github.io/IntelliFall/)
[![Accuracy](https://img.shields.io/badge/Accuracy-97.80%25-brightgreen?style=for-the-badge&logo=tensorflow)](https://nveyounes.github.io/IntelliFall/)
[![Precision](https://img.shields.io/badge/Precision-86.10%25-yellowgreen?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZD0iTTEyIDJjNS41MjMgMCAxMCA0LjQ3NyAxMCAxMHMtNC40NzcgMTAtMTAgMTBTMiAxNy41MjMgMiAxMmMwLTUuNTIzIDQuNDc3LTEwIDEwLTEwem0xIDUuNXYtMS42OWMtLjU4LS41OC0xLjM2LS44MS0yLjQtLjgtLjk5IDAtMS43LjI4LTIuMi44LS41LjUyLS43NCAxLjE1LS43NCAxLjktLjAyLjczLjE5IDEuMzcuNjMgMS45Mi40NC41NiAxLjA3LjgyIDEuODguOC41NyAwIDEuMTEtLjE0IDEuNjQtLjQydi0xLjY1Yy0uMzUuMTYtLjc1LjI0LTEuMjUuMjQtLjQ4IDAtLjguMDUtMS4wNS0uMTVzLS4zNS0uNDMtLjM1LS43NWMwLS40LjE0LS42Ny40NS0uODkuMzEtLjIuNjktLjI4IDEuMTQtLjI4Ljk4LS4wMSAxLjY2LjI2IDIuMDQuNTh6bTIuNDUgNi40NWgtMS43NXYyLjVoLTEuMjVWMTFoMS43NVY4LjVoMS4yVjkuNzVoLjU1djEuMjVoLS41NXYyLjVsMS41NS0xLjI1aDEuMDV2MS43NXoiLz48L3N2ZyI+)](https://nveyounes.github.io/IntelliFall/)
[![Recall](https://img.shields.io/badge/Recall-93.82%25-blueviolet?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZD0iTTEwIDEydi0zSDdWMjBoM3YtMy4wMmMtLjUyLjA2LTEuMDUuMDgtMS41OC4wOC0xLjYyIDAtMy4wNS0uMjgtNC4zMi0uODQtMS4yNy0uNTYtMi4xNi0xLjMtMi44LTIuMTItLjY0LS44Mi0uOTYtMS42NS0uOTYtMi41MiAwLS45Ni4zMi0xLjgxLjk2LTIuNTIuNjQtLjc2IDEuNTQtMS40MSAyLjc1LTEuOTUuOTUtLjQzIDEuOTgtLjcyIDMuMTQtLjg1LjY1LS4wNyAxLjI5LS4wOCAxLjg5LS4wOHYyLjk1YzEuMS0uMDQgMi40NS0uMDIgMy41LjEzLjk3LjE0IDEuNy4zOSAyLjM1Ljc1LjY1LjM2IDEuMTUuOCAxLjUgMS4zLjM1LjUuNTMuOTQuNTMgMS40NSAwIC40Ny0uMTcuOTYtLjUgMS40Ni0uMzQuNS0uOC45My0xLjM2IDEuMy0uNTUuMzgtMS4xOC42OS0xLjg3LjkyLS42OS4yMy0xLjQyLjM4LTIuMi40NXYtNC40eiIvPjwvc3ZnPg==)](https://nveyounes.github.io/IntelliFall/)

---

## ✨ Overview

**IntelliFall** is a cutting-edge, real-time fall detection system designed with a strong emphasis on **privacy and performance**.

Unlike traditional vision-based methods, IntelliFall utilizes **spatiotemporal pose estimation** to transform raw video data into an abstract, privacy-preserving skeletal representation. This innovative approach ensures high accuracy in detecting falls while discarding all personally identifiable visual imagery.

### Key Highlights
* **🛡️ Privacy-First:** Uses MediaPipe keypoints instead of raw video pixels.
* **⏱️ Real-Time:** Optimized for efficiency, running seamlessly on various devices.
* **🌐 Invariance:** Robust to variations in lighting, clothing, scale, and camera angle through custom normalization.
* **🚀 High Performance:** State-of-the-art results powered by a sophisticated **CNN-GRU architecture**.

---

## 🏗️ Technical Architecture & Methodology

The system is built on a robust pipeline that processes video streams into actionable fall-detection signals:

### 1. Keypoint Extraction (Privacy-Preserving)
* **Tool:** Google's **MediaPipe Pose** framework.
* **Process:** Extracts **33 precise human body landmarks** from each video frame, effectively creating a skeletal model that replaces the raw video, guaranteeing privacy.

### 2. Pose Normalization ($\mathcal{N}$)
A two-step normalization process ensures the model focuses solely on movement patterns, not superficial characteristics:
* **Translation:** Centers the pose relative to the hip midpoint.
* **Scaling:** Normalizes the keypoints by the **torso length** (distance between hip center and shoulder center) to achieve size and position invariance.

### 3. Feature Engineering
A comprehensive **71-dimensional feature vector** ($\mathbf{f}(t)$) is computed per frame, capturing both static and dynamic information:
* **Normalized Positions ($\hat{p}$):** Scale and position invariant coordinates.
* **Kinematic Features ($\dot{\hat{p}}$):** Instantaneous velocity of each keypoint, crucial for detecting the rapid movements of a fall.
* **Geometric Features:**
    * **Aspect Ratio ($A_R$):** Distinguishes upright vs. prone postures.
    * **Normalized Hip Height ($H_{\text{Hip}}$):** Direct signal of vertical body position.
    * **Torso Angle ($\theta_{\text{Torso}}$):** Captures leaning and bending motions.

### 4. Deep Learning Model
* **Architecture:** **CNN-GRU** (Convolutional Neural Network - Gated Recurrent Unit).
* **Training:** Trained on a curated dataset of 1,487 videos, utilizing **Class Weighting** to effectively address data imbalance and bias toward the minority class (falls).

---

## 🎯 Model Performance

| Metric | Result | Description |
| :--- | :--- | :--- |
| **Accuracy** | **97.80%** | Overall correctness across all predictions. |
| **Precision** | **86.10%** | Low rate of false alarms, enhancing user trust. |
| **Recall** | **93.82%** | High sensitivity in detecting genuine fall events. |

---

## 💻 Tech Stack & Dependencies

| Category | Technology | Icon |
| :--- | :--- | :--- |
| **Core ML** | Python | ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) |
| **Pose Estimation** | MediaPipe | ![MediaPipe](https://img.shields.io/badge/MediaPipe-000000?style=flat-square&logo=google&logoColor=white) |
| **Deep Learning** | CNN-GRU / TensorFlow (Assumption) | ![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white) |
| **Web Demo** | HTML5 / CSS3 / JavaScript | ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white) ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) |

---

## ⚙️ Complete Platform Features

The core framework is part of a larger, full-featured platform that includes:

| Feature | Description | Icon |
| :--- | :--- | :--- |
| **Dashboard** | Monitor real-time statistics and view comprehensive reports. | 📊 |
| **Live Camera** | Enable fall detection using your device's camera for immediate monitoring. | 📹 |
| **Video Upload** | Analyze recorded videos for post-hoc fall detection and reporting. | 📁 |
| **Notification System** | Instant alerts through multiple channels to ensure timely response. | 🔔 |

**Notification Channels:** 📨 **Gmail** (Email alerts), 💬 **Telegram** (Instant messaging), 📞 **Twilio** (SMS and voice call alerts).

---

## 🚀 Installation & Setup

### Prerequisites

* [List any required dependencies like Python version, specific libraries, etc.]
    * Python 3.x
    * TensorFlow / PyTorch
    * MediaPipe

### Local Setup

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/nveyounes/IntelliFall.git](https://github.com/nveyounes/IntelliFall.git)
    cd IntelliFall
    ```
2.  **Install the necessary libraries:**
    ```bash
    pip install -r requirements.txt
    ```
    *Note: If you don't have a `requirements.txt`, create one or list the main `pip install` commands here.*

3.  **Run the detection script:**
    ```bash
    # Example command to run the core fall detection module
    python run_detection.py --source [video_file or camera_index]
    ```

---

## 🤝 Contributing

We welcome contributions! If you have suggestions for performance improvements, feature enhancements, or bug fixes, please open an issue or submit a pull request.

1.  Fork the Project.
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`).
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`).
4.  Push to the Branch (`git push origin feature/AmazingFeature`).
5.  Open a Pull Request.

---

## 👨‍💻 Authors & Acknowledgments

* **Younes Farhat** ([@nveyounes](https://github.com/nveyounes))
* **Mohamed Ghellab**
* **Technical Report:** Fall Detection Framework

---

## ⚖️ License

Distributed under the **[MIT License / Apache 2.0 License / etc.]**. See `LICENSE` for more information.
