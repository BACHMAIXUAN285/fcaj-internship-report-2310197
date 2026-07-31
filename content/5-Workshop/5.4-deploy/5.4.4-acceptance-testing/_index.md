---
title: "Acceptance Testing and Verification"
date: 2026-07-01
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

After completing the initialization of the ECS Service, the deployment verification and testing process is carried out through the following steps:

## Step 4: Verification and Testing

1. Go to the **Logs** or **Events** tab of the ECS Service to monitor the image pulling and container startup process.
2. Return to the **EC2** console > **Target Groups**, and click on `medflow-client-tg`.
3. Look down at the **Targets** tab. Initially, it will display *Initial*. If all configurations are correct (no application crashes, no firewall blocks), it will switch to **Healthy** (in green).
4. Open **Load Balancers**, copy the **DNS name** (e.g., `medflow-alb-...elb.amazonaws.com`), paste it into your web browser, and view your live website running on the Internet.