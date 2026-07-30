---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

In this section, you will find a summary of the Digital Healthcare system development project proposal, including objectives, AWS Cloud infrastructure architecture, core business flows, and operational budget estimates.

# Smart Healthcare AI Triage & Appointment Booking Platform
## Cloud-native Solution for AI-Powered Medical Triage and Online Appointment Management

### 1. Executive Summary
The Smart Healthcare Platform is designed to modernize the intake, initial triage, and appointment booking processes at clinics and hospitals. The system leverages artificial intelligence (AI) models hosted on **Amazon SageMaker** to classify patient symptoms across 3 risk levels (Red - Yellow - Green) while automatically generating a **Pre-consultation Report** prior to examination sessions. Built on a Microservices/Cloud-native architecture on the **AWS Cloud** platform (Cognito, EC2, RDS PostgreSQL, S3, CloudWatch, SES/SNS), the platform serves thousands of concurrent visits from patients, doctors, and receptionists/administrators.

### 2. Problem Statement
#### What’s the Problem?
Healthcare facilities currently face severe overcrowding at reception desks. Traditional appointment booking processes via phone or walk-ins frequently cause schedule collisions (Double-booking) and prolonged patient wait times. Additionally, doctors spend significant time re-asking basic symptoms due to a lack of pre-collected information.

#### The Solution 
The platform provides a comprehensive solution covering 5 closed-loop business stages:
1. **Stage 1 - System Setup & Account Provisioning:** Admins create doctor profiles on the Admin Portal. **AWS Cognito** combined with **AWS SES** automatically sends an Email containing a Temporary Password. Doctors log into the Doctor Portal and are forced to set a new password on their first login before configuring their availability schedule.
2. **Stage 2 - Patient Onboarding:** Patients register an account on the Mobile Web App (default assigned role: `Patient`). Upon first login, patients fill out an Initial Medical Declaration Form (age, blood type, medical history, allergies) which is encrypted and stored in the database.
3. **Stage 3 - AI Symptom Triage Assistant (Triage Flow):** The AI Bot (on **Amazon SageMaker**) communicates via WebSocket to gather symptoms and categorize them into 3 severity levels:
   - 🔴 **Red Level (Emergency):** Disables the chat window and displays a prominent button to call 115 Emergency immediately.
   - 🟢 **Green Level (Mild):** Provides home self-care guidelines and automatically terminates the chat session.
   - 🟡 **Yellow Level (Medical Consultation Needed):** Displays a UI Card recommending appointment booking directed to the appropriate specialty.
4. **Stage 4 - Specialty Appointment Booking (Booking Flow):** Patients select a time slot via a Bottom Sheet UI. **AWS RDS PostgreSQL** applies row-level locking (**Pessimistic Locking**) to eliminate 100% of double-booking risks (Race Conditions). The system automatically summarizes the conversation into a **Pre-consultation Report** stored in **Amazon S3** and sends a confirmation QR code via Email/SMS through **AWS SES/SNS**.
5. **Stage 5 - Consultation & Diagnosis Session (Consultation Flow):** Doctors access the Doctor Portal featuring a **Split View** layout (one side displays Past Records + AI Summary Report, the other side features diagnosis/prescription entry forms). Consultations occur via Telehealth or in-person, after which results are automatically pushed to the patient's Mobile App.

#### Benefits and Return on Investment (ROI)
- Reduces waiting times at reception by up to 60% through automated QR check-in and self-onboarding processes.
- Boosts doctor productivity by 30% utilizing the Split View interface and AI-generated Pre-consultation Reports.
- Eliminates 100% of appointment slot collision risks using Pessimistic Locking at the database layer.
- Optimizes infrastructure costs through AWS Cloud elasticity based on real-time traffic demand.

### 3. Solution Architecture
The system uses a Multi-tier Web architecture on AWS Cloud, divided into 3 main layers: Frontend (Next.js 14 Responsive), Backend Service (NestJS on EC2), and AI Services (Amazon SageMaker).

![Smart Healthcare AI Architecture](/images/2-Proposal/architecture-diagram.png)

<!--
![IoT Weather Station Architecture](/images/2-Proposal/edge_architecture.jpeg)

![IoT Weather Platform Architecture](/images/2-Proposal/platform_architecture.jpeg)
-->

#### AWS Services Used
- *Amazon Cognito*: Identity management, sign-in/sign-up, RBAC authorization, and temporary password flows for medical staff.
- *AWS EC2*: Deploys the Web Frontend (Next.js) and Backend REST API / WebSocket Gateway (NestJS) via Docker Containers.
- *Amazon SageMaker*: Endpoint hosting the AI model for 3-tier symptom classification and medical report generation.
- *Amazon RDS (PostgreSQL)*: Relational database storing patient, doctor, and schedule data with Pessimistic Locking mechanics.
- *Amazon S3*: Object storage for static files, AI-generated Pre-consultation Reports, prescriptions, and lab test results.
- *AWS CloudWatch*: Aggregates system logs, monitors CPU/Memory utilization, and tracks AI Inference metrics.
- *AWS SES / SNS*: Automates delivery of Temporary Password emails to Doctors and appointment confirmation Email/SMS containing check-in QR codes to Patients.

