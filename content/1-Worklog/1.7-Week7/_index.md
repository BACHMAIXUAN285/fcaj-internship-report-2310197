---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Perform comprehensive system testing (Functional Testing, Integration Testing, Stress Testing).
* Optimize AWS RDS database query performance and ensure medical data security compliance (UUID, CORS, Security Headers).
* Improve User Experience (UX/UI) on the Next.js Web frontend and real-time Chatbot interface.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Perform load and stress testing using tools (k6 / Artillery) simulating hundreds of concurrent booking requests <br> - **Hands-on:** Verify the correctness of the Pessimistic Locking mechanism to prevent double-booking issues (Race Condition) | 13/07/2026 | 13/07/2026 | [Here](<https://k6.io/docs/>) |
| Tue | - Analyze and optimize SQL queries executed through ORMs (Prisma/TypeORM) <br> - Configure database Indexing on high-frequency query fields in AWS RDS PostgreSQL to reduce API response latency | 14/07/2026 | 14/07/2026 | [Here](<https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html>) |
| Wed | - Review and audit system-wide security configurations: <br>&emsp; + Validate UUID encryption to prevent unauthorized data exposure vulnerabilities (IDOR) <br>&emsp; + Configure Helmet, Rate Limiting, and strict CORS Policies on the NestJS Backend | 15/07/2026 | 15/07/2026 | [Here](<https://docs.nestjs.com/security/helmet>) |
| Thu | - Optimize Next.js Frontend User Interface and Experience (UI/UX): <br>&emsp; + Enhance page load speeds using Server-Side Rendering (SSR) & Caching <br>&emsp; + Refine the WebSocket chat interface by adding a "Typing Indicator" state and smooth error handling | 16/07/2026 | 16/07/2026 | [Here](<https://nextjs.org/docs/app/building-your-application/optimizing>) |
| Fri | - Conduct End-to-End (E2E) testing across all 6 business workflow steps: From Cognito Authentication --> Chatbot Triage --> Online Booking & Payment --> Doctor AI Report Review & Prescription --> Counter Payment Collection | 17/07/2026 | 17/07/2026 | Internal System Test |


### Week 7 Achievements:

* Successfully conducted Stress Testing, verifying that the Locking mechanism operates with 100% accuracy, completely safeguarding the system against Race Condition / Double-booking issues when multiple patients attempt to book the same appointment slot simultaneously.
* Successfully optimized response times for primary APIs (reducing latency by over 40%) through strategic indexing on AWS RDS MySQL tables.
* Ensured medical data security compliance: Masked patient identity details via UUID encryption and blocked brute-force/DDoS attack vectors using Middleware Rate Limiting and Helmet policies.
* Enhanced Next.js user experience: Delivered a smooth, real-time interactive Chatbot interface with typing indicators and intuitive appointment scheduling views.
* Completed seamless End-to-End testing for all core business flows, confirming no data bottlenecks or sync failures occurred across AWS Cloud services (Cognito, SageMaker, RDS, S3).
