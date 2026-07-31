---
title: "Week 1 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:

* Conduct general research on modern Web application architectures, Cloud Computing, and Hybrid AI Services models (Cloud + External SaaS + Local Host).
* Study core AWS infrastructure services (**Cognito, EC2, S3, RDS PostgreSQL, CloudWatch, Bedrock Knowledge Base, IAM, VPC**) alongside auxiliary AI services (**GPT-4o-mini**, **ViMQ Local**, **Langfuse**) applied to the Smart Healthcare Platform.
* Analyze and select an appropriate architecture model for the application (Multi-tier Microservices on Docker) and design a comprehensive AWS Well-Architected Hybrid AI Cloud infrastructure diagram.
* Perform a detailed analysis of the core **Business Flow** comprising 5 phases: Auth infrastructure authorization (Cognito RBAC), Patient Onboarding, AI RAG Medical Assistant Chatbot, Anti-slot-conflict Booking (Pessimistic Locking), and Doctor Schedule Lookup.
* Prepare the local development environment and initialize the project with Responsive Next.js (Frontend) and NestJS (Backend & LLM Intent Router).

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Conduct general research on Cloud Computing (IaaS, PaaS, SaaS) and the benefits of deploying Healthcare Web applications on the Cloud.<br>- Analyze the 3-Tier Web Architecture model combined with the RAG AI pipeline applied to the project. | 06/01/2026 | 06/01/2026 | [Here](https://aws.amazon.com/what-is-cloud-computing/) |
| Tue | - Study core AWS services: **AWS Cognito** (Auth & RBAC), **EC2** (Docker Containers), **S3** (Attachment Storage / AI Pre-consultation Report), **RDS PostgreSQL** (`db.t4g.micro`), **AWS Bedrock Knowledge Base** (RAG Pipeline).<br>- Study integrated AI services: **GPT-4o-mini** (Inference), **ViMQ** (Local Medical NER), **Langfuse** (LLM Monitoring). | 06/02/2026 | 06/02/2026 | [Here](https://docs.aws.amazon.com/) |
| Wed | - Research Cloud security solutions: Access management with **AWS IAM**, secure network partitioning with **AWS VPC** (Public/Private Subnets).<br>- Study healthcare data security standards (Anonymous UUID encryption, JWT Token verification, At-Rest & In-Transit data encryption via SSL/TLS). | 06/03/2026 | 06/03/2026 | [Here](https://docs.aws.amazon.com/iam/) |
| Thu | - Install development tools: **AWS CLI**, **Node.js**, **Docker Desktop**, **WSL 2**, and configure AWS IAM accounts.<br>- Initialize the GitHub repository and configure the project directory structure for Frontend (Next.js) and Backend (NestJS Framework). | 06/04/2026 | 06/04/2026 | [Here](https://docs.aws.amazon.com/cli/) |
| Fri | - Draft and render the Hybrid AI Cloud infrastructure architecture diagram (**AWS Architecture Diagram**) for the Smart Healthcare Platform.<br>- Prepare technical requirement analysis documentation and finalize core **Business Flow** details (Cognito RBAC Auth Flow, Medical Intake Form, AI RAG Consultation Chatbot, Booking concurrency with Pessimistic Locking, and Doctor Portal lookup). | 06/05/2026 | 06/05/2026 | [Here](https://aws.amazon.com/architecture/) |


### Week 1 Achievements:

* Mastered multi-tier Web architecture, the RAG AI pipeline, and foundational cloud computing theories alongside core AWS services applied to healthcare projects.
* Completed an AWS Well-Architected **AWS Architecture Diagram** for the Hybrid AI Cloud infrastructure, clearly defining deployment locations for Public/Private Subnets, Docker Containers on EC2, S3, RDS PostgreSQL, AWS Bedrock KB, GPT-4o-mini, ViMQ, and Langfuse.
* Finalized the complete core **Business Flow** analysis documentation detailing 5 phases from Cognito Auth, Onboarding, AI RAG Consultation Chatbot, Anti-slot-conflict Booking to the Doctor Portal schedule lookup.
* Gained a clear understanding of secure network partitioning mechanisms (VPC, Public/Private Subnets) and user/service access authorization using AWS IAM & Cognito (utilizing anonymous UUIDs).
* Successfully initialized the local development environment and initial source codebases for **Next.js** and **NestJS**, pre-connected to GitHub.
