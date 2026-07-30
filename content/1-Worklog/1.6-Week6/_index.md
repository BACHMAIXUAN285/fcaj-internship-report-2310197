---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Connect the NestJS Backend to the AI model hosted on **Amazon SageMaker Endpoint** to analyze medical symptoms and automatically generate **Pre-consultation Reports**.
* Finalize the **Admin Portal** interface (for Hospital Administrators) to manage personnel, automatically dispatch temporary passwords via AWS SES/Cognito, and configure Doctor Availability Calendars.
* Finalize the **Doctor Portal (Split View UI)** interface, supporting doctors in viewing summarized AI reports alongside the diagnostic/prescription entry form.
* Finalize the **Patient Portal (Mobile UI)** interface, supporting initial medical declarations (Full-screen UI), 3-tier AI Triage communication, and specialty appointment scheduling via a sliding selector (Bottom Sheet UI).
* Refactor source code, standardize API documentation using **Swagger / OpenAPI Spec**, and complete full project packaging.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Integrate NestJS Backend with **Amazon SageMaker Endpoint**.<br>- Program logic to classify 3 risk levels based on JSON returned from AI: **Red** (Disable chat + display large "Call 115" button), **Green** (Provide home self-monitoring guidelines), **Yellow** (Display UI Card directing to the appropriate specialty for examination). | 07/06/2026 | 07/06/2026 | [Here](<https://docs.aws.amazon.com/sagemaker/>) |
| Tue | - Build **AI Pre-consultation Report** Module: Automatically extract chatbot conversation logs for AI to summarize into pre-consultation medical reports.<br>- Attach reports to appointment IDs in PostgreSQL/DynamoDB databases to push onto the Doctor Dashboard. | 07/07/2026 | 07/07/2026 | [Here](<https://docs.aws.amazon.com/sagemaker/latest/dg/realtime-endpoints.html>) |
| Wed | - Build **Admin Portal** (Desktop UI): Develop new Doctor onboarding feature (automatically calling Cognito API to send temporary password emails) and weekly Availability Calendar setup interface.<br>- Build **Initial Medical Declaration form (Full-screen view)** on the Patient Portal to store blood type, underlying conditions, and allergies. | 07/08/2026 | 07/08/2026 | [Here](<https://docs.nestjs.com/techniques/database>) |
| Thu | - Finalize **Doctor Portal** applying NestJS Guard & RBAC: Design **Split View** layout (One side displaying past records + AI summary report; the other side featuring diagnosis and prescription entry forms).<br>- Finalize **Patient Booking** flow: Design **Bottom Sheet** sliding UI to select examination date/time slots from doctor availability calendars, and automatically receive electronic prescriptions/diagnoses on Mobile. | 07/09/2026 | 07/09/2026 | [Here](<https://docs.nestjs.com/guards>) |
| Fri | - Refactor code structure, optimize DTOs, and add strict validation for all input data.<br>- Standardize and package RESTful API documentation using **Swagger / OpenAPI Spec**; perform End-to-End system test runs. | 07/10/2026 | 07/10/2026 | [Here](<https://docs.nestjs.com/openapi/introduction>) |


### Week 6 Achievements:

* Successfully connected NestJS Backend with **Amazon SageMaker Endpoint**, accurately classifying 3 risk levels (Red, Green, Yellow) and automatically generating **Pre-consultation Reports**.
* Finalized **Admin Portal** supporting administrators in creating Doctor accounts (sending temporary password emails via AWS SES/Cognito) and flexibly configuring working availability schedules.
* Successfully built **Doctor Portal** featuring an optimized **Split View** design, enabling doctors to instantly review AI summaries without reading through verbose chat histories before entering diagnoses/prescriptions.
* Built **Patient Portal Mobile-friendly** interface: supporting initial Medical Declaration forms, seamless appointment booking via Bottom Sheet sliding UI, and instant delivery of electronic prescriptions.
* Packaged and standardized all system RESTful API documentation using **Swagger (OpenAPI Spec)**.
* Reviewed and refactored the entire codebase, ensuring secure, reliable operations aligned with designed Business Flow standards.
