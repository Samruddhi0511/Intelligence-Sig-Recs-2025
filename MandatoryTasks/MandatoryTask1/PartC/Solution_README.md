# Extractive Question Answering

**Task Link**: https://drive.google.com/drive/folders/1J5tZUSW3pWMBqXEEetbpZmswlN2oM0nP?usp=sharing

##  Dataset
I faced some loading issues with NewsQA dataset hence used SQUAD.Since **SQuAD** is a very large dataset and required nearly **10+ hours of training**, I trained the models on a **subset** of the dataset for faster experimentation.  
Each example in SQuAD contains:
- **Context**: a paragraph of text
- **Question**: a query about the context
- **Answer**: a text span within the context

---

##  Models Explored
I experimented with the following **transformer-based architectures**:

| Model | Architecture | Key Features |
|:------|:--------------|:--------------|
| **BERT (bert-base-uncased)** | Bidirectional Encoder Representations from Transformers | Reads text in both directions (left → right and right → left), enabling contextual understanding of words. |
| **RoBERTa (roberta-base)** | Robustly Optimized BERT | An improved version of BERT with more training data, longer sequences, and removal of the Next Sentence Prediction objective. |
| **DeBERTa (microsoft/deberta-v3-base)** | Decoding-enhanced BERT with Disentangled Attention | Separates word content and position embeddings, improving contextual disambiguation. |
| **Longformer (allenai/longformer-base-4096)** | Long-document Transformer | Uses **sliding window + global attention** to handle long contexts efficiently (up to 4096 tokens). |

---

##  Working Principle
Each of these models was fine-tuned for **extractive QA**, meaning the model learns to identify the **start** and **end token positions** of the answer within the context.

**Pipeline:**
1. **Input**: Question + Context → Tokenized together with special `[CLS]` and `[SEP]` tokens.
2. **Encoder**: Model learns contextual embeddings for all tokens.
3. **Output Heads**: Two linear layers predict:
   - `start_logits` → index of the start of the answer  
   - `end_logits` → index of the end of the answer
4. **Loss**: Cross-entropy between predicted and true start/end positions.

---

##  Evaluation Metrics
The following metrics were used to evaluate model performance:

- **Exact Match (EM)** → Percentage of predictions that exactly match the ground-truth answer.
- **F1 Score** → Measures token-level overlap between predicted and true answers.

| Model | Exact Match (EM) | F1 Score |
|:------|:----------------:|:--------:|
| **BERT** | 66.50 | 72.48 |
| **RoBERTa** | 81.50 | 86.30 |
| **DeBERTa-v3** | 84.00 | 86.18 |
| **Longformer** | 77.00 | 83.30 |

**Deberta performed the best hence used that for the finale task**

---

## Challenges Faced
- **Training Time**: Full SQuAD training required extensive GPU memory and long runtime (~10 hours+).
- **Memory Bottleneck**: Long context examples required gradient checkpointing or smaller batch sizes.
- **Subset Bias**: Using a subset caused the model to generalize less effectively compared to full-scale training.

---

##  Observations
- **DeBERTa-v3** performed the best, likely due to its **disentangled attention** mechanism.
- **RoBERTa** was faster and more stable during training.
- **Longformer** was efficient for long passages but slower per batch due to windowed attention.
- **BERT** remains a solid baseline but struggled with longer contexts.

---
