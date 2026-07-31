---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Thực hiện kiểm thử toàn diện hệ thống (Functional Testing, Integration Testing, Stress Testing), đặc biệt là kiểm thử khả năng xử lý tranh chấp dữ liệu (Race Condition) khi bệnh nhân đặt trùng khung giờ khám.
* Tối ưu hóa hiệu năng truy vấn CSDL AWS RDS PostgreSQL (`healthcare-db`) và đảm bảo an toàn bảo mật dữ liệu y tế (UUID ẩn danh, CORS, Security Headers, Rate Limiting).
* Cải thiện tốc độ, trải nghiệm giao diện Patient Portal (Next.js Mobile View) cũng như hiệu năng trò chuyện thời gian thực với Trợ lý Chatbot AI RAG (LLM Router + Bedrock KB + GPT-4o-mini + ViMQ).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Thực hiện kiểm thử tải (Stress Testing / Load Testing) bằng công cụ (k6 / Artillery) giả lập hàng trăm request đặt lịch đồng thời.<br>- **Thực hành:** Kiểm tra tính đúng đắn của cơ chế **Pessimistic Locking (`FOR UPDATE`)** trong PostgreSQL để đảm bảo không xảy ra lỗi trùng slot (Race Condition / Double-booking). | 13/07/2026 | 13/07/2026 | [Tại đây](<https://k6.io/docs/>) |
| 3   | - Phân tích và tối ưu hóa các câu lệnh SQL trong Prisma ORM.<br>- Thiết lập Indexing (Chỉ mục) cho các trường truy vấn tần suất cao (UUID người dùng, ID bác sĩ, trạng thái lịch hẹn) trong AWS RDS PostgreSQL giúp giảm thời gian phản hồi API. | 14/07/2026 | 14/07/2026 | [Tại đây](<https://www.postgresql.org/docs/current/indexes.html>) |
| 4   | - Rà soát và kiểm thử bảo mật toàn bộ hệ thống:<br>&emsp;+ Xác minh tính bảo mật của việc dùng định danh mã hóa UUID (Anonymization) từ Cognito nhằm ngăn chặn rủi ro lộ thông tin cá nhân.<br>&emsp;+ Cấu hình Helmet, Rate Limiting và CORS Policy chặt chẽ trên NestJS Backend. | 15/07/2026 | 15/07/2026 | [Tại đây](<https://docs.nestjs.com/security/helmet>) |
| 5   | - Tối ưu hóa giao diện người dùng (UI/UX) trên Next.js Mobile View:<br>&emsp;+ Tăng tốc độ tải trang (Server-Side Rendering & Caching).<br>&emsp;+ Tối ưu hóa khung chat RAG tư vấn, bổ sung trạng thái "AI đang gõ..." (Typing Indicator) và xử lý lỗi mượt mà khi mất kết nối.<br>&emsp;+ Kiểm thử hiển thị danh sách lịch trống của Bác sĩ và chọn khung giờ đặt lịch. | 16/07/2026 | 16/07/2026 | [Tại đây](<https://nextjs.org/docs/app/building-your-application/optimizing>) |
| 6   | - Kiểm thử luồng End-to-End (E2E Testing) cho toàn bộ chu trình nghiệp vụ:<br>&emsp;**Xác thực Cognito & Khai báo y tế** --> **Trò chuyện tư vấn với Chatbot AI RAG (Bedrock KB + GPT-4o-mini + ViMQ) & Lưu báo cáo lên S3** --> **Giám sát LLM qua Langfuse** --> **Đặt lịch hẹn chuyên khoa** --> **Doctor Portal tra cứu danh sách ca khám & mở xem Báo cáo AI từ S3**. | 17/07/2026 | 17/07/2026 | Internal System Test |


### Kết quả đạt được tuần 7:

* Đã kiểm thử tải (Stress Testing) thành công bằng k6, xác minh cơ chế **Pessimistic Locking (`FOR UPDATE`)** hoạt động chính xác 100%, bảo vệ hệ thống tuyệt đối khỏi bài toán Race Condition / Double-booking khi có nhiều bệnh nhân cùng thao tác đặt 1 slot khám.
* Tối ưu hóa thành công thời gian phản hồi của các API chính (giảm hơn 40% latency) nhờ việc tạo Index hợp lý trên CSDL AWS RDS PostgreSQL.
* Đảm bảo an toàn bảo mật theo tiêu chuẩn dữ liệu y tế: Ẩn hoàn toàn thông tin định danh bệnh nhân qua mã hóa UUID từ Cognito, chặn các cuộc tấn công Brute-force/DDoS cơ bản nhờ Middleware Rate Limiting & Helmet Policy.
* Tối ưu hóa trải nghiệm người dùng trên Patient Portal: Giao diện Chatbot AI RAG tư vấn phản hồi mượt mà, hỗ trợ giao tiếp thời gian thực tiện lợi.
* Hoàn thành kiểm thử E2E trơn tru cho toàn bộ luồng nghiệp vụ (từ lúc bệnh nhân chat với AI tư vấn, lưu tệp Pre-consultation Report lên Amazon S3, chọn lịch hẹn cho tới khi Bác sĩ mở tra cứu danh sách lịch khám trên Doctor Portal), đảm bảo dữ liệu đồng bộ và không phát sinh lỗi giữa các dịch vụ (Cognito, AWS Bedrock KB, GPT-4o-mini, ViMQ, Langfuse, RDS, S3, CloudWatch).


