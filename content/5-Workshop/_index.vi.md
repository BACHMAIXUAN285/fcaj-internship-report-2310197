---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai Nền tảng Hỗ trợ Khám bệnh & Quản lý Y tế Trực tuyến (MedFlow) trên AWS

#### Tổng quan

Trong bài thực hành này, bạn sẽ tiến hành xây dựng và triển khai **Nền tảng Hỗ trợ Khám bệnh & Quản lý Y tế Trực tuyến (MedFlow)** trên hạ tầng điện toán đám mây AWS. Hệ thống được thiết kế theo chuẩn kiến trúc Cloud hiện đại, đáp ứng các tiêu chuẩn nghiêm ngặt về bảo mật dữ liệu y tế, khả năng xử lý thời gian thực và tích hợp Trí tuệ Nhân tạo (AI).

Hành trình thực hành được chia làm **4 module chiến lược** đại diện cho toàn bộ vòng đời phát triển một hệ thống Cloud-native:
+ **Triển khai Cơ sở Dữ liệu (Amazon Aurora & RDS):** Khởi tạo database PostgreSQL (`healthcare-db`) tối ưu chi phí với chip ARM Graviton2 (`db.t4g.micro`), mã hóa đường truyền bằng chứng chỉ SSL (`global-bundle.pem`) và tự động hóa đồng bộ Schema qua Prisma ORM.
+ **Triển khai Dịch vụ Xác thực & Phân quyền (AWS Cognito):** Quản lý định danh tập trung (User Pool `healthcare`) cho Bệnh nhân, Bác sĩ và Admin (RBAC). Đạt chuẩn an toàn dữ liệu y tế bằng **UUID ẩn danh (Anonymization)** và giải mã JWT bất đối xứng RSA qua **JWKS Endpoint**.
+ **Xây dựng & Triển khai Module AI (MedFlow AI):** Đóng gói và phát hành mô hình AI hỗ trợ sơ chẩn (AI Triage & Chatbot) trên **Amazon SageMaker Endpoint** để xử lý phân loại triệu chứng bệnh nhân theo thời gian thực.
+ **Triển khai Hệ thống (Fullstack Deployment on EC2):** Đóng gói Docker Containers cho Frontend (Next.js) và Backend (NestJS REST API & WebSocket Gateway) lên Amazon EC2, liên kết toàn bộ tài nguyên (RDS, Cognito, SageMaker, S3, SES/SNS, CloudWatch) trong mạng VPC.

#### Nội dung

1. [Phần 1: Triển khai Cơ sở Dữ liệu (Amazon Aurora & RDS)](5.1-Aurora-and-RDS/)
2. [Phần 2: Triển khai Dịch vụ Xác thực & Phân quyền (AWS Cognito)](5.2-Cognito/)
3. [Phần 3: Xây dựng & Triển khai Module AI (MedFlow AI) Trên AWS](5.3-medflow-ai/)
4. [Phần 4: Triển khai Hệ thống Fullstack lên EC2](5.4-deploy/)