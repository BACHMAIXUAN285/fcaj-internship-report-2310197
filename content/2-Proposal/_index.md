---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

In this section, you will find a summary proposal for the development of the Digital Healthcare System, including objectives, AWS Cloud infrastructure architecture, core business flows, and estimated operational budgets.

# Smart Healthcare AI Triage & Appointment Booking Platform
## Cloud-native Solution for AI-Powered Medical Triage and Online Appointment Management

### 1. Executive Summary
The Smart Healthcare Platform is designed to modernize the intake process, handle preliminary medical Q&A, and facilitate online appointment bookings. The system incorporates a **Generative AI & RAG (Retrieval-Augmented Generation)** architecture combining **AWS Bedrock Knowledge Base**, the **ViMQ** medical entity extraction model, and the **GPT-4o-mini** LLM, while supporting the storage of **Pre-consultation Reports** generated from conversation summaries. Built on a Cloud-native architecture over **AWS Cloud** infrastructure (Cognito, EC2, RDS PostgreSQL, S3, CloudWatch) integrated with a dedicated LLM monitoring system (**Langfuse**), the platform serves the access needs of Patients, Doctors, and Administrators.

### 2. Problem Statement
#### What’s the Problem?
Healthcare facilities currently experience reception desk congestion because patients spend significant time inquiring about basic information. Traditional appointment booking processes via telephone or walk-ins frequently cause double-booking issues and extended waiting times. On the doctors' side, tracking appointment schedules and registered patient information remains manual and fragmented.

#### The Solution 
The platform provides a comprehensive solution covering end-to-end business phases:
1. **Phase 1 - System Setup & Authorization (Auth Flow):** Admins manage and provision accounts on the system. **AWS Cognito** handles centralized identity management (RBAC), providing strict access control for Patient, Doctor, and Admin roles.
2. **Phase 2 - Intake & Medical Onboarding:** Patients register/log in via the Mobile Web App. Patients can complete intake forms detailing personal information, medical history, and core health metrics.
3. **Phase 3 - AI RAG Medical Assistant (LLM Pipeline Flow):**
   - The [LLM Intent Router] receives questions and orchestrates processing: extracting medical entities via **ViMQ (Local Host)** and routing intent via **AWS Bedrock Knowledge Base**.
   - The **GPT-4o-mini** model synthesizes knowledge and responds with accurate answers for the patient.
   - The entire conversation flow is logged, with performance and token metrics monitored via **Langfuse** and **AWS CloudWatch**.
4. **Phase 4 - Specialist Appointment Booking (Booking Flow):** Patients proactively select a doctor and an open time slot. **AWS RDS PostgreSQL** applies **Pessimistic Locking** mechanisms to eliminate 100% of double-booking risks (Race Conditions). Consultation chats can be automatically compiled into a **Pre-consultation Report** file stored in **Amazon S3**.
5. **Phase 5 - Schedule Lookup & Management (Doctor/Patient Portal):** Doctors log into the Portal to review booked appointment schedules and look up patient personal information and medical history.

#### Benefits and Return on Investment (ROI)
- Reduce initial reception consultation time by 60% through 24/7 automated AI RAG inquiry responses delivering precise medical data.
- Enable Doctors to seamlessly manage their daily work schedules and patient lists.
- Eliminate 100% of appointment double-booking risks via Database-level Pessimistic Locking.
- Guarantee AI response quality and safety via a centralized LLM monitoring system (**Langfuse**).
- Optimize infrastructure operational costs thanks to the elastic scaling capabilities of AWS Cloud services.

### 3. Solution Architecture
The system utilizes a Multi-tier Web architecture combined with Hybrid AI services (Cloud Services + External SaaS + Local Host Services).

![Smart Healthcare AI Architecture](/images/2-Proposal/architect-diagram.png)

#### AWS Services & Technologies Used
- *Amazon Cognito*: Identity management, sign-in/sign-up, and RBAC authorization for Patients, Doctors, and Admins.
- *AWS EC2*: Hosts the Web Frontend (Next.js) and Backend REST API / WebSocket Gateway / LLM Intent Router (NestJS) containerized via Docker.
- *AWS Bedrock Knowledge Base*: Stores and retrieves medical knowledge bases (RAG Pipeline) for consultation.
- *External SaaS & Local Models*: **GPT-4o-mini** (response generation), **ViMQ Local Host** (NER medical entity extraction), and **Langfuse** (monitoring LLM metrics, latency, and tokens).
- *Amazon RDS (PostgreSQL)*: Relational database storing patient details, doctor information, and appointments with Pessimistic Locking (`FOR UPDATE`) mechanisms.
- *Amazon S3*: Stores static assets, consultation chat history reports (PDF/JSON), and file attachments.
- *AWS CloudWatch*: Collects Backend and EC2 system logs alongside aggregated logs from Langfuse.

