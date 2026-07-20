# Ultralytics YOLO & Streamlit computer vision platform

A fully validated, end-to-end computer vision platform leveraging the state-of-the-art **Ultralytics YOLO** framework for real-time Object Detection, Segmentation, Pose Estimation, and Oriented Bounding Boxes (OBB). Features an interactive, browser-based **Streamlit web application** for direct video inference and analytics.

---

## 🚀 Key Features & Capabilities
* **Full YOLO Support:** Object Detection, Instance Segmentation, Pose Estimation, Oriented Bounding Boxes (OBB), and Semantic Segmentation.
* **Streamlit Web UI:** Upload videos, choose custom YOLO weights, configure confidence parameters, and visualize real-time predictions in your browser.
* **Ultralytics Solutions:** Integrated pipelines for Object Counting, Heatmaps, Speed Estimation, Object Cropper/Blurrer, and Queue Management.
* **Multi-Format Exports:** Export trained models to ONNX, TorchScript, OpenVINO, CoreML, and more.

---

## 🛠️ Technology Stack
* **Core Framework:** Python 3.10+ & PyTorch (CPU/CUDA)
* **Computer Vision & Tracking:** OpenCV, NumPy, BoT-SORT, ByteTracker
* **Web UI Dashboard:** Streamlit
* **Testing & Quality Assurance:** pytest, pytest-cov, pytest-xdist
* **Deployment & Formats:** ONNX, ONNX Slim, TorchScript

---

## 📐 System Architecture

The following diagram illustrates how inputs (images, videos, cameras) flow through the application layers to generate predictions, metrics, and interactive visualizations.

```
       +-------------------------------------------------------+
       |                     Input Sources                     |
       |             (Images / Videos / Live Stream)           |
       +---------------------------+---------------------------+
                                   |
                                   v
       +-------------------------------------------------------+
       |                  Streamlit Dashboard                  |
       |      - Parameter Configuration (Confidence, IoU, etc)  |
       |      - Model Select (yolo11n, custom weights)         |
       +---------------------------+---------------------------+
                                   |
                                   v
       +-------------------------------------------------------+
       |               YOLO Core / Inference Engine            |
       |            - Preprocessing & Input Resizing           |
       |            - Model Forward Pass (PyTorch / ONNX)      |
       |            - Non-Maximum Suppression (NMS)            |
       +---------------------------+---------------------------+
                                   |
                                   v
       +-------------------------------------------------------+
       |                 Ultralytics Solutions                 |
       |    - Object Counting        - Speed Estimation        |
       |    - Heatmap Generation     - Object Cropping/Blur    |
       +---------------------------+---------------------------+
                                   |
                                   v
       +-------------------------------------------------------+
       |                    Output & Export                    |
       |         - Interactive Charts & Plotting (Matplotlib)   |
       |         - Real-time Video Stream Renderer             |
       +-------------------------------------------------------+
```

---

## 🔄 Project Workflow

1. **Environment Initialization:** The system initializes by loading dependencies and checking device availability (CPU/CUDA GPU).
2. **Model Selection & Loading:** The user selects a specific vision task (detect, segment, pose, obb) and loads the corresponding pre-trained or custom YOLO model.
3. **Data Ingestion:** Streamlit receives file uploads (e.g. video files) or connects to local webcams/directories.
4. **Frame Processing Loop:** OpenCV decodes frames sequentially and feeds them into the YOLO pipeline.
5. **Inference & Tracking:**
   * Predictions are calculated.
   * Active trackers (BoT-SORT / ByteTracker) assign persistent IDs.
6. **Solution Overlays:** Solutions like counting lines, zones, heatmaps, or blurring are applied to raw frames.
7. **Rendering & Exporting:** Rendered frames are pushed back to the Streamlit UI frame container at runtime, and final predictions are compiled.

---

## ⚡ Setup & Run Instructions

### 1. Installation
Clone the repository and install dependencies in editable mode:
```powershell
# Navigate to project directory
cd D:\Ultralytics\ultralytics-main

# Install development dependencies
python -m pip install -e .[dev]
```

### 2. Run the Streamlit Local Web Server
Launch the interactive web application:
```powershell
yolo solutions inference
```
Or run directly with Streamlit:
```powershell
streamlit run ultralytics/solutions/streamlit_inference.py
```
This starts the server on `http://localhost:8501`.

### 3. Run the Verification Tests
To verify all CLI, engine, solutions, and exporter modules:
```powershell
# Run complete engine tests
python -m pytest tests/test_engine.py -v

# Run solutions tests
python -m pytest tests/test_solutions.py -v

# Run export tests
python -m pytest tests/test_exports.py -k "test_export_torchscript or test_export_onnx" -v
```

---

## 👥 Authors & Contribution
Developed and verified by **Sabari-D**. Under the AGPL-3.0 License.
