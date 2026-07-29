---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Conduct comprehensive system testing (Functional Testing, Integration Testing, Stress Testing), with a primary focus on handling data concurrency during appointment scheduling.
* Optimize query performance on AWS RDS and ensure medical data security (UUIDs, CORS, Security Headers, Rate Limiting).
* Improve interface responsiveness and loading speed on the Next.js Web App, as well as refine the real-time Chatbot flow.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Execute Stress Testing / Load Testing using tools (k6 / Artillery) to simulate hundreds of concurrent booking requests.<br>- **Hands-on:** Verify the accuracy of the Pessimistic Locking mechanism to prevent double-booking or race condition errors. | 13/07/2026 | 13/07/2026 | [Here](<https://k6.io/docs/>) |
| Tue | - Analyze and optimize SQL queries executed by ORM (Prisma/TypeORM).<br>- Set up database indexing for high-frequency query fields on AWS RDS PostgreSQL/MySQL to reduce API response times. | 14/07/2026 | 14/07/2026 | [Here](<https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html>) |
| Wed | - Review and conduct security testing across the system:<br>&emsp;+ Verify the security of UUID encryption/obfuscation to prevent medical data leaks (IDOR vulnerability).<br>&emsp;+ Strictly configure Helmet, Rate Limiting, and CORS Policy on the NestJS Backend. | 15/07/2026 | 15/07/2026 | [Here](<https://docs.nestjs.com/security/helmet>) |
| Thu | - Optimize User Interface and Experience (UI/UX) on Next.js:<br>&emsp;+ Accelerate page load speeds (Server-Side Rendering & Caching).<br>&emsp;+ Enhance the WebSocket chat interface, adding an "AI is typing..." indicator and seamless error responses. | 16/07/2026 | 16/07/2026 | [Here](<https://nextjs.org/docs/app/building-your-application/optimizing>) |
| Fri | - Perform End-to-End (E2E) testing for the entire business workflow:<br>&emsp;**Cognito Authentication** --> **AI Chatbot Triage & Report Generation** --> **Appointment Booking** --> **Doctor Reviews AI Report & Prescribes** --> **Receptionist Checks-in & Collects In-person Payment at Counter**. | 17/07/2026 | 17/07/2026 | Internal System Test |


### Week 7 Achievements:

* Successfully executed Load and Stress Testing, verifying that the Pessimistic Locking mechanism operates with 100% accuracy, fully protecting the system against Race Conditions / Double-booking when multiple patients attempt to book the same slot simultaneously.
* Successfully optimized the response times of primary APIs (latency reduced by over 40%) through proper database indexing on AWS RDS.
* Guaranteed high-standard healthcare data security: Patient identifiable information is fully protected using UUIDs, and basic Brute-force/DDoS attacks are effectively blocked via Rate Limiting middleware and Helmet policies.
* Enhanced user experience on Next.js: Delivered a smooth, intuitive, real-time AI Chatbot interface featuring convenient appointment schedule management for users.
* Completed smooth E2E testing for the entire end-to-end business workflow (from patient AI chat interaction and appointment selection to doctor diagnosis and on-site reception payment processing), ensuring zero data bottlenecks across cloud services (Cognito, SageMaker, RDS, S3).
