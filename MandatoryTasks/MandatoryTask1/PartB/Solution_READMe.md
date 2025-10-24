#  Machine Translation

**Task Link**: https://drive.google.com/drive/folders/1N-EQhR-wpO7xcfcrLrhBeyOCX9Syod5Z?usp=drive_link

**Dataset:**  
- [OPUS Books Dataset (English–French)](https://opus.nlpl.eu/Books.php)  
- [WMT14 (German–English)](https://huggingface.co/datasets/wmt14)  
- [IIT Bombay (Hindi–English)](https://huggingface.co/datasets/iitb)  

---

## Overview

This task focuses on **Machine Translation**, i.e., converting text from one language to another using various deep learning models — from basic sequence-to-sequence (Seq2Seq) architectures to modern transformer-based multilingual models.  

I experimented with **four different approaches**, each representing a different level of complexity and capability:

1. **LSTM + Attention (Trained from Scratch)**  
2. **mT5 (Multilingual T5)**  
3. **mBART (Multilingual BART)**  
4. **Helsinki OPUS Translation Models**

---

## LSTM with Attention — From Scratch

**Dataset:** OPUS Books (English–French)  
**Epochs:** 2  
**Reason:** Limited compute (training took 6+ hours even for a small subset)


- Implemented a **sequence-to-sequence neural network** using two LSTMs — one as the **encoder** and the other as the **decoder**.
- Added a **Bahdanau-style attention mechanism** to help the decoder focus on relevant parts of the input sequence while generating each word.

###  Architecture
- **Encoder:** Bi-directional LSTM → returns hidden + cell states  
- **Attention Layer:** Computes alignment scores between decoder hidden state and encoder outputs  
- **Decoder:** LSTM that uses attention context vector + word embedding to predict next token  

###  Results
- Due to a **very small dataset** and **only 2 epochs**, translations were mostly incomplete or grammatically incorrect.  
- The model did learn basic word alignments like *“I” → “Je”*, *“book” → “livre”* etc.  
- Could not complete full dataset training — limited **RAM and GPU memory** were the bottlenecks.

>  With more compute (and epochs), this architecture can achieve decent translation performance, but transformers have largely replaced it due to efficiency and better context handling.

---

##  mT5 (Multilingual T5)

**Dataset:** WMT14 (German–English)  
**Model:** `google/mt5-small`

###  What Happens in mT5
mT5 is a **multilingual version of the Text-to-Text Transfer Transformer (T5)**.  
It treats **every NLP task** — including translation — as a text-to-text problem.

- Input: `"translate German to English: <German sentence>"`
- Output: `<English sentence>`

mT5 is trained on **mC4**, a massive multilingual corpus covering 100+ languages, enabling strong cross-lingual generalization.

###  Issue Faced
Training loss stayed constant at **0.00** since the beginning.  
This can happen due to:
- Incorrect label alignment or tokenizer mismatch  
- Mixed precision training overflow (FP16 underflow)  


Because of this, the model didn’t learn — the outputs were almost random.  
Proper preprocessing and careful learning rate scheduling could fix this.

---

##  Fine-tuning mBART — Multilingual BART

**Dataset:** IIT Bombay Hindi–English  
**Model:** `facebook/mbart-large-50-many-to-many-mmt`

###  Architecture Overview
mBART extends the **BART denoising autoencoder** to multiple languages.  
It has:
- **Shared Encoder-Decoder Transformer architecture**
- **Language embeddings** to signal the input and target language
- Trained on 50+ languages using the **CC25** dataset

###  How It Works
1. Input sentences are **noised** (masked or shuffled).  
2. The model learns to reconstruct the **original sentence**.  
3. During fine-tuning, the same encoder-decoder setup is used for **translation**, conditioned on the target language ID.

###  Results
- Translations were **grammatically correct and contextually accurate**.  
- Even with limited fine-tuning, **mBART generalized well** due to pretraining on many language pairs.  
- For Hindi–English, the model produced fluent outputs and respected word order well.

---

## Fine tuning Helsinki-NLP OPUS Models

**Models Used:**  
- `Helsinki-NLP/opus-mt-en-fr`  
  

These are pre-trained transformer-based translation models from the **OPUS project**, built on the **Marian NMT** framework.

### How They Work
- Encoder-decoder transformer trained with parallel corpora (like OPUS, Europarl, etc.)  
- Tokenization via SentencePiece  


###  Results
- Worked reliably with fine-tuning.  
- Produced clean, fluent translations.  
- Training + inference were extremely lightweight compared to LSTM or mT5.



---

##  Conclusion

Each architecture revealed a different aspect of how translation models evolve:

- **LSTMs** can learn language structure, but scaling them is computationally expensive.  
- **mT5** shows the power of unified text-to-text learning, but requires careful preprocessing.  
- **mBART** demonstrates strong multilingual transfer — it works impressively even on unseen pairs.  
- **Helsinki OPUS models** are practical, efficient, and perform well out-of-the-box for real use cases.



---

