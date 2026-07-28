---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Integrate AWS CloudWatch to monitor and log activities for the entire Healthcare Web Application.
* Set up automated alert mechanisms (CloudWatch Alarms) for early detection of infrastructure issues and application errors.
* Build Global Exception Filters in NestJS to prevent system crashes during failures, optimize stability, and integrate AWS SES/SNS for sending notifications.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- |--- | --- | --- | --- |
| Mon | - Research **AWS CloudWatch** services (Logs, Metrics, Alarms, Dashboards) <br> - Configure CloudWatch Agent on EC2 to stream NestJS Backend and Next.js Web Server logs to CloudWatch Logs | 29/06/2026 | 29/06/2026 | [Here](<https://docs.aws.amazon.com/cloudwatch/>) |
| Tue | - Integrate logging libraries (Winston/Pino) into NestJS for structured JSON logging <br> - Stream detailed payment transaction logs (Stripe/VNPay) and Chatbot WebSocket connection logs to CloudWatch Log Streams | 30/06/2026 | 30/06/2026 | [Here](<https://docs.nestjs.com/techniques/logger>) |
| Wed | - Configure **CloudWatch Alarms** to trigger automatic alerts when: <br>&emsp; + EC2/RDS CPU or Memory utilization exceeds 80% threshold <br>&emsp; + API HTTP Status 5xx error rate exceeds allowed thresholds <br> - Build a monitoring dashboard to visualize real-time system performance on CloudWatch | 01/07/2026 | 01/07/2026 | [Here](<https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html>) |
| Thu | - Develop **Global Exception Filters** and **Http Exception Filters** in NestJS for centralized error handling <br> - Implement graceful fallbacks for RDS database disconnection or payment gateway disruptions to ensure an uninterrupted user experience | 02/07/2026 | 02/07/2026 | [Here](<https://docs.nestjs.com/exception-filters>) |
| Fri | - Configure **AWS SES (Simple Email Service)** / **AWS SNS (Simple Notification Service)** <br> - **Hands-on:** Develop a module to automatically send appointment confirmation Emails/SMS containing check-in QR codes to patients upon successful booking | 03/07/2026 | 03/07/2026 | [Here](<https://docs.aws.amazon.com/ses/>) |


### Week 5 Achievements:

* Centralized and standardized all application logs (Next.js & NestJS) onto **AWS CloudWatch Logs**, significantly simplifying and accelerating debugging processes.
* Successfully configured **CloudWatch Alarms** paired with Email notifications to alert administrators when servers experience high load or spike in HTTP 5xx errors.
* Completed **Global Exception Filters** in the NestJS Backend to conceal sensitive system error details while returning user-friendly error messages to patients.
* Ensured high availability and system stability: The Chatbot and Web Application continue operating smoothly even during temporary third-party service outages (e.g., payment gateways).
* Successfully integrated **AWS SES/SNS** for automated appointment confirmation emails, attaching doctor details and appointment booking codes immediately after patients complete the basic consultation fee payment.
* Built a real-time Monitoring Dashboard enabling system administrators to track overall system health efficiently.
