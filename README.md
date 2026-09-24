# VISION_OS // BROWSER-NATIVE VISION ENGINE

A client-side, zero-backend computer vision testbed powered by **Google MediaPipe Tasks-Vision**. Built with a retro terminal interface, `VISION_OS` compiles, runs, and layers multiple edge-AI perception models directly in the browser over WebAssembly and WebGL.

[![Live Demo](https://img.shields.io/badge/DEMO-ONLINE-00ff41?style=for-the-badge&logo=github)](https://mahith-dev.github.io/Vision-os/)
[![MediaPipe](https://img.shields.io/badge/ENGINE-Tasks--Vision-blue?style=for-the-badge)](https://developers.google.com/mediapipe/solutions/vision)
[![License](https://img.shields.io/badge/LICENSE-MIT-green?style=for-the-badge)](LICENSE)

---

## ⚡ Live Deployment

Access the production deployment directly in any modern browser:  
🔗 **[https://mahith-dev.github.io/Vision-os/](https://mahith-dev.github.io/Vision-os/)**

> **Note:** Requires camera permissions. Handled client-side—no video frames or sensory data leave your local hardware.

---

## 🖥️ System Architecture & Features

`VISION_OS` acts as an interactive profiling and demonstration environment for modern browser-based machine learning inference.

### Integrated Vision Modules

| Subsystem | Underlying Model | Execution Target | Output |
| :--- | :--- | :--- | :--- |
| **Face Landmarker** | `face_landmarker.task` | GPU (WebGL) | 468 3D facial landmarks + facial contours |
| **Hand Landmarker** | `hand_landmarker.task` | GPU (WebGL) | 21 3D knuckle & finger joint points per hand |
| **Pose Landmarker** | `pose_landmarker_full.task` | GPU (WebGL) | 33 3D full-body skeletal tracking points |
| **Gesture Recognizer** | `gesture_recognizer.task` | GPU (WebGL) | Real-time classification (Pinch, Fist, Peace, etc.) |
| **Object Detector** | `efficientdet_lite2.tflite` | CPU (WASM) | Multi-class bounding boxes with confidence scores |

---

## 🛠️ Key Engineering Decisions

* **Lazy Allocation Pipeline:** Heavy machine learning models (~5MB–30MB each) are not loaded on page boot. Memory allocation and WASM compilation occur asynchronously only when a specific module is toggled.
* **Dual-Pass Coordinate Decoupling:** Canvas rendering is bifurcated into a mirrored hardware context (to preserve natural selfie-camera tracking) and an unmirrored coordinate pass (ensuring text labels and bounding boxes render correctly left-to-right).
* **Synchronous Hardware Loop:** Uses a single `requestAnimationFrame` thread synchronized to native camera ticks (`video.currentTime`), preventing frame-tearing and thread thrashing when layering concurrent models.
* **Zero Build-Step Architecture:** Written in native ES Modules and HTML5 Canvas API. Runs without Node.js dependencies, bundlers, or compilation pipelines.

---

## 🚀 Local Development Setup

To test or modify the engine locally:

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/Mahith-dev/Vision-os.git](https://github.com/Mahith-dev/Vision-os.git)
   cd Vision-os
