---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Deploy the Healthcare Web Application to AWS cloud infrastructure using a combination of **Amazon EC2** for compute servers and **Amazon S3** for object storage.
* Initialize and configure network resources (VPC, Subnets, Security Groups) to ensure secure access to EC2 instances.
* Integrate **Amazon S3** into the Backend (NestJS) to manage file uploads/downloads for assets such as doctor profile photos, medical records, and check-in QR codes.
* Set up **AWS API Gateway** (or Nginx Reverse Proxy on EC2) for request routing and Backend API security.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Launch an **EC2 Instance** (Ubuntu/Linux) via AWS Console, generate a Key Pair for SSH access <br> - Configure **Security Group** inbound access rules for SSH (22), HTTP (80), and HTTPS (443) ports | 15/06/2026 | 15/06/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Tue | - Set up runtime environment on EC2: Install Docker, Docker Compose, Git, and Node.js <br> - Pull application source code from GitHub to EC2 and execute deployment using Docker Containers | 16/06/2026 | 16/06/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Wed | - Create an **S3 Bucket** for medical asset storage, configure access policies (Bucket Policy, CORS) <br> - Integrate AWS SDK v3 into NestJS Backend to build APIs for uploading/downloading medical record images and appointment QR codes | 17/06/2026 | 17/06/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |
| Thu | - Research and set up **Amazon API Gateway** (or Nginx Reverse Proxy on EC2) to route traffic from public domain to Backend services <br> - Configure Rate Limiting to protect against Denial of Service attacks | 18/06/2026 | 18/06/2026 | [Here](<https://docs.aws.amazon.com/apigateway/>) |
| Fri | - Perform end-to-end connectivity testing between Frontend (Next.js), Backend (NestJS) on EC2, and Amazon S3 storage service <br> - Optimize S3 storage consumption and audit IAM Role security permissions attached to the EC2 Instance | 19/06/2026 | 19/06/2026 | [Here](<https://cloudjourney.awsstudygroup.com/>) |


### Week 3 Achievements:

* Successfully launched and configured the **Amazon EC2** server, smoothly setting up security rules via Security Groups.
* Containerized and deployed the Healthcare Web Application (Next.js & NestJS) operating stably on the EC2 server environment via Docker Containers.
* Successfully integrated **Amazon S3** into the Backend system, enabling patients and doctors to securely upload and view medical documents, record images, and QR codes.
* Established an API routing/gateway system (API Gateway / Nginx) to control and route incoming traffic while enhancing Backend system security.
* Applied **IAM Roles for EC2 Instance** to interact securely with S3 without hardcoding Access Keys in source code.
* Prepared compute and static storage infrastructure for upcoming Cloud Database integration (RDS/DynamoDB) in Week 4.
