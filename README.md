
# Real-Time License Plate Detection & Recognition (ALPR)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Hugging Face](https://img.shields.io/badge/🤗%20Hugging%20Face-Transformers-orange)
![RT-DETR](https://img.shields.io/badge/Model-RT--DETR%20v2-green)
![EasyOCR](https://img.shields.io/badge/OCR-EasyOCR-yellow)


This repository contains a complete, end-to-end **Automatic License Plate Recognition (ALPR)** system built with a strong focus on **real-time performance**, **clean system design**, and **practical computer vision engineering**.

The project demonstrates how modern **Transformer-based object detection models** can be combined with lightweight OCR techniques to build a modular and production-ready ALPR pipeline.

---

## 🔍 Project Overview

The system follows a clean, two-stage pipeline:

```
Input Image
 → License Plate Detection (RT-DETR v2)
 → Crop License Plate Region
 → License Plate Recognition (OCR)
 → Visualization / Output
```

- Detection is handled by a fine-tuned **RT-DETR v2** model.
- Recognition is performed only on cropped license plate regions.
- Detection and OCR are **decoupled**, allowing easy experimentation with different OCR models without retraining the detector.

---

## 🚀 Key Features

- Transformer-based **real-time license plate detection**
- Single-class object detection (`license_plate`)
- Clean dataset engineering using Hugging Face Datasets
- Robust evaluation using mAP and recall metrics
- End-to-end inference with bounding box + license number overlay
- Modular design suitable for real-world deployment

---

## 📁 Repository Structure

```
├── license_plate_detection_dataset.ipynb
├── license_plate_detection_train.ipynb
├── license_plate_detection_eval.ipynb
├── license_plate_recognition_inference.ipynb
├── README.md
```

### Notebook Description

| Notebook | Description |
|--------|-------------|
| `license_plate_detection_dataset.ipynb` | Cleans Roboflow COCO dataset and converts it into Hugging Face format |
| `license_plate_detection_train.ipynb` | Fine-tunes RT-DETR v2 for license plate detection |
| `license_plate_detection_eval.ipynb` | Evaluates detection performance on a held-out test set |
| `license_plate_recognition_inference.ipynb` | End-to-end ALPR inference (Detection + OCR) |

---

## 📊 Dataset

- Source: Roboflow (COCO format)
- Task: License Plate Detection
- Classes: `license_plate` (single class)
- Format: Hugging Face Object Detection Dataset
- License: CC BY 4.0

### Dataset Processing Steps

- Removed unused categories
- Remapped class IDs to start from 0
- Converted COCO annotations to Hugging Face format
- Excluded images without license plates
- Preserved COCO bounding box format `[x, y, width, height]`

---

## 🧠 Model Details

### License Plate Detection

- Model: **RT-DETR v2**
- Architecture: Transformer-based object detector
- Training: Fine-tuned on custom dataset
- Number of classes: 1 (`license_plate`)
- Objective: High recall and accurate localization for OCR readiness

### License Plate Recognition (OCR)

- Applied only during inference
- Lightweight OCR models (EasyOCR)
- OCR module is replaceable and not coupled with detector training

---

## 📈 Evaluation Results

The detection model was evaluated on a **held-out test split** using standard object detection metrics.

| Metric | Value |
|------|-------|
| mAP@0.5 | **0.97** |
| Recall (MAR@100) | **0.98** |
| mAP (Small Objects) | 0.88 |
| mAP (Medium Objects) | 0.99 |
| mAP (Large Objects) | 1.00 |

### Metric Choice Rationale
- mAP@0.5 aligns well with ALPR use cases where OCR requires reasonably tight localization.
- High recall ensures license plates are rarely missed.

---

## 🖼️ Inference Pipeline

During inference, the system:

1. Detects license plates in the input image
2. Crops detected plate regions
3. Applies OCR to extract license numbers
4. Overlays bounding boxes and recognized text

This enables both **quantitative evaluation** and **qualitative inspection**.

---

## ⚙️ Installation

```python
pip install torch transformers datasets pillow torchmetrics matplotlib
```

---

## 🧪 Usage

Recommended execution order:

1. `license_plate_detection_dataset.ipynb`
2. `license_plate_detection_train.ipynb`
3. `license_plate_detection_eval.ipynb`
4. `license_plate_recognition_inference.ipynb`

Each notebook is self-contained and documented.

---

## 🧩 Design Decisions

- Detection and OCR are decoupled for modularity
- RT-DETR v2 chosen for real-time performance and transformer-based design
- Evaluation prioritizes recall to support OCR downstream
- Dataset engineering emphasizes clarity and reproducibility

---

## ⚠️ Limitations

- OCR accuracy depends on crop quality
- Dataset is single-class and biased toward license plate–containing images
- Night-time or low-resolution plates may require OCR fine-tuning

---

## 🔮 Future Work

- Benchmark multiple OCR models
- Add video stream inference
- Fine-tune OCR for region-specific plates
- Measure end-to-end FPS
---

## 📜 License

This project uses datasets licensed under **CC BY 4.0**.
Proper attribution must be maintained when using or redistributing the data.

---

## ✨ Author

Built as a portfolio-grade project focusing on **real-world system design**, **evaluation-driven development**, and **applied computer vision engineering**.
>>>>>>> 02886a6 (README.md)
