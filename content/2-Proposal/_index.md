---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

In this section, you will find an executive summary of the proposed Digital Healthcare System development project, including objectives, AWS Cloud infrastructure architecture, business workflows, and operational budget estimates.

# Smart Healthcare AI Triage & Appointment Booking Platform
## Cloud-native Solution for AI-Powered Medical Triage and Online Appointment Management

### 1. Executive Summary
The Smart Healthcare Platform is designed to modernize initial patient onboarding, triage, and appointment booking processes at clinics and hospitals. The system utilizes an Artificial Intelligence (AI) model hosted on **Amazon SageMaker** to classify patient symptoms into three severity levels (Red - Yellow - Green) and automatically generate standardized medical summary reports for doctors prior to consultations. Built on a Microservices/Cloud-native architecture using **AWS Cloud** (Cognito, EC2, RDS PostgreSQL, S3, CloudWatch), the platform handles thousands of concurrent requests from patients, doctors, and receptionists.

### 2. Problem Statement
#### What’s the Problem?
Healthcare facilities frequently experience overcrowding at reception desks. Traditional appointment scheduling via phone or walk-ins often leads to double-booking and extended patient wait times. Additionally, doctors spend significant time asking basic symptom questions from scratch due to the lack of pre-consultation summary reports.

#### The Solution 
The platform provides a comprehensive solution featuring:  
1. **Real-time AI Chatbot:** Interacts with patients via WebSockets, collects symptoms, and transmits data to **Amazon SageMaker** for emergency severity classification and medical report synthesis.
2. **Conflict-Free Appointment Scheduling:** Employs **Pessimistic Locking** on **AWS RDS PostgreSQL** to definitively resolve Race Conditions during simultaneous booking requests.
3. **Streamlined On-site Payment Workflow:** Allows patients to book appointments seamlessly without requiring upfront payment; all service, lab test, and prescription fees are settled directly at the reception/cashier desk during check-in or after consultation.
4. **Security & Role-Based Access Control (RBAC):** Manages user authentication through **AWS Cognito** and protects sensitive healthcare data using **UUID** encryption/obfuscation.

#### Benefits and Return on Investment (ROI)
- Reduces reception waiting times by up to 60% through automated QR code check-in.
- Increases physician productivity by 30% by providing pre-synthesized AI symptom summaries.
- Eliminates 100% of double-booking risks, significantly improving patient satisfaction.
- Optimizes infrastructure costs via the elasticity and auto-scaling capabilities of AWS Cloud based on real traffic.

### 3. Solution Architecture
The system adopts a Multi-tier Web Architecture hosted on AWS Cloud, structured into three primary layers: Frontend (Next.js), Backend Service (NestJS on EC2), and AI Services (Amazon SageMaker).
<!--
![IoT Weather Station Architecture](/images/2-Proposal/edge_architecture.jpeg)

![IoT Weather Platform Architecture](/images/2-Proposal/platform_architecture.jpeg)
-->

#### AWS Services Used
- *Amazon Cognito*: User identity management, authentication, and role authorization (Patient, Doctor, Receptionist, Admin).
- *AWS EC2*: Hosts Frontend Web (Next.js) and Backend REST API / WebSocket (NestJS) applications via Docker Containers.
- *Amazon SageMaker*: Endpoint hosting and running AI inference models for symptom analysis.
- *Amazon RDS (PostgreSQL)*: Relational database storing patient profiles, doctor availability, schedules, and invoices.
- *Amazon S3*: Object storage for static files, avatars, digital prescriptions, and lab results.
- *AWS CloudWatch*: System logging, CPU/Memory performance monitoring, and real-time alert notifications.
- *AWS SES / SNS*: Automated Email/SMS appointment confirmation delivery with QR check-in codes.

#### Component Design
- *Patient Portal (Next.js)*: Enables patients to chat with the AI Bot, browse doctor profiles, select time slots, and receive appointment QR confirmation codes.
- *Medical Staff Interface (Next.js)*:  
  - **Doctor Portal:** View daily schedules, review AI summary reports, input diagnostic findings, and prescribe medications.
  - **Reception Portal:** Check-in patients via QR code, issue service invoices, and collect payments directly at the counter.
