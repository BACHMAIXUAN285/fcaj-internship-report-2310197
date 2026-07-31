---
title: "5.4.1 Đóng Gói Và Lưu Trữ Image Trên AWS ECR"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

Quá trình triển khai bắt đầu bằng việc tạo kho lưu trữ hình ảnh ứng dụng và đẩy các bản đóng gói (Docker Images) lên AWS ECR.

### 1. Khởi Tạo Repositories
Tạo hai repositories ở chế độ riêng tư (Private) trên AWS ECR phục vụ lưu trữ riêng biệt cho hai thành phần:

* `medflow-client`: Lưu trữ Docker Image của Frontend (Next.js).
* `medflow-server`: Lưu trữ Docker Image của Backend (NestJS).

### 2. Xây Dựng Và Đẩy Image (Build & Push)
Thực hiện quy trình authentication và đóng gói thông qua AWS CLI & Docker Engine:

* **Xác thực AWS CLI với Registry:**
  ```bash
  aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
* **Đóng gói, gắn nhãn (Tagging) và đẩy Image lên ECR:**
  ```bash
  docker build -t medflow-client .
  docker tag medflow-client:latest <aws_account_id>.dkr.ecr.<region>[.amazonaws.com/medflow-client:latest](https://.amazonaws.com/medflow-client:latest)
  docker push <aws_account_id>.dkr.ecr.<region>[.amazonaws.com/medflow-client:latest](https://.amazonaws.com/medflow-client:latest)