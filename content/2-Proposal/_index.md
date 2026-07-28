---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

In this section, you will find a summary of the project proposal for developing the Digital Healthcare System, including project objectives, AWS Cloud infrastructure architecture, business workflows, and estimated operational budget.

# Smart Healthcare AI Triage & Appointment Booking Platform
## Cloud-native Solution for AI-Powered Medical Triage and Online Appointment Management

### 1. Executive Summary
The Smart Healthcare Platform is engineered to modernize patient reception, initial triage, and appointment booking workflows across medical clinics and hospitals. The system leverages Artificial Intelligence (AI) models hosted on **Amazon SageMaker** to classify patient symptoms into 3 severity levels (Red - Yellow - Green) and automatically generate medical summary reports for physicians prior to consultations. Built on a Cloud-native architecture using **AWS Cloud** (Cognito, EC2, RDS PostgreSQL, S3, CloudWatch), the platform seamlessly handles thousands of concurrent requests from patients, doctors, and reception staff.

### 2. Problem Statement
*What’s the Problem?*
Healthcare facilities currently suffer from severe reception counter congestion. Traditional appointment booking via phone or in-person frequently leads to double-booking and prolonged patient wait times. Additionally, doctors spend significant time re-asking basic symptom details due to a lack of pre-consultation summaries.

*The Solution* 
The platform delivers a comprehensive end-to-end solution:  
1. **Real-time AI Chatbot:** Interacts with patients via WebSocket, collects symptoms, and feeds data to **Amazon SageMaker** for urgency triage and pre-consultation report generation.
2. **Conflict-Free Booking Engine:** Implements row-level locking (**Pessimistic Locking**) on **AWS RDS PostgreSQL** to eliminate Race Conditions when multiple users attempt to book the exact same slot.
3. **Flexible Two-Stage Payment:** Supports online initial payments (consultation fee via PayOS/VNPay/Stripe) and secondary payments (medications/lab tests at the counter).
4. **Security & RBAC:** Manages identity authentication through **AWS Cognito** and secures sensitive health data using **UUID** masking.

*Benefits and Return on Investment (ROI)* 
- Reduces front-desk wait times by up to **60%** through automated QR code check-in.
- Boosts doctor consultation efficiency by **30%** with AI-synthesized symptom reports.
- Eliminates double-booking risks completely, enhancing overall patient satisfaction.
- Optimizes infrastructure expenses via dynamic cloud elasticity on AWS.

### 3. Solution Architecture
The system adheres to a Multi-tier Web Architecture deployed on AWS Cloud, divided into three main layers: Frontend (Next.js), Backend Services (NestJS on EC2), and AI Services (Amazon SageMaker).
<!--
![IoT Weather Station Architecture](/images/2-Proposal/edge_architecture.jpeg)

![IoT Weather Platform Architecture](/images/2-Proposal/platform_architecture.jpeg)
-->

*AWS Services Used*
- *Amazon Cognito*: Handles identity management, sign-up/sign-in, and Role-Based Access Control (Patient, Doctor, Receptionist, Admin).
- *AWS EC2*: Hosts Web Frontend (Next.js) and Backend REST API / WebSocket Gateway (NestJS) using Docker Containers.
- *Amazon SageMaker*: Deploys and serves real-time AI endpoints for medical symptom triage.
- *Amazon RDS (PostgreSQL)*: Managed relational database storing patient profiles, doctor schedules, appointments, and billing data.
- *Amazon S3*: Stores static assets, avatars, medical records, and appointment QR codes.
- *AWS CloudWatch*: Aggregates system logs, monitors CPU/Memory utilization, and triggers automated alerts.
- *AWS SES / SNS*: Sends automated email and SMS appointment confirmations embedded with check-in QR codes.

*Component Design*
- *Patient Portal (Next.js)*: Enables patients to chat with the AI Bot, view doctor profiles, select time slots, and complete online payments.
- *Healthcare Staff Portal (Next.js)*:  
  - **Doctor Portal:** View daily appointment schedules, read AI summary reports, input clinical diagnoses, and issue digital prescriptions.
  - **Reception Portal:** Check in patients via QR code scanner, generate invoices, and collect second-stage payments (`POSTPAID`) at the counter.