- *Backend Microservices (NestJS)*: Handles Business Logic, WebSocket Gateway, and AWS RDS PostgreSQL database interactions.

### 4. Technical Implementation
**Implementation Phases**  
The project is executed over an **8-week** (2-month) timeline across four key stages:  
1. *Weeks 1 - 2*: Requirements analysis, AWS Cloud architecture design, Database Schema design, and Base Source Code initialization (Next.js + NestJS).
2. *Weeks 3 - 4*: Infrastructure setup on AWS (EC2, S3, RDS PostgreSQL), ORM Prisma/TypeORM integration, and concurrency control handling.
3. *Weeks 5 - 6*: AWS CloudWatch integration, SageMaker AI model deployment, and completion of role-based dashboards (RBAC).
4. *Weeks 7 - 8*: Stress Testing, E2E testing, Docker containerization, CI/CD deployment pipeline configuration, and final handover/acceptance.

**Technical Requirements**
- *Frontend*: Next.js 14, TailwindCSS, Socket.io-client, React Query.
- *Backend*: NestJS Framework, TypeORM/Prisma, TypeScript, Socket.io.
- *Database*: PostgreSQL 16.x on AWS RDS (Private Subnet).
- *AI/ML*: Python, Amazon SageMaker Endpoints.
- *DevOps*: Docker, AWS CLI, GitHub Actions (CI/CD).

### 5. Timeline & Milestones
*Project Timeline*
- *Phase 1 (Weeks 1 - 2)*: Complete System Architecture & Database Schema design.
- *Phase 2 (Weeks 3 - 4)*: Successfully deploy AWS infrastructure (RDS PostgreSQL, S3, EC2) & Core API.
- *Phase 3 (Weeks 5 - 6)*: Integrate SageMaker AI, complete Doctor / Receptionist Dashboards & AWS CloudWatch monitoring.
- *Phase 4 (Weeks 7 - 8)*: Complete Stress Testing, implement CI/CD pipelines on AWS Cloud, and achieve final project acceptance.

### 6. Budget Estimation
Infrastructure costs are estimated based on AWS Cloud usage for the trial / Development Phase (MVP):

*Monthly AWS Infrastructure Cost Breakdown*  
- *AWS RDS (db.t3.micro - PostgreSQL)*: ~$15.00 USD/month (Single-AZ, 20 GB Storage).
- *AWS EC2 (t3.small - Backend & Frontend)*: ~$14.00 USD/month (24/7 runtime).
- *Amazon SageMaker (ml.t3.medium Endpoint)*: ~$36.00 USD/month (Serverless/On-demand AI Inference).
- *Amazon S3 Standard*: ~$0.50 USD/month (5 GB Data Storage & Transfer).
- *Amazon Cognito*: $0.00 USD/month (Free Tier up to 50,000 MAU).
- *AWS CloudWatch*: ~$2.00 USD/month (Metrics, Logs & Alarms).

*Total Estimated Cloud Infrastructure Cost*: ~$67.50 USD/month.

### 7. Risk Assessment
#### Risk Matrix
- Simultaneous booking conflicts (Race Conditions): High Impact, Medium Probability.
- AI Model connection latency (SageMaker Timeout): Medium Impact, Low Probability.
- Healthcare Data Privacy Leaks: Very High Impact, Low Probability.

#### Mitigation Strategies
- *Race Conditions*: Enforce Pessimistic Locking directly at the PostgreSQL database level.  
- *AI Timeout*: Implement a Fallback flow — If AI fails, the system automatically redirects patients to the traditional manual doctor selection workflow without disrupting the user experience.  
- *Data Privacy*: Utilize UUID strings instead of auto-incrementing integer IDs in URLs and anonymize patient data before logging to CloudWatch.
### 8. Expected Outcomes
- **Technical Improvements:** Automates 80% of patient reception and triage workflows; achieves system availability > 99.9% on AWS Cloud.  
- **Long-term Value:** Provides standardized data sources for health analytics; easily scalable to multi-branch clinic networks in the future.
