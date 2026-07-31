---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Deploy the Healthcare Web application onto AWS cloud infrastructure using a combination of **Amazon EC2** for compute servers and **Amazon S3** for object storage (doctor avatars, medical records, QR codes).
* Configure **Amazon Cognito** to handle authentication and role-based authorization (Admin, Doctor, Patient) aligned with the Business Flow.
* Integrate **Amazon S3** into the Backend (NestJS) to manage the uploading/downloading of medical documents, and integrate **AWS SES/SNS** to send notifications and temporary passwords.
* Set up **AWS API Gateway** (or Nginx Reverse Proxy on EC2) to route incoming requests, apply Rate Limiting, and secure Backend APIs.
* Perform integration testing for the **AI Triage (Symptom Screening Assistant)** flow and the automated generation of the **Pre-consultation Report**, delivering it to the Doctor Portal.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Initialize **EC2 Instance** (Ubuntu/Linux) on AWS Console and create a Key Pair for SSH access.<br>- Configure **Security Group** to allow Inbound access for SSH (22), HTTP (80), and HTTPS (443) ports. | 06/15/2026 | 06/15/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Tue | - Set up runtime environment on EC2: Install Docker, Docker Compose, Git, and Node.js.<br>- Pull application source code from GitHub to EC2 and execute application deployment (Next.js & NestJS) using Docker Containers. | 06/16/2026 | 06/16/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Wed | - Configure **Amazon Cognito User Pools & Client Roles** for role-based access control (Admin, Doctor, Patient) and manage the Doctor account provisioning flow with temporary passwords.<br>- Create **S3 Bucket** for medical media storage, configure access policies (Bucket Policy, CORS), and integrate with NestJS Backend. | 06/17/2026 | 06/17/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Thu | - Set up **Nginx Reverse Proxy / AWS API Gateway** to route traffic from public domain to Backend services and configure rate limiting.<br>- Integrate **AWS SES/SNS** services to send automated emails for Doctor account activation and appointment confirmation notifications for Patients. | 06/18/2026 | 06/18/2026 | [Here](<https://docs.aws.amazon.com/apigateway/>) |
| Fri | - Conduct integration testing for the **AI Triage** flow across 3 severity levels (Red - Emergency, Green - Self-monitoring, Yellow - Book Appointment) and automated generation of **Pre-consultation Reports**.<br>- Test end-to-end connectivity between Frontend (Next.js) and Backend (NestJS) on EC2 and S3; verify security policies of IAM Role attached to the EC2 Instance. | 06/19/2026 | 06/19/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |


### Week 3 Achievements:

* Successfully launched and configured the **Amazon EC2** server, smoothly setting up security rules via Security Groups.
* Packaged and deployed the Healthcare Web Application (Next.js & NestJS) to operate stably on the EC2 server environment via Docker Containers.
* Completed **Amazon Cognito** configuration supporting role management according to Business Flow (auto-assigning Patient role upon registration; managing Doctor account activation via Temporary Passwords).
* Successfully integrated **Amazon S3** into the Backend system, enabling secure storage of doctor photos, medical records, and check-in QR codes.
* Successfully integrated **AWS SES/SNS** to automate sending temporary passwords via email for Doctors and appointment booking notifications for Patients.
* Tested end-to-end flow for **3-tier AI Triage** and automated summary mechanism for **Pre-consultation Reports** displayed in Split View on the Doctor Portal prior to consultation sessions.
* Established an API Gateway / Nginx proxy entry point to manage traffic routing, rate limit requests, and enhance security for Backend services.
* Applied **IAM Roles for EC2 Instance** to interact securely with S3/SES without hardcoding Access Keys inside source code.
* Prepared compute and static storage infrastructure ready for Cloud Database integration in Week 4.
