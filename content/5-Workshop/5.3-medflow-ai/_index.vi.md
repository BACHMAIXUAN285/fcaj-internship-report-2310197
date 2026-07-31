---
title : "Xây Dựng & Triển Khai Module AI (MedFlow AI) Trên AWS"
date : 2026-07-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Tổng quan kiến trúc hệ thống AI

Module **`medflow-ai`** là hệ thống Trợ lý Sơ loại Bệnh nhân & Hỗ trợ Quyết định Lâm sàng (AI Medical Triage & CDSS). Hệ thống kết hợp mô hình xử lý ngôn ngữ tự nhiên cục bộ **ViMQ (NER)**, hạ tầng **AWS Cloud-Native (S3, Bedrock Knowledge Base, CloudWatch)** và mô hình **GPT-4o-mini** được giám sát qua **Langfuse**.

```text
                  [ Khách hàng / Bệnh nhân ]
                              │
                              ▼
                [ Trích xuất thực thể y khoa ]
                    (Local ViMQ NER Model)
                              │
                              ▼
                  [ Định tuyến ý định LLM ]
                    (LLM Intent Router)
                              │
                              ▼
              [ Truy xuất tri thức y khoa RAG ]
                (AWS Bedrock Knowledge Base)
                              │
                              ▼
                [ Tổng hợp phản hồi lâm sàng ]
                    (GPT-4o-mini Engine)
                              │
              ┌───────────────┴───────────────┐
              ▼                               ▼
    [ Giám sát luồng LLM ]          [ Ghi nhận log hệ thống ]
          (Langfuse)                   (AWS CloudWatch)

```

#### Nội dung
- [Cấu hình Amazon S3](5.3.1-data-storage/)
- [Cấu hình AWS Bedrock Knowledge Base](5.3.2-bedrock/)
- [Khởi Tạo Server Cục Bộ ViMQ & gRPC Server](5.3.3-vimq-grpc-deployment/)
- [Tích Hợp RAG, Langfuse Tracing & CloudWatch Logging](5.3.4-rag-tracing-monitoring/)