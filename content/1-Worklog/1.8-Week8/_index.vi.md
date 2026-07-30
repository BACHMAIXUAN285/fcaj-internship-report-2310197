---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Hoàn thiện đóng gói container (Docker) và tự động hóa quy trình triển khai ứng dụng lên hạ tầng AWS (AWS ECS/App Runner, EC2, RDS).
* Hoàn thiện và tối ưu hóa Admin Portal (Onboarding Bác sĩ, quản lý lịch làm việc) và Doctor Portal (Split View Báo cáo AI, kết luận khám & đẩy đơn thuốc) đúng chuẩn Business Flow.
* Chuẩn bị tài liệu kỹ thuật, hướng dẫn sử dụng (User Manual) cho Bệnh viện & Bác sĩ và tiến hành nghiệm thu toàn bộ hệ thống.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Xây dựng Dockerfile và docker-compose cho cả NestJS Backend và Next.js Frontend.<br>- Cấu hình quy trình CI/CD (GitHub Actions / AWS CodePipeline) để tự động hóa việc build và deploy ứng dụng lên AWS. | 20/07/2026 | 20/07/2026 | [Tại đây](<https://docs.docker.com/>) |
| 3   | - Cấu hình hạ tầng Cloud production trên AWS: Cấu hình Domain, HTTPS/SSL qua AWS Certificate Manager (ACM) và Route 53.<br>- Thiết lập CloudWatch Logs và AWS SES/SNS để giám sát hệ thống, tự động gửi Email cấp phát mật khẩu tạm thời cho Bác sĩ và Email/SMS xác nhận lịch hẹn cho Bệnh nhân. | 21/07/2026 | 21/07/2026 | [Tại đây](<https://docs.aws.amazon.com/>) |
| 4   | - Tối ưu hóa các cổng quản trị hệ thống theo Flow:<br>&emsp;+ **Admin Portal (Desktop/Tablet):** Tối ưu luồng khởi tạo Bác sĩ, tự động kích hoạt tài khoản qua AWS Cognito (Email Temporary Password) và thiết lập Lịch làm việc/Khung giờ trống.<br>&emsp;+ **Doctor Portal (Desktop):** Tối ưu giao diện Split View (Báo cáo AI + Form chẩn đoán) và tính năng đẩy kết quả/đơn thuốc trực tiếp về Mobile App của Bệnh nhân. | 22/07/2026 | 22/07/2026 | Internal Docs |
| 5   | - Kiểm thử tổng duyệt toàn hệ thống trên môi trường Production (Staging/Production Smoke Test).<br>- Tối ưu hóa dung lượng build frontend và bộ nhớ cache để giảm tối đa chi phí vận hành đám mây. | 23/07/2026 | 23/07/2026 | Internal Test |
| 6   | - Viết tài liệu bàn giao hệ thống: Tài liệu kiến trúc (Architecture Document), Hướng dẫn cài đặt/vận hành và Hướng dẫn sử dụng cho Quản trị viên Bệnh viện (Admin Portal) & Bác sĩ (Doctor Portal).<br>- Tổng kết dự án, đánh giá kết quả đạt được và nghiệm thu. | 24/07/2026 | 24/07/2026 | Project Deliverables |


### Kết quả đạt được tuần 8:

* Đã đóng gói ứng dụng thành công bằng Docker và thiết lập xong pipeline CI/CD tự động hoá 100% quá trình triển khai hệ thống lên hạ tầng cloud AWS.
* Hệ thống vận hành ổn định trên môi trường Production với đầy đủ chứng chỉ bảo mật HTTPS/SSL, tên miền chính thức và hệ thống giám sát CloudWatch.
* Hoàn thiện hoàn hảo luồng nghiệp vụ trên Desktop Portal: Quản trị viên khởi tạo/phân quyền Bác sĩ và thiết lập lịch làm việc trơn tru; Bác sĩ khai thác hiệu quả Báo cáo AI tóm tắt (Split View) và gửi trả chẩn đoán/đơn thuốc về ứng dụng Mobile của Bệnh nhân tức thì.
* Hệ thống tự động gửi Email/SMS xác nhận lịch hẹn và kích hoạt tài khoản qua AWS SES/SNS/Cognito hoạt động ổn định và chính xác.
* Hoàn thành đầy đủ bộ tài liệu kỹ thuật, tài liệu hướng dẫn vận hành và bàn giao nghiệm thu dự án đúng tiến độ đề ra.


