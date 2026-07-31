---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Design the ERD diagram for the relational database (PostgreSQL) and construct core Module structures for the NestJS Backend (including the **LLM Intent Router** Module for the AI suite).
* Integrate the **AWS Cognito SDK** into the Backend to handle authentication and authorization flows (Authentication & Authorization) for 3 role groups: Admin, Doctor, and Patient following RBAC standards (verifying `cognito:groups` via JWKS).
* Develop key RESTful APIs adhering to the new Business Flow: Account Registration / Login APIs, Patient Initial Medical Intake Form API, and Doctor Directory / Work Schedule Management APIs.
* Develop Responsive user interfaces on the Frontend (Next.js) for the flows: Doctor Portal (login, appointment viewing, and work schedule slot management) and Patient Mobile Web App (initial medical intake form & AI chat frame).
* Connect Frontend - Backend APIs, handle CORS, synchronize application state (React Query), and containerize the application using Docker Compose for local execution.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | --- | ---- | --- |
| Mon | - Design detailed ERD diagram for PostgreSQL (Patients, Medical Intake Forms, Doctors, Working Slots, Appointments).<br>- Initialize Module, Controller, and Service structures in NestJS (AuthModule, UserModule, DoctorModule, PatientModule, LlmModule). | 06/08/2026 | 06/08/2026 | [Here](https://cloudjourney.awsstudygroup.com/) |
| Tue | - Integrate **AWS Cognito SDK** into NestJS AuthModule: Write Passport JWT Strategy to automatically verify Tokens via Cognito's JWKS Public Key.<br>- Build RESTful APIs for **Phases 1 & 2**: Registration/Login APIs (Cognito User Pool), Patient Initial Medical Intake Form API (age, blood type, underlying conditions, allergies), and Doctor Work Schedule Configuration API. | 06/09/2026 | 06/09/2026 | [Here](https://docs.nestjs.com/) |
| Wed | - Build Web Next.js & TailwindCSS interfaces standardized around the new Business Flow.<br>- Design **Doctor Portal (Desktop View)**: Weekly Working Schedule Management / Setup view, Appointment Schedule Viewing interface.<br>- Design **Patient App (Mobile View)**: Initial Medical Intake Form and medical consultation chat interface. | 06/10/2026 | 06/10/2026 | [Here](https://nextjs.org/docs) |
| Thu | - Integrate API calls from Next.js to NestJS Backend using Axios & React Query.<br>- Configure NestJS Guards/Middleware to check JWT Tokens from Cognito, handle RBAC authorization (Patient/Doctor/Admin), and configure CORS. | 06/11/2026 | 06/11/2026 | [Here](https://cloudjourney.awsstudygroup.com/) |
| Fri | - Write Dockerfiles for both Next.js Frontend and NestJS Backend applications.<br>- Integrate local PostgreSQL container via Docker Compose to package and run the entire application in a Local environment. | 06/12/2026 | 06/12/2026 | [Here](https://docs.docker.com/) |


### Week 2 Achievements:

* Completed the PostgreSQL ERD database schema, clearly defining tables storing sensitive medical information, anonymous account profiles (UUID), and doctor working schedules.
* Successfully built a centralized authentication system via **AWS Cognito**, handling smooth Registration/Login flows and automatic RBAC authorization for roles (Patient, Doctor, Admin).
* Completed Next.js interfaces tailored to the Business Flow: Mobile initial medical intake form / AI chat frame for Patients and Desktop working schedule management / appointment list views for Doctors.
* Integrated smooth end-to-end connections between Frontend and Backend, enforcing strict RBAC authorization via Cognito's JWKS Endpoint verification.
* Successfully containerized the system with Docker Compose, preparing it for the AWS Cloud infrastructure deployment and AI service integration steps in upcoming weeks.
