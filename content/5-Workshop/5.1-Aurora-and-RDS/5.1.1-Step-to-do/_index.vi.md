---
title : "Các bước Thực hiện"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1.1. </b> "
---

#### Bước 1: Khởi tạo Cụm Cơ sở Dữ liệu (Database Creation)

1. Truy cập **AWS Management Console**, tìm kiếm và chọn dịch vụ **Aurora and RDS**.
2. Chọn **Databases** --> bấm **Create database**:
   * **Creation method**: Chọn **Standard create**.
   * **Engine options**: Lựa chọn **PostgreSQL** (Đảm bảo sự nhất quán với thiết kế ban đầu và tương thích hoàn toàn với Prisma ORM của Backend NestJS).
   * **Settings**:
     + DB instance identifier: `healthcare-db`
     + Master username / password: Thiết lập tài khoản quản trị hệ thống.
   * **Instance configuration**: Lựa chọn cấu hình `db.t4g.micro`.

##### Phân tích Kỹ thuật (Cost Optimization):

Dòng máy chủ `db.t4g.micro` sử dụng bộ vi xử lý kiến trúc ARM (**AWS Graviton2**). Đây là một điểm cộng rất lớn về mặt tư duy vận hành Cloud: Dòng chip ARM mang lại hiệu năng xử lý cao hơn với chi phí duy trì rẻ hơn đáng kể so với các dòng chip x86 truyền thống, rất phù hợp cho môi trường Dev/Test của dự án.

![Figure 1](/images/5-Workshop/5.1.1-Step-to-do/Aurora-and-RDS.png)

#### Bước 2: Cấu hình Mạng và Bảo mật (Network & Security)

1. Định tuyến cơ sở dữ liệu vào một **Virtual Private Cloud (VPC)** cụ thể của hệ thống.
2. **Cấu hình Security Group (VPC Firewall)**:
   * Mở cổng mặc định `5432` của PostgreSQL để nhận kết nối từ Backend.
3. **Mã hóa đường truyền (Encryption in Transit)**: Tải file chứng chỉ mã hóa SSL (`global-bundle.pem`) do AWS cung cấp để chuẩn bị cho việc kết nối an toàn.

![Figure 2](/images/5-Workshop/5.1.1-Step-to-do/Aurora-and-RDS(2).png)

##### Đánh giá Bảo mật & Phản biện (Security Review):

* **Hiện trạng trong hình**: Phần *Security group rules* ở dòng `CIDR/IP - Inbound` đang đặt quy tắc `0.0.0.0/0` (mở cho toàn bộ Internet).
* **Mục đích Dev/Test**: Cấu hình này hỗ trợ các thành viên dễ dàng truy vấn dữ liệu từ máy cá nhân bằng công cụ như DBeaver, TablePlus hay Prisma Studio.
* **Khắc phục khi lên Production**: Đối với hệ thống y tế chứa dữ liệu bệnh án nhạy cảm, việc mở toang cổng Database ra Internet là cực kỳ nguy hiểm. Khi đưa vào vận hành thực tế, bắt buộc phải xóa quy tắc `0.0.0.0/0` và chỉ cho phép duy nhất IP của Backend Server (EC2) hoặc Bastion Host truy cập qua cổng `5432`.

#### Bước 3: Trích xuất Chuỗi Kết nối (Connection String)

1. Sau khi máy chủ chuyển sang trạng thái **Available**, truy cập vào tab **Connectivity & security**.
2. Lấy địa chỉ máy chủ (**Endpoint**): `healthcare-db.cdu4ym0ac08t.ap-southeast-2.rds.amazonaws.com`
3. Tải file chứng chỉ SSL mã hóa đường truyền bằng lệnh:  
   `curl -o global-bundle.pem https://truststore.pki.rds.amazonaws.com/global/global-bundle.pem`
4. Tổng hợp thông tin (*Endpoint, Port 5432, Username, Password*) để tạo chuỗi kết nối `DATABASE_URL` đạt chuẩn mã hóa y tế (`sslmode=verify-full`):  
   ```bash
   postgresql://<username>:<password>@healthcare-db.cdu4ym0ac08t.ap-southeast-2.rds.amazonaws.com:5432/postgres?sslmode=verify-full&sslrootcert=global-bundle.pem
   ```

#### Bước 4: Đồng bộ Schema từ NestJS lên AWS RDS

1. Cập nhật biến môi trường `DATABASE_URL` trong file `.env` tại thư mục gốc mã nguồn Backend NestJS:  
   ```bash
   DATABASE_URL="postgresql://<username>:<password>@healthcare-db.cdu4ym0ac08t.ap-southeast-2.rds.amazonaws.com:5432/postgres?sslmode=verify-full&sslrootcert=global-bundle.pem"
   ```
2. Mở Terminal và thực thi lệnh Prisma CLI để khởi tạo cấu trúc bảng tự động lên AWS RDS:  
   ```bash
   npx prisma db push
   # Hoặc dùng cho sản xuất:
   npx prisma migrate deploy
   ```
3. Công cụ Prisma sẽ tự động kết nối qua kênh mã hóa SSL và sinh ra toàn bộ các bảng dữ liệu (`User`, `Appointment`, `DoctorProfile`,...) trên Cloud mà không cần thao tác DDL SQL thủ công.

#### Tóm tắt Kết quả Triển khai

Qua 4 bước triển khai, nhóm đã xây dựng thành công "trái tim" dữ liệu cho ứng dụng y tế:
1. **Khởi tạo hạ tầng vững chắc**: Đảm bảo tính tương thích giữa **PostgreSQL** và **Prisma ORM**, đồng thời tối ưu ngân sách với lớp máy chủ **ARM Graviton2** (`db.t4g.micro`).
2. **Đạt tiêu chuẩn an toàn dữ liệu**: Bắt buộc mã hóa đường truyền bằng **SSL Certificate** (`global-bundle.pem`).
3. **Tự động hóa đồng bộ**: Đã thực thi Prisma CLI để đẩy toàn bộ Schema của dự án NestJS lên AWS RDS sẵn sàng cho các luồng nghiệp vụ đọc/ghi dữ liệu.