- *Backend Microservices (NestJS)*: Handles Core Business Logic, WebSocket Gateway, Payment Integrations (PayOS/VNPay/Stripe), and PostgreSQL RDS connectivity.

### 4. Technical Implementation
*Implementation Phases*
The project is executed over an **8-week** timeframe (2 months) structured as follows:  
1. *Weeks 1 - 2*: Requirements analysis, AWS Cloud architecture design, PostgreSQL Schema design, and Base Source Code initialization (Next.js + NestJS).
2. *Weeks 3 - 4*: Infrastructure provisioning (EC2, S3, RDS PostgreSQL), ORM integration (TypeORM/Prisma), and Pessimistic Locking implementation.
3. *Weeks 5 - 6*: AWS CloudWatch setup, Amazon SageMaker AI endpoint integration, payment gateway implementation (PayOS/VNPay/Stripe), and RBAC Dashboards.
4. *Weeks 7 - 8*: Stress testing (k6/Artillery), E2E testing, database index optimization, Swagger API documentation, and final system demo.

*Technical Requirements*
- *Frontend*: Next.js 14, TailwindCSS, Socket.io-client, React Query.
- *Backend*: NestJS Framework, TypeORM/Prisma, TypeScript, Socket.io.
- *Database*: PostgreSQL 16.x on AWS RDS (Private Subnet).
- *AI/ML*: Python, Amazon SageMaker Endpoints.
- *DevOps*: Docker, AWS CLI, GitHub Actions (CI/CD).

### 5. Timeline & Milestones
*Project Timeline*
- *Phase 1 (Week 1 - Week 2)*: Complete System Architecture & Database Schema design.
- *Phase 2 (Week 3 - Week 4)*: Successfully deploy AWS Infrastructure (RDS PostgreSQL, S3, EC2) & Core APIs.
- *Phase 3 (Week 5 - Week 6)*: Integrate SageMaker AI, Payment Gateways (PayOS/VNPay/Stripe) & AWS CloudWatch.
- *Phase 4 (Week 7 - Week 8)*: Complete Stress Testing, UI/UX optimizations, and project handover.

### 6. Budget Estimation
Infrastructure expenses are estimated based on AWS Cloud pricing for the Minimum Viable Product (MVP / Development Phase):

*Monthly AWS Infrastructure Cost Breakdown*  
- *AWS RDS (db.t3.micro - PostgreSQL)*: ~$15.00 USD/month (Single-AZ, 20 GB Storage).
- *AWS EC2 (t3.small - Backend & Frontend)*: ~$14.00 USD/month (Running 24/7).
- *Amazon SageMaker (ml.t3.medium Endpoint)*: ~$36.00 USD/month (Serverless / On-Demand AI Inference).
- *Amazon S3 Standard*: ~$0.50 USD/month (5 GB Data Storage & Transfer).
- *Amazon Cognito*: $0.00 USD/month (Free Tier up to 50,000 MAU).
- *AWS CloudWatch*: ~$2.00 USD/month (Metrics, Logs, & Alarms).
- *Payment Gateways (PayOS / VNPay / Stripe Sandbox)*: $0.00 (Free testing environment).

*Total Estimated Cloud Infrastructure Cost*: ~$67.50 USD/month.

### 7. Risk Assessment
#### Risk Matrix
- Race Condition (Double-Booking): High Impact, Medium Probability.
- AI Service Timeout (SageMaker): Medium Impact, Low Probability.
- Healthcare Data Privacy (IDOR): Very High Impact, Low Probability.

#### Mitigation Strategies
- *Race Condition*: Implemented row-level Pessimistic Locking directly at the PostgreSQL database layer.  
- *AI Timeout*: Designed a graceful fallback mechanism — if the AI service times out, the system automatically routes the user to standard manual doctor selection without breaking the user experience.  
- *Data Privacy*: Masked database IDs with UUIDs in URLs and anonymized sensitive patient metrics before streaming logs to CloudWatch.
### 8. Expected Outcomes
- **Technical Enhancements:** Automates 80% of patient reception and triage workflows; achieves > 99.9% system availability on AWS Cloud.  
- **Long-term Value:** Provides standardized data structures for medical analytics and disease forecasting; offers seamless scalability to support multi-branch clinic chains in the future.
