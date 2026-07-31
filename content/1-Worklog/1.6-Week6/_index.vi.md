---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Kết nối Backend NestJS với mô hình AI trên **Amazon SageMaker Endpoint** để phân tích triệu chứng y tế và tự động khởi tạo **Báo cáo Y khoa Tóm tắt (Pre-consultation Report)**.
* Hoàn thiện giao diện **Admin Portal** (dành cho Quản trị viên Bệnh viện) để quản lý nhân sự, tự động gửi mật khẩu tạm qua AWS SES/Cognito và cấu hình lịch làm việc trống (Availability Calendar) cho Bác sĩ.
* Hoàn thiện giao diện **Doctor Portal (Split View UI)** hỗ trợ Bác sĩ xem báo cáo AI tóm tắt song song với form nhập chẩn đoán/kê đơn thuốc.
* Hoàn thiện giao diện **Patient Portal (Mobile UI)** hỗ trợ khai báo y tế ban đầu (Full-screen UI), giao tiếp AI Triage 3 cấp độ và đặt lịch chuyên khoa qua bảng chọn trượt (Bottom Sheet UI).
* Refactor mã nguồn, chuẩn hóa tài liệu API bằng **Swagger / OpenAPI Spec** và hoàn tất đóng gói toàn bộ dự án.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Tích hợp Backend NestJS với **Amazon SageMaker Endpoint**. <br>- Lập trình logic phân loại 3 mức độ nguy cơ dựa trên JSON trả về từ AI: **Đỏ** (Khóa chat + hiện nút lớn "Gọi 115"), **Xanh** (Hướng dẫn tự theo dõi tại nhà), **Vàng** (Hiển thị thẻ Card UI trỏ đúng Chuyên khoa cần khám). | 06/07/2026 | 06/07/2026 | [Tại đây](<https://docs.aws.amazon.com/sagemaker/>) |
| 3   | - Xây dựng Module **AI Pre-consultation Report**: Tự động trích xuất hội thoại Chatbot để AI tổng hợp thành Báo cáo y khoa tóm tắt. <br>- Đính kèm báo cáo vào mã số lịch hẹn trong CSDL PostgreSQL/DynamoDB[cite: 2, 8] để đẩy lên Dashboard của Bác sĩ. | 07/07/2026 | 07/07/2026 | [Tại đây](<https://docs.aws.amazon.com/sagemaker/latest/dg/realtime-endpoints.html>) |
| 4   | - Xây dựng **Admin Portal** (Desktop UI): Phát triển tính năng thêm Bác sĩ mới (tự động gọi Cognito API gửi mail mật khẩu tạm) và giao diện thiết lập Lịch trống làm việc theo tuần (Availability Calendar). <br>- Xây dựng form **Khai báo y tế ban đầu (Full-screen view)** trên Patient Portal lưu trữ nhóm máu, bệnh nền, dị ứng. | 08/07/2026 | 08/07/2026 | [Tại đây](<https://docs.nestjs.com/techniques/database>) |
| 5   | - Hoàn thiện **Doctor Portal** áp dụng NestJS Guard & RBAC: Thiết kế màn hình **Split View** (Một nửa hiển thị Hồ sơ cũ + Báo cáo tóm tắt AI, một nửa là form chẩn đoán và kê đơn thuốc). <br>- Hoàn thiện luồng **Patient Booking**: Thiết kế giao diện trượt **Bottom Sheet** chọn ngày/giờ khám từ lịch trống bác sĩ và tự động nhận đơn thuốc/chẩn đoán trên Mobile. | 09/07/2026 | 09/07/2026 | [Tại đây](<https://docs.nestjs.com/guards>) |
| 6   | - Refactor cấu trúc Code, tối ưu DTOs và bổ sung Validation chặt chẽ cho tất cả dữ liệu đầu vào. <br>- Chuẩn hóa và đóng gói tài liệu RESTful API bằng **Swagger / OpenAPI Spec**; tiến hành chạy thử nghiệm toàn bộ hệ thống (End-to-End Test). | 10/07/2026 | 10/07/2026 | [Tại đây](<https://docs.nestjs.com/openapi/introduction>) |


### Kết quả đạt được tuần 6:
* Kết nối thành công Backend NestJS với **Amazon SageMaker Endpoint**, phân loại chuẩn xác 3 mức độ nguy cơ (Đỏ, Xanh, Vàng) và tự động xuất **Báo cáo Y khoa Tóm tắt (Pre-consultation Report)**.
* Hoàn thiện **Admin Portal** hỗ trợ Quản trị viên khởi tạo tài khoản Bác sĩ (gửi mail mật khẩu tạm qua AWS SES/Cognito) và cấu hình linh hoạt Lịch làm việc trống.
* Xây dựng thành công **Doctor Portal** với thiết kế **Split View** tối ưu, giúp Bác sĩ đọc ngay tóm tắt AI mà không cần đọc lại lịch sử chat dài dòng trước khi nhập chẩn đoán/kê đơn.
* Xây dựng giao diện **Patient Portal Mobile-friendly**: hỗ trợ form Khai báo y tế ban đầu, đặt lịch khám mượt mà qua giao diện trượt Bottom Sheet và nhận đơn thuốc điện tử tức thì.
* Đóng gói và chuẩn hóa toàn bộ tài liệu RESTful API của hệ thống bằng **Swagger (OpenAPI Spec)**.
* Rà soát, refactor lại toàn bộ mã nguồn, đảm bảo hệ thống vận hành an toàn, tin cậy, đạt chuẩn thiết kế Business Flow.


