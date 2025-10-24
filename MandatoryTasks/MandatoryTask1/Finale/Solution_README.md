#  English → French Question Answering System

**Task Link**: https://drive.google.com/drive/folders/1LIvIvvhZC4-7D76-ayM1YT7tX0GYx-L6?usp=drive_link

**English-to-French QA system** that takes a context paragraph in English, allows the user to ask a question, and provides the answer in French. The system combines **extractive QA** and **machine translation** in a seamless pipeline.

---

##  Overview
implements a **multilingual QA pipeline**:

1. **Extractive QA in English** using DeBERTa.  
2. **Translate the extracted answer** to French using Helsinki-NLP's OPUS-MT model.

Users can ask questions in English about any context paragraph and receive accurate answers in French. The pipeline is designed for efficiency and high-quality responses.

---

##  How It Works

### **Step 1: Extractive Question Answering (English)**
- **Model:** `DeBERTa` (Decoding-enhanced BERT)  
- **Purpose:** Finds the exact answer to a question from an English context.  
- **DeBERTa**
  - High accuracy on extractive QA tasks  
  - Less compute than larger transformer models  
  - Predicts answer spans (start & end tokens) directly from context  

**Process:**
1. User inputs a **context paragraph** in English.  
2. User asks a **question** about that context.  
3. DeBERTa tokenizes the context + question, computes attention, and predicts the **start and end positions** of the answer.  
4. The system outputs the **answer in English**.

> **Example:**  
> **Context:** "Harry Potter was a wizard who lived at 4 Privet Drive with his aunt and uncle."  
> **Question:** "Where did Harry Potter live?"  
> **Answer (EN):** "4 Privet Drive"

---

### **Step 2: Machine Translation (English → French)**
- **Model:** `Helsinki-NLP/opus-mt-en-fr` (fine-tuned on OPUS Books)  
- **Purpose:** Translate the extracted English answer into French.  
- **Helsinki M?**
  - Lightweight and efficient transformer-based translation  
  - Fine-tuned on literary English → French data (OPUS Books), improving quality  
  - Perfect for translating short QA answers  

**Process:**
1. Take the **English answer** from DeBERTa.  
2. Feed it into the **Helsinki MT model**.  
3. The model outputs the **answer in French**.

> **Example:**  
> **English Answer:** "4 Privet Drive"  
> **French Answer:** "4, allée Privet"

---

##  Pipeline Overview
Context (EN) + Question (EN)
            ---
            >
DeBERTa QA Model
            ---
            >
Answer (EN)
            ---
            >
Helsinki MT Model EN→FR
            ---
            >
Answer (FR)


---

##  Features
- Interactive English QA with French translation  
- Efficient transformer models for low compute  
- End-to-end pipeline without manual intervention  
- Supports literary and general English contexts  

---
