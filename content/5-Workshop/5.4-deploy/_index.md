---
title : "System Deployment"
date : 2026-07-01 
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Deployment Architecture Overview

After completing the development and packaging phase using Containerization technology (Docker), the **MedFlow** system is deployed onto the Amazon Web Services (AWS) cloud infrastructure. The model utilizes a Serverless Container architecture on AWS ECS Fargate combined with an Application Load Balancer (ALB) to ensure high availability, flexible scalability, and operational cost optimization.


#### Table of Contents

- [Packaging and Storing Images on AWS ECR](5.4.1-ecr-push/)
- [Configuring Application Load Balancer (ALB)](5.4.2-alb-setup/)
- [Initializing and Deploying Services on AWS ECS](5.4.3-ecs-deployment/)
- [Verification and Testing Deployment](5.4.4-acceptance-testing/)