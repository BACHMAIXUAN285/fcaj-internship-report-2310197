---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

Tại phần này, bạn sẽ thấy bản tóm tắt đề xuất dự án phát triển hệ thống Y tế số, bao gồm mục tiêu, kiến trúc hạ tầng AWS Cloud, luồng nghiệp vụ cốt lõi và ước tính ngân sách vận hành.

# Smart Healthcare AI Triage & Appointment Booking Platform  
## Giải pháp Cloud-native hỗ trợ Sàng lọc Bệnh Y khoa qua AI và Quản lý Lịch hẹn Trực tuyến  

### 1. Tóm tắt điều hành  
Smart Healthcare Platform được thiết kế nhằm hiện đại hóa quy trình tiếp nhận, sàng lọc ban đầu và đặt lịch khám bệnh tại các phòng khám/bệnh viện. Hệ thống ứng dụng mô hình trí tuệ nhân tạo (AI) trên **Amazon SageMaker** để phân loại triệu chứng của bệnh nhân theo 3 cấp độ (Đỏ - Vàng - Xanh), đồng thời tự động tạo **Báo cáo y khoa tóm tắt (Pre-consultation Report)** trước ca khám. Nền tảng được xây dựng theo kiến trúc Microservices/Cloud-native trên nền tảng **AWS Cloud** (Cognito, EC2, RDS PostgreSQL, S3, CloudWatch, SES/SNS), phục vụ hàng nghìn lượt truy cập đồng thời từ bệnh nhân, bác sĩ và đội ngũ lễ tân/quản trị viên.  

### 2. Tuyên bố vấn đề  
#### Vấn đề hiện tại  
Các cơ sở y tế hiện nay thường gặp tình trạng quá tải tại quầy tiếp đón. Quy trình đặt lịch hẹn truyền thống qua điện thoại hoặc tại quầy dễ gây ra tình trạng trùng lịch (Double-booking), thời gian chờ đợi của bệnh nhân kéo dài. Bên cạnh đó, bác sĩ tốn nhiều thời gian hỏi lại từ đầu các triệu chứng cơ bản của bệnh nhân do thiếu thông tin chuẩn bị trước.  

#### Giải pháp  
Nền tảng cung cấp giải pháp toàn diện trải qua 5 giai đoạn nghiệp vụ khép kín:
1. **Giai đoạn 1 - Thiết lập Hệ thống & Cấp phát Tài khoản:** Admin khởi tạo bác sĩ trên Admin Portal. **AWS Cognito** kết hợp **AWS SES** tự động gửi Email chứa Mật khẩu tạm thời (Temporary Password). Bác sĩ đăng nhập Doctor Portal và bắt buộc tạo mật khẩu mới ngay lần đầu truy cập trước khi thiết lập lịch trống làm việc.
2. **Giai đoạn 2 - Tiếp nhận Bệnh nhân (Onboarding):** Bệnh nhân đăng ký tài khoản trên Mobile Web App (mặc định gán role Patient). Lần đầu đăng nhập, bệnh nhân điền Form khai báo y tế ban đầu (tuổi, nhóm máu, tiền sử bệnh nền, dị ứng) được lưu trữ mã hóa trong CSDL.
3. **Giai đoạn 3 - Trợ lý AI Sàng lọc Triệu chứng (Triage Flow):** Bot AI (trên **Amazon SageMaker**) giao tiếp qua WebSocket để khai thác triệu chứng và phân loại 3 mức độ:
   - 🔴 **Mức độ Đỏ (Khẩn cấp):** Vô hiệu hóa khung chat, hiển thị nút bấm gọi Cấp Cứu 115 lập tức.
   - 🟢 **Mức độ Xanh (Nhẹ):** Hướng dẫn chăm sóc tại nhà và tự động kết thúc phiên chat.
   - 🟡 **Mức độ Vàng (Cần Bác sĩ):** Hiển thị Card UI gợi ý đặt lịch trỏ đúng Chuyên khoa phù hợp.
4. **Giai đoạn 4 - Đặt Lịch Hẹn Chuyên Khoa (Booking Flow):** Bệnh nhân chọn giờ qua giao diện Bottom Sheet. **AWS RDS PostgreSQL** áp dụng cơ chế khóa dòng (**Pessimistic Locking**) để triệt tiêu 100% rủi ro trùng lịch (Race Condition). Hệ thống tự động tổng hợp đoạn chat thành **Pre-consultation Report** lưu vào **Amazon S3** và gửi Email/SMS mã QR xác nhận qua **AWS SES/SNS**.
5. **Giai đoạn 5 - Phiên Khám Bệnh & Kết Luận (Consultation Flow):** Bác sĩ mở Doctor Portal với giao diện **Split View** (một bên xem Hồ sơ cũ + Báo cáo tóm tắt AI, một bên nhập chẩn đoán/đơn thuốc). Khám qua Telehealth hoặc trực tiếp, sau đó kết quả được tự động đẩy về ứng dụng Mobile của bệnh nhân.

