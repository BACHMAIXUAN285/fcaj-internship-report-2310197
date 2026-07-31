---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Triển khai ứng dụng Web Healthcare lên hạ tầng đám mây AWS sử dụng kết hợp **Amazon EC2** cho Server tính toán và **Amazon S3** cho lưu trữ đối tượng (ảnh đại diện bác sĩ, hồ sơ bệnh án, mã QR).
* Cấu hình **Amazon Cognito** xử lý xác thực (Authentication) và phân quyền dựa trên vai trò (Role-based: Admin, Doctor, Patient) phù hợp với Business Flow.
* Tích hợp dịch vụ **Amazon S3** vào Backend (NestJS) để quản lý tải lên/tải về tài liệu y tế và tích hợp **AWS SES/SNS** gửi thông báo/mật khẩu tạm thời.
* Thiết lập **AWS API Gateway** (hoặc Nginx Reverse Proxy trên EC2) để định tuyến các yêu cầu (Routing), áp dụng Rate Limiting và bảo vệ hệ thống API Backend.
* Kiểm thử tích hợp luồng **Trợ lý AI Sàng lọc Triệu chứng (AI Triage)** và tính năng tự động tạo **Báo cáo y khoa tóm tắt (Pre-consultation Report)** đẩy về Doctor Portal.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Khởi tạo **EC2 Instance** (Ubuntu/Linux) trên AWS Console, tạo Key Pair để truy cập SSH. <br> - Cấu hình **Security Group** cấp quyền truy cập Inbound cho các cổng SSH (22), HTTP (80) và HTTPS (443). | 15/06/2026 | 15/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 3   | - Thiết lập môi trường chạy trên EC2: Cài đặt Docker, Docker Compose, Git và Node.js. <br> - Kéo (Pull) bộ mã nguồn ứng dụng từ GitHub về EC2 và thực thi triển khai ứng dụng (Next.js & NestJS) bằng Docker Container. | 16/06/2026 | 16/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 4   | - Cấu hình **Amazon Cognito User Pools & Client Roles** phân quyền vai trò (Admin, Doctor, Patient) và quản lý luồng cấp tài khoản Bác sĩ với mật khẩu tạm. <br> - Tạo **S3 Bucket** lưu trữ tài nguyên y tế, cấu hình chính sách truy cập (Bucket Policy, CORS) và tích hợp vào NestJS Backend. | 17/06/2026 | 17/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 5   | - Thiết lập **Nginx Reverse Proxy / AWS API Gateway** để điều hướng traffic từ domain công cộng vào các dịch vụ Backend và cấu hình giới hạn tần suất (Rate Limiting). <br> - Tích hợp dịch vụ **AWS SES/SNS** để gửi email tự động kích hoạt tài khoản Bác sĩ và thông báo xác nhận lịch hẹn cho Bệnh nhân. | 18/06/2026 | 18/06/2026 | [Tại đây](<https://docs.aws.amazon.com/apigateway/>) |
| 6   | - Tiến hành kiểm thử tích hợp luồng **AI Triage** phân loại 3 mức độ (Đỏ - Khẩn cấp, Xanh - Tự theo dõi, Vàng - Đặt lịch khám) và tự động tạo **Báo cáo y khoa tóm tắt (Pre-consultation Report)**. <br> - Kiểm thử kết nối giữa Frontend (Next.js), Backend (NestJS) trên EC2 và S3, kiểm tra phân quyền bảo mật IAM Role gắn cho EC2 Instance. | 19/06/2026 | 19/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |


### Kết quả đạt được tuần 3:

* Khởi tạo và cấu hình thành công máy chủ **Amazon EC2**, thiết lập mượt mà các cổng bảo mật với Security Groups.
* Đóng gói và triển khai ứng dụng Web Healthcare (Next.js & NestJS) vận hành ổn định trên môi trường máy chủ EC2 thông qua Docker Containers.
* Cấu hình hoàn tất **Amazon Cognito** hỗ trợ phân quyền chuẩn theo Business Flow (tự động gán role Patient khi đăng ký; quản lý kích hoạt tài khoản Doctor qua Temporary Password).
* Tích hợp thành công **Amazon S3** vào hệ thống Backend cho phép lưu trữ an toàn ảnh bác sĩ, hồ sơ bệnh án và mã QR check-in.
* Tích hợp thành công **AWS SES/SNS** để tự động hóa gửi email mật khẩu tạm cho Bác sĩ và thông báo đặt lịch hẹn cho Bệnh nhân.
* Kiểm thử kết nối thông suốt luồng **AI Triage 3 mức độ** và cơ chế tự động tổng hợp **Báo cáo Y khoa Tóm tắt (Pre-consultation Report)** hiển thị dạng Split View trên Doctor Portal trước phiên khám.
* Thiết lập hệ thống cổng giao tiếp API (API Gateway / Nginx) giúp kiểm soát, định tuyến luồng dữ liệu truy cập và tăng cường tính bảo mật cho hệ thống Backend.
* Áp dụng **IAM Roles cho EC2 Instance** để tương tác an toàn với S3/SES mà không cần lưu cứng chìa khóa truy cập (Access Keys) trong mã nguồn.
* Chuẩn bị sẵn sàng hạ tầng tính toán và lưu trữ tĩnh để tiếp tục tích hợp Cơ sở dữ liệu đám mây ở Tuần 4.


