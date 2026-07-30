---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# [FCAJ2026] AWS S3 Bucket: The Cloud-Native Storage "Missing Piece" for the Smart Healthcare System

---

### Introduction

During the development of the Smart Healthcare System (An AI-assisted medical consultation and appointment management platform), right after solving the challenges of slot conflict management, AI model integration, and user authentication flows, I was confronted with another painful issue: **File Storage Management**.

My system continuously generates various types of file data:
* **Patients**: Avatars, medical summary reports, and prescription files in PDF format.
* **Doctors & Staff**: Professional diplomas, medical practice certificates.
* **AI Model**: Training weight files (`.pt`, `.bin`) reaching sizes up to several hundred MBs, along with consultation log data.

Initially, the most convenient local habit was dumping certificate files and avatars directly into the `uploads/` directory of the NestJS Backend server, while committing AI weight files straight into Git. However, as I prepared to deploy the system to Production, I realized this was a total "disaster" in terms of security and scalability: the Git repository became bloated, the Backend server suffered from stateful storage burdens, and the risk of leaking personal medical files was extremely high.

That was when I turned my attention to exploring and applying **Amazon S3 (Simple Storage Service)**.

---

### Practical Application in the Project

Instead of turning the Backend server into a storage dumping ground, I restructured the entire system to offload all file assets to S3 Buckets. Specifically, strategic applications include:
* **Securing Doctor Practice Certificates**: Medical qualifications are sensitive personal data that must never be exposed publicly. I created a **Private S3 Bucket** to host these files. When an Admin needs to review a doctor's profile, the NestJS Backend generates an **S3 Presigned URL** with a short expiration time. Once expired, the URL automatically invalidates, ensuring absolute security.
* **Managing AI Model Weights**: Model weight files (`model.pt`) are completely decoupled from the source code. All weight files and training checkpoints are stored on S3. When the AI service container boots up, a Python script automatically pulls the latest weights version from S3 into memory to load the model. Model versioning for AI thus becomes exceptionally lightweight and manageable.
* **Exporting Medical Reports & Storing Chat Logs**: Every time a patient completes a consultation or appointment session, the system automatically generates a PDF report file and logs conversation history from the AI Service. These files are pushed directly to the S3 Bucket for download or long-term archiving.

---

### Key Values Gained by Migrating to Amazon S3

After successfully integrating S3 Buckets into the system, here are the most significant benefits the project received:
1. **Unburdening the Backend into a "Stateless" Architecture**: The NestJS Backend server now purely handles business logic and APIs. Removing static file overhead keeps the server remarkably lightweight, making it effortless to scale out across multiple instances without file synchronization conflicts.
2. **Absolute Security for Sensitive Health Data**: Eliminates the risk of exposing direct file paths. Access control managed via IAM Roles and Presigned URLs guarantees that only authorized users can access medical documents at specific times.
3. **High Reliability & Cost Optimization**: S3 commits to 99.999999999% (11 9's) data durability. Furthermore, AWS offers 5GB of free storage for the first 12 months. Combined with setting up **Lifecycle Rules** (automatically deleting temporary logs or transitioning older files to low-cost Glacier storage), the storage infrastructure maintenance cost for the project is virtually $0.

---

### Conclusion

Adopting Cloud-Native services like Amazon S3 to manage files represents a fundamental mindset for standardizing modern system architecture. Instead of turning your Backend server into a bulky warehouse plagued with security vulnerabilities, delegate the storage burden and asset management to AWS S3.

This not only makes your project more professional and flexible but also allows you to focus 100% of your energy on developing core business features.

---

### References

1. **AWS**. *"Amazon Simple Storage Service (S3) User Guide"*. (<https://docs.aws.amazon.com/AmazonS3/latest/userguide/>)
2. **AWS**. *"Amazon S3 Product Overview"*. (<https://aws.amazon.com/s3/>)

---

View the article on Facebook [Here](<https://www.facebook.com/groups/awsstudygroupfcj/permalink/2229299597835000/?rdid=53JdldxFDjYrRw5Q#>)
