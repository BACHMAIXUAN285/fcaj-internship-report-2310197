---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Tích hợp dịch vụ **AWS CloudWatch** kết hợp **Langfuse** để giám sát (Monitoring), theo dõi hiệu năng hệ thống (CPU/Memory trên EC2, RDS PostgreSQL) và tập trung log hoạt động hệ thống cũng như log vận hành LLM.
* Hoàn thiện giao diện **Admin Portal** (dành cho Quản trị viên) phục vụ quản lý nhân sự Bác sĩ, tài khoản người dùng (Cognito RBAC) và xem báo cáo thống kê vận hành hệ thống.
* Hoàn thiện giao diện **Doctor Portal** tối ưu hóa công việc tra cứu: Cho phép Bác sĩ xem danh sách lịch hẹn đã đặt trong ngày và mở xem file báo cáo tóm tắt cuộc trò chuyện AI (Pre-consultation Report) từ Amazon S3.
* Hoàn thiện giao diện **Patient Portal (Mobile View)**: Hỗ trợ cập nhật thông tin y tế cá nhân, trò chuyện tư vấn với Chatbot AI RAG (LLM Router + Bedrock KB + GPT-4o-mini) và chọn khung giờ đặt lịch khám.
* Refactor mã nguồn, chuẩn hóa tài liệu API bằng **Swagger / OpenAPI Spec** và hoàn tất đóng gói toàn bộ ứng dụng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Thiết lập **AWS CloudWatch Logs Agent** trên EC2 để thu thập log từ Backend NestJS và Frontend Next.js. <br>- Tích hợp đồng bộ log giám sát LLM từ **Langfuse** về CloudWatch Logs; cấu hình **CloudWatch Alarms** tự động cảnh báo khi CPU/RAM EC2 vượt 80% hoặc đụng độ khóa dữ liệu trên RDS PostgreSQL. | 06/07/2026 | 06/07/2026 | [Tại đây](<https://docs.aws.amazon.com/cloudwatch/>) |
| 3   | - Hoàn thiện **Admin Portal** (Desktop UI): Xây dựng giao diện thêm mới/quản lý tài khoản Bác sĩ (gán nhóm Cognito `Doctor`), xem danh sách người dùng và thống kê tổng số lịch hẹn. <br>- Xây dựng giao diện cập nhật thông tin y tế cá nhân (nhóm máu, bệnh nền, dị ứng) cho Bệnh nhân. | 07/07/2026 | 07/07/2026 | [Tại đây](<https://docs.nestjs.com/techniques/database>) |
| 4   | - Hoàn thiện **Doctor Portal** (Desktop UI): Xây dựng màn hình danh sách ca khám đã được bệnh nhân đặt, cho phép mở xem file báo cáo tư vấn **Pre-consultation Report** từ Amazon S3 bằng Presigned URL. | 08/07/2026 | 08/07/2026 | [Tại đây](<https://docs.nestjs.com/guards>) |
| 5   | - Hoàn thiện **Patient Portal** (Mobile View): Tối ưu giao diện khung chat với AI Chatbot RAG tư vấn (hiển thị typing indicator, câu trả lời sinh từ GPT-4o-mini) và giao diện chọn khung giờ đặt lịch hẹn từ danh sách lịch làm việc trống của Bác sĩ. | 09/07/2026 | 09/07/2026 | [Tại đây](<https://nextjs.org/docs>) |
| 6   | - Refactor cấu trúc Code Backend/Frontend, bổ sung Validation DTOs cho các đầu API. <br>- Chuẩn hóa và tự động sinh tài liệu RESTful API bằng **Swagger / OpenAPI Spec** (`@nestjs/swagger`); tiến hành chạy thử nghiệm toàn bộ hệ thống (End-to-End Test). | 10/07/2026 | 10/07/2026 | [Tại đây](<https://docs.nestjs.com/openapi/introduction>) |


### Kết quả đạt được tuần 6:
* Triển khai thành công hệ thống giám sát **AWS CloudWatch** kết hợp **Langfuse**, thu thập log tập trung và cấu hình cảnh báo Alarms giúp phát hiện sớm rủi ro sự cố hạ tầng cũng như bất thường trong luồng phản hồi AI.
* Hoàn thiện **Admin Portal** hỗ trợ Quản trị viên dễ dàng quản lý danh mục Bác sĩ, phân quyền tài khoản Cognito và theo dõi số liệu vận hành.
* Xây dựng thành công **Doctor Portal** giao diện tinh gọn, giúp Bác sĩ dễ dàng nắm bắt danh sách ca khám trong ngày và đọc báo cáo tóm tắt câu hỏi của bệnh nhân do AI RAG tổng hợp trước ca tư vấn.
* Xây dựng giao diện **Patient Portal** thân thiện trên di động: hỗ trợ khai báo thông tin cá nhân, trò chuyện với Chatbot AI RAG tư vấn y tế và đặt lịch hẹn khám bệnh minh bạch.
* Đóng gói và chuẩn hóa toàn bộ tài liệu RESTful API của hệ thống bằng **Swagger (OpenAPI Spec)**.
* Rà soát, refactor lại toàn bộ mã nguồn, đảm bảo hệ thống vận hành an toàn, tin cậy, đạt chuẩn thiết kế Business Flow.


