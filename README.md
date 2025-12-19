# prompt-based-3d-object-reconstruction
Prompt-based 3D object reconstruction pipeline that converts a single RGB image and text prompt into a colored 3D point cloud using YOLO-World, SAM, and Depth Anything v2.


# Prompt-Based 3D Object Reconstruction from a Single Image

This project implements an end-to-end computer vision pipeline that takes
a single RGB image and a text prompt as input, and produces a 3D point cloud
of the specified object.

## Current Features
- Zero-shot object detection using YOLO-World
- Prompt-guided object segmentation using Segment Anything (SAM)
- Object-specific depth estimation using Depth Anything v2
- 3D point cloud reconstruction from monocular depth

## Pipeline Overview
Image + Prompt  
→ YOLO-World (object localization)  
→ SAM (precise segmentation)  
→ Depth Anything v2 (object-only depth estimation)  
→ RGB-D back-projection (3D point cloud)

## Results (Current)
- Generates a colored 3D point cloud of the detected object
- Supports interactive visualization (Plotly / Open3D)
- Works on arbitrary objects via text prompts

## Work in Progress
- Point cloud denoising and scaling
- Surface reconstruction (mesh generation)
- Multi-view fusion for improved 3D completeness
- NeRF / Gaussian Splatting based reconstruction

## Tech Stack
- Python
- PyTorch
- YOLO-World
- Segment Anything (SAM)
- Depth Anything v2
- Open3D / Plotly

## Status
🚧 Actively under development. Core pipeline implemented; improvements ongoing.

