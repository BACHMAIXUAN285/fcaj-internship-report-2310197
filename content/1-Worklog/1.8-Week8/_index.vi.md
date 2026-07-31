---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Hoàn thiện đóng gói container (Docker) và tự động hóa quy trình triển khai ứng dụng (CI/CD GitHub Actions) lên máy chủ **Amazon EC2**.
* Tối ưu hóa và kiểm thử tổng duyệt toàn bộ ứng dụng: **Admin Portal** (quản lý Bác sĩ, cấu hình RBAC), **Doctor Portal** (tra cứu ca khám & mở xem Pre-consultation Report từ S3) và **Patient Portal** (xem lịch hẹn & chat tư vấn AI RAG).
* Cấu hình tên miền, chứng chỉ bảo mật HTTPS/SSL và tối ưu hóa chi phí vận hành hạ tầng AWS Cloud.
* Chuẩn bị tài liệu kỹ thuật (Architecture Document), tài liệu API Swagger và hướng dẫn sử dụng (User Manual) cho Quản trị viên & Bác sĩ; tiến hành bàn giao nghiệm thu dự án.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Xây dựng Dockerfile tối ưu đa tầng (Multi-stage build) và docker-compose cho cả NestJS Backend và Next.js Frontend.<br>- Cấu hình quy trình CI/CD (GitHub Actions) để tự động hóa việc build Docker image và deploy ứng dụng lên máy chủ AWS EC2 khi push code về nhánh main. | 20/07/2026 | 20/07/2026 | [Tại đây](<https://docs.docker.com/>) |
| 3   | - Cấu hình hạ tầng Cloud production trên AWS: Cấu hình Reverse Proxy Nginx, HTTPS/SSL và cài đặt chứng chỉ SSL tự động gia hạn.<br>- Rà soát cấu hình **AWS CloudWatch Logs** kết hợp tích hợp log từ **Langfuse** để giám sát sự cố máy chủ và theo dõi hiệu năng vận hành LLM. | 21/07/2026 | 21/07/2026 | [Tại đây](<https://docs.aws.amazon.com/>) |
| 4   | - Tối ưu hóa giao diện các cổng quản trị theo Business Flow mới:<br>&emsp;+ **Admin Portal (Desktop View):** Tối ưu luồng khởi tạo/quản lý Bác sĩ, tự động phân quyền tài khoản qua AWS Cognito (`cognito:groups`) và xem thống kê tổng quan.<br>&emsp;+ **Doctor Portal (Desktop View):** Tối ưu giao diện danh sách ca khám trong ngày và tính năng tải/mở file báo cáo **Pre-consultation Report** lưu từ Amazon S3. | 22/07/2026 | 22/07/2026 | Internal Docs |
| 5   | - Kiểm thử tổng duyệt toàn hệ thống trên môi trường Production (Production Smoke Test) đảm bảo các kết nối giữa EC2, RDS PostgreSQL, Cognito, S3, AWS Bedrock KB, ViMQ, GPT-4o-mini và Langfuse vận hành trơn tru.<br>- Tối ưu hóa dung lượng build Frontend Next.js và bộ nhớ cache để giảm tối đa chi phí vận hành đám mây. | 23/07/2026 | 23/07/2026 | Internal Test |
| 6   | - Viết tài liệu bàn giao hệ thống: Tài liệu kiến trúc (Architecture Document), Hướng dẫn cài đặt/vận hành và Hướng dẫn sử dụng cho Quản trị viên (Admin Portal) & Bác sĩ (Doctor Portal).<br>- Tổng kết dự án, đánh giá kết quả đạt được và tiến hành nghiệm thu. | 24/07/2026 | 24/07/2026 | Project Deliverables |


### Kết quả đạt được tuần 8:

* Đã đóng gói ứng dụng thành công bằng Docker Containers và thiết lập xong pipeline CI/CD (GitHub Actions) tự động hóa 100% quá trình build & deploy hệ thống lên máy chủ AWS EC2.
* Hệ thống vận hành ổn định trên môi trường Production với đầy đủ chứng chỉ bảo mật HTTPS/SSL, kết nối mạng VPC an toàn và hệ thống giám sát AWS CloudWatch kết hợp Langfuse.
* Hoàn thiện mượt mà luồng nghiệp vụ trên các Portals: Quản trị viên khởi tạo và phân quyền RBAC cho Bác sĩ trơn tru qua Cognito; Bác sĩ tra cứu danh sách ca khám dễ dàng và mở đọc báo cáo tư vấn AI tóm tắt (Pre-consultation Report) từ Amazon S3 nhanh chóng.
* Cơ chế đặt lịch chống trùng slot (Pessimistic Locking `FOR UPDATE` trên RDS PostgreSQL) và bộ định tuyến RAG AI Chatbot (LLM Intent Router + AWS Bedrock KB + GPT-4o-mini + ViMQ) hoạt động chuẩn xác 100%.
* Hoàn thành đầy đủ bộ tài liệu kỹ thuật (Architecture Document, Swagger API Spec), tài liệu hướng dẫn vận hành và nghiệm thu dự án đúng tiến độ đề ra.


