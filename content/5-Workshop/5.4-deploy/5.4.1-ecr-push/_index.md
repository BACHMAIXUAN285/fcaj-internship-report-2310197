---
title: "Packaging and Storing Images on AWS ECR"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

The deployment process begins by creating application image repositories and pushing packaged Docker images to AWS ECR.

## Pushing Images to the ECR (Elastic Container Registry) Repository

ECR acts as a repository to store your source code Docker images.

1. **Create Repositories:**
   * Navigate to **AWS ECR** > **Repositories** > **Create repository**.
   * Create 2 separate repositories: for example, `medflow-client` (for the Next.js Frontend) and `medflow-server` (for the NestJS Backend).
   * Keep the visibility settings as **Private**.
  ![ECR](/images/5-Workshop/5.4-deploy/ECR.png)

2. **Build and Push Images (Usually automated via GitHub Actions):**
   * If performing manually, click the **View push commands** button in the top right corner of the repository. AWS will provide 4 standard commands:
     1. *Authenticate Docker to AWS:*
        ```bash
        aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
        ```
     2. *Build image:*
        ```bash
        docker build -t medflow-client .
        ```
     3. *Tag image:*
        ```bash
        docker tag medflow-client:latest <aws_account_id>.dkr.ecr.<region>[.amazonaws.com/medflow-client:latest](https://.amazonaws.com/medflow-client:latest)
        ```
     4. *Push image to cloud:*
        ```bash
        docker push <aws_account_id>.dkr.ecr.<region>[.amazonaws.com/medflow-client:latest](https://.amazonaws.com/medflow-client:latest)
        ```