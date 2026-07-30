---
title: "Blogs Posted"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

This section will list and introduce the blogs posted to [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj):

###  [Blog 1 - WHAT IS AWS COGNITO? WHY IS IT AN INDISPENSABLE PIECE OF THE SMART HEALTHCARE SYSTEM?](3.1-Blog1/)
This blog explains the reasoning behind choosing AWS Cognito over developing a custom authentication (Auth) system from scratch for the Smart Healthcare Platform. The article provides an in-depth analysis of multi-role-based access control challenges (RBAC for Patients, Doctors, and Receptionists), the secure identity management flow using JWT Tokens, and how AWS Cognito helps optimize development time and operational costs thanks to its 50,000 MAU free tier.

###  [Blog 2 - WHAT IS AWS BEDROCK KNOWLEDGE BASES? WHY IS IT THE PERFECT MISSING PIECE FOR SERVERLESS RAG ARCHITECTURE?](3.2-Blog2/)
This blog shares practical experience in solving the Data Pipeline challenge for an AI Healthcare Assistant system using AWS Bedrock Knowledge Bases. The article analyzes the benefits of replacing bulky, self-hosted Vector Databases with a Fully-Managed Serverless solution. By automating the entire Chunking, Embedding, and Indexing pipeline—and seamlessly integrating with Amazon S3 and LangChain—the service allows engineers to focus on optimizing clinical logic rather than managing infrastructure.

###  [Blog 3 - AWS S3 BUCKET: THE CLOUD-NATIVE STORAGE "MISSING PIECE" FOR THE SMART HEALTHCARE SYSTEM](3.3-Blog3/)
This blog explains why Amazon S3 was selected over traditional backend server file storage for the Digital Healthcare Platform. The article breaks down how security risks and manual file-saving habits were eliminated by utilizing Private S3 Buckets alongside S3 Presigned URLs to secure doctor profiles, decouple AI model weight files (.pt), and automate the generation and archiving of PDF medical reports. Ultimately, this service transforms the Backend into a lightweight, Stateless architecture, enhancing scalability and optimizing operational costs.
