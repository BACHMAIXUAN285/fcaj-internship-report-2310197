---
title: "5.4.4 Nghiệm Thu Và Kiểm Thử Triển Khai"
date: 2026-07-01
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

Sau khi hoàn tất khởi tạo ECS Service, tiến trình kiểm thử và đánh giá trạng thái triển khai được thực hiện qua các bước:

1. **Kiểm tra nhật ký hệ thống (Logs & Events):** Theo dõi tiến trình Pull Image từ ECR và chu trình khởi chạy container thông qua Amazon CloudWatch Logs được tích hợp sẵn.
2. **Kiểm tra Trạng thái Health Check:**
   * Truy cập **EC2 Management Console** > **Target Groups** > `medflow-client-tg`.
   * Quan sát mục **Targets:** Trạng thái chuyển đổi thành công từ `Initial` sang `Healthy` (màu xanh), xác nhận ứng dụng đã khởi động thành công và phản hồi chính xác các gói tin kiểm tra từ ALB.
3. **Xác nhận truy cập qua tên miền ALB:**
   * Lấy tên miền công khai (DNS Name) của Load Balancer (ví dụ: `medflow-alb-xxxxxx.elb.amazonaws.com`).
   * Thực hiện truy cập qua trình duyệt web. Ứng dụng hiển thị giao diện Frontend hoàn chỉnh và kết nối thành công với Backend API.