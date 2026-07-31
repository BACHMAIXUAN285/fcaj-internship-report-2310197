---
title : "TRIỂN KHAI DỊCH VỤ XÁC THỰC & PHÂN QUYỀN (AWS COGNITO)"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Giới thiệu về AWS Cognito

* **Amazon Cognito** là dịch vụ quản lý định danh, xác thực (Authentication) và ủy quyền (Authorization) tập trung được quản lý hoàn toàn bởi AWS, hỗ trợ mở rộng hàng triệu người dùng một cách an toàn.
* Trong ứng dụng y tế, việc bảo vệ thông tin bệnh án và dữ liệu cá nhân là bắt buộc. Cognito giúp ứng dụng đạt chuẩn an toàn nhờ cơ chế **mã hóa Token chuẩn RSA (JWKS)**, **phân quyền đa vai trò (RBAC)** và **ẩn danh hóa dữ liệu (Anonymization)** ở tầng xác thực.
  
#### Tổng quan về cách triển khai

Trong bài thực hành này, bạn sẽ tiến hành khởi tạo và tích hợp **AWS Cognito User Pool** (`healthcare`) vào hệ thống để phục vụ cho Frontend **Next.js** và Backend **NestJS**:
* Khởi tạo **User Pool** với chính sách mật khẩu bảo mật cao và tự động hóa luồng xác thực qua Email.
* Thiết lập các **User Groups** (`Admin`, `Doctor`, `Patient`) để phục vụ cơ chế phân quyền dựa trên vai trò (**Role-Based Access Control - RBAC**).
* Tích hợp **JWKS Endpoint** vào Backend NestJS để xác minh chữ ký JWT Token bất đối xứng mà không cần gọi ngược về AWS, tối ưu hiệu năng tối đa.
  
#### Nội dung Các bước Thực hiện

* Bước 1: Khởi tạo User Pool (Kho lưu trữ người dùng)
* Bước 2: Phân quyền đa vai trò (RBAC - Role-Based Access Control)
* Bước 3: Cấu hình Ứng dụng khách (App Client cho Next.js)
* Bước 4: Tích hợp Giải mã JWT vào Backend (NestJS)