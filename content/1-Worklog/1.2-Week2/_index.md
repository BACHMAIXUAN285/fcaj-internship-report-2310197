---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Design the database schema and build core module structures for the Backend (NestJS) of the Healthcare Web Application.
* Develop key RESTful APIs: Registration/Login (Authentication with JWT), Doctor Management, Appointment Booking, and Patient Record Management.
* Develop Frontend user interfaces (Next.js) for primary workflows: Homepage, Doctor/Specialty Search, and Appointment Booking forms.
* Integrate API connections between Frontend and Backend, handle CORS, synchronize data states (State Management), and containerize applications using Docker Compose for local development.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | --- | ---- | --- |
| Mon | - Design Entity-Relationship Diagrams (ERD) for the Healthcare application (Patients, Doctors, Time Slots, Appointments) <br> - Initialize Module, Controller, and Service structures in NestJS | 08/06/2026 | 08/06/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Tue | - Build the Authentication Module in NestJS (using Passport.js and JWT) for user identity verification <br> - Develop core RESTful APIs: Doctor Directory, Create New Appointment, Update Appointment Status | 09/06/2026 | 09/06/2026 | [Here](<https://docs.nestjs.com/>) |
| Wed | - Construct Web Application interfaces using Next.js and TailwindCSS <br> - Design functional pages: Doctor search homepage, Consultation service details page, Patient info form, and time-slot picker | 10/06/2026 | 10/06/2026 | [Here](<https://nextjs.org/docs>) |
| Thu | - Integrate API requests from Next.js to NestJS Backend using Axios/Fetch API <br> - Configure CORS middleware, access permission checks (Guards/Protected Routes), and secure token storage on the Client | 11/06/2026 | 11/06/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Fri | - Write Dockerfiles for Next.js Frontend and NestJS Backend applications <br> - Create docker-compose.yml file to package the entire application stack and run the complete web environment locally | 12/06/2026 | 12/06/2026 | [Here](<https://docs.docker.com/>) |


### Week 2 Achievements:

* Completed detailed database ERD diagrams for the Healthcare Web system, establishing clear data structures for patients and doctors.
* Successfully developed core Backend RESTful APIs in NestJS supporting secure JWT authentication and appointment scheduling logic.
* Completed responsive and interactive Web UI on the Frontend using Next.js, providing a smooth user experience for browsing and booking appointments.
* Successfully integrated end-to-end API calls from Frontend to Backend, seamlessly handling authorization flows and CORS rules.
* Containerized both Frontend and Backend applications with Docker Compose, preparing them for AWS Cloud deployment in Week 3.
