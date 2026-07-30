---
title: "Worklog Tuần 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Nghiên cứu tổng quan về kiến trúc ứng dụng Web hiện đại và điện toán đám mây (Cloud Computing).
* Tìm hiểu các dịch vụ hạ tầng cốt lõi trên **AWS** (Cognito, EC2, S3, RDS PostgreSQL, CloudWatch, SES/SNS, IAM, VPC) ứng dụng cho hệ thống Y tế số Smart Healthcare Platform.
* Phân tích, lựa chọn mô hình kiến trúc phù hợp cho ứng dụng (Multi-tier Microservices on Docker) và thiết kế sơ đồ tổng quan hạ tầng Cloud chuẩn AWS Well-Architected.
* Phân tích chi tiết quy trình nghiệp vụ cốt lõi (**Business Flow**) gồm 5 giai đoạn: Thiết lập hệ thống, Onboarding bệnh nhân, AI Triage 3 cấp độ, Đặt lịch chống trùng slot và Khám bệnh Split View.
* Chuẩn bị môi trường phát triển cục bộ (Local Environment) và khởi tạo dự án với Next.js 14 Responsive (Frontend) và NestJS (Backend).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ---- | --- | --- | --- |
| 2   | - Nghiên cứu tổng quan về điện toán đám mây (IaaS, PaaS, SaaS) và lợi ích khi triển khai ứng dụng Web Healthcare trên Cloud.<br>- Phân tích mô hình kiến trúc Web 3 lớp (3-Tier Architecture: Presentation - Application - Database) ứng dụng trong dự án. | 01/06/2026 | 01/06/2026 | [Tại đây](<https://aws.amazon.com/what-is-cloud-computing/>) |
| 3   | - Tìm hiểu các dịch vụ cốt lõi của AWS: **AWS Cognito** (Auth & Temp Password), **EC2** (Docker Containers), **S3** (Lưu đơn thuốc/AI Report), **RDS PostgreSQL** (PostgreSQL 16.x), **SageMaker** (AI Triage Endpoint).<br>- Đánh giá ưu/nhược điểm giữa việc tự quản lý server trên EC2 với việc sử dụng dịch vụ quản lý hoàn toàn (Managed Services). | 02/06/2026 | 02/06/2026 | [Tại đây](<https://docs.aws.amazon.com/>) |
| 4   | - Nghiên cứu giải pháp an toàn thông tin trên Cloud: Quản lý truy cập với **AWS IAM**, phân vùng mạng an toàn với **AWS VPC** (Public/Private Subnets cho Multi-AZ).<br>- Tìm hiểu các tiêu chuẩn bảo mật dữ liệu y tế (Mã hóa UUID, JWT Token verification, mã hóa dữ liệu At-Rest & In-Transit). | 03/06/2026 | 03/06/2026 | [Tại đây](<https://docs.aws.amazon.com/iam/>) |
| 5   | - Cài đặt công cụ phát triển: **AWS CLI**, **Node.js**, **Docker Desktop**, **WSL 2**, cấu hình tài khoản AWS IAM.<br>- Khởi tạo Repository trên GitHub và cấu hình cấu trúc thư mục dự án cho Frontend (Next.js 14) và Backend (NestJS Framework). | 04/06/2026 | 04/06/2026 | [Tại đây](<https://docs.aws.amazon.com/cli/>) |
| 6   | - Phác thảo và vẽ sơ đồ kiến trúc hạ tầng Cloud (**AWS Architecture Diagram**) cho hệ thống Smart Healthcare Platform.<br>- Lập tài liệu phân tích yêu cầu kỹ thuật (Technical Requirements) và chốt chi tiết quy trình **Business Flow** (Admin Onboard Doctor, Form khai báo y tế ban đầu, AI Triage 3 cấp độ, Bottom Sheet Booking và Doctor Split View UI). | 05/06/2026 | 05/06/2026 | [Tại đây](<https://aws.amazon.com/architecture/>) |


### Kết quả đạt được tuần 1:

* Nắm vững kiến trúc Web đa tầng và lý thuyết nền tảng về điện toán đám mây cùng các dịch vụ cốt lõi của AWS áp dụng cho dự án Healthcare.
* Hoàn thành sơ đồ kiến trúc hạ tầng Cloud (**AWS Architecture Diagram**) chuẩn AWS Well-Architected cho hệ thống, xác định rõ vị trí triển khai Public/Private Subnets, Load Balancers, Containers và Database.
* Chốt hoàn chỉnh tài liệu phân tích luồng nghiệp vụ cốt lõi (**Business Flow**) gồm 5 giai đoạn chi tiết từ Onboarding, AI Triage đến Consultation.
* Hiểu rõ cơ chế phân vùng mạng an toàn (VPC, Public/Private Subnet) và phân quyền người dùng/dịch vụ bằng AWS IAM & Cognito.
* Khởi tạo thành công môi trường phát triển cục bộ và bộ mã nguồn ban đầu cho **Next.js 14** và **NestJS** kết nối sẵn với GitHub.

