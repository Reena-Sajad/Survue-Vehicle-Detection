# 🚴‍♂️ Survue Object Detection System

## Project Overview

This project was developed for **Survue**, a startup focused on building smart bike-light systems to enhance rider safety through real-time situational awareness.  
The goal was to design and benchmark an efficient deep learning model capable of detecting three key hazards:

- **Humans**
- **Vehicles**
- **Traffic Signs**

Because the final model will run on **low-power, bike-mounted hardware**, it needed to be:

- **Lightweight** (small file size)  
- **Accurate**  
- **Fast** (low inference latency)

---

## Key Deliverables

- **Optimal Architecture Selection**  
  Compared YOLOv5 vs. YOLOv8 (two major object detection families).

- **Performance Validation**  
  Benchmarked models on:
  - speed (ms)
  - accuracy (mAP)
  - size (MB)

- **Final Recommendation**  
  Selected a deployment-ready candidate: **YOLOv8m**

---

## Methodology and Models

### Dataset Analysis

The system was trained on **500 high-resolution images** containing **9,787 annotations**.

Key challenges identified:

- **Class Imbalance:**  
  Vehicle class dominated; Traffic Signs were the smallest class.

- **Small Object Problem:**  
  Median object size was **34×34 px**, requiring strong small-object detection capability.

---

### Models Trained

Four models across two YOLO families were evaluated:

| Model     | Parameters (M) | Size (MB) | Description |
|-----------|----------------|-----------|-------------|
| **YOLOv5m** | 20.9M         | 42.1 MB   | Strong baseline, anchor-based |
| **YOLOv8m** | 25.8M         | 52.0 MB   | New anchor-free architecture |
| **YOLOv5s** | 7.0M          | 14.4 MB   | Small, lightweight baseline |
| **YOLOv8s** | 11.1M         | 22.5 MB   | Small anchor-free variant |

---

### Training Configuration

All models were trained under identical conditions for fairness:

- **Image Size:** 640 × 640  
- **Epochs:** 50  
- **Optimizer:** SGD  
- **Hardware:** JupyterLab runtime with 4 CPUs, 12GB RAM  

---

## Results and Recommendation

Benchmarking confirmed that the **YOLOv8 architecture outperformed YOLOv5** for Survue’s real-time safety use case.

### Final Model Comparison

| Model     | mAP@50 (Accuracy) | Inference Speed | Size |
|-----------|-------------------|------------------|------|
| **YOLOv5m** | 62.5%             | ~15 ms           | 42.1 MB |
| **YOLOv8m** | **63.2%**         | **7.0 ms**       | 52.0 MB |

### Key Findings

- **Fastest Model:**  
  YOLOv8m achieved **7 ms inference** (~142 FPS), ideal for real-time alerts.

- **Best Accuracy:**  
  YOLOv8m delivered the **highest accuracy**, especially in mAP@50-95 (39.9%).

- **Traffic Sign Performance:**  
  Traffic Signs remained the hardest class (~54% mAP), consistent with small object sizes in the dataset.

### **Official Recommendation: YOLOv8m**

YOLOv8m provides the best combination of:

- High accuracy  
- Extremely fast inference  
- Strong performance on small objects  

Making it the ideal deployment candidate.

---

## Future Work & Deployment Strategy

### **1. Model Quantization (Lightweight Goal)**
Reduce the **52 MB** model to **15–20 MB** through post-training quantization to meet firmware limits.

### **2. Dataset Augmentation (Accuracy Goal)**
Increase diversity of Traffic Signs by adding:

- External open-source driving datasets  
- Additional proprietary data  

### **3. Hardware Validation (Speed Goal)**
Verify the **7 ms latency** on Survue’s embedded hardware (not just GPU-based testing).

---

## ⚙️ Reproduction

All EDA, model training code, and visualizations are included in:

