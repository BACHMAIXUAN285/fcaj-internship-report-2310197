---
title: "Đóng Gói Và Lưu Trữ Image Trên AWS ECR"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

Quá trình triển khai bắt đầu bằng việc tạo kho lưu trữ hình ảnh ứng dụng và đẩy các bản đóng gói (Docker Images) lên AWS ECR.

## Đẩy Image lên kho chứa ECR (Elastic Container Registry)

ECR đóng vai trò như một "nhà kho" để lưu trữ các bản đóng gói (Docker Image) mã nguồn của bạn.

1. **Tạo Repository (Kho chứa):**
   * Truy cập **AWS ECR** > **Repositories** > **Create repository**.
   * Tạo 2 kho riêng biệt: ví dụ `medflow-client` (cho Frontend Next.js) và `medflow-server` (cho Backend NestJS).
   * Để chế độ **Private**.
  ![ECR](/images/5-Workshop/5.4-deploy/ECR.png)

2. **Build và Push Image (Thường được tự động hóa bằng GitHub Actions):**
   * Nếu làm thủ công, bạn bấm vào nút **View push commands** ở góc phải repo. AWS sẽ cung cấp 4 lệnh chuẩn:
     1. *Đăng nhập Docker vào AWS:*
        ```bash
        aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
        ```
     2. *Build ảnh:*
        ```bash
        docker build -t medflow-client .
        ```
     3. *Gắn thẻ:*
        ```bash
        docker tag medflow-client:latest <aws_account_id>.dkr.ecr.<region>[.amazonaws.com/medflow-client:latest](https://.amazonaws.com/medflow-client:latest)
        ```
     4. *Đẩy lên cloud:*
        ```bash
        docker push <aws_account_id>.dkr.ecr.<region>[.amazonaws.com/medflow-client:latest](https://.amazonaws.com/medflow-client:latest)
        ```