---
title: "Dynamic Routing Architecture & Advanced RAG Engine"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

The integration of clinical entities extracted by the local ViMQ NER model with a managed Cloud RAG engine hosted on AWS Bedrock establishes an ultra-precise processing workflow, maximizing diagnostic accuracy and patient medical safety.

---

### 1. Intent Classification & Dynamic Multi-Prompt Routing (`Intelligent Router & RunnableBranch`)

Rather than forcing all queries through a generic monolithic prompt, the system implements dynamic contextual routing leveraging LangChain's `RunnableBranch`:

- **LLM Router (`router_prompt`)**: Utilizes a high-speed LLM (GPT-4o-mini) to evaluate the patient's raw input prompt combined with the clinical entities extracted by ViMQ NER. The router classifies the interaction into one of **6 specialized clinical intents**: `BOOKING`, `TREATMENT`, `CAUSE`, `SEVERITY`, `DIAGNOSIS`, and `OTHER`.
- **Dynamic Branching (`RunnableBranch`)**: Based on the intent classification, the RAG retrieval pipeline directs the query into the corresponding specialized prompt architecture defined in `prompt.py`:
  - **`BOOKING Prompt`**: Guides patients through the 5-step appointment reservation process on the MedFlow platform (providing the direct link `#expert`). Crucially, the AI informs the patient that an automated **AI Triage Report** summarizing their reported symptoms and clinical vitals will be attached directly to their reservation for the attending physician to review prior to the consultation!
  - **`TREATMENT Prompt`**: Supplies initial home-care recommendations and safe first-aid protocols. Explicitly mandates **recommending the exact optimal hospital specialty** from MedFlow Hospital's official clinical departments (Internal Medicine, Surgery, Pediatrics, Obstetrics/Gynecology, Dermatology, ENT, Ophthalmology, Odonto-Stomatology, 24/7 Emergency).
  - **`CAUSE Prompt`**: Explains the scientific pathophysiology underlying symptoms or pharmacological adverse effects, offering preventative medical advice and clinical consultation guidance.
  - **`SEVERITY Prompt`**: Enumerates critical **Red-Flag Warnings** requiring immediate emergency room intervention, clearly delineating conditions suitable for home monitoring versus urgent ambulance dispatch.
  - **`DIAGNOSIS Prompt`**: Interprets clinical laboratory metrics and symptoms while strictly enforcing a **Medical Disclaimer**, emphasizing that the AI operates solely as a Clinical Decision Support System (CDSS) and directing the patient to schedule a formal consultation.
  - **`OTHER Prompt`**: Manages general conversational interactions with empathetic, professional healthcare communication.

---

### 2. Cloud-Native Managed RAG Engine (AWS Bedrock KB + Cohere Rerank)

The `medflow-ai` module operates on a managed cloud architecture hosted on Amazon Web Services to maximize system scalability and reliability:

```text
[Văn bản CSV/PDF tại data/] 
       │ (src/upload_to_s3_bedrock.py)
       ▼
[Amazon S3 Bucket: medical-data/] ──(StartIngestionJob)──> [AWS Bedrock KB (Managed Vector Index)]
                                                                    │
                                                           (AmazonKnowledgeBasesRetriever)
                                                                    ▼
[Top 3 Passage Cô đọng] <──(ContextualCompressionRetriever / Cohere Rerank v3.0)<── [Top K=5 Raw Docs]
```

- **Amazon S3 & Bedrock Knowledge Bases Synchronization**: Standardized clinical protocol guidelines (.csv, .pdf) stored in the `data/` directory are uploaded to Amazon S3 via `src/upload_to_s3_bedrock.py`. This script invokes the AWS Bedrock `StartIngestionJob` API, automating text chunking and managed vector index generation.
- **Two-Stage Hybrid Retrieval & Compression Pipeline**:
  - **Stage 1 (Contextualization & Coarse Retrieval)**: A `Contextualize Query Generator` transforms multi-turn conversational history into a standalone, grammatically complete Vietnamese query. The `AmazonKnowledgeBasesRetriever` then queries the Bedrock Knowledge Base to retrieve the Top $k=5$ most relevant raw clinical documents via cosine similarity.
  - **Stage 2 (Precision Reranking & Compression)**: The $k=5$ raw documents are passed through a `ContextualCompressionRetriever` powered by the **Cohere Rerank (`rerank-multilingual-v3.0`)** neural model. Cohere evaluates deep multilingual semantic relevance, retaining only the **Top 3 most authoritative clinical passages**. This completely eliminates noise and optimizes token expenditure before generation.

---
*Proceed to the next section: **[4. Context Management, gRPC Streaming & Observability](../5.3.4-memory-streaming-observability/)**.*
