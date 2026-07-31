---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Deploying the Online Medical Management & Consultation Platform (MedFlow) on AWS

#### Overview

In this hands-on workshop, you will build and deploy the **Online Medical Management & Consultation Platform (MedFlow)** on AWS cloud infrastructure. The system is designed following modern Cloud architectural standards, adhering to strict medical data security compliance, real-time processing capabilities, and Artificial Intelligence (AI) integration.

The practical journey is divided into **4 strategic modules** representing the entire lifecycle of developing a Cloud-native system:
+ **Database Deployment (Amazon Aurora & RDS):** Initialize a cost-optimized PostgreSQL database (`healthcare-db`) utilizing ARM Graviton2 processors (`db.t4g.micro`), enforce transit encryption with an SSL certificate (`global-bundle.pem`), and automate Schema synchronization via Prisma ORM.
+ **Deploying Authentication & Authorization Services (AWS Cognito):** Centralized identity management (User Pool `healthcare`) for Patients, Doctors, and Admins (RBAC). Achieve healthcare data security standards using **UUID Anonymization** and asymmetric RSA JWT verification via the **JWKS Endpoint**.
+ **Building & Deploying the AI Module (MedFlow AI):** Package and deploy a pre-diagnosis AI assistance model (AI Triage & Chatbot) on **Amazon SageMaker Endpoints** to process real-time patient symptom classification.
+ **System Deployment (Fullstack Deployment on EC2):** Package Docker Containers for the Frontend (Next.js) and Backend (NestJS REST API & WebSocket Gateway) onto Amazon EC2, connecting all resources (RDS, Cognito, SageMaker, S3, SES/SNS, CloudWatch) within a VPC network.

#### Content

1. [Part 1: Database Deployment (Amazon Aurora & RDS)](5.1-Aurora-and-RDS/)
2. [Part 2: Deploying Authentication & Authorization Services (AWS Cognito)](5.2-Cognito/)
3. [Part 3: Building & Deploying the AI Module (MedFlow AI) on AWS](5.3-medflow-ai/)
4. [Part 4: Fullstack System Deployment on EC2](5.4-deploy/)