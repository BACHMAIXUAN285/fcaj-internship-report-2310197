---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Hoàn thiện đóng gói container (Docker) và tự động hóa quy trình triển khai ứng dụng lên hạ tầng AWS (AWS ECS/App Runner, EC2, RDS).
* Tối ưu hóa tính năng Check-in, tiếp nhận và thu phí khám trực tiếp dành cho Lễ tân / Thu ngân.
* Chuẩn bị tài liệu kỹ thuật, hướng dẫn sử dụng (User Manual) và tiến hành nghiệm thu toàn bộ hệ thống.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Xây dựng Dockerfile và docker-compose cho cả NestJS Backend và Next.js Frontend.<br>- Cấu hình quy trình CI/CD (GitHub Actions / AWS CodePipeline) để tự động hóa việc build và deploy ứng dụng lên AWS. | 20/07/2026 | 20/07/2026 | [Tại đây](<https://docs.docker.com/>) |
| 3   | - Cấu hình hạ tầng Cloud production trên AWS: Cấu hình Domain, HTTPS/SSL qua AWS Certificate Manager (ACM) và Route 53.<br>- Thiết lập CloudWatch Logs và AWS SES/SNS để giám sát hệ thống và tự động gửi email/SMS xác nhận lịch hẹn cho bệnh nhân. | 21/07/2026 | 21/07/2026 | [Tại đây](<https://docs.aws.amazon.com/>) |
| 4   | - Hoàn thiện và tối ưu giao diện Dashboard Lễ tân/Thu ngân:<br>&emsp;+ Hỗ trợ tra cứu nhanh lịch hẹn bệnh nhân qua mã QR/Số điện thoại.<br>&emsp;+ Tối ưu luồng xác nhận check-in và xuất hóa đơn/phiếu thu phí dịch vụ trực tiếp tại quầy. | 22/07/2026 | 22/07/2026 | Internal Docs |
| 5   | - Kiểm thử tổng duyệt toàn hệ thống trên môi trường Production (Staging/Production Smoke Test).<br>- Tối ưu hóa dung lượng build frontend và bộ nhớ cache để giảm tối đa chi phí vận hành đám mây. | 23/07/2026 | 23/07/2026 | Internal Test |
| 6   | - Viết tài liệu bàn giao hệ thống: Tài liệu kiến trúc (Architecture Document), Hướng dẫn cài đặt/vận hành và Hướng dẫn sử dụng cho Bác sĩ & Lễ tân.<br>- Tổng kết dự án, đánh giá kết quả đạt được và nghiệm thu. | 24/07/2026 | 24/07/2026 | Project Deliverables |


### Kết quả đạt được tuần 8:

* Đã đóng gói ứng dụng thành công bằng Docker và thiết lập xong pipeline CI/CD tự động hoá 100% quá trình triển khai hệ thống lên hạ tầng cloud AWS.
* Hệ thống vận hành ổn định trên môi trường Production với đầy đủ chứng chỉ bảo mật HTTPS/SSL, tên miền chính thức và hệ thống giám sát CloudWatch.
* Hoàn thiện mượt mà luồng nghiệp vụ tại quầy cho Lễ tân: Tốc độ tra cứu thông tin bệnh nhân và xử lý thu phí trực tiếp diễn ra nhanh chóng, chính xác, không còn phụ thuộc vào các cổng thanh toán trung gian trực tuyến.
* Hệ thống gửi thông báo xác nhận lịch hẹn (Email/SMS) tự động hoạt động ổn định và chính xác.
* Hoàn thành đầy đủ bộ tài liệu kỹ thuật, tài liệu hướng dẫn vận hành và bàn giao nghiệm thu dự án đúng tiến độ đề ra.