#### Lợi ích và hoàn vốn đầu tư (ROI)  
- Giảm đến 60% thời gian chờ đợi tại quầy nhờ quy trình check-in tự động bằng mã QR và onboarding tự động.
- Tăng 30% hiệu suất làm việc của Bác sĩ nhờ giao diện Split View và Báo cáo tóm tắt triệu chứng do AI tổng hợp.
- Triệt tiêu 100% rủi ro trùng lịch khám nhờ cơ chế Pessimistic Locking từ tầng Database.
- Tối ưu hóa chi phí hạ tầng nhờ khả năng linh hoạt của AWS Cloud theo lưu lượng truy cập thực tế.  

### 3. Kiến trúc giải pháp  
Hệ thống sử dụng kiến trúc Web Multi-tier trên nền tảng AWS Cloud, chia làm 3 lớp chính: Frontend (Next.js 14 Responsive), Backend Service (NestJS trên EC2), và AI Services (Amazon SageMaker).  

![Smart Healthcare AI Architecture](/images/2-Proposal/architecture-diagram.png)

<!--
![IoT Weather Station Architecture](/images/2-Proposal/edge_architecture.jpeg)

![IoT Weather Platform Architecture](/images/2-Proposal/platform_architecture.jpeg)
-->

#### Dịch vụ AWS sử dụng  
- *Amazon Cognito*: Quản lý định danh, đăng nhập/đăng ký, phân quyền RBAC và luồng mật khẩu tạm thời cho nhân viên y tế.
- *AWS EC2*: Triển khai ứng dụng Web Frontend (Next.js) và Backend REST API / WebSocket Gateway (NestJS) qua Docker Containers.
- *Amazon SageMaker*: Endpoint lưu trữ và chạy mô hình AI phân loại triệu chứng 3 cấp độ & sinh báo cáo y khoa.
- *Amazon RDS (PostgreSQL)*: Cơ sở dữ liệu quan hệ lưu trữ thông tin bệnh nhân, bác sĩ, lịch làm việc với cơ chế Pessimistic Locking.
- *Amazon S3*: Lưu trữ file tĩnh, Pre-consultation Reports do AI sinh ra, đơn thuốc và kết quả cận lâm sàng.
- *AWS CloudWatch*: Thu thập log hệ thống, giám sát hiệu năng CPU/Memory và chỉ số AI Inference.
- *AWS SES / SNS*: Tự động gửi Email Mật khẩu tạm thời cho Bác sĩ và Email/SMS xác nhận lịch hẹn kèm mã QR check-in.  

#### Thiết kế thành phần  
- *Giao diện Bệnh nhân (Next.js - Mobile View)*: Cho phép khai báo y tế ban đầu, chat Triage với Bot AI, đặt lịch hẹn qua Bottom Sheet UI và nhận mã QR xác nhận.
- *Giao diện Nhân viên Y tế (Next.js - Desktop View)*:  
  - **Doctor Portal:** Đăng nhập bằng Temporary Password, đổi mật khẩu lần đầu, thiết lập lịch làm việc, xem danh sách lịch hẹn và khám bệnh qua giao diện **Split View** (Hồ sơ AI Report + Form chẩn đoán).
  - **Admin & Reception Portal:** Quản lý nhân sự/khởi tạo bác sĩ, check-in bệnh nhân qua mã QR, lập hóa đơn dịch vụ và thu tiền trực tiếp tại quầy.
- *Backend Microservices (NestJS)*: Xử lý Business Logic, WebSocket Gateway (Chat AI & Telehealth Signaling) và kết nối CSDL RDS PostgreSQL.  

### 4. Triển khai kỹ thuật  
**Các giai đoạn triển khai**  
Dự án được triển khai trong vòng **8 tuần** (2 tháng) qua các giai đoạn:  
1. *Tuần 1 - 2*: Phân tích yêu cầu Business Flow, thiết kế kiến trúc Cloud AWS, thiết kế ERD CSDL và khởi tạo Base Source Code (Next.js 14 + NestJS).
2. *Tuần 3 - 4*: Cấu hình AWS Cognito (Temp Password flow), triển khai hạ tầng AWS (EC2, S3, RDS PostgreSQL), tích hợp TypeORM và xử lý cơ chế chống trùng lịch (Pessimistic Locking).
3. *Tuần 5 - 6*: Tích hợp mô hình AI Triage 3 cấp độ trên Amazon SageMaker qua WebSocket, sinh Pre-consultation Report lên S3, hoàn thiện Doctor Portal (Split View) & Patient Mobile UI.
4. *Tuần 7 - 8*: Tích hợp AWS CloudWatch, kiểm thử tải (Stress Test Race Condition), đóng gói container Docker, cấu hình CI/CD GitHub Actions và bàn giao nghiệm thu.

