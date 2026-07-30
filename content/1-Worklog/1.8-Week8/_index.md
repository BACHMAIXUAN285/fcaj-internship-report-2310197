---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Finalize container packaging (Docker) and automate the application deployment workflow onto AWS infrastructure (AWS ECS/App Runner, EC2, RDS).
* Complete and optimize the Admin Portal (Doctor Onboarding, schedule management) and Doctor Portal (Split View AI Report, consultation conclusion & prescription delivery) strictly aligned with Business Flow standards.
* Prepare technical documentation, user manuals for Hospitals & Doctors, and conduct full system acceptance testing.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Build Dockerfiles and docker-compose configurations for both NestJS Backend and Next.js Frontend.<br>- Configure CI/CD pipelines (GitHub Actions / AWS CodePipeline) to automate building and deploying the application onto AWS. | 07/20/2026 | 07/20/2026 | [Here](<https://docs.docker.com/>) |
| Tue | - Configure AWS Production Cloud Infrastructure: Set up Domain name, HTTPS/SSL via AWS Certificate Manager (ACM) and Route 53.<br>- Set up CloudWatch Logs and AWS SES/SNS to monitor system operations, automate temporary password emails for Doctors, and dispatch appointment confirmation Emails/SMS to Patients. | 07/21/2026 | 07/21/2026 | [Here](<https://docs.aws.amazon.com/>) |
| Wed | - Optimize system administration portals according to the designed Flow:<br>&emsp;+ **Admin Portal (Desktop/Tablet):** Optimize Doctor onboarding workflow, automated account provisioning via AWS Cognito (Email Temporary Password), and Availability Calendar setup.<br>&emsp;+ **Doctor Portal (Desktop):** Optimize Split View interface (AI Summary Report + Diagnostic Form) and instant push delivery of consultation results/prescriptions to the Patient Mobile App. | 07/22/2026 | 07/22/2026 | Internal Docs |
| Thu | - Conduct final system-wide dress rehearsal testing in the Production environment (Staging/Production Smoke Test).<br>- Optimize frontend build size and memory caching to minimize cloud operational costs. | 07/23/2026 | 07/23/2026 | Internal Test |
| Fri | - Write system handover documentation: System Architecture Document, Installation & Operations Guide, and User Manuals for Hospital Administrators (Admin Portal) & Doctors (Doctor Portal).<br>- Conclude project, evaluate achieved results, and complete project acceptance sign-off. | 07/24/2026 | 07/24/2026 | Project Deliverables |


### Week 8 Achievements:

* Successfully containerized applications using Docker and set up a CI/CD pipeline, achieving 100% automated deployment onto AWS cloud infrastructure.
* System operates stably in the Production environment with complete HTTPS/SSL security certificates, official domain routing, and active CloudWatch system monitoring.
* Perfectly finalized Desktop Portal business flows: Administrators smoothly onboard/assign roles to Doctors and configure availability calendars; Doctors effectively utilize summarized AI Reports (Split View) and push diagnoses/prescriptions to Patient Mobile Apps instantly.
* Automated Email/SMS dispatching for appointment confirmations and account activations via AWS SES/SNS/Cognito operates reliably and accurately.
* Completed a full suite of technical documentation, operational user manuals, and successfully handed over the project on schedule.
