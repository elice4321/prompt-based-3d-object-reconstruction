# Zero-Shot RGB-D Point Cloud Generation from 2D Images

This project implements a **zero-shot, prompt-based pipeline** for generating object-level RGB-D point clouds from unlabeled 2D images. By combining recent foundation models for object detection, segmentation, and monocular depth estimation, the system reconstructs 3D geometry from a single RGB image **without any task-specific training**.

---

## Project Overview

The complete pipeline converts a **single RGB image** into a **3D point cloud** of a selected object using the following stages:

### 1. Zero-Shot Object Detection
- Object detection is performed using **YOLO-World / YOLOv8**, which supports text-prompt-based detection
- Enables detection of objects **without requiring predefined class labels or retraining**

### 2. Prompt-Based Segmentation
- The **Segment Anything Model (SAM)** is used to obtain precise pixel-level segmentation
- The bounding box predicted by YOLO is used as a **prompt**, rather than cropping the image
- Preserves **contextual information** and improves segmentation accuracy

### 3. Depth Estimation
Two depth estimation models are used:
- **Depth-Anything-V2** as a strong zero-shot baseline
- **ZoeDepth** (trained on NYU Depth V2) for refined metric depth estimation
- Depth is always predicted on the **full image** to maintain camera geometry and avoid distortions

### 4. 3D Point Cloud Generation
- The segmented depth map is projected into 3D space using a **pinhole camera model**
- RGB values are mapped to each 3D point
- Produces an **object-only RGB-D point cloud**, saved in `.ply` format using **Open3D**

---

## Key Design Choices

- ✅ **SAM is applied using the bounding box only** as a guidance prompt, not as a hard crop
- ✅ **Depth estimation is performed on the entire image** to preserve camera symmetry
- ✅ **Depth-Anything-V2** provides a general-purpose zero-shot baseline
- ✅ **ZoeDepth** demonstrates how supervised metric depth improves reconstruction quality

---

## Repository Structure

```
3DCloudCreationProject/
├── Depth-Anything-V2/
│   ├── depth_anything_v2/
│   ├── ZoeDepth/
│   ├── checkpoints/
│   └── run.py
├── datasets/
│   └── nyu_depth_v2/
├── test_images/
├── output/
│   ├── depth maps (.png, .npy)
│   ├── 3D point clouds (.ply)
│   └── visualizations
├── notebooks/
│   ├── pipeline.ipynb
│   └── depth_refinement.ipynb
├── requirements.txt
└── README.md
```

---

## Models, Outputs & Checkpoints (Google Drive)

Due to large file sizes, pretrained models, checkpoints, depth outputs, and generated 3D point clouds are stored separately in **Google Drive**.

**📂 Google Drive Link:**  
[https://drive.google.com/drive/folders/1RF1tMwIdm1KmmpnEy-YbA7-5bwQeyBWj?usp=sharing](https://drive.google.com/drive/folders/1RF1tMwIdm1KmmpnEy-YbA7-5bwQeyBWj?usp=sharing)

**This folder contains:**
- Depth-Anything-V2 pretrained checkpoints
- ZoeDepth pretrained models
- Output depth maps
- Final 3D point clouds
- Sample results

---

## Installation

Install the required dependencies using:

```bash
pip install -r requirements.txt
```

**Note:**  
PyTorch with CUDA support should be installed separately depending on your system.  
See: [https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)

---

## Running the Pipeline

### Depth Estimation (Depth-Anything-V2)

```bash
cd Depth-Anything-V2
python run.py --encoder vits --img-path ../test_images/room.png --outdir ../output
```

### 3D Point Cloud Generation

1. Detect the object using **YOLO**
2. Segment the object using **SAM**
3. Apply the segmentation mask to the depth map
4. Project depth values to 3D using **Open3D**
5. Save the resulting point cloud as a `.ply` file

**The `.ply` file can be viewed using:**
- MeshLab
- CloudCompare
- Blender

**No Python environment is required to view the final results.**

---

## Results

- ✅ The pipeline successfully generates **object-only RGB-D point clouds** from a single RGB image
- ✅ **Depth-Anything-V2** provides a reliable zero-shot baseline
- ✅ **ZoeDepth** significantly improves depth smoothness and geometric consistency for indoor scenes
- ⚠️ Remaining artifacts are mainly due to monocular depth ambiguity and approximate camera intrinsics

---

## Limitations

- Monocular depth estimation introduces noise near object boundaries
- Camera intrinsics are approximated when metadata is unavailable
- Metric accuracy varies across indoor and outdoor domains

---

## Future Work

- Fine-tuning ZoeDepth on domain-specific datasets
- Camera intrinsic estimation from metadata
- Mesh reconstruction from point clouds
- Multi-view consistency using video input
- Synthetic dataset generation for underrepresented object categories

---

## Acknowledgements

- [YOLO-World / YOLOv8](https://github.com/ultralytics/ultralytics)
- [Segment Anything Model (SAM)](https://github.com/facebookresearch/segment-anything)
- [Depth-Anything-V2](https://github.com/DepthAnything/Depth-Anything-V2)
- [ZoeDepth](https://github.com/isl-org/ZoeDepth)
- [Open3D](https://github.com/isl-org/Open3D)

---

## Author

**Nidhi Sharma**  
IIT Guwahati

---

## What's Next?

If you need help with:
- 📄 Shortening this for a one-page project README
- 📝 Writing a paper-style abstract
- 📊 Preparing result figures and captions
- 📤 Final submission formatting

Just let me know! 👍
