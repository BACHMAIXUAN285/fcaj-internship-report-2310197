---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Kết nối Backend NestJS với mô hình AI triển khai trên Amazon SageMaker để phân tích triệu chứng y tế và tự động khởi tạo Báo cáo Tóm tắt (Summary Report).
* Xây dựng Module quản lý thu phí trực tiếp tại cơ sở y tế (Thanh toán phí dịch vụ/khám tại quầy lễ tân) và ghi nhận trạng thái thanh toán.
* Xây dựng giao diện Dashboard phân quyền theo vai trò (Role-Based Access Control) cho Bác sĩ và Lễ tân; refactor mã nguồn và chuẩn hóa tài liệu RESTful API.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Tích hợp Backend NestJS với mô hình AI chạy trên **Amazon SageMaker Endpoint**.<br>- Phát triển logic phân loại 3 mức độ nguy cơ (Đỏ - Vàng - Xanh) dựa trên kết quả trả về từ AI và điều hướng luồng giao diện người dùng. | 06/07/2026 | 06/07/2026 | [Tại đây](<https://docs.aws.amazon.com/sagemaker/>) |
| 3   | - Xây dựng Module AI Pre-consultation: Tự động trích xuất lịch sử đoạn chat để AI tổng hợp thành **Báo cáo Tóm tắt chuẩn y khoa**.<br>- Đính kèm báo cáo vào lịch hẹn tương ứng trong CSDL để phục vụ việc tra cứu trên Portal của Bác sĩ. | 07/07/2026 | 07/07/2026 | [Tại đây](<https://docs.aws.amazon.com/sagemaker/latest/dg/realtime-endpoints.html>) |
| 4   | - Xây dựng Module Thanh toán trực tiếp (**In-person Payment / POS**) trong NestJS.<br>- **Thực hành:** Thiết kế Database Schema lưu trữ hóa đơn, viết API tạo hóa đơn thu phí trực tiếp tại quầy, cập nhật trạng thái phiếu khám và in biên lai thanh toán. | 08/07/2026 | 08/07/2026 | [Tại đây](<https://docs.nestjs.com/techniques/database>) |
| 5   | - Xây dựng Portal dành cho Nhân viên Y tế áp dụng **Role-Based Access Control (RBAC)** với NestJS Guard:<br>&emsp;+ **Doctor Dashboard:** Xem danh sách lịch hẹn, đọc Báo cáo Tóm tắt AI, nhập chẩn đoán cuối cùng và kê đơn thuốc.<br>&emsp;+ **Receptionist Dashboard:** Check-in bệnh nhân, thực hiện thu tiền mặt/quẹt thẻ trực tiếp tại quầy và xuất hóa đơn. | 09/07/2026 | 09/07/2026 | [Tại đây](<https://docs.nestjs.com/guards>) |
| 6   | - Refactor cấu trúc Code, tối ưu hóa các DTO (Data Transfer Object) và bổ sung Validation chặt chẽ cho dữ liệu đầu vào.<br>- Chuẩn hóa và đóng gói tài liệu API bằng **Swagger / OpenAPI Spec**. | 10/07/2026 | 10/07/2026 | [Tại đây](<https://docs.nestjs.com/openapi/introduction>) |


### Kết quả đạt được tuần 6:
* Kết nối thành công Backend NestJS với **Amazon SageMaker Endpoint**, trích xuất chính xác thông tin triệu chứng từ Chatbot và tự động xuất **Báo cáo Tóm tắt chuẩn y khoa**, giúp bác sĩ nắm bắt nhanh lịch sử bệnh án trước phiên khám.
* Hoàn thiện luồng xử lý phân loại 3 cấp độ nguy hiểm:
   * **Đỏ:** Cảnh báo khẩn cấp / Hướng dẫn gọi cấp cứu 115.
   * **Vàng:** Điều hướng bệnh nhân sang màn hình Đặt lịch khám.
   * **Xanh:** Đưa ra lời khuyên tự chăm sóc sức khỏe tại nhà.
* Hoàn thiện Module Quản lý Thu phí & Hóa đơn trực tiếp tại cơ sở y tế.
* Xây dựng API và giao diện cho phép Lễ tân thu phí trực tiếp (Tiền mặt / POS quẹt thẻ), tự động cập nhật trạng thái lịch hẹn từ `UNPAID` sang `PAID` và xuất biên lai thanh toán cho bệnh nhân.
* Xây dựng hệ thống Portal phân quyền chuẩn xác với NestJS Guard:
   * **Doctor Dashboard:** Bác sĩ tra cứu báo cáo AI, cập nhật kết quả chẩn đoán và kê đơn thuốc.
   * **Receptionist Dashboard:** Lễ tân tiếp nhận check-in bệnh nhân, tính tổng chi phí (phí khám + tiền thuốc/dịch vụ phát sinh) và thu tiền trực tiếp tại quầy.
* Đóng gói và chuẩn hóa toàn bộ tài liệu RESTful API của hệ thống bằng **Swagger (OpenAPI Spec)**.
* Rà soát, refactor lại mã nguồn và áp dụng DTO Validation toàn diện, đảm bảo tính an toàn, tin cậy và dễ bảo trì cho toàn bộ dự án.


