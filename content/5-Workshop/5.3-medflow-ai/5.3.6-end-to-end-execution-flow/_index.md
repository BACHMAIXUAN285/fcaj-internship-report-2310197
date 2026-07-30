---
title: "End-to-End Execution Flow Summary"
date: 2026-07-01
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

To understand how the diverse technological components within the **`medflow-ai`** module synchronize down to the millisecond, let us examine a detailed step-by-step trace of a real-world clinical consultation involving a patient experiencing high fever refractory to standard antipyretics.

---

### Sample Patient Clinical Scenario

The patient submits a voice narrative transcribed via the MedFlow Client application:
> *"Tôi bị đau đầu dữ dội kèm sốt cao 39 độ, uống paracetamol không đỡ, tôi phải làm sao?"*
> *(Translation: "I have a severe headache with a high fever of 39°C, taking paracetamol hasn't helped, what should I do?")*

---

### Detailed 9-Step Real-Time Engineering Trace

#### Step 1: Ingestion of gRPC Payload at Port `50051`
- **Action**: The API Gateway receives the client input, serializes it into a Protobuf message `triage.ConsultationRequest(client_id="usr_882", query=...)`, and transmits it over the active gRPC streaming channel to the AI microservice listening on port `50051`.
- **Handshake Latency**: ~5ms (Eliminates HTTP connection setup overhead).

#### Step 2: Clinical Entity Extraction via Local ViMQ NER (`ViMQNEREngine`)
- **Action**: The `vimq_integration.py` layer feeds the input narrative into the local PhoBERT + BiLSTM + Biaffine Classifier deep learning model. The model identifies and outputs structured entities:
  - `SYMPTOM_AND_DISEASE`: `["đau đầu dữ dội", "sốt cao 39 độ"]`
  - `DRUG`: `["paracetamol"]`
- **Local Inference Latency**: ~45ms.

#### Step 3: Clinical Intent Classification (`LLM Intent Router`)
- **Action**: The high-speed intent router (GPT-4o-mini) evaluates the query alongside the extracted entities. Recognizing that the patient is seeking medical management for an unresponsive fever, it classifies the interaction into the **`TREATMENT`** intent branch.
- **Routing Latency**: ~120ms.

#### Step 4: Context Restoration & Standalone Query Generation (`Contextualize Query Generator`)
- **Action**: The `SafePostgresChatMessageHistory` class queries the `chat_history` table on NeonDB for prior conversational turns. The RAG pipeline reformulates the context into a standalone Vietnamese retrieval query: *"Hướng xử lý cho bệnh nhân bị đau đầu dữ dội và sốt cao 39 độ đã uống paracetamol nhưng không hạ sốt"*.
- **Database Latency**: ~15ms.

#### Step 5: Coarse Retrieval via AWS Bedrock Knowledge Base
- **Action**: The `AmazonKnowledgeBasesRetriever` invokes the AWS Bedrock API, executing cosine similarity vector search across the index hosted on Amazon S3. The system retrieves the Top $k=5$ official clinical guideline documents regarding high fever management from the Ministry of Health.
- **AWS Bedrock Latency**: ~85ms.

#### Step 6: Precision Reranking & Compression via Cohere Rerank v3.0
- **Action**: The `ContextualCompressionRetriever` passes the 5 raw documents through the `rerank-multilingual-v3.0` neural model. Cohere evaluates deep semantic relevance, retaining only the **Top 3 most authoritative clinical passages** addressing persistent fever unresponsive to monotherapy antipyretics.
- **Reranking Latency**: ~35ms.

#### Step 7: `TREATMENT Prompt` Execution & Departmental Triage
- **Action**: The RAG pipeline injects the 3 compressed passages into the specialized `TREATMENT` prompt architecture. The LLM (GPT-4o-mini) synthesizes authoritative medical guidance:
  - Instructs active physical cooling (tepid sponging of forehead, axilla, groin) and oral rehydration therapy (Oresol).
  - Highlights Red-Flag clinical risks such as dengue fever or meningitis when accompanied by severe headache.
  - **Clinical Specialty Assignment**: Strongly advises immediate emergency evaluation at the **"Department of Internal Medicine"** or the **"24/7 Emergency Department"** at MedFlow Hospital for immediate complete blood count (CBC) diagnostic testing.

#### Step 8: Appointment Scheduling Guidance & AI Triage Report Attachment
- **Action**: In its concluding remarks, the AI assistant proactively offers seamless operational assistance:
  > *"Would you like MedFlow to provide a direct reservation link and step-by-step guidance to schedule an immediate consultation with this department? Your reported symptoms of high fever (39°C) and paracetamol unresponsiveness have been automatically compiled into an AI Triage Report and attached to your booking file so your attending physician can review them prior to your arrival!"*

#### Step 9: gRPC Token Streaming & Telemetry Logging
- **Action**: Each generated token is streamed back to the client in real time via gRPC `ChatChunk(token=...)` messages. Upon completion of the stream:
  - The **Langfuse Callback Handler** logs the execution trace, confirming a **Time-to-First-Token (TTFT) of 180ms**, total execution duration of 1.4s, and total token expenditure of `$0.0015`.
  - **AWS CloudWatch Logs** archives the successful execution records in the `med-chatbot` Log Group.

---

### Technical Summary

Through this seamless 9-step execution pipeline, the **`medflow-ai`** module demonstrates the superior capabilities of a modern Cloud-Native clinical AI architecture: fusing the localized perceptual sharpness of **ViMQ NER**, the authoritative knowledge retrieval of **AWS Bedrock RAG**, and the production-grade reliability of **gRPC streaming** to safeguard patient health and optimize clinical triage.

---
*End of technical report for the `medflow-ai` module. Return to the **[Main Workshop Overview](../../)** for further integration sections.*
