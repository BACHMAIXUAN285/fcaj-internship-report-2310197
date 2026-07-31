---
title: "Khởi Tạo Server Cục Bộ ViMQ & gRPC Server"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---


---

### Cấu hình EC2 / Server Cục Bộ Chạy Mô Hình ViMQ & gRPC Server

* **Mục đích**: Dựng môi trường chạy mô hình tự build ViMQ NER để trích xuất thực thể y khoa cục bộ trước khi chuyển sang LLM.
* **Các bước thực hiện**:
  1. Khởi tạo một **EC2 Instance** (Linux / Ubuntu) hoặc môi trường máy chủ cục bộ.
  2. Gắn **IAM Role** cho EC2 với chính sách `AmazonBedrockFullAccess` và `CloudWatchLogsFullAccess`.
  3. Cài đặt các thư viện phụ thuộc:
     ```bash
     pip install torch transformers grpcio grpcio-tools langchain-aws
     ```
  4. Tải và đóng gói mô hình ViMQ NER cục bộ vào module `vimq_integration.py` để sẵn sàng nhận câu hỏi từ Client, trích xuất từ khóa (ví dụ: *khó thở*, *sốt*, *paracetamol*).