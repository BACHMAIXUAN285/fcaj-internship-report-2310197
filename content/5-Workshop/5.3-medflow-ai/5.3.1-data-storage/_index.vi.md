---
title: "Cấu hình Amazon S3"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---


---

### Lưu trữ tài liệu y khoa trên Amazon S3

* **Mục đích**: Lưu trữ các tập dữ liệu y khoa (.csv, .pdf) phục vụ quá trình huấn luyện mô hình và làm nguồn dữ liệu đầu vào cho Bedrock Knowledge Base.
* **Các bước thực hiện**:
  1. Truy cập **Amazon S3 Console**. Chọn **Create bucket**.
  ![Create bucket](/images/5-Workshop/5.3-medflow-ai/S3-1.png)
  2. Đặt tên Bucket (Ví dụ: `medflow-data`) và chọn Region (Ví dụ: `ap-southeast-1`).
  ![Name bucket](/images/5-Workshop/5.3-medflow-ai/S3-name.png)
  3. Bật cấu hình mã hóa **Server-side encryption (SSE-S3)** để bảo mật tài liệu y tế.
  ![SSE-S3](/images/5-Workshop/5.3-medflow-ai/S3-SSE.png)
  4. Tạo cấu trúc thư mục `/raw-documents/` và tiến hành Upload các tài liệu y khoa chuẩn lâm sàng.
  ![S3-now](/images/5-Workshop/5.3-medflow-ai/S3-now.png)