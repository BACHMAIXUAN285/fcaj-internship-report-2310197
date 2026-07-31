---
title : "DATABASE DEPLOYMENT (AMAZON AURORA & RDS)"
date : 2024-01-01 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

#### Introduction to Amazon RDS & Aurora

* **Amazon RDS (Relational Database Service)** and **Amazon Aurora** are fully managed relational database services provided by AWS that simplify setting up, operating, and scaling databases in the Cloud.
* In healthcare systems, the database serves as the core store for all sensitive structured data (user information, medical records, appointment schedules). Deploying RDS within a **VPC Private Subnet** combined with **SSL encryption** ensures high security, safety, and compliance with strict healthcare data standards.

#### Deployment Overview

In this hands-on lab, you will initialize and configure a **PostgreSQL** database on Amazon RDS (`healthcare-db`) to serve the **NestJS Backend (using Prisma ORM)**:
* Initialize a `healthcare-db` database instance using the `db.t4g.micro` instance class (AWS Graviton2) to optimize operational costs.
* Configure network protection via **Security Groups** and enable transit encryption using an **SSL Certificate** (`global-bundle.pem`).
* Extract the connection string (`DATABASE_URL`) and synchronize the database schema migration from the NestJS project to AWS RDS via Prisma CLI.

#### Implementation Steps Summary

* Step 1: Database Creation
* Step 2: Network & Security Configuration
* Step 3: Extract Connection String
* Step 4: Synchronize Schema from NestJS to AWS RDS