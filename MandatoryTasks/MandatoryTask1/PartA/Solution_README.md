#  Word Embeddings Comparison

**Task Link:** [Google Drive Folder](https://drive.google.com/drive/folders/1FlLZUye6GEAXfgCCyH9cuxs14lNG2bel?usp=sharing)  
**Dataset Used:** NewsQA Dataset  
**Goal:** To understand how different embedding techniques capture semantic meaning in text — moving from simple frequency-based methods to deep contextual representations.

---

##  Overview

In this task, I explored **five embedding methods** — starting with **Bag of Words (BoW)**, which captures no semantic meaning, and progressing to **Transformers**, which not only understand the meaning of individual words but also how they relate to every other word in the sentence.



---

## Methods Explored

###  Bag of Words (BoW)
**Concept:**  
Represents text as a frequency count of words, ignoring grammar , meaning and order.

**Example:**  
> “I love AI” → [I:1, love:1, AI:1]  
> “AI loves me” → [AI:1, loves:1, me:1]  

The model treats both sentences as completely different, despite their similar meaning.

**Advantages:**  
- Simple and easy to implement  
- Works well for basic text classification tasks  

**Disadvantages:**  
- Ignores word order  
- No understanding of semantics or context  
- Vocabulary size grows rapidly  

---

###  TF-IDF (Term Frequency – Inverse Document Frequency)
**Concept:**  
Weights words by how *important* they are in a document relative to the corpus.  
Words that appear frequently across all documents (like *the*, *is*, *and*) are downweighted.

**Advantages:**  
- Reduces the influence of common but uninformative words  
- Better than BoW for feature extraction  

**Disadvantages:**  
- Still ignores semantics  
- Cannot capture relationships between words  

---

### CBOW (Continuous Bag of Words)
**Concept:**  
Predicts a **target word** based on its **surrounding context words**.  
This is one of the two Word2Vec architectures introduced by Google.
From here on, **deep learning techniques** are used. The target word is predicted using neural networks and sigmoid fucntion over the vocabulary.

**Advantages:**  
- Learns distributed representations of words  
- Captures basic semantic similarity (e.g., *king – man + woman ≈ queen*)  

**Disadvantages:**  
- Loses sense of word order  
- Works poorly for rare words  

---

###  Skip-Gram
**Concept:**  
Opposite of CBOW — predicts **context words** given a **target word**.  
It performs better on small datasets and can learn representations for infrequent words.

**Advantages:**  
- Works better with smaller or imbalanced datasets  
- Learns meaningful relationships between words  

**Disadvantages:**  
- Training is computationally expensive  
- Sensitive to hyperparameters like window size and negative sampling  

---

### Transformers (BERT)
**Concept:**  
Uses **self-attention** to learn contextual embeddings — every word’s meaning is influenced by all the other words in the sentence.  
Unlike sequential RNNs, Transformers process text **in parallel**, making them faster and more powerful.

**Advantages:**  
- Understands context and semantics deeply  
- Works well for transfer learning  
- Captures both syntax and meaning  

**Disadvantages:**  
- Requires large datasets and compute power  
- More complex to fine-tune  

---

## Challenges Faced

- **Word2Vec Training Time:**  
  Training **CBOW** and **Skip-Gram** took a lot of time because:
  - They learn word embeddings from scratch.
  - Every word pair within a context window contributes to training.
  - Skip-Gram especially updates parameters for many context words per target word.

  This makes them **computationally heavy**, especially on large corpora like NewsQA.

- **Transformer Fine-tuning:**  
  Handling large transformer models required GPU support; fine-tuning and embedding extraction were memory-intensive.





---

Each method has its use-case — but for modern NLP, **transformer-based embeddings** provide the richest and most context-aware representations.

---

