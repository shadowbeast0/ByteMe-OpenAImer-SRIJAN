# ByteMe-OpenAImer-SRIJAN

The given Repository consists of the outputs and the link to the notebooks of Track-1 and Track-2 prelims round of OpenAImer SRIJAN
- **Track-1:** Supervised Contrastive Learning  
- **Track-2:** ResNet18 Model Compression  

---

## 📌 Table of Contents
- [Team Information](#team-information)
- [Overview](#overview)
- [Track-1: Supervised Contrastive Learning](#track-1-supervised-contrastive-learning)
- [Track-2: ResNet18 Compression](#track-2-resnet18-compression)
- [Results](#results)

---

## 👥 Team Information
**Team:** ByteMe  
**Affiliation:** BCSE UG’27, Jadavpur University  
**Members:**  
- Arjeesh Palai  
- Arko Dasgupta  
- Sombrata Biswas  
- Abhirup Pal  

---

## 🔍 Overview
This repository summarizes our approach and results for **OpenAImer SRIJAN Prelims**.

- **Track-1:** Implemented a two-stage pipeline using **DenseNet201** with **Supervised Contrastive (SupCon) Learning** followed by linear evaluation.  
- **Track-2:** Performed **post-training pruning and slimming** on **ResNet18** for model compression.

---

## 📂 Track-1: Supervised Contrastive Learning

### ✅ Pipeline
1. **SupCon Pre-training**  
   - Encoder: DenseNet201  
   - Projection Head: MLP  
   - Loss: Supervised Contrastive Loss (temperature τ)  
2. **Linear Evaluation**  
   - Freeze encoder  
   - Train softmax classifier with cross-entropy  

### ✅ Performance
- **F1:** 0.9948  
- **Accuracy:** 0.9936  
- **Precision:** 0.9944  
- **Recall:** 0.9952  

### ✅ Visualization
- t-SNE plots show **well-separated class clusters** after SupCon pre-training.

### ✅ Other Backbones Tried
- ResNet50, InceptionV3, InceptionResNetV2, DenseNet169.

---

## 📂 Track-2: ResNet18 Compression

### ✅ Method
- **Pruning:** L1 unstructured weighted pruning (lottery-ticket style)  
- **Slimming:** Removed Residual Layers 2–4 and Block 2 of Layer 1  

### ✅ Metrics
- Disk Size: **~0.38 MB**  
- Latency: **8.63 ms**  
- Validation Accuracy: **52.8%**

---

## 📊 Results

| Track  | Model        | F1     | Accuracy | Precision | Recall | Disk Size | Latency  | Val Acc |
|--------|-------------|--------|----------|-----------|--------|-----------|----------|---------|
| Track-1| DenseNet201 | 0.9948 | 0.9936   | 0.9944    | 0.9952 | —         | —        | —       |
| Track-2| ResNet18    | —      | —        | —         | —      | 0.38 MB   | 8.63 ms  | 52.8%   |

---
