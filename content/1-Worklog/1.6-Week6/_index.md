---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Integrate the **AWS CloudWatch** service combined with **Langfuse** for monitoring (Monitoring), system performance tracking (CPU/Memory on EC2, RDS PostgreSQL), and centralizing system operational logs as well as LLM operational logs.
* Complete the **Admin Portal** interface (for Administrators) serving Doctor personnel management, user account management (Cognito RBAC), and operational analytics reporting.
* Complete the **Doctor Portal** interface optimized for lookup workflows: Allowing Doctors to review daily booked appointment schedules and open AI conversation summary reports (Pre-consultation Reports) from Amazon S3.
* Complete the **Patient Portal (Mobile View)** interface: Supporting updates for personal medical information, consultation chats with the AI RAG Chatbot (LLM Router + Bedrock KB + GPT-4o-mini), and appointment slot selection.
* Refactor source code, standardize API documentation using **Swagger / OpenAPI Spec**, and finalize overall application packaging.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Install the **AWS CloudWatch Logs Agent** on EC2 to collect logs from the NestJS Backend and Next.js Frontend. <br>- Integrate synchronized LLM monitoring logs from **Langfuse** into CloudWatch Logs; configure **CloudWatch Alarms** to trigger automated alerts when EC2 CPU/RAM exceeds 80% or when data lock conflicts occur on RDS PostgreSQL. | 07/06/2026 | 07/06/2026 | [Here](https://docs.aws.amazon.com/cloudwatch/) |
| Tue | - Complete the **Admin Portal** (Desktop UI): Build interfaces to add/manage Doctor accounts (assigning Cognito `Doctor` group), view user lists, and track total appointment statistics. <br>- Build interfaces for Patients to update personal medical information (blood type, underlying conditions, allergies). | 07/07/2026 | 07/07/2026 | [Here](https://docs.nestjs.com/techniques/database) |
| Wed | - Complete the **Doctor Portal** (Desktop UI): Build screens to view appointment lists booked by patients, enabling them to open **Pre-consultation Report** consultation files from Amazon S3 via Presigned URLs. | 07/08/2026 | 07/08/2026 | [Here](https://docs.nestjs.com/guards) |
| Thu | - Complete the **Patient Portal** (Mobile View): Optimize the chat interface with the consultation AI RAG Chatbot (displaying typing indicator, generated answers from GPT-4o-mini) and the slot selection interface based on Doctor open working hours. | 07/09/2026 | 07/09/2026 | [Here](https://nextjs.org/docs) |
| Fri | - Refactor Backend/Frontend code structures and add Validation DTOs for all API endpoints. <br>- Standardize and auto-generate RESTful API documentation using **Swagger / OpenAPI Spec** (`@nestjs/swagger`); execute complete End-to-End system testing. | 07/10/2026 | 07/10/2026 | [Here](https://docs.nestjs.com/openapi/introduction) |


### Week 6 Achievements:

* Successfully deployed the **AWS CloudWatch** monitoring system combined with **Langfuse**, centralizing log collection and configuring Alarms to detect early infrastructure incident risks as well as anomalies in the AI response stream.
* Completed the **Admin Portal**, enabling Administrators to effortlessly manage the Doctor directory, assign Cognito account roles, and monitor operational metrics.
* Successfully built a lean **Doctor Portal** interface, helping Doctors easily manage daily appointment schedules and review AI RAG-summarized patient inquiry reports prior to consultation sessions.
* Constructed a mobile-friendly **Patient Portal** interface: supporting personal information declarations, medical AI RAG Chatbot consultations, and transparent appointment bookings.
* Packaged and standardized all system RESTful API documentation using **Swagger (OpenAPI Spec)**.
* Reviewed and refactored the entire codebase, ensuring the system runs securely, reliably, and fully compliant with Business Flow designs.