**Yêu cầu kỹ thuật**  
- *Frontend*: Next.js 14, TailwindCSS, Socket.io-client, React Query.
- *Backend*: NestJS Framework, TypeORM/Prisma, TypeScript, Socket.io.
- *Database*: PostgreSQL 16.x trên AWS RDS (Private Subnet).
- *AI/ML*: Python, Amazon SageMaker Endpoints.
- *DevOps*: Docker, AWS CLI, GitHub Actions (CI/CD).

### 5. Lộ trình & Mốc triển khai  
- *Giai đoạn 1 (Tuần 1 - Tuần 2)*: Hoàn thiện thiết kế System Architecture & CSDL Schema theo Business Flow.
- *Giai đoạn 2 (Tuần 3 - Tuần 4)*: Triển khai thành công hạ tầng AWS (Cognito Auth Flow, RDS PostgreSQL, S3, EC2) & Booking Concurrency API.
- *Giai đoạn 3 (Tuần 5 - Tuần 6)*: Tích hợp thành công SageMaker AI Triage, hoàn thiện Doctor Split View Portal & AWS CloudWatch.
- *Giai đoạn 4 (Tuần 7 - Tuần 8)*: Hoàn thành Stress Test đặt lịch đồng thời, triển khai CI/CD trên AWS Cloud và nghiệm thu dự án.

### 6. Ước tính ngân sách  
Chi phí hạ tầng được ước tính trên môi trường AWS Cloud cho giai đoạn thử nghiệm (MVP / Development Phase): 

*Chi phí hạ tầng AWS hàng tháng*  
- *AWS RDS (db.t3.micro - PostgreSQL)*: ~15.00 USD/tháng (Single-AZ, 20 GB Storage).
- *AWS EC2 (t3.small - Backend & Frontend)*: ~14.00 USD/tháng (Chạy 24/7).
- *Amazon SageMaker (ml.t3.medium Endpoint)*: ~36.00 USD/tháng (Phục vụ Serverless/On-demand AI Inference).
- *Amazon S3 Standard*: ~0.50 USD/tháng (5 GB Data Storage & Transfer).
- *Amazon Cognito*: 0.00 USD/tháng (Miễn phí 50,000 MAU đầu tiên).
- *AWS CloudWatch & SES/SNS*: ~2.00 USD/tháng (Metrics, Logs, Alarms & Automated Emails).

*Tổng chi phí hạ tầng Cloud*: ~67.50 USD/tháng.

### 7. Đánh giá rủi ro  
#### Ma trận rủi ro  
- Trùng lịch khám do thao tác đồng thời (Race Condition): Ảnh hưởng cao, xác suất trung bình.
- Gián đoạn kết nối mô hình AI (SageMaker Timeout): Ảnh hưởng trung bình, xác suất thấp.
- Lộ thông tin y tế bệnh nhân (Data Privacy): Ảnh hưởng rất cao, xác suất thấp. 

#### Chiến lược giảm thiểu  
- *Race Condition*: Sử dụng Pessimistic Locking trực tiếp từ tầng Database PostgreSQL khi chốt slot lịch.  
- *AI Timeout*: Xây dựng luồng Fallback — Nếu AI bị lỗi, hệ thống tự động chuyển sang luồng chọn bác sĩ thủ công truyền thống mà không làm gián đoạn trải nghiệm người dùng.  
- *Data Privacy*: Mã hóa thông tin y tế ban đầu, sử dụng chuỗi UUID thay cho ID tự tăng trên URL, ẩn danh thông tin bệnh nhân khi lưu log lên CloudWatch. 

### 8. Kết quả kỳ vọng  
- **Cải tiến kỹ thuật:** Tự động hóa 80% quy trình tiếp nhận và phân luồng bệnh nhân; đạt chỉ số sẵn sàng của hệ thống > 99.9% trên nền tảng AWS Cloud.  
- **Giá trị dài hạn:** Cung cấp nguồn dữ liệu chuẩn hóa cho công tác phân tích và dự báo dịch bệnh; hệ thống dễ dàng mở rộng cho chuỗi nhiều chi nhánh phòng khám trong tương lai.
