---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Conduct comprehensive system testing (Functional Testing, Integration Testing, Stress Testing), with a specific focus on handling data concurrency (Race Conditions) during patient appointment scheduling.
* Optimize AWS RDS database query performance and ensure the security of medical data (UUIDs, CORS, Security Headers, Rate Limiting).
* Improve speed and user experience on the Patient Portal (Next.js Mobile-first) as well as the real-time AI Triage & symptom screening chatbot flow.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Execute load/stress testing using tools (k6 / Artillery) to simulate hundreds of concurrent appointment booking requests.<br>- **Hands-on practice:** Verify the correctness of the database slot locking mechanism (Pessimistic Locking / Row-level Lock) to guarantee zero slot collision errors (Race Condition / Double-booking). | 07/13/2026 | 07/13/2026 | [Here](<https://k6.io/docs/>) |
| Tue | - Analyze and optimize SQL queries in the ORM (Prisma/TypeORM).<br>- Set up Indexing for high-frequency query fields in AWS RDS PostgreSQL to reduce API response latency. | 07/14/2026 | 07/14/2026 | [Here](<https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html>) |
| Wed | - Review and perform security testing across the entire system:<br>&emsp;+ Verify the security of using UUID encoding to prevent Insecure Direct Object Reference (IDOR) medical data leaks.<br>&emsp;+ Configure Helmet, Rate Limiting, and strict CORS policies on the NestJS Backend. | 07/15/2026 | 07/15/2026 | [Here](<https://docs.nestjs.com/security/helmet>) |
| Thu | - Optimize User Interface/User Experience (UI/UX) on Next.js Mobile View:<br>&emsp;+ Accelerate page load speeds (Server-Side Rendering & Caching).<br>&emsp;+ Optimize the WebSocket chat window, adding an "AI is typing..." indicator and smooth error feedback.<br>&emsp;+ Test the display of appointment recommendation cards (Card UI) and sliding time selectors (Bottom Sheet). | 07/16/2026 | 07/16/2026 | [Here](<https://nextjs.org/docs/app/building-your-application/optimizing>) |
| Fri | - Perform End-to-End (E2E) testing for the entire business workflow:<br>&emsp;**Cognito Authentication & Medical Declaration** --> **AI Triage Assistant & Report Generation** --> **Specialty Appointment Booking (Bottom Sheet)** --> **Doctor Portal (Split View AI Report Inspection)** --> **Doctor Diagnosis, Prescription & Data Push to Patient App**. | 07/17/2026 | 07/17/2026 | Internal System Test |


### Week 7 Achievements:

* Successfully conducted Stress Testing, verifying that the Slot Locking mechanism functions with 100% accuracy and fully protecting the system against Race Conditions / Double-booking when multiple patients attempt to book the same slot simultaneously.
* Successfully optimized main API response times (reducing latency by over 40%) through proper indexing on the AWS RDS database.
* Ensured medical data security standards: completely masked patient identifying information using UUID encoding and blocked basic Brute-force/DDoS attacks via Rate Limiting Middleware & Helmet Policies.
* Enhanced user experience on the Patient Portal: achieved smooth real-time Chatbot responses, dynamic display of specialty recommendation Card UI, and a convenient Bottom Sheet booking selector.
* Completed smooth E2E testing for the entire business flow (from initial patient AI chat and booking, to doctors reviewing standardized AI reports on the Doctor Portal Split View, and finalizing prescriptions synchronized to the patient app), ensuring data integrity across AWS services (Cognito, SageMaker, RDS, SES/SNS).
