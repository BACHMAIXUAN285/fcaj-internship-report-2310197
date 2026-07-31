---
title: "Khởi Tạo Và Triển Khai Dịch Vụ Trên AWS ECS"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

Toàn bộ ứng dụng được vận hành dưới dạng một ECS Task multi-container quản lý bởi AWS Fargate.

## Triển khai chạy ứng dụng trên ECS (Elastic Container Service)

Đây là nơi bạn "khởi động máy" để chạy các Image đã lưu ở Bước 1.

### 1. Tạo Task Definition (Bản thiết kế)
1. Vào **ECS** > **Task Definitions** > **Create new Task Definition**.
2. Đặt tên (VD: `medflow-task`).
3. **Infrastructure:** Chọn **AWS Fargate** (Serverless, không cần quản lý máy chủ vật lý).
4. **Task execution role:** Chọn role `ecsTaskExecutionRole` (Nếu có dùng Parameter Store/Secrets, đảm bảo Role này đã được cấp quyền `ssm:GetParameters`).
5. **Container 1 (Frontend):**
   - Đặt tên: `medflow-client`.
   - **Image URI:** Copy đường link Image URI từ ECR ở Bước 1 dán vào.
   - **Port mappings:** Mở cổng `3000` (Giao thức TCP).
   - Khai báo các biến môi trường nếu cần.
6. **Container 2 (Backend) - Bấm Add more containers:**
   - Đặt tên: `medflow-server`.
   - **Image URI:** Dán link ECR của Backend.
   - **Port mappings:** Mở cổng `4000`.
   - *Mẹo: Hai container chung 1 Task có thể gọi nhau qua `127.0.0.1`.*
7. Bấm **Create**.
![ECS cluster](/images/5-Workshop/5.4-deploy/ECS_cluster.png)

### 2. Tạo Service (Chạy thực tế)
1. Vào **ECS Clusters** > Chọn Cluster của bạn (hoặc tạo mới) > Tab **Services** > **Create**.
2. **Compute options:** Chọn Launch type là **Fargate**.
3. **Deployment configuration:**
   - Application type: **Service**.
   - Task Definition: Chọn bản thiết kế vừa tạo ở mục 3.1.
   - Service name: `medflow-service`.
   - Desired tasks: `1` (Số lượng bản sao muốn chạy).
4. **Networking:**
   - Chọn VPC và Subnets.
   - **Security Group (Tường lửa cho Container):** Tạo mới hoặc chọn SG đã có. **Quan trọng:** Mở Inbound Rules cho cổng `3000` và `4000`. An toàn nhất là thiết lập Source chỉ nhận traffic từ cái *Security Group của ALB*.
5. **Load balancing:**
   - Load balancer type: Chọn **Application Load Balancer**.
   - Container to load balance: Chọn container `medflow-client:3000`.
   - Use an existing target group: Chọn `medflow-client-tg` (đã tạo ở Bước 2).
6. Bấm **Create** và chờ quá trình Deploy diễn ra.
![ECS service](/images/5-Workshop/5.4-deploy/ECS_service.png)