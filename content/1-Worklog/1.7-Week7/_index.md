---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Conduct comprehensive system testing (Functional Testing, Integration Testing, Stress Testing), with a specific focus on testing data concurrency conflict resolution (Race Condition) when patients book identical appointment slots.
* Optimize query performance on the AWS RDS PostgreSQL database (`healthcare-db`) and guarantee healthcare data privacy and security (anonymous UUIDs, CORS, Security Headers, Rate Limiting).
* Improve speed and UI/UX responsiveness on the Patient Portal (Next.js Mobile View) alongside real-time chat performance with the AI RAG Consultation Assistant (LLM Router + Bedrock KB + GPT-4o-mini + ViMQ).

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Execute stress and load testing (Stress Testing / Load Testing) using tools (k6 / Artillery) simulating hundreds of concurrent booking requests.<br>- **Hands-on:** Verify the correctness of the **Pessimistic Locking (`FOR UPDATE`)** mechanism in PostgreSQL to ensure no slot conflict errors occur (Race Condition / Double-booking). | 07/13/2026 | 07/13/2026 | [Here](https://k6.io/docs/) |
| Tue | - Analyze and optimize SQL statements in Prisma ORM.<br>- Establish Indexing on high-frequency query fields (user UUIDs, doctor IDs, appointment status) in AWS RDS PostgreSQL to reduce API response latency. | 07/14/2026 | 07/14/2026 | [Here](https://www.postgresql.org/docs/current/indexes.html) |
| Wed | - Review and security-test the entire system:<br>&emsp;+ Verify the security of using anonymous UUID identifiers (Anonymization) from Cognito to prevent personal data exposure risks.<br>&emsp;+ Configure strict Helmet policies, Rate Limiting, and CORS Policies on the NestJS Backend. | 07/15/2026 | 07/15/2026 | [Here](https://docs.nestjs.com/security/helmet) |
| Thu | - Optimize User Interface / User Experience (UI/UX) on Next.js Mobile View:<br>&emsp;+ Accelerate page loading speeds (Server-Side Rendering & Caching).<br>&emsp;+ Optimize consultation RAG chat frames, adding a "Typing Indicator..." state and graceful connection loss handling.<br>&emsp;+ Test viewing open Doctor working slot lists and time-slot selection. | 07/16/2026 | 07/16/2026 | [Here](https://nextjs.org/docs/app/building-your-application/optimizing) |
| Fri | - Perform End-to-End (E2E Testing) flow verification for the entire business lifecycle:<br>&emsp;**Cognito Auth & Medical Onboarding** --> **AI RAG Chatbot Consultation (Bedrock KB + GPT-4o-mini + ViMQ) & S3 Report Saving** --> **LLM Monitoring via Langfuse** --> **Specialist Appointment Booking** --> **Doctor Portal Schedule Lookup & AI Report Viewing from S3**. | 07/17/2026 | 07/17/2026 | Internal System Test |


### Week 7 Achievements:

* Successfully conducted stress testing (Stress Testing) using k6, verifying that the **Pessimistic Locking (`FOR UPDATE`)** mechanism operates with 100% precision, completely protecting the system against Race Condition / Double-booking issues when multiple patients attempt to book the same slot simultaneously.
* Successfully optimized response times for key APIs (reducing latency by over 40%) through strategic index creation on the AWS RDS PostgreSQL database.
* Guaranteed healthcare security compliance standards: Fully anonymized patient identity information via Cognito UUIDs, while mitigating basic Brute-force/DDoS attack vectors using Rate Limiting Middleware & Helmet policies.
* Optimized user experiences on the Patient Portal: The AI RAG Consultation Chatbot interface responds smoothly with robust real-time communication support.
* Completed flawless E2E testing for the entire business workflow (from patient AI chat, Pre-consultation Report archiving to Amazon S3, slot booking, up to Doctor schedule lookups on the Doctor Portal), ensuring data synchronization without errors across services (Cognito, AWS Bedrock KB, GPT-4o-mini, ViMQ, Langfuse, RDS, S3, CloudWatch).
