---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Triển khai thử nghiệm ứng dụng Web Healthcare lên hạ tầng đám mây AWS sử dụng kết hợp **Amazon EC2** cho Server tính toán và **Amazon S3** cho lưu trữ đối tượng (ảnh đại diện, báo cáo lịch sử chat AI RAG dạng PDF/JSON, tài nguyên tĩnh).
* Hoàn thiện cấu hình **Amazon Cognito** trên Cloud để xử lý xác thực (Authentication) và phân quyền dựa trên vai trò (Role-based: Admin, Doctor, Patient) với `cognito:groups`.
* Tích hợp dịch vụ **Amazon S3** vào Backend (NestJS) bằng AWS SDK v3, sử dụng cơ chế **IAM Role gắn cho EC2** và **Presigned URLs** để tải/truy xuất file an toàn.
* Thiết lập **Nginx Reverse Proxy** trên EC2 để định tuyến các yêu cầu (Routing), cấu hình SSL/TLS và áp dụng Rate Limiting bảo vệ hệ thống API Backend.
* Kiểm thử kết nối và chuẩn bị luồng lưu trữ file **Báo cáo cuộc trò chuyện (Pre-consultation Report)** từ Chatbot AI RAG tư vấn y tế về S3.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Khởi tạo **EC2 Instance** (Ubuntu/Linux) trên AWS Console, tạo Key Pair để truy cập SSH. <br> - Cấu hình **Security Group** cấp quyền truy cập Inbound cho các cổng SSH (22), HTTP (80) và HTTPS (443). | 15/06/2026 | 15/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 3   | - Thiết lập môi trường chạy trên EC2: Cài đặt Docker, Docker Compose, Git và Node.js. <br> - Kéo (Pull) bộ mã nguồn ứng dụng từ GitHub về EC2 và thực thi triển khai ứng dụng (Next.js & NestJS) bằng Docker Containers. | 16/06/2026 | 16/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 4   | - Cấu hình **Amazon Cognito User Pool & App Client** phân quyền vai trò (Admin, Doctor, Patient) dựa trên `cognito:groups`. <br> - Tạo **S3 Bucket** lưu trữ tài nguyên y tế, cấu hình chính sách truy cập (Bucket Policy, CORS) và viết Service upload/download trong NestJS Backend bằng AWS SDK. | 17/06/2026 | 17/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 5   | - Thiết lập **Nginx Reverse Proxy** trên EC2 để điều hướng traffic từ domain công cộng vào các dịch vụ Frontend/Backend và cấu hình giới hạn tần suất (Rate Limiting). <br> - Gán **IAM Role** cho EC2 Instance để ứng dụng tự động phân quyền tương tác với S3 mà không cần lưu hardcode Access Keys trong mã nguồn. | 18/06/2026 | 18/06/2026 | [Tại đây](<https://docs.aws.amazon.com/>) |
| 6   | - Kiểm thử tích hợp luồng lưu trữ file **Pre-consultation Report** (lịch sử chat tư vấn của Chatbot AI) từ Backend lên Amazon S3 dưới dạng Presigned URL. <br> - Kiểm thử kết nối end-to-end giữa Frontend (Next.js), Backend (NestJS) trên EC2 với Cognito và S3, đảm bảo phân quyền RBAC hoạt động chính xác. | 19/06/2026 | 19/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |


### Kết quả đạt được tuần 3:

* Khởi tạo và cấu hình thành công máy chủ **Amazon EC2**, thiết lập mượt mà các cổng bảo mật với Security Groups.
* Đóng gói và triển khai ứng dụng Web Healthcare (Next.js & NestJS) vận hành ổn định trên môi trường máy chủ EC2 thông qua Docker Containers.
* Cấu hình hoàn tất **Amazon Cognito** trên Cloud hỗ trợ phân quyền RBAC chuẩn theo Business Flow (gán nhóm `Patient`, `Doctor`, `Admin` và trích xuất `cognito:groups` trong JWT Token).
* Tích hợp thành công **Amazon S3** vào hệ thống Backend NestJS cho phép lưu trữ an toàn ảnh bác sĩ, tệp đính kèm và file lịch sử tư vấn y tế (Pre-consultation Report).
* Áp dụng **IAM Role cho EC2 Instance** để tương tác an toàn với S3 mà không cần lưu cứng chìa khóa truy cập (Access Keys) trong file cấu hình `.env`.
* Kiểm thử kết nối thông suốt luồng tạo và truy xuất file **Pre-consultation Report** của Chatbot AI thông qua cơ chế Presigned URLs của S3.
* Cấu hình Nginx Reverse Proxy giúp kiểm soát, định tuyến luồng dữ liệu truy cập và tăng cường tính bảo mật cho hệ thống API.
* Chuẩn bị sẵn sàng hạ tầng tính toán và lưu trữ tĩnh để tiếp tục tích hợp Cơ sở dữ liệu đám mây AWS RDS ở Tuần 4.


