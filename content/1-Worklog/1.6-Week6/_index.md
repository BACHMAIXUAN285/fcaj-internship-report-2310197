---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Connect the NestJS Backend with AI models hosted on Amazon SageMaker to analyze medical symptoms and automatically generate medical-grade Summary Reports.
* Build modules to handle appointment check-ins, on-site payment processing (Cash / Credit Card via POS at the reception desk), and invoice generation.
* Implement Role-Based Access Control (RBAC) Dashboards for Doctors and Receptionists; refactor code structure and standardize RESTful APIs.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Integrate NestJS Backend with AI models running on **Amazon SageMaker Endpoint**.<br>- Develop 3-level triage logic (Red - Yellow - Green) based on AI response payloads and handle user UI navigation flows. | 06/07/2026 | 06/07/2026 | [Here](<https://docs.aws.amazon.com/sagemaker/>) |
| Tue | - Develop AI Pre-consultation Module: Automatically extract chat history for AI to summarize into a **medical-grade Summary Report**.<br>- Attach reports to appointment records in the Database for delivery to the Doctor Portal. | 07/07/2026 | 07/07/2026 | [Here](<https://docs.aws.amazon.com/sagemaker/latest/dg/realtime-endpoints.html>) |
| Wed | - Design Database Schema and build the **In-Person Payment & Billing Module** in NestJS.<br>- **Hands-on:** Develop APIs for receiving appointment requests, creating invoices for counter payments, updating appointment statuses, and issuing billing receipts. | 08/07/2026 | 08/07/2026 | [Here](<https://docs.nestjs.com/techniques/database>) |
| Thu | - Build Healthcare Staff Portal with **Role-Based Access Control (RBAC)** mechanisms using NestJS Guards:<br>&emsp;+ **Doctor Dashboard:** View appointment lists, read AI Summary Reports, submit final diagnoses, and issue prescriptions.<br>&emsp;+ **Receptionist Dashboard:** Check-in patients, process direct payments (Cash / POS card reader) at the reception desk, and generate invoices. | 09/07/2026 | 09/07/2026 | [Here](<https://docs.nestjs.com/guards>) |
| Fri | - Refactor code structure, optimize Data Transfer Objects (DTOs), and validate incoming request payloads.<br>- Standardize and bundle system API documentation using **Swagger / OpenAPI Spec**. | 10/07/2026 | 10/07/2026 | [Here](<https://docs.nestjs.com/openapi/introduction>) |


### Week 6 Achievements:

* Successfully connected NestJS with **Amazon SageMaker Endpoint**, enabling symptom extraction from Chatbot conversations and automated generation of **medical-grade Summary Reports** to save doctors preparation time before consultations.
* Completed the 3-level triage classification flow:
   * **Red:** Emergency alert / Guidance for calling 115 hotline.
   * **Yellow:** Navigate patient to appointment scheduling.
   * **Green:** Provide self-care guidance.
* Completed the In-Person Payment & Billing Management Module for the clinic.
* Delivered APIs and UI features allowing Receptionists to check-in patients, process direct payments (Cash / POS terminal), automatically transition appointment status from `PENDING` to `CONFIRMED`/`COMPLETED`, and generate receipts.
* Implemented secure RBAC mechanism using NestJS Guards:
   * **Doctor Dashboard:** Review AI reports, update diagnostic results, and prescribe medication.
   * **Receptionist Dashboard:** Check-in patients, collect payments at the desk, and print invoice receipts.
* Standardized all system RESTful APIs using **Swagger (OpenAPI Spec)**.
* Refactored codebase and applied comprehensive DTO Validation to ensure system reliability, security, and maintainability.
