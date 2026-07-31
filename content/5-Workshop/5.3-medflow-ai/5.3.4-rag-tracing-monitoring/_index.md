---
title: "Integrating RAG, Langfuse Tracing & CloudWatch Logging"
date: 2026-07-01
weight: 4
chapter: false
pre: " <b> 5.3.4. </b> "
---

This section provides a step-by-step programming guide to integrating the RAG workflow, setting up Tracing with Langfuse, and configuring system log shipping to AWS CloudWatch.

---

### Integrating RAG Workflow & Tracing with Langfuse

* **Purpose**: Integrate data from ViMQ NER, query Bedrock KB, generate responses using GPT-4o-mini, and send traces to Langfuse.
* **Step-by-step instructions**:
  1. Integrate the `langchain-aws` SDK into the source code to query Bedrock KB:
     ```python
     from langchain_aws import AmazonKnowledgeBasesRetriever

     retriever = AmazonKnowledgeBasesRetriever(
         knowledge_base_id="YOUR_BEDROCK_KB_ID",
         retrieval_config={"vectorSearchConfiguration": {"numberOfResults": 3}}
     )
     ```
  2. Configure the Langfuse Callback to monitor LLM call details and latency:
     ```python
     from langfuse.callback import CallbackHandler

     langfuse_handler = CallbackHandler(
         public_key="pk-lf-...",
         secret_key="sk-lf-...",
         host="[https://cloud.langfuse.com](https://cloud.langfuse.com)"
     )
     ```
  3. Build the complete workflow in `grpc_server.py`:
     * Extract keywords via ViMQ -> Route intent -> Query Bedrock KB for context -> Call LLM to synthesize response -> Stream tokens back to the gRPC Client.

---

### Configuring Log Monitoring on AWS CloudWatch

* **Purpose**: Record all System Logs, Error Logs, and gRPC Server activity logs to CloudWatch.
* **Step-by-step instructions**:
  1. Access the **Amazon CloudWatch Console**. Navigate to **Logs** and select **Log groups**.
  2. Click **Create log group** with the name: `/aws/medflow/med-chatbot`.
  3. In the `grpc_server.py` source code, configure the `watchtower` or `boto3` library to automatically push logs during application runtime:
     ```python
     import logging
     import watchtower

     logging.basicConfig(level=logging.INFO)
     logger = logging.getLogger("MedFlowAI")
     logger.addHandler(watchtower.CloudWatchLogHandler(log_group="/aws/medflow/med-chatbot"))
     ```

![Langfuse](/images/5-Workshop/5.3-medflow-ai/langfuse%20tracing%20router.png)
---