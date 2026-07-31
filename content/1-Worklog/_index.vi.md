---
title: "Nhật ký công việc"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

Trang này tổng quan lại toàn bộ nhật ký công việc (Worklog) trong quá trình nghiên cứu, thiết kế và phát triển dự án **Smart Healthcare AI Assistant & Appointment Booking Platform** trên nền tảng AWS Cloud kết hợp Hybrid AI Services. Dự án được hoàn thành trong thời gian **8 tuần** bám sát quy trình thiết kế Cloud-native, RAG Pipeline và Business Flow với các mốc công việc chi tiết như sau:

**Tuần 1:** [Phân tích yêu cầu Business Flow & Thiết kế System Architecture Hybrid AI, CSDL ERD](1.1-week1/)

**Tuần 2:** [Khởi tạo Base Source Code (Next.js Responsive + NestJS REST API, WebSocket & LLM Intent Router)](1.2-week2/)

**Tuần 3:** [Cấu hình AWS Cognito (Phân quyền RBAC cho Patient, Doctor, Admin) & Kết nối Amazon S3](1.3-week3/)

**Tuần 4:** [Triển khai CSDL AWS RDS PostgreSQL (`db.t4g.micro`) & Xử lý cơ chế Pessimistic Locking chống trùng slot](1.4-week4/)

**Tuần 5:** [Tích hợp RAG Pipeline (AWS Bedrock Knowledge Base, ViMQ, GPT-4o-mini), Giám sát Langfuse & Tạo Pre-consultation Report](1.5-week5/)

**Tuần 6:** [Giám sát hệ thống với AWS CloudWatch, Hoàn thiện Doctor Portal (Tra cứu lịch hẹn & Báo cáo AI) & Patient Mobile App](1.6-week6/)

**Tuần 7:** [Kiểm thử bảo mật (UUID Anonymization), Stress Test k6 bài toán Race Condition đặt lịch đồng thời](1.7-week7/)

**Tuần 8:** [Đóng gói Docker Containers, Cấu hình CI/CD GitHub Actions lên AWS EC2, tổng kết và bàn giao](1.8-week8/)
