---
title: "Cấu Hình AWS Bedrock Knowledge Base"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---


---

### Cấu hình AWS Bedrock Knowledge Base (Chunking & Indexing)

* **Mục đích**: Biến đổi tài liệu thô trên S3 thành cơ sở dữ liệu tri thức (Knowledge Base) tự động phân đoạn (Chunking) để phục vụ tra cứu RAG.
* **Các bước thực hiện**:
  1. Truy cập **Amazon Bedrock Console**. Chọn **Knowledge bases**. Nhấn **Create knowledge base**.
  2. **Cấu hình IAM Role**: Chọn tạo mới IAM Role có quyền truy cập đọc S3 Bucket `medflow-medical-knowledge-base`.
  3. **Kết nối Data Source**:
     * Chọn nguồn dữ liệu là **Amazon S3**.
     * Trỏ đường dẫn S3 URI đến thư mục chứa tài liệu y khoa đã tạo ở **Bước 1**.
  4. **Cấu hình Chunking Strategy**:
     * Chọn phương thức **Fixed-size chunking** (Kích thước đoạn: 300 - 500 tokens, Overlap: 20%).
  5. **Cấu hình Vector Store**: Chọn tự động tạo **Amazon OpenSearch Serverless** vector index để lưu trữ các đoạn văn bản dưới dạng Vector Embeddings.
  6. Chọn **Sync** để tiến hành quét dữ liệu từ S3, phân đoạn (chunking) và đánh chỉ mục.

  ![Bedrock](/images/5-Workshop/5.3-medflow-ai/bedrock.png)
