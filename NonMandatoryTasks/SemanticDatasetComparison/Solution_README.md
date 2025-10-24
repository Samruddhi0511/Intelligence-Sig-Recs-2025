# Semantic Dataset Comparison

**Task Link**: https://drive.google.com/drive/folders/1R0RJPRF9J0iTfJ4fhyrGi-Y1u9iwxFA2?usp=sharing

## Overview
The goal of this project is to compute **semantic similarity** scores between two image datasets. Unlike pixel-level similarity, semantic similarity measures whether two images share the same **meaning or content**, even if their appearance differs (e.g., a cat in different poses or colors).  

Ive used **transformer-based models**, particularly **CLIP**, to extract high-dimensional embeddings that capture the semantic content of images. Cosine similarity between these embeddings is then used to quantify the similarity between datasets.

---


Traditional image comparison methods (like pixel-wise differences) fail to capture semantic meaning. For example:
- Two images of a cat in different poses are visually different but semantically similar.  
- Semantic similarity aims to capture the "meaning" rather than exact pixel values.  

Transformers, especially **Vision Transformers (ViT)**, are ideal for this task because they:
- Capture long-range dependencies via attention.
- Learn rich, high-level features representing objects, scenes, and context.

---

## Reference Papers
1. **CLIP (Contrastive Language-Image Pretraining)** – [Paper Link](https://arxiv.org/abs/2103.00020)  
   - Dual-encoder architecture: image encoder + text encoder.  
   - Maps images and texts into a shared embedding space using contrastive learning.  
   - Enables semantic comparison between images or between images and text.  

2. **DINOv2** – [Paper Link](https://arxiv.org/abs/2304.07193)  
   - Self-supervised ViT model for learning image representations from unlabeled data.  
   - Highly transferable features for tasks like classification, segmentation, and more.

---

## Methodology

### 1. Pipeline
1. **Load datasets** (CIFAR-10 and CIFAKE).  
2. **Preprocess images** using CLIP's preprocessing pipeline.  
3. **Extract embeddings** for each image using the CLIP image encoder.  
4. **Compute cosine similarity** between embeddings of two datasets.  
5. **Visualize embedding overlap** using t-SNE to understand semantic proximity.

### 2. Tools & Libraries
- PyTorch & Torchvision  
- CLIP (`ViT-B/32`)  
- NumPy, scikit-learn (cosine similarity), Matplotlib, t-SNE  

### 3. Stepwise Approach
- Extract embeddings for selected subsets of images.  
- Normalize embeddings.  
- Compute **mean cosine similarity** to quantify semantic similarity.  
- Visualize embeddings in 2D with **t-SNE** to show clusters and overlaps.

---

## Experiments

### Experiment 1: CIFAR-10 Classes
Semantic similarity was computed between different classes:

| Class Pair       | Mean Semantic Similarity |
|-----------------|---------------------------|
| Cat & Dog        | 0.827                    |
| Airplane & Auto  | 0.728                    |
| Deer & Dog       | 0.78                     |
| Auto & Truck     | 0.77                     |
| Ship & Bird      | 0.73                     |

- Observations:  
  - Classes with semantically related objects (e.g., Auto & Truck) showed higher similarity.  
  - Dissimilar classes (e.g., Ship & Bird) had lower similarity scores.  
  - t-SNE plots confirmed embeddings of similar classes cluster closer in space.

### Experiment 2: CIFAKE (Real vs Generated Data)
- Applied the same embedding and cosine similarity pipeline to compare real vs generated images.  
- Observed how close the generated data is to the real distribution semantically.
- However, the dataset was consuming too much RAM and the session was collapsing, hence training not complete.

---


