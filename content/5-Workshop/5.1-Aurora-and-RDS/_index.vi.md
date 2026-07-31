---
title : "TRIỂN KHAI CƠ SỞ DỮ LIỆU (AMAZON AURORA & RDS)"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Giới thiệu về Amazon RDS & Aurora

* **Amazon RDS (Relational Database Service)** và **Amazon Aurora** là các dịch vụ cơ sở dữ liệu quan hệ được quản lý hoàn toàn bởi AWS, giúp đơn giản hóa việc thiết lập, vận hành và mở rộng quy mô cơ sở dữ liệu trên Cloud.
* Trong hệ thống y tế, cơ sở dữ liệu đóng vai trò lưu trữ toàn bộ dữ liệu cấu trúc nhạy cảm (thông tin người dùng, hồ sơ bệnh án, lịch hẹn khám). Việc triển khai RDS trong **VPC Private Subnet** kết hợp với **mã hóa SSL** đảm bảo tính an toàn, bảo mật và tuân thủ các tiêu chuẩn dữ liệu y tế nghiêm ngặt.

#### Tổng quan về cách triển khai

Trong bài thực hành này, bạn sẽ tiến hành khởi tạo và cấu hình cơ sở dữ liệu **PostgreSQL** trên Amazon RDS (`healthcare-db`) để phục vụ cho Backend **NestJS (sử dụng Prisma ORM)**:  
* Khởi tạo database instance `healthcare-db` sử dụng lớp máy chủ `db.t4g.micro` (AWS Graviton2) để tối ưu chi phí vận hành.
* Cấu hình lớp bảo vệ mạng **Security Group** và kích hoạt cơ chế mã hóa đường truyền **SSL Certificate** (`global-bundle.pem`).
* Trích xuất chuỗi kết nối (`DATABASE_URL`) và đồng bộ hóa cấu trúc bảng (Schema Migration) từ dự án NestJS lên AWS RDS thông qua Prisma CLI.

#### Nội dung Các bước Thực hiện

* Bước 1: Khởi tạo Cụm Cơ sở Dữ liệu (Database Creation)
* Bước 2: Cấu hình Mạng và Bảo mật (Network & Security)
* Bước 3: Trích xuất Chuỗi Kết nối (Connection String)
* Bước 4: Đồng bộ Schema từ NestJS lên AWS RDS