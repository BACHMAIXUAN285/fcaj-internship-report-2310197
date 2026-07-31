---
title : "Triển Khai Hệ Thống"
date : 2026-07-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Tổng quan kiến trúc triển khai

Sau khi hoàn thành giai đoạn phát triển và đóng gói ứng dụng bằng công nghệ Containerization (Docker), hệ thống **MedFlow** được triển khai lên hạ tầng điện toán đám mây Amazon Web Services (AWS). Mô hình sử dụng kiến trúc Serverless Container trên AWS ECS Fargate kết hợp với Application Load Balancer (ALB) nhằm đảm bảo tính sẵn sàng cao (High Availability), khả năng mở rộng linh hoạt (Scalability) và tối ưu hóa chi phí vận hành.


#### Nội dung

- [Đóng Gói Và Lưu Trữ Image Trên AWS ECR](5.4.1-ecr-push/)
- [Cấu Hình Cân Bằng Tải Application Load Balancer (ALB)](5.4.2-alb-setup/)
- [Khởi Tạo Và Triển Khai Dịch Vụ Trên AWS ECS](5.4.3-ecs-deployment/)
- [Kiểm tra Và Kiểm Thử Triển Khai](5.4.4-acceptance-testing/)