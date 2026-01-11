
# Prompt-Based 3D Object Reconstruction from a Single Image

# Prompt-Based 3D Object Reconstruction

This project implements an end-to-end computer vision pipeline that transforms a single RGB image and a text prompt into an interactive 3D point cloud. By integrating state-of-the-art zero-shot models, the system can detect, segment, and reconstruct specific objects from a scene without requiring custom training data.

## 🚀 Features

- **Zero-Shot Object Detection:** Uses **YOLOv8-World** to detect objects based on natural language prompts (e.g., "chair", "cat", "car").
- **High-Precision Segmentation:** Leverages the **Segment Anything Model (SAM)** to generate accurate pixel-level masks using the detection bounding box.
- **Monocular Depth Estimation:** Utilizes **Depth Anything** to compute a high-fidelity depth map of the complete image.
- **3D Visualization:** Back-projects the masked RGB-D data into 3D space and renders the result as an interactive point cloud using **Plotly**.

## 🛠️ Pipeline Overview

The system processes the input image in the following sequential steps:

1.  **Input:** The user provides an image and a text prompt.
2.  **Detection (YOLOv8-World):** The model performs zero-shot detection to find the bounding box of the object specified in the prompt.
3.  **Segmentation (SAM):** The bounding box coordinates are passed as a prompt to SAM, which segments the object from the background.
4.  **Depth Estimation (Depth Anything):** The model estimates a relative depth map for the entire image to capture the geometry.
5.  **Reconstruction:** The segmentation mask is applied to the depth map and RGB image. The filtered data is back-projected into a 3D point cloud.
6.  **Output:** The final 3D object is visualized interactively in the browser via Plotly.

## 🧰 Tech Stack

- **Language:** Python
- **Detection:** YOLOv8-World (Ultralytics)
- **Segmentation:** Segment Anything Model (SAM)
- **Depth Estimation:** Depth Anything
- **Visualization:** Plotly
- **Libraries:** PyTorch, OpenCV, NumPy, Torchvision

## 📋 Installation

```bash
# Clone the repository
git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
cd your-repo-name

# Install dependencies
pip install -r requirements.txt
