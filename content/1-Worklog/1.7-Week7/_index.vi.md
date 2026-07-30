---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Thực hiện kiểm thử toàn diện hệ thống (Functional Testing, Integration Testing, Stress Testing), đặc biệt là xử lý tranh chấp dữ liệu (Race Condition) khi bệnh nhân đặt lịch hẹn.
* Tối ưu hóa hiệu năng truy vấn CSDL AWS RDS và đảm bảo an toàn bảo mật dữ liệu y tế (UUID, CORS, Security Headers, Rate Limiting).
* Cải thiện tốc độ, trải nghiệm giao diện Patient Portal (Next.js Mobile-first) cũng như luồng Chatbot AI tư vấn & sàng lọc triệu chứng thời gian thực.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Thực hiện kiểm thử tải (Stress Testing / Load Testing) bằng công cụ (k6 / Artillery) giả lập hàng trăm request đặt lịch đồng thời.<br>- **Thực hành:** Kiểm tra tính đúng đắn của cơ chế Lock slot (Pessimistic Locking / Row-level Lock) trong CSDL để đảm bảo không xảy ra lỗi trùng slot (Race Condition / Double-booking). | 13/07/2026 | 13/07/2026 | [Tại đây](<https://k6.io/docs/>) |
| 3   | - Phân tích và tối ưu hóa các câu lệnh SQL trong ORM (Prisma/TypeORM).<br>- Thiết lập Indexing (Chỉ mục) cho các trường truy vấn tần suất cao trong AWS RDS PostgreSQL giúp giảm thời gian phản hồi API. | 14/07/2026 | 14/07/2026 | [Tại đây](<https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html>) |
| 4   | - Rà soát và kiểm thử bảo mật toàn bộ hệ thống:<br>&emsp;+ Xác minh tính bảo mật của việc dùng mã hóa UUID nhằm ngăn chặn lỗi lộ thông tin y tế (IDOR).<br>&emsp;+ Cấu hình Helmet, Rate Limiting và CORS Policy chặt chẽ trên NestJS Backend. | 15/07/2026 | 15/07/2026 | [Tại đây](<https://docs.nestjs.com/security/helmet>) |
| 5   | - Tối ưu hóa giao diện người dùng (UI/UX) trên Next.js Mobile View:<br>&emsp;+ Tăng tốc độ tải trang (Server-Side Rendering & Caching).<br>&emsp;+ Tối ưu hóa khung chat WebSocket, bổ sung trạng thái "AI đang gõ..." (Typing Indicator) và phản hồi lỗi mượt mà.<br>&emsp;+ Kiểm thử hiển thị Thẻ gợi ý đặt lịch (Card UI) và bảng chọn giờ trượt (Bottom Sheet). | 16/07/2026 | 16/07/2026 | [Tại đây](<https://nextjs.org/docs/app/building-your-application/optimizing>) |
| 6   | - Kiểm thử luồng End-to-End (E2E Testing) cho toàn bộ chu trình nghiệp vụ:<br>&emsp;**Xác thực Cognito & Khai báo y tế** --> **Trợ lý AI Triage & Tạo báo cáo** --> **Đặt lịch hẹn chuyên khoa (Bottom Sheet)** --> **Doctor Portal (Split View xem Báo cáo AI)** --> **Bác sĩ kết luận, kê đơn & Đẩy dữ liệu về App Bệnh nhân**. | 17/07/2026 | 17/07/2026 | Internal System Test |


### Kết quả đạt được tuần 7:

* Đã kiểm thử tải (Stress Testing) thành công, xác minh cơ chế Locking slot hoạt động chính xác 100%, bảo vệ hệ thống tuyệt đối khỏi bài toán Race Condition / Double-booking khi có nhiều bệnh nhân cùng thao tác đặt 1 slot khám.
* Tối ưu hóa thành công thời gian phản hồi của các API chính (giảm hơn 40% latency) nhờ việc tạo Index hợp lý trên CSDL AWS RDS.
* Đảm bảo an toàn bảo mật theo tiêu chuẩn dữ liệu y tế: Ẩn hoàn toàn thông tin định danh bệnh nhân qua mã hóa UUID, chặn các cuộc tấn công Brute-force/DDoS cơ bản nhờ Middleware Rate Limiting & Helmet Policy.
* Tối ưu hóa trải nghiệm người dùng trên Patient Portal: Giao diện Chatbot phản hồi thời gian thực mượt mà, hiển thị linh hoạt Card UI gợi ý chuyên khoa và Bottom Sheet đặt lịch tiện lợi.
* Hoàn thành kiểm thử E2E trơn tru cho toàn bộ luồng nghiệp vụ (từ lúc bệnh nhân chat với AI, đặt lịch, Bác sĩ đọc báo cáo AI chuẩn form trên Doctor Portal Split View cho tới khi chốt đơn thuốc đồng bộ về máy bệnh nhân), đảm bảo dữ liệu đồng bộ và không phát sinh lỗi giữa các dịch vụ AWS (Cognito, SageMaker, RDS, SES/SNS).


