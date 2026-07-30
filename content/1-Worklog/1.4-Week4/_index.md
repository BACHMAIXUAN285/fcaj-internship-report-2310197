---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Provision and integrate the **Amazon RDS (PostgreSQL)** relational database management system with data encryption to store structured data (account information, initial medical declaration profiles, doctor availability calendars, appointment schedules, and diagnosis/prescription results).
* Provision and configure the **Amazon DynamoDB** NoSQL database to store real-time AI Triage Chatbot conversation histories and pre-consultation medical summary reports.
* Establish a **Concurrency Control & Database Locking** mechanism (Row-level lock in PostgreSQL) on the NestJS Backend to handle race conditions and prevent double-booking when patients select appointment time slots.
* Configure secure network partitioning (VPC Private Subnet, DB Subnet Groups) and Security Groups for RDS to ensure the database is accessible only internally from the EC2 Backend server.
* Integrate an ORM (TypeORM/Prisma) into the NestJS Backend for Database Migration, connecting to and querying relational data on RDS, alongside the AWS SDK for DynamoDB.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Provision **Amazon RDS Instance (PostgreSQL)** on the AWS Console inside a Private Subnet.<br>- Configure DB Subnet Group, setup Admin credentials, enable storage encryption (At-Rest Encryption), and activate Automated Backups. | 06/22/2026 | 06/22/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Tue | - Provision tables on **Amazon DynamoDB** with optimal Partition Key/Sort Key for real-time querying.<br>- Configure Auto-Scaling/On-Demand Capacity mode to ensure minimum latency for AI Triage conversation read/write performance. | 06/23/2026 | 06/23/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Wed | - Configure **Security Group for RDS**: Accept Inbound Traffic exclusively from the EC2 Backend Security Group over port 5432.<br>- Build PostgreSQL Schema to store: Initial medical profiles (blood type, allergies), Doctor Availability Calendars, and Consultation Outcomes. Perform Data Migration. | 06/24/2026 | 06/24/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Thu | - Integrate ORM (Prisma/TypeORM) into NestJS Backend to connect to RDS PostgreSQL; implement **Database Transaction & Row-level Locking** mechanism to prevent double-booking.<br>- Integrate DynamoDB SDK into AI Chatbot Module to store conversation history and automatically retrieve aggregated Pre-consultation Report data. | 06/25/2026 | 06/25/2026 | [Here](<https://docs.nestjs.com/techniques/database>) |
| Fri | - Perform testing of CRUD operations on RDS PostgreSQL and DynamoDB from EC2 Backend; execute concurrency load testing to prevent double-booking when multiple patients book the same time slot.<br>- Optimize Connection Pooling (using PgBouncer or ORM pool config) and verify database access permissions via IAM / KMS. | 06/26/2026 | 06/26/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |


### Week 4 Achievements:

* Successfully deployed **Amazon RDS PostgreSQL** entirely within a Private Subnet with secure data encryption, ensuring absolute security for patient medical declarations and prescriptions.
* Successfully provisioned **Amazon DynamoDB** for storing AI Triage chat histories and Pre-consultation Reports with low millisecond latency.
* Completed Database Migration on PostgreSQL, clearly defining Doctor Availability Calendars and Patient Medical Profiles.
* Successfully applied **Row-level Lock / Transaction** mechanisms in the NestJS Backend, thoroughly resolving Race Condition (Double-booking) issues during concurrent appointment scheduling.
* Ensured infrastructure security via strict Security Group isolation (allowing connections to RDS exclusively from the EC2 Backend).
* Established a solid data foundation for the Doctor Portal (Split View mode: viewing AI summary reports alongside issuing prescriptions) and Patient Portal (checking examination results).
* Fully prepared complete DB and Backend infrastructure, ready for Week 5 integration of **AWS CloudWatch** monitoring and centralized error handling.
