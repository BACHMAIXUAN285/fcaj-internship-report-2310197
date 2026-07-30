---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Integrate **AWS CloudWatch** services to monitor performance, log activities across microservices/APIs, and maintain system logs for the entire Healthcare Web system.
* Conduct in-depth monitoring of the **AI Triage (AWS SageMaker)** workflow, **Concurrency Control (Row-level Lock)** transactions on RDS PostgreSQL, and authentication responses from Amazon Cognito.
* Configure automated alert mechanisms (**CloudWatch Alarms**) to detect early infrastructure failures, database overload, or high failure rates in AI Triage.
* Build a **Global Exception Filter** in NestJS for centralized error handling, safe fallback mechanisms for AI Bot/SES/SNS, and protection of user experience across both Patient and Doctor Portals.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- |--- | --- | --- | --- |
| Mon | - Research **AWS CloudWatch** services (Logs, Metrics, Alarms, Dashboards).<br>- Configure CloudWatch Agent on EC2 Instance to send logs from NestJS Backend, Next.js Web Server, and Chatbot WebSocket connections to CloudWatch Logs. | 06/29/2026 | 06/29/2026 | [Here](<https://docs.aws.amazon.com/cloudwatch/>) |
| Tue | - Integrate Logger libraries (Winston/Pino) into NestJS to record JSON-structured logs.<br>- Stream detailed logs to CloudWatch covering: AI Triage symptom screening flow (3 severity levels: Red/Green/Yellow), Doctor account provisioning via Cognito, RDS row-level locks during booking, and confirmation email dispatching (AWS SES/SNS). | 06/30/2026 | 06/30/2026 | [Here](<https://docs.nestjs.com/techniques/logger>) |
| Wed | - Set up **CloudWatch Alarms** for automated alerts when:<br>&emsp; + EC2/RDS PostgreSQL CPU/Memory utilization exceeds 80% or lock contention is too high.<br>&emsp; + Failure response rate or timeout from AI Triage (SageMaker) exceeds the threshold.<br>&emsp; + HTTP Status 5xx API error rate exceeds permissible levels.<br>- Visualize all metrics on a **CloudWatch Dashboard**. | 07/01/2026 | 07/01/2026 | [Here](<https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html>) |
| Thu | - Develop **Global Exception Filter** & **Http Exception Filter** in NestJS to catch errors centrally and mask sensitive error details.<br>- Implement safe Fallback scripts: If AI Triage is interrupted -> automatically redirect patients to direct appointment booking UI; if AWS SES/SNS fails -> queue notifications for later delivery. | 07/02/2026 | 07/02/2026 | [Here](<https://docs.nestjs.com/exception-filters>) |
| Fri | - Conduct comprehensive End-to-End Testing of the integrated operations flow with monitoring & error handling: Patient Registration -> Medical Declaration -> 3-branch AI Triage -> Appointment Booking with anti-double-booking -> Auto-generation of Pre-consultation Report -> Email Confirmation -> Doctor Split View review & Prescription finalization.<br>- Optimize performance and finalize acceptance of the complete AWS infrastructure and Healthcare Web application. | 07/03/2026 | 07/03/2026 | [Here](<https://docs.aws.amazon.com/ses/>) |


### Week 5 Achievements:

* Centralized and standardized all application logs (Next.js, NestJS) alongside AI Triage execution history on **AWS CloudWatch Logs**, facilitating effective debugging and data flow control.
* Successfully established **CloudWatch Alarms** to send immediate notifications via Email/SNS during server overload, database lock contention, or AI service outages.
* Completed **Global Exception Filters** and flexible Fallback strategies to maintain seamless user experience even during temporary disruptions of AI Triage or SES/SNS services.
* Optimized performance for sending automated appointment confirmation emails (AWS SES/SNS) and provisioning Doctor accounts with Temporary Passwords.
* Successfully delivered a visual **CloudWatch Dashboard**, enabling Admins to monitor real-time infrastructure health, AI Chatbot traffic, and successful appointment bookings.
* Successfully completed the full roadmap for AWS cloud infrastructure deployment and application integration aligned with Business Flow standards.
