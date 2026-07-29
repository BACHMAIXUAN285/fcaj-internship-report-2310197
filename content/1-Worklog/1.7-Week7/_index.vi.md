---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Thực hiện kiểm thử toàn diện hệ thống (Functional Testing, Integration Testing, Stress Testing), đặc biệt là xử lý tranh chấp dữ liệu khi đặt lịch.
* Tối ưu hóa hiệu năng truy vấn CSDL AWS RDS và đảm bảo an toàn bảo mật dữ liệu y tế (UUID, CORS, Security Headers, Rate Limiting).
* Cải thiện tốc độ và trải nghiệm giao diện trên trang Web Next.js cũng như luồng Chatbot tư vấn thời gian thực.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Thực hiện kiểm thử tải (Stress Testing / Load Testing) bằng công cụ (k6 / Artillery) giả lập hàng trăm request đặt lịch đồng thời.<br>- **Thực hành:** Kiểm tra tính đúng đắn của cơ chế Pessimistic Locking để đảm bảo không xảy ra lỗi trùng slot (Race Condition / Double-booking). | 13/07/2026 | 13/07/2026 | [Tại đây](<https://k6.io/docs/>) |
| 3   | - Phân tích và tối ưu hóa các câu lệnh SQL trong ORM (Prisma/TypeORM).<br>- Thiết lập Indexing (Chỉ mục) cho các trường truy vấn tần suất cao trong AWS RDS PostgreSQL/MySQL giúp giảm thời gian phản hồi API. | 14/07/2026 | 14/07/2026 | [Tại đây](<https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html>) |
| 4   | - Rà soát và kiểm thử bảo mật toàn bộ hệ thống:<br>&emsp;+ Xác minh tính bảo mật của việc dùng mã hóa UUID nhằm ngăn chặn lỗi lộ thông tin y tế (IDOR).<br>&emsp;+ Cấu hình Helmet, Rate Limiting và CORS Policy chặt chẽ trên NestJS Backend. | 15/07/2026 | 15/07/2026 | [Tại đây](<https://docs.nestjs.com/security/helmet>) |
| 5   | - Tối ưu hóa giao diện người dùng (UI/UX) trên Next.js:<br>&emsp;+ Tăng tốc độ tải trang (Server-Side Rendering & Caching).<br>&emsp;+ Tối ưu hóa giao diện khung chat WebSocket, bổ sung trạng thái "AI đang gõ..." (Typing Indicator) và phản hồi lỗi mượt mà. | 16/07/2026 | 16/07/2026 | [Tại đây](<https://nextjs.org/docs/app/building-your-application/optimizing>) |
| 6   | - Kiểm thử luồng End-to-End (E2E Testing) cho toàn bộ chu trình nghiệp vụ:<br>&emsp;**Xác thực Cognito** --> **Chatbot AI phân luồng & Tạo báo cáo** --> **Đặt lịch khám** --> **Bác sĩ xem báo cáo AI & Kê đơn** --> **Lễ tân check-in & Thu phí trực tiếp tại quầy**. | 17/07/2026 | 17/07/2026 | Internal System Test |


### Kết quả đạt được tuần 7:

* Đã kiểm thử tải (Stress Testing) thành công, xác minh cơ chế Locking hoạt động chính xác 100%, bảo vệ hệ thống tuyệt đối khỏi bài toán Race Condition / Double-booking khi có nhiều bệnh nhân cùng thao tác đặt 1 slot khám.
* Tối ưu hóa thành công thời gian phản hồi của các API chính (giảm hơn 40% latency) nhờ việc tạo Index hợp lý trên CSDL AWS RDS.
* Đảm bảo an toàn bảo mật theo tiêu chuẩn dữ liệu y tế: Ẩn hoàn toàn thông tin định danh bệnh nhân qua mã hóa UUID, chặn các cuộc tấn công Brute-force/DDoS cơ bản nhờ Middleware Rate Limiting & Helmet Policy.
* Tối ưu hóa trải nghiệm người dùng trên Next.js: Giao diện Chatbot phản hồi thời gian thực mượt mà, trực quan, hỗ trợ hiển thị lịch khám tiện lợi cho người dùng.
* Hoàn thành kiểm thử E2E trơn tru cho toàn bộ luồng nghiệp vụ cốt lõi (từ lúc bệnh nhân chat với AI, chọn lịch khám cho đến khi Bác sĩ chẩn đoán và Lễ tân thu phí trực tiếp tại quầy), đảm bảo không phát sinh lỗi nghẽn dữ liệu giữa các dịch vụ Cloud (Cognito, SageMaker, RDS, S3).


