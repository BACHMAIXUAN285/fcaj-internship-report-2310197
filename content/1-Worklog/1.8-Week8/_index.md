---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Finalize containerization (Docker) and automate the deployment process onto AWS cloud infrastructure (AWS ECS/App Runner, EC2, RDS).
* Optimize patient check-in, reception, and direct payment collection features for Receptionists / Cashiers (eliminating online payment integrations).
* Prepare technical documentation, user manuals, and conduct final system acceptance testing.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Build Dockerfiles and docker-compose configurations for both NestJS Backend and Next.js Frontend.<br>- Set up CI/CD pipelines (GitHub Actions / AWS CodePipeline) to automate application build and deployment to AWS. | 20/07/2026 | 20/07/2026 | [Here](<https://docs.docker.com/>) |
| Tue | - Configure AWS production Cloud infrastructure: Set up Custom Domains, HTTPS/SSL certificates via AWS Certificate Manager (ACM) and Route 53.<br>- Configure AWS CloudWatch Logs and AWS SES/SNS for system monitoring and automated email/SMS appointment confirmations. | 21/07/2026 | 21/07/2026 | [Here](<https://docs.aws.amazon.com/>) |
| Wed | - Complete and optimize the Receptionist/Cashier Dashboard UI:<br>&emsp;+ Support fast appointment lookups via QR code or phone number.<br>&emsp;+ Streamline check-in verification and in-person service invoice/receipt issuance at the counter. | 22/07/2026 | 22/07/2026 | Internal Docs |
| Thu | - Conduct final system smoke testing in the Production environment.<br>- Optimize frontend build size and caching strategies to minimize cloud operational costs. | 23/07/2026 | 23/07/2026 | Internal Test |
| Fri | - Author final project documentation: Architecture Documentation, Deployment/Operations Manual, and User Guides for Doctors & Receptionists.<br>- Summarize project achievements and conduct final handover/acceptance. | 24/07/2026 | 24/07/2026 | Project Deliverables |


### Week 8 Achievements:

* Successfully containerized applications using Docker and established a 100% automated CI/CD pipeline for AWS deployment.
* The system is fully operational in the Production environment with HTTPS/SSL security, a official domain name, and active CloudWatch logging.
* Delivered a seamless on-site receptionist workflow: Patient lookup and in-person payment processing are fast and accurate, eliminating reliance on online third-party payment gateways.
* Automated appointment confirmation notifications (Email/SMS via AWS SES/SNS) function reliably and accurately.
* Completed a comprehensive technical documentation suite, user manuals, and successfully passed the final project acceptance review on schedule.
