---
title: "Amazon S3 Configuration"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---


---

### Storing Medical Documents on Amazon S3

* **Purpose**: Store medical datasets (.csv, .pdf) used for model training and as data sources for Bedrock Knowledge Base.
* **Step-by-step instructions**:
  1. Access the **Amazon S3 Console**. Select **Create bucket**.
  ![Create bucket](/images/5-Workshop/5.3-medflow-ai/S3-1.png)
  2. Enter a Bucket name (e.g., `medflow-data`) and select the Region (e.g., `ap-southeast-1`).
  ![Name bucket](/images/5-Workshop/5.3-medflow-ai/S3-name.png)
  3. Enable **Server-side encryption (SSE-S3)** to secure medical documents.
  ![SSE-S3](/images/5-Workshop/5.3-medflow-ai/S3-SSE.png)
  4. Create the folder structure `/raw-documents/` and upload clinical-grade medical documents.
  ![S3-now](/images/5-Workshop/5.3-medflow-ai/S3-now.png)