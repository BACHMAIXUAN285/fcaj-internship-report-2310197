---
title: "Module medflow-ai: Cloud-Native RAG, ViMQ NER & Clinical Triage"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

Module **`medflow-ai`** là bộ não trí tuệ nhân tạo lâm sàng của hệ sinh thái y tế **MedFlow**. Hệ thống là sự kết hợp giữa **Mô hình Học sâu Cục bộ chuyên biệt cho y khoa tiếng Việt (ViMQ)**, nền tảng **Cloud-Native Managed RAG (AWS Bedrock Knowledge Bases)**, kiến trúc **Định tuyến Đa ý định (Dynamic Multi-Prompt Routing)** và vi dịch vụ **gRPC Streaming** tốc độ cao.

Dưới đây là báo cáo kỹ thuật chuyên sâu về toàn bộ kiến trúc, mô hình ViMQ, quy trình huấn luyện dữ liệu, luồng thực thi và các điểm nổi bật độc bản của module `medflow-ai`:

---

### Danh sách các chuyên đề trong Báo cáo Kỹ thuật:

1. **[Tổng Quan Kiến Trúc (Architecture Overview)](5.3.1-architecture-overview/)**  
   Khám phá cấu trúc vi dịch vụ gRPC (cổng `50051`), vai trò Trợ lý Sơ loại Bệnh viện & Hỗ trợ Quyết định Lâm sàng (CDSS), và sơ đồ luồng dữ liệu toàn phần từ Client đến Cloud RAG.

2. **[Chuyên Sâu Về Mô Hình ViMQ: Kiến Trúc, Dữ Liệu & Thuật Toán Huấn Luyện](5.3.2-vimq-ner-deep-dive/)**  
   Báo cáo tổng quan về mô hình Span-based NER kết hợp Biaffine Classifier chuyên biệt cho y khoa tiếng Việt, phương pháp chuẩn hóa bộ dữ liệu và giải pháp tự huấn luyện bồi đắp nhãn (Self-Training).

3. **[Kiến Trúc Định Tuyến & RAG Engine Tiên Tiến](5.3.3-routing-rag-engine/)**  
   Cơ chế định tuyến thông minh qua `RunnableBranch` vào 6 Prompt chuyên biệt (`BOOKING`, `TREATMENT`, `CAUSE`, `SEVERITY`, `DIAGNOSIS`, `OTHER`), kết hợp nền tảng quản lý AWS Bedrock Knowledge Bases và Cohere Rerank v3.0.

4. **[Quản Lý Ngữ Cảnh, Streaming & Observability](5.3.4-memory-streaming-observability/)**  
   Thiết lập bộ nhớ bền vững tự phục hồi (`SafePostgresChatMessageHistory` trên NeonDB/Postgres), giao thức truyền phát song hướng gRPC Streaming (`triage.proto`), và hệ thống giám sát kép Langfuse + AWS CloudWatch (`watchtower`).

5. **[Điểm Nổi Bật & Giá Trị Độc Bản Của medflow-ai (USPs)](5.3.5-unique-selling-points/)**  
   5 trụ cột chiến lược: Sự giao thoa Edge AI & Cloud AI, khả năng tự tiến hóa dữ liệu lâm sàng, luồng sơ loại liền mạch đính kèm AI Triage Report vào lịch khám, bảo vệ an toàn y khoa tuyệt đối, và độ tin cậy chuẩn Production.

6. **[Tóm Tắt Quy Trình Xử Lý Một Truy Vấn (End-to-End Execution Flow)](5.3.6-end-to-end-execution-flow/)**  
   Mô phỏng chi tiết từng mili-giây xử lý ca lâm sàng thực tế: từ bước tiếp nhận triệu chứng sốt cao/đau đầu, bóc tách thực thể ViMQ, định tuyến `TREATMENT`, truy xuất S3/Bedrock, cô đọng Cohere, cho đến phát luồng tư vấn chỉ định chuyên khoa khám.

---
*Bắt đầu đi vào chi tiết báo cáo đầu tiên: **[1. Tổng Quan Kiến Trúc (Architecture Overview)](5.3.1-architecture-overview/)**.*
