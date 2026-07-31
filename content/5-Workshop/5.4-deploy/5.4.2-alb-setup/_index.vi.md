---
title: "5.4.2 Cấu Hình Cân Bằng Tải Application Load Balancer (ALB)"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

Để đảm bảo khả năng tiếp nhận và định tuyến lưu lượng mạng từ bên ngoài vào container, hạ tầng mạng ALB được thiết lập như sau:

### 1. Cấu Hình Target Group (`medflow-client-tg`)
* **Target Type:** Chọn `IP addresses` (bắt buộc khi tích hợp với mạng VPC của AWS Fargate).
* **Protocol & Port:** Giao thức `HTTP`, cổng `3000` (được định tuyến tới dịch vụ Frontend).
* **Health Check Configuration:** Thiết lập đường dẫn kiểm tra sức khỏe tại đường dẫn mốc `/` với giao thức `HTTP`. Điều kiện phản hồi hợp lệ là mã trạng thái `200 OK`.

### 2. Cấu Hình Application Load Balancer
* **Scheme:** Định cấu hình `Internet-facing` để mở công khai cho người dùng cuối.
* **Subnet Mapping:** Đăng ký ALB trên tối thiểu 2 Availability Zones (AZs) trong VPC mặc định nhằm tối ưu tính sẵn sàng.
* **Security Group (ALB SG):** Khởi tạo Security Group riêng cho ALB, định cấu hình Inbound Rules mở cổng `80 (HTTP)` và `443 (HTTPS)` cho địa chỉ IP nguồn `0.0.0.0/0`.
* **Listeners & Routing Rules:** Thiết lập quy tắc Listener ở cổng `80`, tự động chuyển hướng toàn bộ lưu lượng truy cập (Forward) về Target Group `medflow-client-tg`.