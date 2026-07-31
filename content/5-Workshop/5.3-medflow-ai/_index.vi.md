---
title: "Xây Dựng & Triển Khai Module AI (MedFlow AI) Trên AWS"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

Module **`medflow-ai`** là hệ thống Trợ lý Sơ loại Bệnh nhân & Hỗ trợ Quyết định Lâm sàng (AI Medical Triage & CDSS). Hệ thống kết hợp mô hình xử lý ngôn ngữ tự nhiên cục bộ **ViMQ (NER)**, hạ tầng **AWS Cloud-Native (S3, Bedrock Knowledge Base, CloudWatch)** và mô hình **GPT-4o-mini** được giám sát qua **Langfuse**.

Phần này hướng dẫn chi tiết các bước thực hành cấu hình, tích hợp và vận hành module AI trên hạ tầng đám mây AWS.

---

### 1. Luồng Xử Lý Logic & Tổng Quan Kiến Trúc (Model Flow & Logic)

#### Luồng xử lý thực tế (Execution Flow)
1. **Tiếp nhận truy vấn**: Khách hàng/Bệnh nhân gửi câu hỏi (Ví dụ: *"Con tôi bị khó thở có sao không?"*).
2. **Trích xuất thực thể (Local ViMQ NER)**: Mô hình ViMQ nhận diện và bóc tách các từ khóa y khoa cốt lõi (Ví dụ: `SYMPTOM: khó thở`).
3. **Định tuyến ý định (LLM Intent Router)**: Dựa trên từ khóa và ngữ cảnh, hệ thống phân loại luồng phản hồi phù hợp (Cấp cứu / Đặt lịch / Triệu chứng / Điều trị).
4. **Truy xuất tri thức (AWS Bedrock Knowledge Base)**: Truy vấn dữ liệu tri thức y khoa đã được chunking và index sẵn từ Amazon S3.
5. **Tổng hợp câu trả lời (LLM Generation)**: Mô hình GPT-4o-mini tổng hợp câu trả lời chuẩn y khoa dựa trên tri thức từ Bedrock KB và từ khóa do ViMQ trích xuất.
6. **Tracing & Telemetry**: Toàn bộ luồng suy luận được ghi nhận qua **Langfuse** và log hệ thống đẩy về **AWS CloudWatch**.

```mermaid
flowchart TD
    Client[MedFlow Client / API Gateway] <-->|gRPC Bi-directional Stream| gRPC_Server[gRPC LangGraph Server :50051]
    
    subgraph AI_Core [MedFlow AI Brain]
        gRPC_Server --> ViMQ_Inferencer[Local ViMQ NER Model\nTrích xuất từ khóa: khó thở]
        ViMQ_Inferencer --> LLM_Router[Intelligent Intent Router\nPhân loại luồng xử lý]
        LLM_Router --> Branch{RunnableBranch Routing}
    end

    subgraph AWS_Cloud [AWS Infrastructure & Bedrock]
        S3_Storage[(Amazon S3\nLưu trữ tài liệu y khoa .pdf/.csv)] -->|Data Source| Bedrock_KB[AWS Bedrock Knowledge Base\nChunking & Vector Indexing]
    end

    Branch -->|Query Context| Bedrock_KB
    Bedrock_KB -->|Retrieve Top Docs| LLM_Gen[GPT-4o-mini Generator\nTổng hợp câu trả lời]
    LLM_Gen -->|Token Streaming| gRPC_Server

    subgraph Observability [Tracing & Logging]
        LLM_Gen -.->|Trace Prompt & Latency| Langfuse[Langfuse Callback Handler]
        gRPC_Server -.->|System & Error Logs| CloudWatch[AWS CloudWatch Logs]
    end