---
title: "Configuring Application Load Balancer (ALB)"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

## Setting Up Application Load Balancer (ALB)

ALB acts as the "receptionist" receiving traffic from the Internet and routing requests to your containers.

1. **Create Target Group:**
   - Navigate to **EC2** > scroll down the left menu to **Target Groups** > **Create target group**.
   - **Target type:** Must select **IP addresses** (since ECS Fargate uses virtual static IPs for containers).
   - **Target group name:** e.g., `medflow-client-tg`.
   - **Protocol & Port:** `HTTP` and port `3000` (port used by the Next.js Frontend).
   - **VPC:** Select the default VPC.
   - **Health checks:** Set the health check path to `/` (Next.js must return a 200 OK status on the home page).
   - *Save and skip the IP registration step (ECS will automatically register IP addresses here later).*
   ![EC2 Target group](/images/5-Workshop/5.4-deploy/EC2_target_group.png)

2. **Create Load Balancer:**
   - Navigate to **EC2** > **Load Balancers** > **Create Load Balancer**.
   - Select **Application Load Balancer**.
   - **Scheme:** Select **Internet-facing** (to allow access from the public Internet).
   - **Network mapping:** Select the default VPC, check **all Subnets** (at least 2) for redundancy.
   - **Security Groups (Firewall for the Receptionist):** Create a new SG, open ports `HTTP (80)` and `HTTPS (443)` for Source `0.0.0.0/0` (anywhere).
   - **Listeners and routing:** Under the HTTP:80 listener, for the Default action, select **Forward to** and point to the `medflow-client-tg` Target Group created above.
   - Click **Create**.
   ![EC2 Load Balancer](/images/5-Workshop/5.4-deploy/EC2_load_balancer.png)