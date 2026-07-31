---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Design the ERD diagram for the relational database (PostgreSQL) and build the core Module structure for the NestJS Backend.
* Integrate **AWS Cognito SDK** into the Backend to handle the Authentication & Authorization flow for 3 role groups: Admin, Doctor, and Patient based on RBAC standards.
* Develop critical RESTful APIs according to Business Flow v2: Admin Doctor Onboarding API (account initialization & sending Temporary Passwords via SES), Patient Registration API (automatically assigning the `Patient` role), and Initial Medical Declaration Form API.
* Develop Responsive Frontend User Interfaces (Next.js 14) for the following flows: Doctor Portal (Temp Password login & mandatory first-time password change, availability scheduling) and Patient Mobile Web App (full-screen initial medical declaration form).
* Connect Frontend - Backend APIs, configure CORS, synchronize state (React Query), and containerize the application using Docker Compose for local deployment.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | --- | ---- | --- |
| Mon | - Design detailed ERD diagram for PostgreSQL (Patients, Medical Declarations, Doctors, Working Hours, Appointments).<br>- Initialize Module, Controller, and Service structures in NestJS (AuthModule, UserModule, DoctorModule, PatientModule). | 06/08/2026 | 06/08/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Tue | - Integrate **AWS Cognito SDK** into NestJS AuthModule: Write middleware to verify JWT Tokens using Cognito's Public Key.<br>- Build RESTful APIs for **Phases 1 & 2**: Admin creates Doctor account (sends Temporary Password via AWS SES), API for Doctors to change password on first login, and API for Patients to fill out the initial medical declaration form (age, blood type, underlying conditions, allergies). | 06/09/2026 | 06/09/2026 | [Here](<https://docs.nestjs.com/>) |
| Wed | - Build Next.js 14 & TailwindCSS Web interfaces standardized to Business Flow.<br>- Design **Doctor Portal (Desktop)**: First-time password change interface, weekly "Set Availability" screen.<br>- Design **Patient App (Mobile)**: Full-screen initial medical declaration form (Full-screen View). | 06/10/2026 | 06/10/2026 | [Here](<https://nextjs.org/docs>) |
| Thu | - Integrate API calls from Next.js 14 to NestJS Backend using Axios & React Query.<br>- Configure NestJS Guards/Middleware to verify JWT Tokens from Cognito, enforce role-based access control (Patient/Doctor/Admin), and handle CORS. | 06/11/2026 | 06/11/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Fri | - Write Dockerfiles for Next.js 14 Frontend and NestJS Backend applications.<br>- Integrate local PostgreSQL container to package and launch the entire application in the Local environment. | 06/12/2026 | 06/12/2026 | [Here](<https://docs.docker.com/>) |


### Week 2 Achievements:

* Successfully completed the ERD database schema for PostgreSQL, clearly defining tables storing sensitive medical records and doctor working schedules.
* Successfully built a standardized authentication system via **AWS Cognito**, smoothly handling the Temporary Password flow for medical personnel and automated Onboarding for patients.
* Completed Next.js 14 interfaces matching Business Flow requirements: Initial medical declaration form for Patients on Mobile and Account Activation/Availability Setup screens for Doctors on Desktop.
* Achieved smooth end-to-end API integration between Frontend and Backend, strictly enforcing RBAC authorization via Cognito Public Key verification.
* Successfully containerized the application stack with Docker Compose, ready for Cloud AWS infrastructure deployment in Week 3.
