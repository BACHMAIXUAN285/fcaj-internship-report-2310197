---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Provision and integrate the relational database management system **Amazon RDS (PostgreSQL/MySQL)** to store structured data for the Healthcare Web Application (user information, appointment schedules, doctor details).
* Initialize and configure the NoSQL database **Amazon DynamoDB** to store high-frequency or flexible read/write data (Chatbot conversation history, user sessions).
* Configure secure network partitioning (VPC Private Subnet, Subnet Groups) and Security Groups for RDS to ensure the database is accessible exclusively from the EC2 Backend Server.
* Integrate an ORM (TypeORM/Prisma) into the NestJS Backend application to connect and query data from Amazon RDS, alongside the AWS SDK for DynamoDB.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Provision an **Amazon RDS Database Instance** (PostgreSQL/MySQL) via AWS Console in a Private Subnet <br> - Configure DB Subnet Group, setup Admin credentials, and enable Automated Backups feature | 22/06/2026 | 22/06/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Tue | - Create **Amazon DynamoDB Tables** (ChatHistory, UserSessions) with appropriate Partition Keys and Sort Keys <br> - Configure Auto-Scaling/On-Demand Capacity mode to optimize costs and processing performance for Chatbot data | 23/06/2026 | 23/06/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Wed | - Configure **RDS Security Group**: Restrict Inbound Traffic strictly to the EC2 Backend Security Group on port 5432 (PostgreSQL) or 3306 (MySQL) <br> - Perform database migration from local database to Amazon RDS | 24/06/2026 | 24/06/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Thu | - Integrate ORM (Prisma/TypeORM) into NestJS Backend to connect with Amazon RDS <br> - Integrate AWS DynamoDB SDK into the NestJS Chatbot Module to store and retrieve real-time patient-chatbot conversation history | 25/06/2026 | 25/06/2026 | [Here](<https://docs.nestjs.com/techniques/database>) |
| Fri | - Conduct CRUD operations testing on both RDS and DynamoDB from Staging/EC2 environment <br> - Verify Connection Pooling performance and Encryption At-Rest (AWS KMS) across both database systems | 26/06/2026 | 26/06/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |


### Week 4 Achievements:

* Successfully deployed **Amazon RDS** isolated within a Private Subnet, guaranteeing absolute security for healthcare databases and protecting against direct Internet attacks.
* Successfully initialized **Amazon DynamoDB** for storing Chatbot message histories and user sessions with ultra-fast responsiveness (millisecond latency).
* Completed Database Schema Migration and seamlessly connected the NestJS Backend application on EC2 to Amazon RDS using an ORM library.
* Ensured strict security configuration via Security Groups that follow the principle of least privilege (only the EC2 Backend is allowed to access RDS).
* Enabled patients to chat with the Chatbot and retrieve conversation history while securely preserving appointment data integrity on the AWS Cloud.
* Fully prepared the data layer and complete application infrastructure, setting the stage for Week 5 integration with **AWS CloudWatch** monitoring and centralized log handling.
