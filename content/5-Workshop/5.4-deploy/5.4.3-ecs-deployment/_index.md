---
title: "Initializing and Deploying Services on AWS ECS"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

The entire application is operated as a multi-container ECS Task managed by AWS Fargate.

## Deploying and Running the Application on ECS (Elastic Container Service)

This is where you "spin up the machine" to run the images saved in Step 1.

### 1. Create Task Definition (Blueprint)
1. Navigate to **ECS** > **Task Definitions** > **Create new Task Definition**.
2. Enter a name (e.g., `medflow-task`).
3. **Infrastructure:** Select **AWS Fargate** (Serverless, no physical server management required).
4. **Task execution role:** Select the `ecsTaskExecutionRole` role (If using Parameter Store/Secrets, ensure this role is granted `ssm:GetParameters` permissions).
5. **Container 1 (Frontend):**
   - Name: `medflow-client`.
   - **Image URI:** Copy and paste the Image URI link from ECR in Step 1.
   - **Port mappings:** Open port `3000` (TCP protocol).
   - Define environment variables if necessary.
6. **Container 2 (Backend) - Click Add more containers:**
   - Name: `medflow-server`.
   - **Image URI:** Paste the Backend ECR link.
   - **Port mappings:** Open port `4000`.
   - *Tip: Two containers sharing the same Task can communicate with each other via `127.0.0.1`.*
7. Click **Create**.
![ECS cluster](/images/5-Workshop/5.4-deploy/ECS_cluster.png)

### 2. Create Service (Running State)
1. Go to **ECS Clusters** > Select your Cluster (or create a new one) > **Services** tab > **Create**.
2. **Compute options:** Select Launch type as **Fargate**.
3. **Deployment configuration:**
   - Application type: **Service**.
   - Task Definition: Select the blueprint created in section 1.
   - Service name: `medflow-service`.
   - Desired tasks: `1` (Number of replicas to run).
4. **Networking:**
   - Select VPC and Subnets.
   - **Security Group (Container Firewall):** Create new or select an existing SG. **Important:** Open Inbound Rules for ports `3000` and `4000`. For optimal security, set the Source to only accept traffic from the *ALB Security Group*.
5. **Load balancing:**
   - Load balancer type: Select **Application Load Balancer**.
   - Container to load balance: Select container `medflow-client:3000`.
   - Use an existing target group: Select `medflow-client-tg` (created in Step 2).
6. Click **Create** and wait for the deployment process to complete.
![ECS service](/images/5-Workshop/5.4-deploy/ECS_service.png)