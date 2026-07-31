---
title: "Nghiệm Thu Và Kiểm Thử Triển Khai"
date: 2026-07-01
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

Sau khi hoàn tất khởi tạo ECS Service, tiến trình kiểm thử và đánh giá trạng thái triển khai được thực hiện qua các bước:

## Bước 4: Kiểm tra và Kiểm Thử Triển Khai
1. Vào tab **Logs** hoặc **Events** của ECS Service để theo dõi quá trình kéo Image và khởi động.
2. Quay lại giao diện **EC2** > **Target Groups**, bấm vào `medflow-client-tg`.
3. Nhìn xuống tab **Targets**. Ban đầu sẽ hiện *Initial*, nếu mọi cấu hình chuẩn xác (không bị sập code, không chặn tường lửa), nó sẽ chuyển sang **Healthy** (Màu xanh).
4. Mở **Load Balancers**, copy **DNS name** (ví dụ: `medflow-alb-...elb.amazonaws.com`) dán vào trình duyệt và chiêm ngưỡng thành quả trang web của bạn chạy trên Internet.