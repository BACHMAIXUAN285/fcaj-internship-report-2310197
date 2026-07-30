---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# [FCAJ2026] What is AWS Bedrock Knowledge Bases? Why is it the perfect "missing piece" for Serverless RAG architecture?

---

### Introduction

After learning how to build Medical AI Assistant systems using the RAG (Retrieval-Augmented Generation) approach from scratch, I began facing a series of difficulties in building Data Pipelines on my own. What surprised me was that when reading AWS official documentation and sample solutions, most architectures utilized "AWS Bedrock Knowledge Bases" rather than providing instructions to deploy standalone Vector Databases.

This made me wonder: "If setting up custom chunking and a vector database is the standard way to do RAG, why did AWS invent Bedrock Knowledge Bases?"

After reading the official documentation and directly deploying this service for a medical assistant project, I realized that Bedrock Knowledge Bases is not just a "vector storage place" but a fully managed service that oversees the entire RAG workflow, turning every complex stage into Serverless.

---

### Self-managing RAG Infrastructure - An Operational Nightmare

Previously, I thought building a RAG system mainly revolved around writing scripts. For instance, for the system to read tens of thousands of medical PDF or CSV pages, I had to manually write code to chunk the text, call embedding model APIs to convert the text, and then self-host a Vector Database like Milvus or Qdrant.

This approach is quite fun for small projects. However, as the volume of medical data increases, managing this infrastructure becomes difficult. Maintaining a stable Vector Database or writing cronjobs/Airflow pipelines to continuously synchronize data generates numerous operational (Ops) issues.

This is why modern cloud systems encourage the use of Managed Serverless services - a method of offloading the entire burden of managing underlying infrastructure to the cloud provider.

---

### What is AWS Bedrock Knowledge Bases?

According to official AWS documentation, "Knowledge bases for Amazon Bedrock" is a fully managed capability that helps connect Foundation Models with enterprise internal data sources to perform RAG.

In other words, AWS Bedrock Knowledge Bases fully automates the data processing pipeline. Instead of having to do every step manually, this service handles:

1. **Automated Chunking**: Semantically splitting complex medical documents.
2. **Automated Embedding**: Transforming text into vectors using models like Amazon Titan or Cohere.
3. **Automated Indexing**: Storing and indexing data in a hidden Serverless Vector Database backend (such as Amazon OpenSearch Serverless).

This is the point that changed my perspective on building AI applications. Previously, I thought AI engineers had to manually control every step of the Data Pipeline. However, after using Bedrock Knowledge Bases, I realized that "infrastructure operational work should be automated to focus on application logic".

---

### Workflow with AWS Bedrock Knowledge Bases

During the system building process, integration and operation became incredibly simple:

**Upload Data to Amazon S3**
*Function*: Amazon S3 acts as the raw Data Source. Clinical documents and treatment protocols simply need to be dropped into an S3 Bucket.

**Start Ingestion Job (Data Synchronization)**
*Function*: With just a click on the AWS Console or an API call, the system automatically synchronizes new documents from S3, handles chunking and embedding to update the AI's knowledge base without causing any downtime.

**Integration via LangChain**
*Function*: Allows Python applications to retrieve context easily. Instead of writing complex database connection code, I only need to use `AmazonKnowledgeBasesRetriever` combined with the Knowledge Base ID to query (including Hybrid Search capabilities).

---

### The Role of Amazon S3 in the Architecture

Initially, I only viewed Amazon S3 as a place to store static files. However, when combined with Bedrock Knowledge Bases, I realized S3 is the "knowledge gateway" of the entire system. Whenever the hospital issues a new medication list or protocol, the administrator simply pushes the file to S3. With no code intervention and no application redeployment required, the AI system instantly gains the latest knowledge.

It is safe to say that Amazon S3 combined with Bedrock Knowledge Bases creates an automated, infinite stream of knowledge updates.

---

### Why is AWS Bedrock Knowledge Bases the "true love" for AI Engineers?

This is the conclusion I reached after completing the project. The biggest difference lies in resource liberation.

If building RAG manually, an engineer has to play the role of an entire DevOps team: struggling with infrastructure, fixing pipeline errors, and monitoring the Vector Database. Conversely, Bedrock Knowledge Bases shifts all that burden to AWS. This service handles all complex implicit tasks and returns to us the cleanest, simplest APIs.

Consequently, AWS Bedrock Knowledge Bases helps engineering teams save weeks of work, allowing them to channel their complete focus into optimizing clinical business logic and improving patient experiences.

---

### References

1. AWS. "Knowledge bases for Amazon Bedrock". ([https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html))
2. LangChain. "Amazon Knowledge Bases Integrations". ([https://python.langchain.com/docs/integrations/retrievers/bedrock/](https://python.langchain.com/docs/integrations/retrievers/bedrock/))

---

View the article on Facebook [Here](<https://www.facebook.com/groups/awsstudygroupfcj/permalink/2227962487968711/?rdid=DpIlk8AoW652AXKC#>)