#### Component Design
- *Patient Interface (Next.js - Mobile View)*: Enables initial medical declarations, AI Triage chat, appointment booking via Bottom Sheet UI, and receipt of confirmation QR codes.
- *Medical Staff Interface (Next.js - Desktop View)*:  
  - **Doctor Portal:** Temp Password sign-in, forced first-time password change, availability calendar setup, appointment list review, and consultations via **Split View** (AI Report Profile + Diagnostic Form).
  - **Admin & Reception Portal:** Staff management/doctor onboarding, QR code patient check-in, service invoicing, and over-the-counter payment collection.
- *Backend Microservices (NestJS)*: Handles Business Logic, WebSocket Gateway (AI Chat & Telehealth Signaling), and AWS RDS PostgreSQL database connections.

### 4. Technical Implementation
**Implementation Phases**  
The project is deployed over **8 weeks** (2 months) across the following phases:  
1. *Weeks 1 - 2*: Business Flow requirements analysis, AWS Cloud architecture design, Database ERD design, and Base Source Code initialization (Next.js 14 + NestJS).
2. *Weeks 3 - 4*: AWS Cognito configuration (Temp Password flow), AWS Infrastructure deployment (EC2, S3, RDS PostgreSQL), TypeORM integration, and concurrency control handling (Pessimistic Locking).
3. *Weeks 5 - 6*: Amazon SageMaker 3-tier AI Triage model integration via WebSocket, S3 Pre-consultation Report generation, Doctor Portal (Split View) & Patient Mobile UI completion.
4. *Weeks 7 - 8*: AWS CloudWatch integration, stress testing (Race Condition verification), Docker container packaging, GitHub Actions CI/CD setup, and project handover acceptance.

**Technical Requirements**
- *Frontend*: Next.js 14, TailwindCSS, Socket.io-client, React Query.
- *Backend*: NestJS Framework, TypeORM/Prisma, TypeScript, Socket.io.
- *Database*: PostgreSQL 16.x on AWS RDS (Private Subnet).
- *AI/ML*: Python, Amazon SageMaker Endpoints.
- *DevOps*: Docker, AWS CLI, GitHub Actions (CI/CD).

### 5. Timeline & Milestones
*Project Timeline*
- *Phase 1 (Weeks 1 - 2)*: Complete System Architecture & Database Schema designs according to Business Flow.
- *Phase 2 (Weeks 3 - 4)*: Successfully deploy AWS infrastructure (Cognito Auth Flow, RDS PostgreSQL, S3, EC2) & Booking Concurrency API.
- *Phase 3 (Weeks 5 - 6)*: Successfully integrate SageMaker AI Triage, finalize Doctor Split View Portal & AWS CloudWatch.
- *Phase 4 (Weeks 7 - 8)*: Complete concurrency load stress tests, deploy CI/CD on AWS Cloud, and achieve final project acceptance sign-off.

### 6. Budget Estimation
Infrastructure costs are estimated based on AWS Cloud environment pricing for the testing phase (MVP / Development Phase):

*Monthly AWS Infrastructure Cost Breakdown*  
- *AWS RDS (db.t3.micro - PostgreSQL)*: ~$15.00 USD/month (Single-AZ, 20 GB Storage).
- *AWS EC2 (t3.small - Backend & Frontend)*: ~$14.00 USD/month (Running 24/7).
- *Amazon SageMaker (ml.t3.medium Endpoint)*: ~$36.00 USD/month (Serverless/On-demand AI Inference).
- *Amazon S3 Standard*: ~$0.50 USD/month (5 GB Data Storage & Transfer).
- *Amazon Cognito*: $0.00 USD/month (Free tier covers up to 50,000 MAU).
- *AWS CloudWatch & SES/SNS*: ~$2.00 USD/month (Metrics, Logs, Alarms & Automated Emails).

*Total Estimated Cloud Infrastructure Cost*: ~$67.50 USD/month.

### 7. Risk Assessment
#### Risk Matrix
- Appointment slot collisions during concurrent bookings (Race Condition): High impact, Medium probability.
- AI model connection timeouts (SageMaker Timeout): Medium impact, Low probability.
- Patient medical data leaks (Data Privacy): Very High impact, Low probability.

#### Mitigation Strategies
- *Race Condition*: Use Pessimistic Locking directly at the PostgreSQL Database layer during slot reservation.  
- *AI Timeout*: Implement a Fallback mechanism — If the AI encounters an issue, the system automatically redirects patients to traditional manual doctor selection without breaking the user experience.  
- *Data Privacy*: Encrypt initial medical data, utilize UUID strings instead of auto-incrementing IDs in URL parameters, and anonymize patient details when streaming logs to CloudWatch.
### 8. Expected Outcomes
- **Technical Improvements:** Automate 80% of patient intake and routing processes; achieve > 99.9% system availability on the AWS Cloud platform.  
- **Long-term Value:** Provide standardized data sources for epidemic analysis and forecasting; enable effortless multi-branch clinic chain expansion in the future.
