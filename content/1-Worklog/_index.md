---
title: "Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

This page summarizes the complete worklog throughout the research, design, and development lifecycle of the **Smart Healthcare AI Assistant & Appointment Booking Platform** on the AWS Cloud platform combined with Hybrid AI Services. The project was completed over an **8-week** period, strictly adhering to Cloud-native design principles, the RAG Pipeline, and business flows across the following detailed milestones:

**Week 1:** [Business Flow Requirements Analysis & Design of Hybrid AI System Architecture, Database ERD](1.1-week1/)

**Week 2:** [Initialization of Base Source Code (Responsive Next.js + NestJS REST API, WebSocket & LLM Intent Router)](1.2-week2/)

**Week 3:** [AWS Cognito Configuration (RBAC Authorization for Patient, Doctor, Admin) & Amazon S3 Integration](1.3-week3/)

**Week 4:** [AWS RDS PostgreSQL Database Deployment (`db.t4g.micro`) & Pessimistic Locking Implementation to Prevent Slot Conflicts](1.4-week4/)

**Week 5:** [RAG Pipeline Integration (AWS Bedrock Knowledge Base, ViMQ, GPT-4o-mini), Langfuse Monitoring & Pre-consultation Report Generation](1.5-week5/)

**Week 6:** [System Monitoring with AWS CloudWatch, Completion of Doctor Portal (Schedule & AI Report Lookup) & Patient Mobile App](1.6-week6/)

**Week 7:** [Security Testing (UUID Anonymization), k6 Stress Testing for Concurrent Booking Race Conditions](1.7-week7/)

**Week 8:** [Docker Container Packaging, GitHub Actions CI/CD Configuration to AWS EC2, Project Summary & Final Hand-off](1.8-week8/)
