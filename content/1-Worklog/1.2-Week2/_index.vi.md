---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Thiết kế sơ đồ ERD cho cơ sở dữ liệu quan hệ (PostgreSQL) và xây dựng cấu trúc các Module cốt lõi cho Backend NestJS (bao gồm Module **LLM Intent Router** cho bộ AI).
* Tích hợp **AWS Cognito SDK** ở Backend để xử lý luồng xác thực (Authentication & Authorization) cho 3 nhóm vai trò: Admin, Bác sĩ và Bệnh nhân theo chuẩn RBAC (kiểm tra `cognito:groups` qua JWKS).
* Lập trình các API RESTful quan trọng theo Business Flow mới: API Đăng ký / Đăng nhập tài khoản, API Bệnh nhân điền Form khai báo thông tin cá nhân/tiền sử y tế ban đầu, và API Quản lý danh mục Bác sĩ/Lịch làm việc.
* Phát triển giao diện Responsive người dùng Frontend (Next.js) cho các luồng: Doctor Portal (đăng nhập, xem danh sách ca khám và quản lý khung giờ làm việc) và Patient Mobile Web App (Form khai báo thông tin y tế ban đầu & khung chat AI).
* Kết nối API Frontend - Backend, xử lý CORS, đồng bộ trạng thái (React Query) và Container hóa ứng dụng bằng Docker Compose để chạy cục bộ.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Thiết kế sơ đồ ERD chi tiết cho PostgreSQL (Bệnh nhân, Khai báo thông tin y tế, Bác sĩ, Khung giờ làm việc, Lịch hẹn).<br>- Khởi tạo cấu trúc các Module, Controller và Service trong NestJS (AuthModule, UserModule, DoctorModule, PatientModule, LlmModule). | 08/06/2026 | 08/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 3   | - Tích hợp **AWS Cognito SDK** vào NestJS AuthModule: Viết Passport JWT Strategy tự động verify Token qua JWKS Public Key của Cognito.<br>- Xây dựng RESTful API cho **Giai đoạn 1 & 2**: API Đăng ký/Đăng nhập (Cognito User Pool), API Bệnh nhân cập nhật Form khai báo thông tin y tế ban đầu (tuổi, nhóm máu, bệnh nền, dị ứng) và API cấu hình lịch làm việc cho Bác sĩ. | 09/06/2026 | 09/06/2026 | [Tại đây](<https://docs.nestjs.com/>) |
| 4   | - Xây dựng giao diện Web Next.js & TailwindCSS chuẩn hóa theo Business Flow mới.<br>- Thiết kế **Doctor Portal (Desktop View)**: Màn hình Quản lý / Thiết lập lịch làm việc trong tuần, khung giao diện Xem danh sách ca khám.<br>- Thiết kế **Patient App (Mobile View)**: Form khai báo thông tin y tế ban đầu và khung giao diện chat tư vấn y tế. | 10/06/2026 | 10/06/2026 | [Tại đây](<https://nextjs.org/docs>) |
| 5   | - Tích hợp gọi API từ Next.js sang NestJS Backend bằng Axios & React Query.<br>- Cấu hình NestJS Guards/Middleware kiểm tra Token JWT từ Cognito, xử lý phân quyền RBAC (Patient/Doctor/Admin) và cấu hình CORS. | 11/06/2026 | 11/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 6   | - Viết file Dockerfile cho ứng dụng Frontend Next.js và Backend NestJS.<br>- Tích hợp container PostgreSQL cục bộ bằng Docker Compose để đóng gói và khởi chạy toàn bộ ứng dụng ở môi trường Local. | 12/06/2026 | 12/06/2026 | [Tại đây](<https://docs.docker.com/>) |


### Kết quả đạt được tuần 2:

* Hoàn thành sơ đồ cơ sở dữ liệu ERD cho PostgreSQL, định hình rõ các bảng lưu trữ thông tin y tế nhạy cảm, thông tin tài khoản ẩn danh (UUID) và lịch làm việc của bác sĩ.
* Xây dựng thành công hệ thống xác thực tập trung qua **AWS Cognito**, xử lý luồng Đăng ký/Đăng nhập mượt mà và tự động phân quyền RBAC cho các vai trò (Patient, Doctor, Admin).
* Hoàn thiện giao diện Next.js đáp ứng đúng Business Flow: Form khai báo thông tin y tế ban đầu/khung chat AI cho Bệnh nhân trên di động và màn hình Quản lý lịch làm việc/Danh sách lịch hẹn cho Bác sĩ trên Desktop.
* Tích hợp kết nối end-to-end mượt mà giữa Frontend và Backend, xử lý phân quyền RBAC chặt chẽ thông qua JWKS Endpoint verification của Cognito.
* Container hóa thành công hệ thống với Docker Compose, sẵn sàng cho bước triển khai hạ tầng Cloud AWS và dịch vụ AI ở các tuần tiếp theo.

