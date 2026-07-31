---
title : "Building & Deploying the AI Module (MedFlow AI) on AWS"
date : 2026-07-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### AI Architecture Overview

The **`medflow-ai`** module is an AI-powered Medical Triage & Clinical Decision Support System (CDSS). The system combines a local **ViMQ (NER)** natural language processing model, **AWS Cloud-Native infrastructure (S3, Bedrock Knowledge Base, CloudWatch)**, and the **GPT-4o-mini** model monitored via **Langfuse**.

```text
                     [ Patient / Client ]
                              │
                              ▼
               [ Medical Entity Extraction ]
                    (Local ViMQ NER Model)
                              │
                              ▼
                   [ LLM Intent Routing ]
                    (LLM Intent Router)
                              │
                              ▼
            [ Knowledge Retrieval via RAG ]
              (AWS Bedrock Knowledge Base)
                              │
                              ▼
              [ Clinical Response Generation ]
                    (GPT-4o-mini Engine)
                              │
              ┌───────────────┴───────────────┐
              ▼                               ▼
     [ LLM Flow Monitoring ]          [ System Log Storage ]
           (Langfuse)                   (AWS CloudWatch)
```

#### Nội dung
- [Amazon S3 Configuration](5.3.1-data-storage/)
- [AWS Bedrock Knowledge Base Configuration](5.3.2-bedrock/)
- [Initializing Local ViMQ Server & gRPC Server](5.3.3-vimq-grpc-deployment/)
- [Integrating RAG, Langfuse Tracing & CloudWatch Logging](5.3.4-rag-tracing-monitoring/)