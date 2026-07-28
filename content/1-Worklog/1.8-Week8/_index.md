---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Package and verify the complete application across the Production Cloud environment.
* Finalize the comprehensive technical documentation suite (Database ERD Diagram, Swagger API Specifications, AWS Cloud Architecture Document).
* Construct an End-to-End Demo script, summarize outcomes, and evaluate final achievements for the Healthcare Web Application project.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Audit and review all AWS infrastructure configurations (EC2, RDS, S3, CloudWatch, Cognito) <br> - Ensure environment variables (.env) and SSL/HTTPS certificates operate reliably in the Production environment | 20/07/2026 | 20/07/2026 | [Here](<https://docs.aws.amazon.com/ec2/>) |
| Tue | - Standardize and synthesize project technical documentation: <br>&emsp; + Entity-Relationship Diagram (ERD) design in RDS PostgreSQL <br>&emsp; + High-level Cloud-native System Architecture Diagram <br>&emsp; + Bundle Postman Collections / Swagger API Specs for all modules | 21/07/2026 | 21/07/2026 | [Here](<https://swagger.io/docs/specification/about/>) |
| Wed | - Build a complete End-to-End Demo script matching the 6-step Business Workflow: <br>&emsp; 1. Registration/Login via AWS Cognito <br>&emsp; 2. Chatbot AI medical symptom triage <br>&emsp; 3. Appointment scheduling & Online fee payment (`PREPAID`) <br>&emsp; 4. Doctor reviews AI Summary Report on the Portal <br>&emsp; 5. Doctor submits final diagnosis & issues prescription <br>&emsp; 6. Receptionist check-in & secondary invoice billing (`POSTPAID`) at the counter | 22/07/2026 | 22/07/2026 | [Here](<https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html>) |
| Thu | - Conduct dry-run Demo rehearsals, record product demonstration videos, and prepare presentation for project final defense | 23/07/2026 | 23/07/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Fri | - Summarize 8-week internship deliverables, evaluate technical goal completion rates, and propose future feature enhancement roadmaps | 24/07/2026 | 24/07/2026 | Project Final Report |


### Week 8 Achievements:

* Successfully deployed and packaged the entire Healthcare Web Application on AWS Cloud, ensuring high availability and robust security via SSL/HTTPS.
* Completed standardized technical documentation including the Database ERD diagram, AWS Cloud Architecture map, and interactive Swagger API documentation.
* Developed and executed a seamless End-to-End Demo script, proving the feasibility and fluidity of the 6-step core Business Flow.
* Evaluated the project as having met all target technical standards:
  * Secure identity authentication via **AWS Cognito**.
  * Automated symptom triage and medical Summary Report generation using **Amazon SageMaker**.
  * Complete prevention of double-booking issues (Race Condition) on **AWS RDS MySQL** via Row-level Locks.
  * Flexible two-stage payment integration (`PREPAID` online and `POSTPAID` at the counter).
  * Centralized system health monitoring and logging through **AWS CloudWatch**.
* Successfully met the 8-week project milestone schedule, fully prepared for final project acceptance and defense.
