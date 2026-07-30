---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Khởi tạo và tích hợp hệ quản trị cơ sở dữ liệu quan hệ **Amazon RDS (PostgreSQL)** mã hóa dữ liệu an toàn để lưu trữ dữ liệu có cấu trúc (thông tin tài khoản, hồ sơ khai báo y tế ban đầu, lịch làm việc trống của bác sĩ, lịch hẹn khám và kết quả chẩn đoán/đơn thuốc).
* Khởi tạo và cấu hình cơ sở dữ liệu NoSQL **Amazon DynamoDB** lưu trữ lịch sử trò chuyện Chatbot AI Triage real-time và các báo cáo tóm tắt y khoa (Pre-consultation Report).
* Thiết lập cơ chế **Concurrency Control & Database Locking** (Row-level lock trong PostgreSQL) trên NestJS Backend nhằm xử lý bài toán chống trùng lịch (Race Condition/Double-booking) khi bệnh nhân chọn khung giờ khám.
* Cấu hình phân vùng mạng an toàn (VPC Private Subnet, DB Subnet Groups) và Security Groups cho RDS nhằm đảm bảo CSDL chỉ có thể truy cập nội bộ từ Server Backend EC2.
* Tích hợp ORM (TypeORM/Prisma) vào NestJS Backend để thực hiện Database Migration, kết nối và truy vấn dữ liệu quan hệ trên RDS cùng AWS SDK cho DynamoDB.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Khởi tạo **Amazon RDS Instance (PostgreSQL)** trên AWS Console nằm trong Private Subnet. <br> - Cấu hình DB Subnet Group, thiết lập tài khoản quản trị Admin, bật mã hóa lưu trữ (At-Rest Encryption) và kích hoạt tính năng sao lưu tự động (Automated Backups). | 22/06/2026 | 22/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 3   | - Khởi tạo các bảng trên **Amazon DynamoDB** với Partition Key/Sort Key tối ưu cho truy vấn real-time. <br> - Cấu hình chế độ Auto-Scaling/On-Demand Capacity để đảm bảo hiệu năng đọc/ghi hội thoại AI Triage với độ trễ tối thiểu. | 23/06/2026 | 23/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 4   | - Cấu hình **Security Group cho RDS**: Chỉ chấp nhận Inbound Traffic từ Security Group của EC2 Backend qua cổng 5432. <br> - Xây dựng Schema PostgreSQL lưu trữ: Hồ sơ y tế ban đầu (nhóm máu, dị ứng), Lịch làm việc trống của Bác sĩ (Availability Calendar) và Kết luận phiên khám. Tiến hành Migration dữ liệu. | 24/06/2026 | 24/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 5   | - Tích hợp ORM (Prisma/TypeORM) vào NestJS Backend kết nối RDS PostgreSQL; xây dựng cơ chế **Database Transaction & Row-level Locking** ngăn chặn trùng lịch (Double-booking). <br> - Tích hợp DynamoDB SDK vào Module AI Chatbot để lưu trữ lịch sử hội thoại và tự động truy xuất dữ liệu tổng hợp Báo cáo y khoa tóm tắt. | 25/06/2026 | 25/06/2026 | [Tại đây](<https://docs.nestjs.com/techniques/database>) |
| 6   | - Kiểm thử các thao tác CRUD trên RDS PostgreSQL và DynamoDB từ EC2 Backend; kiểm thử khả năng chịu tải chống Double-booking khi nhiều bệnh nhân đặt cùng slot giờ. <br> - Tối ưu hóa Connection Pooling (sử dụng PgBouncer hoặc ORM pool config) và kiểm tra phân quyền truy cập CSDL qua IAM / KMS. | 26/06/2026 | 26/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |


### Kết quả đạt được tuần 4:

* Triển khai thành công **Amazon RDS PostgreSQL** nằm hoàn toàn trong Private Subnet, mã hóa dữ liệu an toàn, đảm bảo bảo mật tuyệt đối cho thông tin khai báo y tế và đơn thuốc bệnh nhân.
* Khởi tạo thành công **Amazon DynamoDB** phục vụ lưu trữ lịch sử hội thoại AI Triage và các Báo cáo y khoa tóm tắt (Pre-consultation Report) với độ trễ thấp ở mức millisecond.
* Hoàn thành Database Migration trên PostgreSQL, định nghĩa rõ ràng cấu hình lịch làm việc trống (Availability Calendar) của Bác sĩ và hồ sơ y tế bệnh nhân.
* Áp dụng thành công cơ chế **Row-level Lock / Transaction** trong NestJS Backend, giải quyết triệt để bài toán Race Condition (Double-booking) khi nhiều bệnh nhân đặt trùng lịch hẹn.
* Đảm bảo an toàn hạ tầng nhờ Security Group phân vùng nghiêm ngặt (chỉ EC2 Backend mới có quyền kết nối vào RDS).
* Tạo nền tảng dữ liệu vững chắc cho Doctor Portal hiển thị dạng Split View (xem báo cáo AI tóm tắt song song với nhập đơn thuốc) và Patient Portal tra cứu kết quả khám.
* Chuẩn bị đầy đủ hạ tầng CSDL và Backend hoàn chỉnh để sẵn sàng cho Tuần 5 tích hợp hệ thống giám sát **AWS CloudWatch** và xử lý lỗi tập trung.


