---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Tích hợp dịch vụ **AWS CloudWatch** để theo dõi (Monitoring), giám sát hiệu năng các microservices/APIs và ghi nhật ký hoạt động (Logging) cho toàn bộ hệ thống Web Healthcare.
* Giám sát chuyên sâu hoạt động của luồng **AI Triage (AWS SageMaker)**, các giao dịch **Concurrency Control (Row-level Lock)** trên RDS PostgreSQL và các phản hồi từ Amazon Cognito.
* Thiết lập các cơ chế cảnh báo tự động (**CloudWatch Alarms**) giúp phát hiện sớm sự cố hạ tầng, tình trạng quá tải Database hoặc tỷ lệ thất bại của AI Triage.
* Xây dựng bộ xử lý ngoại lệ toàn cục (**Global Exception Filters**) trong NestJS để bắt lỗi tập trung, xử lý Fallback an toàn cho AI Bot/SES/SNS và bảo vệ trải nghiệm người dùng trên cả Patient Portal và Doctor Portal.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu  |
| --- | --- | --- | --- | --- |
| 2   | - Tìm hiểu dịch vụ **AWS CloudWatch** (Logs, Metrics, Alarms, Dashboards). <br> - Cấu hình CloudWatch Agent trên EC2 Instance để đẩy log hệ thống Backend NestJS, Server Web Next.js và log kết nối WebSocket Chatbot về CloudWatch Logs. | 29/06/2026 | 29/06/2026 | [Tại đây](<https://docs.aws.amazon.com/cloudwatch/>) |
| 3   | - Tích hợp thư viện Logger (Winston/Pino) vào NestJS ghi log cấu trúc JSON. <br> - Đẩy log chi tiết về: Luồng phân loại triệu chứng AI Triage (3 mức độ Đỏ/Xanh/Vàng), log cấp phát tài khoản Doctor qua Cognito, log khóa hàng RDS (Row-level Lock) khi đặt lịch và log gửi Email xác nhận (AWS SES/SNS) lên CloudWatch. | 30/06/2026 | 30/06/2026 | [Tại đây](<https://docs.nestjs.com/techniques/logger>) |
| 4   | - Thiết lập **CloudWatch Alarms** cảnh báo tự động khi: <br>&emsp; + Tải CPU/Memory của EC2/RDS PostgreSQL vượt 80% hoặc đụng độ khóa dữ liệu (Lock contention) quá cao. <br>&emsp; + Tỷ lệ phản hồi thất bại hoặc Timeout từ dịch vụ AI Triage (SageMaker) vượt ngưỡng. <br>&emsp; + Tỷ lệ lỗi API HTTP Status 5xx vượt mức cho phép. <br> - Trực quan hóa toàn bộ chỉ số trên **CloudWatch Dashboard**. | 01/07/2026 | 01/07/2026 | [Tại đây](<https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html>) |
| 5   | - Phát triển cơ chế **Global Exception Filter** & **Http Exception Filter** trong NestJS để bắt lỗi tập trung và che giấu chi tiết lỗi nhạy cảm. <br> - Lập kịch bản Fallback an toàn: Khi AI Triage gián đoạn -> tự động chuyển bệnh nhân sang giao diện Đặt lịch khám trực tiếp; khi AWS SES/SNS lỗi -> lưu queue gửi lại thông báo sau. | 02/07/2026 | 02/07/2026 | [Tại đây](<https://docs.nestjs.com/exception-filters>) |
| 6   | - Kiểm thử toàn diện (End-to-End Testing) luồng vận hành tích hợp giám sát & xử lý lỗi: Đăng ký Bệnh nhân -> Khai báo y tế -> AI Triage 3 phân nhánh -> Đặt lịch chống Double-booking -> Tự động sinh Pre-consultation Report -> Gửi Email xác nhận -> Bác sĩ xem Split View & chốt đơn thuốc. <br> - Tối ưu hóa hiệu năng và nghiệm thu toàn bộ hạ tầng AWS cùng ứng dụng Web Healthcare. | 03/07/2026 | 03/07/2026 | [Tại đây](<https://docs.aws.amazon.com/ses/>) |


### Kết quả đạt được tuần 5:

* Tập trung và chuẩn hóa toàn bộ Log của ứng dụng (Next.js, NestJS) cùng lịch sử gọi AI Triage lên **AWS CloudWatch Logs**, giúp tra cứu vết lỗi (Debugging) và kiểm soát luồng dữ liệu y tế hiệu quả.
* Thiết lập thành công hệ thống cảnh báo **CloudWatch Alarms** gửi thông báo ngay qua Email/SNS khi máy chủ quá tải, nghẽn Database Lock hoặc dịch vụ AI gặp sự cố.
* Hoàn thiện bộ xử lý lỗi toàn cục (**Global Exception Filters**), xây dựng kịch bản Fallback linh hoạt giúp duy trì trải nghiệm người dùng liền mạch kể cả khi dịch vụ AI Triage hoặc SES/SNS gặp sự cố gián đoạn.
* Tối ưu hóa hiệu năng gửi email tự động xác nhận lịch hẹn (AWS SES/SNS) và cấp tài khoản Bác sĩ với Mật khẩu tạm thời.
* Nghiệm thu hệ thống giám sát trực quan (**CloudWatch Dashboard**) cho phép Admin theo dõi sức khỏe hạ tầng, lưu lượng Chatbot AI và số lượng đặt lịch thành công theo thời gian thực (Real-time).
* Hoàn thành xuất sắc toàn bộ lộ trình triển khai hạ tầng đám mây AWS và tích hợp ứng dụng Web Healthcare chuẩn theo Business Flow.


