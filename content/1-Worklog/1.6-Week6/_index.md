---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Develop advanced features: Connect the NestJS Backend with AI models hosted on Amazon SageMaker to analyze medical symptoms and generate Summary Reports.
* Integrate online payment gateways (PayOS / VNPay / Stripe) to handle deposit and basic consultation fee payment flows (`PREPAID`).
* Build Role-Based Access Control (RBAC) Dashboards for Doctors and Receptionists; refactor code structure and standardize RESTful APIs.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Integrate NestJS Backend with AI models running on **Amazon SageMaker Endpoint** <br> - Develop 3-level triage logic (Red - Yellow - Green) based on AI response payloads and handle user UI navigation flows | 06/07/2026 | 06/07/2026 | [Here](<https://docs.aws.amazon.com/sagemaker/>) |
| Tue | - Develop AI Pre-consultation Module: Automatically extract chat history for AI to summarize into a **medical-grade Summary Report** <br> - Attach reports to appointment records in the Database for delivery to the Doctor Portal | 07/07/2026 | 07/07/2026 | [Here](<https://docs.aws.amazon.com/sagemaker/latest/dg/realtime-endpoints.html>) |
| Wed | -- Integrate Online Payment Gateways (**PayOS / VNPay / Stripe**) into NestJS <br> - **Hands-on:** Develop APIs to initiate basic consultation fee transactions (`PREPAID`) and handle automated Webhook verification | 08/07/2026 | 08/07/2026 | [Here](<https://stripe.com/docs/api>) |
| Thu | - Build Healthcare Staff Portal with **Role-Based Access Control (RBAC)** mechanisms using NestJS Guards: <br>&emsp; + **Doctor Dashboard:** View appointment lists, read AI Summary Reports, submit final diagnoses, and issue prescriptions <br>&emsp; + **Receptionist Dashboard:** Check-in patients and generate invoices for secondary payments (`POSTPAID`) at the desk | 09/07/2026 | 09/07/2026 | [Here](<https://docs.nestjs.com/guards>) |
| Fri | - Refactor code structure, optimize Data Transfer Objects (DTOs), and validate incoming request payloads <br> - Standardize and bundle system API documentation using **Swagger / OpenAPI Spec** | 10/07/2026 | 10/07/2026 | [Here](<https://docs.nestjs.com/openapi/introduction>) |


### Week 6 Achievements:

* Successfully connected NestJS with **Amazon SageMaker Endpoint**, enabling symptom extraction from Chatbot conversations and automated generation of **medical-grade Summary Reports** to save doctors preparation time before consultations.
* Completed the 3-level emergency classification flow (Red: Emergency alert / 115 hotline — Green: Self-care advice — Yellow: Navigate to appointment scheduling).
* Successfully integrated online payment gateways (PayOS / VNPay / Stripe), automatically updating appointment status from `PENDING_PAYMENT` to `CONFIRMED` upon receiving Webhook signals.
* Developed complete RBAC interfaces and APIs: Doctors can review AI reports and record medical results; Receptionists can easily check-in patients and issue invoices for secondary costs/medications (`POSTPAID`) at the counter.
* Standardized all system APIs using **Swagger (OpenAPI)** and applied strict payload validation to all incoming requests, enhancing code reliability and maintainability.
