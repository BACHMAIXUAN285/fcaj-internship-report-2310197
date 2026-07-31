---
title: "Week 1 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:

* Conduct general research on modern Web Application Architecture and Cloud Computing.
* Explore core infrastructure services on **AWS** (Cognito, EC2, S3, RDS PostgreSQL, CloudWatch, SES/SNS, IAM, VPC) tailored for the Smart Healthcare Digital Platform.
* Analyze and select an appropriate architectural pattern for the application (Multi-tier Microservices on Docker), and design an overview Cloud Infrastructure Diagram following AWS Well-Architected Framework standards.
* Perform detailed analysis of the core **Business Flow** comprising 5 stages: System Setup, Patient Onboarding, 3-Level AI Triage, Overbooking Prevention Slot Booking, and Split View Consultation.
* Prepare local development environment (Local Environment) and initialize projects with Next.js 14 Responsive (Frontend) and NestJS (Backend).

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Overview research on cloud computing (IaaS, PaaS, SaaS) and benefits of deploying Healthcare Web Applications on Cloud.<br>- Analyze 3-Tier Web Architecture (Presentation - Application - Database) applied to the project. | 06/01/2026 | 06/01/2026 | [Here](<https://aws.amazon.com/what-is-cloud-computing/>) |
| Tue | - Research core AWS services: **AWS Cognito** (Auth & Temp Password), **EC2** (Docker Containers), **S3** (Prescription/AI Report Storage), **RDS PostgreSQL** (PostgreSQL 16.x), **SageMaker** (AI Triage Endpoint).<br>- Evaluate pros and cons of self-managing servers on EC2 vs. utilizing fully Managed Services. | 06/02/2026 | 06/02/2026 | [Here](<https://docs.aws.amazon.com/>) |
| Wed | - Research cloud information security solutions: Access management via **AWS IAM**, secure network partitioning via **AWS VPC** (Public/Private Subnets for Multi-AZ).<br>- Study healthcare data security standards (UUID encryption, JWT Token verification, Data At-Rest & In-Transit encryption). | 06/03/2026 | 06/03/2026 | [Here](<https://docs.aws.amazon.com/iam/>) |
| Thu | - Install development tools: **AWS CLI**, **Node.js**, **Docker Desktop**, **WSL 2**, configure AWS IAM account.<br>- Initialize GitHub Repository and set up project directory structure for Frontend (Next.js 14) and Backend (NestJS Framework). | 06/04/2026 | 06/04/2026 | [Here](<https://docs.aws.amazon.com/cli/>) |
| Fri | - Draft and render Cloud Infrastructure Architecture Diagram (**AWS Architecture Diagram**) for the Smart Healthcare Platform.<br>- Prepare Technical Requirements document and finalize detailed **Business Flow** (Admin Onboard Doctor, Initial Medical Declaration Form, 3-Level AI Triage, Bottom Sheet Booking, and Doctor Split View UI). | 06/05/2026 | 06/05/2026 | [Here](<https://aws.amazon.com/architecture/>) |


### Week 1 Achievements:

* Mastered Multi-tier Web Architecture, foundational cloud computing concepts, and core AWS services applied to Healthcare domain.
* Completed AWS Well-Architected Cloud Infrastructure Diagram (**AWS Architecture Diagram**), clearly defining deployment topologies for Public/Private Subnets, Load Balancers, Containers, and Databases.
* Finalized core Business Flow document covering 5 detailed stages from Onboarding, AI Triage to Consultation.
* Gained clear understanding of secure network partitioning (VPC, Public/Private Subnet) and access control/authorization via AWS IAM & Cognito.
* Successfully initialized local development environment and base repository structure for **Next.js 14** and **NestJS** integrated with GitHub.
