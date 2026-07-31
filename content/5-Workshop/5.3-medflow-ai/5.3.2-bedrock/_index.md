---
title: "ViMQ NER Deep Dive: Architecture, Dataset & Training Algorithms"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

The core technical differentiator that elevates the **`medflow-ai`** module above conventional healthcare AI implementations is its proprietary **Named Entity Recognition (NER)** neural model, localized and optimized specifically for Vietnamese clinical narratives.

---

### 1. ViMQ High-Level Model Architecture

The ViMQ model adopts a **Span-based NER architecture combined with a Biaffine Classifier**, effectively recognizing compound medical terms, abbreviations, and nested clinical entities within Vietnamese text:

```text
[Input Clinical Narrative]
            │
            ├──(1) Subword Tokenization (PhoBERT Base Embeddings)
            │
            └──(2) Character Embedding (BiLSTM / Conv Layer)
                                │
                                ▼
                       [Word Representation Layer]
                                │
                                ▼
                     [3-Layer BiLSTM Contextual Net]
                                │
                   ┌────────────┴────────────┐
                   ▼                         ▼
         [feedStart (MLP Layer)]   [feedEnd (MLP Layer)]
                   │                         │
                   └────────────┬────────────┘
                                ▼
                   [Biaffine Classifier Layer]
                                │
                                ▼
                  [Boundary & Entity Prediction]
```

- **Deep Semantic Features**: The model leverages `vinai/phobert-base` as its core linguistic feature extractor, reinforced by character-level embeddings. This combination maintains high extraction accuracy even when patients utilize medical slang, abbreviations, foreign drug names, or typographical errors.
- **Sequential Context Learning**: A 3-layer Bidirectional LSTM (BiLSTM) captures complex syntactic relationships across forward and backward conversational turns in patient histories.
- **Entity Boundary Classification**: Dual MLP networks (`feedStart` and `feedEnd`) coupled with a Biaffine scoring matrix compute the precise probability distribution for the starting and ending boundaries of clinical entities.

---

### 2. Standardized Clinical Dataset Engineering

The ViMQ training dataset is structured under rigorous medical curation standards, partitioned into training (`train.json`), validation (`dev.json`), and test (`test.json`) sets:

- **Clinical Entity Classifications (`entity_set.txt`)**: 
  - `SYMPTOM_AND_DISEASE`: Patient-reported symptoms and underlying pathologies (e.g., *đau đầu*, *sốt cao*, *tiểu đường type 2*).
  - `DRUG`: Pharmacological compounds and active ingredients (e.g., *paracetamol*, *aspirin*, *insulin*).
  - `MEDICAL_PROCEDURE`: Diagnostic tests, medical imaging, and clinical examinations (e.g., *nội soi*, *chụp MRI*, *xét nghiệm máu*).
- **Character Vocabulary (`char2index.json`)**: A standardized character mapping table supporting robust processing of diverse real-world textual inputs.

---

### 3. Self-Training & Iterative Labeling Workflow

Departing from static supervised learning, ViMQ implements an **Iterative Bootstrapping & Self-Training** methodology to continuously expand its clinical vocabulary:

1. **Active Data Noising**:  
   During training, the system introduces controlled boundary perturbations on ground-truth entity spans. This prevents the neural network from memorizing rigid word boundaries, enhancing resilience against informal or grammatically unstructured patient expressions.

2. **Major Vote Pseudo-Labeling**:  
   To mitigate gaps in manual clinical annotation, the system executes automated prediction and consensus voting across training cycles. High-confidence entity predictions appearing consistently across epochs are automatically confirmed and appended back into the training set for subsequent cycles.

3. **Rigorous Benchmarking**:  
   Model performance is evaluated against standardized `IOB` metrics, verifying precision, recall, and comprehensive F1-score reliability.

{{% notice note %}}
**Extended Reference:** For deeper exploration of the source code implementation, Biaffine loss matrix formulations, and training hyperparameters, please consult the official repository: [ViMQ NER Official Repository](https://github.com/tadeephuy/vimq).
{{% /notice %}}

---
*Proceed to the next section: **[3. Dynamic Routing Architecture & Advanced RAG Engine](../5.3.3-routing-rag-engine/)**.*
