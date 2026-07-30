---
title: "Module medflow-ai: Cloud-Native RAG, ViMQ NER & Clinical Triage"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

The **`medflow-ai`** module serves as the core clinical artificial intelligence brain of the **MedFlow** healthcare ecosystem. The system represents a convergence of a **Localized Vietnamese Medical Deep Learning Model (ViMQ)**, a **Cloud-Native Managed RAG Platform (AWS Bedrock Knowledge Bases)**, **Dynamic Multi-Prompt Routing**, and ultra-low-latency **gRPC Streaming** microservices.

Below is the comprehensive technical report detailing the architecture, ViMQ neural model design, training dataset engineering, cloud RAG retrieval pipelines, and unique selling points of the `medflow-ai` module:

---

### Technical Submodules in This Report:

1. **[Architecture Overview](5.3.1-architecture-overview/)**  
   Exploring the standalone gRPC microservice architecture (port `50051`), its role as an AI Medical Triage & Clinical Decision Support System (CDSS), and the end-to-end data flow from client gateways to Cloud RAG engines.

2. **[ViMQ NER Deep Dive: Architecture, Dataset & Training Algorithms](5.3.2-vimq-ner-deep-dive/)**  
   A high-level technical report on the PhoBERT-based Span NER architecture with Biaffine Classifiers tailored for Vietnamese healthcare, standardized clinical datasets, and self-training iterative labeling workflows.

3. **[Dynamic Routing Architecture & Advanced RAG Engine](5.3.3-routing-rag-engine/)**  
   Intelligent intent classification via `RunnableBranch` routing into 6 specialized clinical prompts (`BOOKING`, `TREATMENT`, `CAUSE`, `SEVERITY`, `DIAGNOSIS`, `OTHER`), integrated with AWS Bedrock Knowledge Bases and Cohere Rerank v3.0.

4. **[Context Management, gRPC Streaming & Observability](5.3.4-memory-streaming-observability/)**  
   Implementing self-healing persistent conversational memory (`SafePostgresChatMessageHistory` on NeonDB/Postgres), bidirectional gRPC streaming (`triage.proto`), and dual-layer observability via Langfuse + AWS CloudWatch (`watchtower`).

5. **[Unique Selling Points (USPs) of medflow-ai](5.3.5-unique-selling-points/)**  
   The 5 strategic pillars: Edge AI & Cloud AI synergy, clinical data self-evolution, seamless triage with AI Triage Report attachment to bookings, Medical Safety First prompt architecture, and production-grade reliability.

6. **[End-to-End Execution Flow Summary](5.3.6-end-to-end-execution-flow/)**  
   A millisecond-by-millisecond trace of a real clinical query: from severe headache and high fever symptom intake, ViMQ entity extraction, `TREATMENT` routing, S3/Bedrock retrieval, Cohere reranking, to live departmental triage recommendations.

---
*Proceed to the first technical report section: **[1. Architecture Overview](5.3.1-architecture-overview/)**.*
