---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Khởi tạo và tích hợp hệ quản trị cơ sở dữ liệu quan hệ **Amazon RDS (PostgreSQL)** mã hóa dữ liệu an toàn nằm trong Private Subnet để lưu trữ dữ liệu có cấu trúc (thông tin tài khoản ẩn danh theo UUID, hồ sơ khai báo y tế ban đầu, lịch làm việc của Bác sĩ và thông tin lịch hẹn khám).
* Cấu hình instance RDS ở lớp máy chủ `db.t4g.micro` (AWS Graviton2 ARM) nhằm tối ưu chi phí vận hành (Cost Optimization) và mã hóa đường truyền với chứng chỉ SSL (`global-bundle.pem`).
* Thiết lập cơ chế **Pessimistic Locking (`FOR UPDATE`)** và Database Transaction trên NestJS Backend (Prisma ORM) nhằm xử lý bài toán chống trùng lịch (Race Condition/Double-booking) khi bệnh nhân đặt lịch hẹn.
* Cấu hình phân vùng mạng an toàn (VPC Private Subnet, Security Groups) cho RDS nhằm đảm bảo CSDL chấp nhận truy cập nội bộ an toàn từ Server Backend EC2 qua cổng 5432.
* Tích hợp Prisma ORM vào NestJS Backend để thực hiện Database Migration (`npx prisma db push`), tự động tạo các bảng dữ liệu trên Cloud AWS.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Khởi tạo **Amazon RDS Instance (PostgreSQL)** với tên `healthcare-db` trên AWS Console nằm trong Private Subnet. <br> - Lựa chọn lớp máy chủ `db.t4g.micro` (chip ARM Graviton2), bật mã hóa lưu trữ (At-Rest Encryption) và cấu hình kết nối bắt buộc qua SSL (`global-bundle.pem`). | 22/06/2026 | 22/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |
| 3   | - Thiết lập **Security Group cho RDS**: Cấu hình Inbound Rules cho cổng 5432 (chấp nhận kết nối từ Security Group của EC2 Backend và kết nối Dev/Test kiểm tra qua SSL). <br> - Xây dựng tệp `schema.prisma` lưu trữ: Thông tin người dùng định danh bằng chuỗi UUID, Form khai báo y tế ban đầu (nhóm máu, bệnh nền, dị ứng), Lịch làm việc trống của Bác sĩ, Danh sách lịch hẹn và đường dẫn báo cáo cuộc trò chuyện. | 23/06/2026 | 23/06/2026 | [Tại đây](<https://docs.nestjs.com/techniques/database>) |
| 4   | - Thực thi Prisma CLI (`npx prisma db push`) từ Backend để tự động đồng bộ Schema và tạo cấu trúc các bảng dữ liệu trên AWS RDS PostgreSQL. <br> - Tích hợp biến môi trường `DATABASE_URL` kết nối bảo mật kèm tham số `sslmode=verify-full&sslrootcert=global-bundle.pem` vào file `.env`. | 24/06/2026 | 24/06/2026 | [Tại đây](<https://www.prisma.io/docs/>) |
| 5   | - Lập trình API Đặt lịch khám bệnh trong NestJS Backend tích hợp kỹ thuật **Pessimistic Locking (`FOR UPDATE`)** trực tiếp ở tầng Database PostgreSQL. <br> - Đảm bảo khi một bệnh nhân chọn khung giờ khám, slot đó sẽ được khóa hàng (row-level lock) trong suốt transaction để tránh tuyệt đối rủi ro 2 người đặt trùng 1 suất. | 25/06/2026 | 25/06/2026 | [Tại đây](<https://docs.nestjs.com/techniques/database>) |
| 6   | - Tiến hành kiểm thử các thao tác CRUD trên RDS PostgreSQL từ EC2 Backend; thực hiện giả lập bài kiểm thử tải (Stress Test) đặt lịch đồng thời để xác minh tính hiệu quả của cơ chế Pessimistic Locking. <br> - Tối ưu hóa Connection Pooling trên Prisma ORM và kiểm tra trạng thái vận hành `Available` của `healthcare-db` trên AWS Console. | 26/06/2026 | 26/06/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |


### Kết quả đạt được tuần 4:

* Triển khai thành công cơ sở dữ liệu **Amazon RDS PostgreSQL (`healthcare-db`)** nằm trong Private Subnet sử dụng máy chủ Graviton2 `db.t4g.micro`, tối ưu hóa chi phí vận hành và đảm bảo an toàn mã hóa SSL.
* Đồng bộ thành công cấu trúc CSDL từ NestJS thông qua Prisma CLI (`npx prisma db push`), định nghĩa rõ ràng các bảng lưu trữ thông tin khai báo y tế, lịch làm việc của Bác sĩ và thông tin lịch hẹn.
* Áp dụng thành công cơ chế **Pessimistic Locking (`FOR UPDATE`)** trong NestJS Backend, giải quyết triệt để bài toán Race Condition (Double-booking) khi nhiều bệnh nhân đặt trùng khung giờ khám.
* Đảm bảo an toàn tầng mạng và đường truyền nhờ cấu hình Security Group cổng 5432 kết hợp chứng chỉ mã hóa đường truyền `global-bundle.pem`.
* Tạo nền tảng dữ liệu vững chắc cho Doctor Portal tra cứu danh sách ca khám trong ngày và Patient Portal thực hiện chọn bác sĩ/đặt lịch hẹn.
* Chuẩn bị đầy đủ hạ tầng CSDL và Backend hoàn chỉnh để sẵn sàng cho Tuần 5 tích hợp **RAG Pipeline (AWS Bedrock Knowledge Base, ViMQ, GPT-4o-mini & Langfuse)** tư vấn y tế ban đầu.