#### Component Design
- *Patient Interface (Next.js - Mobile View)*: Allows patients to update personal profiles, chat with the AI RAG Assistant for medical inquiries, and perform appointment bookings.
- *Doctor Interface (Next.js - Desktop View)*: Enables Doctors to log in, look up scheduled appointments, review patient medical backgrounds, and view AI consultation report files from S3.
- *Admin Portal*: Manages doctor directories, user accounts, and views operational analytics reports.
- *Backend Services (NestJS)*: Handles Business Logic, LLM Intent Router, RDS PostgreSQL database connections, S3, and AI APIs (Bedrock, GPT-4o-mini, ViMQ, Langfuse).

### 4. Technical Implementation
**Implementation Phases**  
The project is scheduled for deployment over **8 weeks** (2 months) across the following phases:  
1. *Weeks 1 - 2*: Analyze Business Flow requirements, design AWS Hybrid AI Cloud Architecture, construct Database ERD, and initialize Base Source Code (Next.js + NestJS).
2. *Weeks 3 - 4*: Configure AWS Cognito (RBAC Auth Flow), deploy AWS infrastructure (EC2, S3, RDS PostgreSQL), integrate Prisma ORM, and implement concurrency control (Pessimistic Locking).
3. *Weeks 5 - 6*: Integrate RAG Pipeline (AWS Bedrock KB + GPT-4o-mini + ViMQ Local), connect Langfuse for LLM monitoring, complete Doctor lookup interfaces & Patient booking views.
4. *Weeks 7 - 8*: Integrate AWS CloudWatch, perform load testing (Stress Test Concurrency Booking), package Docker containers, configure CI/CD pipelines, and finalize project hand-off.

**Technical Requirements**
- *Frontend*: Next.js, TailwindCSS, Socket.io-client, React Query.
- *Backend*: NestJS Framework, Prisma ORM, TypeScript, Socket.io.
- *Database*: PostgreSQL 16.x on AWS RDS (`db.t4g.micro` - Private Subnet).
- *AI/ML*: AWS Bedrock KB, OpenAI API (GPT-4o-mini), ViMQ Local Service, Langfuse.
- *DevOps*: Docker, AWS CLI, GitHub Actions (CI/CD).

### 5. Timeline & Milestones
*Project Timeline*
- *Phase 1 (Weeks 1 - 2)*: Complete System Architecture & Database Schema designs according to the updated Business Flow.
- *Phase 2 (Weeks 3 - 4)*: Successfully deploy AWS infrastructure (Cognito Auth Flow, RDS PostgreSQL, S3, EC2) & Booking Concurrency APIs.
- *Phase 3 (Weeks 5 - 6)*: Successfully integrate RAG Pipeline (Bedrock + GPT-4o-mini + ViMQ), Langfuse monitoring, and Doctor schedule lookup portals.
- *Phase 4 (Weeks 7 - 8)*: Complete concurrency booking stress tests, deploy CI/CD pipelines on AWS Cloud, and achieve project acceptance.

### 6. Budget Estimation
Infrastructure costs are estimated based on an AWS Cloud & AI Services environment for the testing phase (MVP / Development Phase):

*Monthly Infrastructure & Service Cost Breakdown*  
- *AWS RDS (db.t4g.micro - PostgreSQL)*: ~$12.00 USD/month (Single-AZ, ARM Graviton2).
- *AWS EC2 (t3.small - Backend & Frontend)*: ~$14.00 USD/month (Running Docker 24/7).
- *AWS Bedrock Knowledge Base*: ~$10.00 USD/month (Vector Storage & Search Query costs).
- *OpenAI API (GPT-4o-mini)*: ~$5.00 USD/month (Token costs based on actual usage).
- *Amazon S3 Standard*: ~$0.50 USD/month (5 GB Data Storage & Transfer).
- *Amazon Cognito*: $0.00 USD/month (First 50,000 MAUs Free).
- *AWS CloudWatch & Langfuse*: ~$3.00 USD/month (Metrics, Logs, Alarms & LLM Monitoring).

*Total Monthly Cloud & AI Infrastructure Cost*: ~$44.50 USD/month.

### 7. Risk Assessment
#### Risk Matrix
- Concurrent booking conflicts (Race Condition): High impact, medium probability.
- Disconnected LLM APIs (OpenAI / Bedrock Timeout): Medium impact, low probability.
- AI response hallucination of medical knowledge (Hallucination): High impact, low probability.

#### Mitigation Strategies
- *Race Condition*: Apply Pessimistic Locking (`FOR UPDATE`) directly at the PostgreSQL Database layer during slot confirmation.  
- *API Timeout & Fallback*: Build Fallback flows — If LLM APIs encounter failure, the system automatically transitions the patient to the direct Appointment Booking interface.  
- *Hallucination Reduction & Monitoring*: Utilize RAG via **AWS Bedrock Knowledge Base** to isolate accurate medical data, combined with **Langfuse** to track response quality and trigger alerts on anomalous AI answers.

### 8. Expected Outcomes
- **Technical Improvements:** Automate initial patient medical consultations using precise RAG AI; achieve system availability metrics > 99.9% on AWS Cloud.  
- **Practical Value:** Provide a transparent and accurate appointment booking solution, empowering patients to manage their schedules while enabling doctors to easily manage daily consultation workflows.
