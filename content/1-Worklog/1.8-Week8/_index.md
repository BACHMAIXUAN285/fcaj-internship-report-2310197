---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Finalize container packaging (Docker) and automate application deployment pipelines (CI/CD GitHub Actions) to **Amazon EC2** servers.
* Optimize and conduct final review testing for the entire application: **Admin Portal** (Doctor management, RBAC configuration), **Doctor Portal** (consultation lookups & opening Pre-consultation Reports from S3), and **Patient Portal** (appointment viewing & AI RAG consultation chat).
* Configure custom domain names, HTTPS/SSL security certificates, and optimize AWS Cloud infrastructure operational costs.
* Prepare technical documentation (Architecture Document), Swagger API documentation, and User Manuals for Administrators & Doctors; conduct final project hand-off and acceptance.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Construct optimized multi-stage build Dockerfiles and docker-compose configurations for both NestJS Backend and Next.js Frontend.<br>- Configure CI/CD pipelines (GitHub Actions) to automate Docker image builds and application deployment to AWS EC2 servers upon code pushes to the main branch. | 07/20/2026 | 07/20/2026 | [Here](https://docs.docker.com/) |
| Tue | - Configure AWS production cloud infrastructure: Set up Nginx Reverse Proxy, HTTPS/SSL, and install auto-renewing SSL certificates.<br>- Review **AWS CloudWatch Logs** combined with log integration from **Langfuse** to monitor server incidents and track LLM operational performance. | 07/21/2026 | 07/21/2026 | [Here](https://docs.aws.amazon.com/) |
| Wed | - Optimize portal management interfaces based on the new Business Flow:<br>&emsp;+ **Admin Portal (Desktop View):** Optimize Doctor onboarding/management flows, automated account role assignment via AWS Cognito (`cognito:groups`), and overview analytics viewing.<br>&emsp;+ **Doctor Portal (Desktop View):** Optimize daily consultation list interfaces and features to download/open **Pre-consultation Report** files saved in Amazon S3. | 07/22/2026 | 07/22/2026 | Internal Docs |
| Thu | - Perform a complete final system smoke test on Production (Production Smoke Test) ensuring connections between EC2, RDS PostgreSQL, Cognito, S3, AWS Bedrock KB, ViMQ, GPT-4o-mini, and Langfuse operate seamlessly.<br>- Optimize Next.js Frontend build sizes and caching mechanisms to minimize cloud operational expenses. | 07/23/2026 | 07/23/2026 | Internal Test |
| Fri | - Write system hand-off documentation: Architecture Document, Installation/Operation Guides, and User Manuals for Administrators (Admin Portal) & Doctors (Doctor Portal).<br>- Summarize the project, evaluate achievements, and execute final project acceptance. | 07/24/2026 | 07/24/2026 | Project Deliverables |


### Week 8 Achievements:

* Successfully packaged the application with Docker Containers and established a 100% automated CI/CD pipeline (GitHub Actions) for building & deploying the system to AWS EC2 servers.
* The system operates stably in Production with full HTTPS/SSL security certificates, secure VPC network connectivity, and AWS CloudWatch monitoring combined with Langfuse.
* Smoothly completed business flows across all Portals: Administrators provision and assign RBAC roles to Doctors seamlessly via Cognito; Doctors effortlessly look up daily consultation lists and quickly open AI summary consultation reports (Pre-consultation Reports) from Amazon S3.
* The anti-slot-conflict booking mechanism (Pessimistic Locking `FOR UPDATE` on RDS PostgreSQL) and AI RAG Chatbot router (LLM Intent Router + AWS Bedrock KB + GPT-4o-mini + ViMQ) perform with 100% accuracy.
* Completed the full technical documentation suite (Architecture Document, Swagger API Spec), operational user guides, and achieved project hand-off right on schedule.
