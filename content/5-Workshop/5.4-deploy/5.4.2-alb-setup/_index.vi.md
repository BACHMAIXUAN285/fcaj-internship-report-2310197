---
title: "Cấu Hình Cân Bằng Tải Application Load Balancer (ALB)"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

## Thiết lập Cân bằng tải ALB (Application Load Balancer)

ALB đóng vai trò là "lễ tân" đón khách từ Internet và dẫn họ vào đúng Container của bạn.

1. **Tạo Target Group (Nhóm mục tiêu):**
   - Truy cập **EC2** > cuộn menu trái xuống mục **Target Groups** > **Create target group**.
   - **Target type:** Bắt buộc chọn **IP addresses** (vì ECS Fargate dùng IP tĩnh ảo cho container).
   - **Target group name:** Ví dụ `medflow-client-tg`.
   - **Protocol & Port:** `HTTP` và cổng `3000` (cổng của Frontend Next.js).
   - **VPC:** Chọn VPC mặc định.
   - **Health checks:** Để đường dẫn `/` (Next.js phải trả về 200 OK ở trang chủ).
   - *Lưu lại và bỏ qua bước chọn IP (ECS sẽ tự động điền IP vào đây sau).*
   ![EC2 Target group](/images/5-Workshop/5.4-deploy/EC2_target_group.png)

2. **Tạo Load Balancer:**
   - Vào **EC2** > **Load Balancers** > **Create Load Balancer**.
   - Chọn **Application Load Balancer**.
   - **Scheme:** Chọn **Internet-facing** (để ra Internet).
   - **Network mapping:** Chọn VPC mặc định, đánh dấu tích vào **tất cả các Subnets** (ít nhất 2 cái) để dự phòng.
   - **Security Groups (Tường lửa cho Lễ tân):** Tạo một SG mới, mở cổng `HTTP (80)` và `HTTPS (443)` cho Source `0.0.0.0/0` (tất cả mọi người).
   - **Listeners and routing:** Ở cổng HTTP:80, phần Default action, chọn **Forward to** và trỏ vào cái Target Group `medflow-client-tg` vừa tạo ở trên.
   - Bấm **Create**.
   ![EC2 Load Balencer](/images/5-Workshop/5.4-deploy/EC2_load_balancer.png)