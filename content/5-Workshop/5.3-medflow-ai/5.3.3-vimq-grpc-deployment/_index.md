---
title: "Initializing Local ViMQ Server & gRPC Server"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---


---

### Configuring EC2 / Local Server to Run the ViMQ Model & gRPC Server

* **Purpose**: Set up an environment to run the self-built ViMQ NER model to extract local medical entities before routing them to the LLM.
* **Step-by-step instructions**:
  1. Launch an **EC2 Instance** (Linux / Ubuntu) or set up a local server environment.
  2. Attach an **IAM Role** to the EC2 instance with the `AmazonBedrockFullAccess` and `CloudWatchLogsFullAccess` policies.
  3. Install the required dependency libraries:
     ```bash
     pip install torch transformers grpcio grpcio-tools langchain-aws
     ```
  4. Download and package the local ViMQ NER model into the `vimq_integration.py` module to handle incoming client queries and extract keywords (e.g., *difficulty breathing*, *fever*, *paracetamol*).