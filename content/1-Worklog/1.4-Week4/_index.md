---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Initialize and integrate the relational database management system **Amazon RDS (PostgreSQL)** featuring secure data encryption located within a Private Subnet to store structured data (anonymized account info by UUID, initial medical intake profiles, doctor working schedules, and appointment details).
* Configure the RDS instance on the `db.t4g.micro` server class (AWS Graviton2 ARM) to achieve Cost Optimization and enforce transit encryption with an SSL certificate (`global-bundle.pem`).
* Implement **Pessimistic Locking (`FOR UPDATE`)** mechanisms and Database Transactions on the NestJS Backend (Prisma ORM) to resolve anti-slot-conflict challenges (Race Conditions/Double-booking) during patient appointment bookings.
* Configure secure network partitioning (VPC Private Subnet, Security Groups) for RDS to ensure the database safely accepts internal connections from the EC2 Backend Server via port 5432.
* Integrate Prisma ORM into the NestJS Backend to execute Database Migration (`npx prisma db push`), automatically generating data tables on AWS Cloud.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Launch an **Amazon RDS Instance (PostgreSQL)** named `healthcare-db` within a Private Subnet on the AWS Console. <br> - Select the `db.t4g.micro` server class (ARM Graviton2 chip), enable At-Rest Encryption, and configure mandatory connections over SSL (`global-bundle.pem`). | 06/22/2026 | 06/22/2026 | [Here](https://cloudjourney.awsstudygroup.com/) |
| Tue | - Configure **Security Group for RDS**: Set up Inbound Rules for port 5432 (accepting connections from the EC2 Backend Security Group and Dev/Test verification connections via SSL). <br> - Construct the `schema.prisma` file storing: User data identified by UUID strings, Initial Medical Intake Forms (blood type, underlying conditions, allergies), Doctor Open Working Slots, Appointment Lists, and conversation report file paths. | 06/23/2026 | 06/23/2026 | [Here](https://docs.nestjs.com/techniques/database) |
| Wed | - Execute Prisma CLI (`npx prisma db push`) from the Backend to automatically synchronize Schema and generate table structures on AWS RDS PostgreSQL. <br> - Integrate the secure connection environment variable `DATABASE_URL` appending parameters `sslmode=verify-full&sslrootcert=global-bundle.pem` into the `.env` file. | 06/24/2026 | 06/24/2026 | [Here](https://www.prisma.io/docs/) |
| Thu | - Develop Appointment Booking APIs in NestJS Backend integrating **Pessimistic Locking (`FOR UPDATE`)** directly at the PostgreSQL Database layer. <br> - Guarantee that when a patient selects a time slot, that row is locked (row-level lock) throughout the transaction to absolutely eliminate the risk of 2 people booking the same slot. | 06/25/2026 | 06/25/2026 | [Here](https://docs.nestjs.com/techniques/database) |
| Fri | - Perform CRUD operation testing on RDS PostgreSQL from the EC2 Backend; execute simulated load testing (Stress Test) for concurrent bookings to verify the effectiveness of the Pessimistic Locking mechanism. <br> - Optimize Connection Pooling on Prisma ORM and verify the `Available` operational status of `healthcare-db` on the AWS Console. | 06/26/2026 | 06/26/2026 | [Here](https://cloudjourney.awsstudygroup.com/) |


### Week 4 Achievements:

* Successfully deployed the **Amazon RDS PostgreSQL (`healthcare-db`)** database within a Private Subnet using Graviton2 `db.t4g.micro` servers, optimizing operational costs and ensuring SSL encryption safety.
* Successfully synchronized database structures from NestJS via Prisma CLI (`npx prisma db push`), clearly defining tables storing medical intake profiles, doctor working schedules, and appointment details.
* Successfully applied **Pessimistic Locking (`FOR UPDATE`)** in the NestJS Backend, thoroughly resolving Race Condition (Double-booking) issues when multiple patients book the same appointment slot concurrently.
* Ensured network layer and transit safety through port 5432 Security Group configurations combined with transit encryption certificates `global-bundle.pem`.
* Built a solid data foundation for the Doctor Portal to look up daily consultation lists and the Patient Portal to select doctors and book appointments.
* Fully prepared database infrastructure and Backend completeness ready for Week 5 integration of the **RAG Pipeline (AWS Bedrock Knowledge Base, ViMQ, GPT-4o-mini & Langfuse)** for initial medical consultations.
