---
title: "AWS Bedrock Knowledge Base Configuration"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---


---

### AWS Bedrock Knowledge Base Configuration (Chunking & Indexing)

* **Purpose**: Transform raw documents stored on S3 into a Knowledge Base with automated chunking for Retrieval-Augmented Generation (RAG) queries.
* **Step-by-step instructions**:
  1. Access the **Amazon Bedrock Console**. Select **Knowledge bases**. Click **Create knowledge base**.
  2. **Configure IAM Role**: Create a new IAM Role with read access permissions for the S3 Bucket `medflow-medical-knowledge-base`.
  3. **Connect Data Source**:
     * Select **Amazon S3** as the data source.
     * Point the S3 URI path to the folder containing the medical documents created in **Step 1**.
  4. **Configure Chunking Strategy**:
     * Choose the **Fixed-size chunking** method (Chunk size: 300 - 500 tokens, Overlap: 20%).
  5. **Configure Vector Store**: Choose to automatically create an **Amazon OpenSearch Serverless** vector index to store text passages as Vector Embeddings.
  6. Click **Sync** to scan data from S3, perform chunking, and build the index.

  ![Bedrock](/images/5-Workshop/5.3-medflow-ai/bedrock.png)