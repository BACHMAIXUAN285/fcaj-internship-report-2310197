---
title: "Worklog Tuần 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Nghiên cứu tổng quan về kiến trúc ứng dụng Web hiện đại, điện toán đám mây (Cloud Computing) và mô hình Hybrid AI Services (Cloud + External SaaS + Local Host).
* Tìm hiểu các dịch vụ hạ tầng cốt lõi trên **AWS** (Cognito, EC2, S3, RDS PostgreSQL, CloudWatch, Bedrock Knowledge Base, IAM, VPC) cùng các dịch vụ AI phụ trợ (**GPT-4o-mini**, **ViMQ Local**, **Langfuse**) ứng dụng cho hệ thống Y tế số Smart Healthcare Platform.
* Phân tích, lựa chọn mô hình kiến trúc phù hợp cho ứng dụng (Multi-tier Microservices on Docker) và thiết kế sơ đồ tổng quan hạ tầng Cloud Hybrid AI chuẩn AWS Well-Architected.
* Phân tích chi tiết quy trình nghiệp vụ cốt lõi (**Business Flow**) gồm 5 giai đoạn: Phân quyền hạ tầng Auth (Cognito RBAC), Onboarding bệnh nhân, Trợ lý Chatbot AI RAG tư vấn y tế, Đặt lịch chống trùng slot (Pessimistic Locking) và Tra cứu danh sách lịch hẹn cho Bác sĩ.
* Chuẩn bị môi trường phát triển cục bộ (Local Environment) và khởi tạo dự án với Next.js Responsive (Frontend) và NestJS (Backend & LLM Intent Router).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ---- | --- | --- | --- |
| 2   | - Nghiên cứu tổng quan về điện toán đám mây (IaaS, PaaS, SaaS) và lợi ích khi triển khai ứng dụng Web Healthcare trên Cloud.<br>- Phân tích mô hình kiến trúc Web 3 lớp (3-Tier Architecture) kết hợp pipeline RAG AI ứng dụng trong dự án. | 01/06/2026 | 01/06/2026 | [Tại đây](<https://aws.amazon.com/what-is-cloud-computing/>) |
| 3   | - Tìm hiểu các dịch vụ cốt lõi của AWS: **AWS Cognito** (Auth & RBAC), **EC2** (Docker Containers), **S3** (Lưu tệp đính kèm/AI Pre-consultation Report), **RDS PostgreSQL** (`db.t4g.micro`), **AWS Bedrock Knowledge Base** (RAG Pipeline).<br>- Tìm hiểu các dịch vụ AI kết hợp: **GPT-4o-mini** (Inference), **ViMQ** (Local Medical NER), **Langfuse** (LLM Monitoring). | 02/06/2026 | 02/06/2026 | [Tại đây](<https://docs.aws.amazon.com/>) |
| 4   | - Nghiên cứu giải pháp an toàn thông tin trên Cloud: Quản lý truy cập với **AWS IAM**, phân vùng mạng an toàn với **AWS VPC** (Public/Private Subnets).<br>- Tìm hiểu các tiêu chuẩn bảo mật dữ liệu y tế (Mã hóa UUID ẩn danh, JWT Token verification, mã hóa dữ liệu At-Rest & In-Transit qua SSL/TLS). | 03/06/2026 | 03/06/2026 | [Tại đây](<https://docs.aws.amazon.com/iam/>) |
| 5   | - Cài đặt công cụ phát triển: **AWS CLI**, **Node.js**, **Docker Desktop**, **WSL 2**, cấu hình tài khoản AWS IAM.<br>- Khởi tạo Repository trên GitHub và cấu hình cấu trúc thư mục dự án cho Frontend (Next.js) và Backend (NestJS Framework). | 04/06/2026 | 04/06/2026 | [Tại đây](<https://docs.aws.amazon.com/cli/>) |
| 6   | - Phác thảo và vẽ sơ đồ kiến trúc hạ tầng Cloud Hybrid AI (**AWS Architecture Diagram**) cho hệ thống Smart Healthcare Platform.<br>- Lập tài liệu phân tích yêu cầu kỹ thuật (Technical Requirements) và chốt chi tiết quy trình **Business Flow** (Cognito RBAC Auth Flow, Form khai báo thông tin y tế, Chatbot AI RAG tư vấn, Booking concurrency với Pessimistic Locking và Doctor Portal tra cứu ca khám). | 05/06/2026 | 05/06/2026 | [Tại đây](<https://aws.amazon.com/architecture/>) |


### Kết quả đạt được tuần 1:

* Nắm vững kiến trúc Web đa tầng, pipeline RAG AI và lý thuyết nền tảng về điện toán đám mây cùng các dịch vụ cốt lõi của AWS áp dụng cho dự án Healthcare.
* Hoàn thành sơ đồ kiến trúc hạ tầng Cloud Hybrid AI (**AWS Architecture Diagram**) chuẩn AWS Well-Architected cho hệ thống, xác định rõ vị trí triển khai Public/Private Subnets, Docker Containers trên EC2, S3, RDS PostgreSQL, AWS Bedrock KB, GPT-4o-mini, ViMQ và Langfuse.
* Chốt hoàn chỉnh tài liệu phân tích luồng nghiệp vụ cốt lõi (**Business Flow**) gồm 5 giai đoạn chi tiết từ Cognito Auth, Onboarding, Chatbot AI RAG tư vấn, Đặt lịch chống trùng giờ đến Doctor Portal tra cứu danh sách lịch.
* Hiểu rõ cơ chế phân vùng mạng an toàn (VPC, Public/Private Subnet) và phân quyền người dùng/dịch vụ bằng AWS IAM & Cognito (sử dụng UUID ẩn danh).
* Khởi tạo thành công môi trường phát triển cục bộ và bộ mã nguồn ban đầu cho **Next.js** và **NestJS** kết nối sẵn với GitHub.

