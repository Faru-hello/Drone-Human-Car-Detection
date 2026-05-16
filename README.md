# Drone Human Detection & Counting System

Technical Assessment for ANTS Internship Program (AI/ML)

## Project Overview

This project implements a computer vision pipeline for drone/aerial imagery using the VisDrone dataset. The system detects humans and cars, counts total humans, and visualizes predictions with bounding boxes.

### Objectives
- Detect humans and cars
- Count total humans
- Visualize prediction outputs
- Evaluate model performance

---

## Dataset

Dataset Used: **VisDrone Dataset**

The dataset contains aerial/drone images with object annotations.

Dataset structure:

```text
VisDrone2019-DET-train
│── images
│── labels

VisDrone2019-DET-val
│── images
│── labels

VisDrone2019-DET-test-dev
│── images
```

YOLO annotation format:

```text
class_id x_center y_center width height
```

---

## Preprocessing

Since the original dataset contains multiple object classes, only task-relevant classes were selected:

| Original Class | New Class |
|----------------|------------|
| Person | 0 |
| People | 1 |
| Car | 2 |

Class remapping was performed because YOLO requires class indices starting from **0**.

### Challenges in Dataset
- Small human objects in aerial views
- Crowd detection difficulty
- Occlusion between objects
- Dense scenes

---

## Model Used

**YOLOv8n (Fine-tuned)**

Reason for selection:
- Lightweight architecture
- Faster training
- Efficient inference speed
- Good performance for object detection

Transfer learning was used with pretrained YOLOv8 weights.

---

## Training Configuration

| Parameter | Value |
|-----------|------|
| Epochs | 30 |
| Image Size | 640 |
| Batch Size | 16 |
| Framework | Ultralytics YOLOv8 |

---

## Human & Car Detection

The system:

✅ Detects humans  
✅ Detects cars  
✅ Draws bounding boxes  
✅ Counts total humans

Human count logic:
- `person` class counted as human
- `people` class counted as human group

---

## Evaluation

Evaluation metrics used:

- Precision
- Recall
- mAP50
- mAP50-95

The model performance was analyzed using:
- Confusion Matrix
- Prediction visualizations
- Training curves

---

## Sample Outputs

(Add your prediction screenshots here)

(Add confusion matrix image here)

(Add results graph here)

---

## Strengths
- Fast inference speed
- Lightweight model
- Effective car detection
- Simple human counting system

## Limitations
- Small humans are difficult to detect
- Crowd counting may be less accurate
- Drone angle causes object scale issues

## Future Improvements
- Object tracking using ByteTrack / DeepSORT
- Hyperparameter tuning
- Real-time drone deployment

---

## Requirements

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Project Structure

```text
Drone-Human-Car-Detection-VisDrone
│── README.md
│── Drone_Human_Detection.ipynb
│── requirements.txt
│
├── outputs
│   ├── prediction_1.jpg
│   ├── prediction_2.jpg
│   ├── confusion_matrix.png
│   ├── results.png
│
├── model
│   └── best.pt
```
