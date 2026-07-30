---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Thiết kế sơ đồ ERD cho cơ sở dữ liệu quan hệ (PostgreSQL) và xây dựng cấu trúc các Module cốt lõi cho Backend NestJS.
* Tích hợp **AWS Cognito SDK** ở Backend để xử lý luồng xác thực (Authentication & Authorization) cho 3 nhóm vai trò: Admin, Bác sĩ và Bệnh nhân theo chuẩn RBAC.
* Lập trình các API RESTful quan trọng theo Business Flow v2: API Admin Onboarding Bác sĩ (khởi tạo tài khoản & gửi Temporary Password qua SES), API Bệnh nhân đăng ký (tự động gán role `Patient`), và API điền Form khai báo y tế ban đầu.
* Phát triển giao diện Responsive người dùng Frontend (Next.js 14) cho các luồng: Doctor Portal (đăng nhập Temp Password & bắt buộc đổi mật khẩu lần đầu, thiết lập lịch trống) và Patient Mobile Web App (Form khai báo y tế ban đầu full-screen).
* Kết nối API Frontend - Backend, xử lý CORS, đồng bộ trạng thái (React Query) và Container hóa ứng dụng bằng Docker Compose để chạy cục bộ.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Thiết kế sơ đồ ERD chi tiết cho PostgreSQL (Bệnh nhân, Khai báo y tế, Bác sĩ, Khung giờ làm việc, Lịch hẹn).<br>- Khởi tạo cấu trúc các Module, Controller và Service trong NestJS (AuthModule, UserModule, DoctorModule, PatientModule). | 08/06/2026 | 08/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 3   | - Tích hợp **AWS Cognito SDK** vào NestJS AuthModule: Viết middleware verify JWT Token qua Public Key của Cognito.<br>- Xây dựng RESTful API cho **Giai đoạn 1 & 2**: Admin tạo tài khoản Bác sĩ (gửi Temporary Password qua AWS SES), API cho Bác sĩ đổi mật khẩu ở lần đăng nhập đầu tiên, và API Bệnh nhân điền Form khai báo y tế ban đầu (tuổi, nhóm máu, bệnh nền, dị ứng). | 09/06/2026 | 09/06/2026 | [Tại đây](<https://docs.nestjs.com/>) |
| 4   | - Xây dựng giao diện Web Next.js 14 & TailwindCSS chuẩn hóa theo Business Flow v2.<br>- Thiết kế **Doctor Portal (Desktop)**: Giao diện đổi mật khẩu lần đầu, màn hình "Thiết lập Lịch trống" trong tuần.<br>- Thiết kế **Patient App (Mobile)**: Form khai báo y tế ban đầu toàn màn hình (Full-screen View). | 10/06/2026 | 10/06/2026 | [Tại đây](<https://nextjs.org/docs>) |
| 5   | - Tích hợp gọi API từ Next.js 14 sang NestJS Backend bằng Axios & React Query.<br>- Cấu hình NestJS Guards/Middleware kiểm tra Token JWT từ Cognito, xử lý phân quyền (Patient/Doctor/Admin) và xử lý CORS. | 11/06/2026 | 11/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 6   | - Viết file Dockerfile cho ứng dụng Frontend Next.js 14 và Backend NestJS.<br>- Tích hợp container PostgreSQL cục bộ để đóng gói và khởi chạy toàn bộ ứng dụng ở môi trường Local. | 12/06/2026 | 12/06/2026 | [Tại đây](<https://docs.docker.com/>) |


### Kết quả đạt được tuần 2:

* Hoàn thành sơ đồ cơ sở dữ liệu ERD cho PostgreSQL, định hình rõ các bảng lưu trữ thông tin y tế nhạy cảm và lịch làm việc của bác sĩ.
* Xây dựng thành công hệ thống xác thực chuẩn hóa qua **AWS Cognito**, xử lý mượt mà luồng Temporary Password cho nhân viên y tế và Onboarding tự động cho bệnh nhân.
* Hoàn thiện giao diện Next.js 14 đáp ứng đúng Business Flow: Form khai báo y tế ban đầu cho Bệnh nhân trên Mobile và màn hình Kích hoạt tài khoản/Thiết lập lịch trống cho Bác sĩ trên Desktop.
* Tích hợp kết nối end-to-end mượt mà giữa Frontend và Backend, xử lý phân quyền RBAC chặt chẽ thông qua Cognito Public Key verification.
* Container hóa thành công hệ thống với Docker Compose, sẵn sàng cho bước triển khai hạ tầng Cloud AWS ở Tuần 3.

