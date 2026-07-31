---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Initialize, integrate, and deploy an initial medical consultation **RAG Pipeline (Retrieval-Augmented Generation)** system combining **AWS Bedrock Knowledge Base**, the **ViMQ (Local Host)** model, **GPT-4o-mini**, and the **Langfuse** monitoring tool.
* Program the **[LLM Intent Router]** in the NestJS Backend to route incoming Patient questions, send medical entity extraction through ViMQ, retrieve knowledge on Bedrock KB, and synthesize responses via GPT-4o-mini in real time.
* Build a feature to automatically summarize conversation content into a **Pre-consultation Report (PDF/JSON)** file and push it to secure storage on **Amazon S3** via Presigned URLs.
* Construct a **Safe Fallback** mechanism in the NestJS Backend: When connections to LLM/Bedrock services experience timeout or disruption, the system automatically redirects the patient to the direct Appointment Booking screen without disrupting the user experience.
* Integrate **Langfuse** to monitor LLM metrics (Token count, Latency, Prompt performance) and synchronize logs to **AWS CloudWatch**.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- |--- | --- | --- | --- |
| Mon | - Set up **AWS Bedrock Knowledge Base** containing standardized medical documents for RAG retrieval. <br> - Configure the **ViMQ (Local Host)** model for Medical Named Entity Recognition (Medical NER) and prepare the **GPT-4o-mini** API. | 06/29/2026 | 06/29/2026 | [Here](https://docs.aws.amazon.com/bedrock/) |
| Tue | - Build the **[LLM Intent Router]** Module in the NestJS Backend: Receive user questions -> Route entity extraction via ViMQ -> Query RAG knowledge from AWS Bedrock KB -> Send synthesized Prompt to GPT-4o-mini to return to client. <br> - Connect **Langfuse** to log LLM monitoring metrics and push metrics to **AWS CloudWatch**. | 06/30/2026 | 06/30/2026 | [Here](https://langfuse.com/docs) |
| Wed | - Write an automated module to summarize consultation conversation history into a **Pre-consultation Report (PDF/JSON)** file. <br> - Call Amazon S3 services to upload report files to the S3 Bucket and store path links (S3 URI / Presigned URL) into appointment details within the RDS PostgreSQL database. | 07/01/2026 | 07/01/2026 | [Here](https://docs.aws.amazon.com/s3/) |
| Thu | - Develop a **Global Exception Filter** & **Fallback Service** mechanism in NestJS. <br> - Script a safe Fallback scenario: When LLM/Bedrock APIs experience network congestion -> automatically transition the patient to the manual Appointment Booking interface, ensuring core business flows remain uninterrupted. | 07/02/2026 | 07/02/2026 | [Here](https://docs.nestjs.com/exception-filters) |
| Fri | - Perform comprehensive end-to-end testing for the AI RAG Chatbot conversation flow on the Patient mobile interface; confirm Pre-consultation Report files are successfully uploaded to Amazon S3. <br> - Test the Doctor Portal view for appointment list lookups and open/read the summary report file of patient inquiries prior to consultation sessions. | 07/03/2026 | 07/03/2026 | [Here](https://cloudjourney.awsstudygroup.com/) |


### Week 5 Achievements:

* Successfully deployed the **RAG Pipeline (AWS Bedrock KB + ViMQ + GPT-4o-mini)** system serving as an AI Chatbot Assistant to resolve queries and provide precise initial medical consultation information 24/7.
* Fully built the **[LLM Intent Router]** router and successfully integrated **Langfuse** to track performance and token consumption, while pushing system logs to **AWS CloudWatch**.
* Automated conversation data aggregation and packaging into **Pre-consultation Report** files, pushed directly to secure storage on **Amazon S3**.
* Fully built a **Safe Fallback** mechanism, guaranteeing the system automatically transitions to standard appointment booking flows if AI services encounter failure or downtime.
* Finalized features for the Doctor Portal: Doctors can effortlessly look up daily appointment schedules and review patient inquiry summary report files directly from S3.
* Complete AI infrastructure and supporting services are fully prepared, ready for Week 6 optimization of **AWS CloudWatch** system monitoring and concurrent booking load testing.
