---
title: "5.4.3 Khởi Tạo Và Triển Khai Dịch Vụ Trên AWS ECS"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

Toàn bộ ứng dụng được vận hành dưới dạng một ECS Task multi-container quản lý bởi AWS Fargate.

### 1. Định Nghĩa Task Definition (`medflow-task`)
* **Launch Type:** AWS Fargate (Serverless compute engine).
* **Task Execution Role:** Sử dụng `ecsTaskExecutionRole` được cấp quyền truy cập ECR (`ecr:GetDownloadUrlForLayer`, `ecr:BatchGetImage`) và AWS Systems Manager Parameter Store (`ssm:GetParameters`) để đọc biến môi trường bảo mật.
* **Cấu hình Container 1 (`medflow-client`):**
  * Trỏ URI về Image ECR `medflow-client:latest`.
  * **Port Mapping:** Cổng `3000/TCP`.
* **Cấu hình Container 2 (`medflow-server`):**
  * Trỏ URI về Image ECR `medflow-server:latest`.
  * **Port Mapping:** Cổng `4000/TCP`.
* *Lưu ý kiến trúc:* Hai container trong cùng một Task có thể giao tiếp nội bộ thông qua giao thức Loopback (`127.0.0.1`).

### 2. Khởi Tạo ECS Service (`medflow-service`)
* **Deployment Configuration:** Thiết lập chạy trên ECS Cluster với `Desired tasks = 1`.
* **Networking & Security Groups:** Cấu hình Security Group cho Task sao cho chỉ cho phép lưu lượng Inbound ở cổng `3000` và `4000` đi qua nếu truy cập xuất phát từ Security Group của ALB (giúp chặn toàn bộ các truy cập trực tiếp không qua Load Balancer).
* **Load Balancing Integration:** Tích hợp dịch vụ ECS với ALB bằng cách trỏ container `medflow-client` (cổng `3000`) vào Target Group `medflow-client-tg` đã cấu hình trước đó.