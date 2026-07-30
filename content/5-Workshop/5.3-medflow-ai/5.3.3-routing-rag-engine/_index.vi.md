---
title: "Kiến Trúc Định Tuyến & RAG Engine Tiên Tiến"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Sự kết hợp giữa kết quả bóc tách thực thể của mô hình ViMQ NER và hệ thống Cloud RAG được quản lý trên AWS Bedrock tạo ra luồng xử lý mượt mà, chuẩn xác tuyệt đối và bảo vệ an toàn y khoa tối đa cho bệnh nhân.

---

### 1. Phân Loại Ý Định & Định Tuyến Đa Prompt (Intelligent Router & RunnableBranch)

Hệ thống không sử dụng một Prompt chung chung cho mọi truy vấn mà áp dụng cơ chế định tuyến ngữ cảnh năng động thông qua LangChain `RunnableBranch`:

- **LLM Router (`router_prompt`)**: Sử dụng mô hình LLM tốc độ cao (GPT-4o-mini) nhận vào câu hỏi gốc của bệnh nhân kết hợp cùng các thực thể lâm sàng vừa trích xuất từ ViMQ NER. Mô hình sẽ đánh giá và phân loại vào **6 nhãn ý định chuyên sâu**: `BOOKING`, `TREATMENT`, `CAUSE`, `SEVERITY`, `DIAGNOSIS`, và `OTHER`.
- **Định Tuyến Ngữ Cảnh (`RunnableBranch`)**: Tùy thuộc vào nhãn ý định, luồng RAG được định hướng chính xác vào bộ Prompt chuyên biệt tương ứng định nghĩa trong `prompt.py`:
  - **`BOOKING Prompt` (Đặt lịch hẹn)**: Hướng dẫn chi tiết quy trình 5 bước đặt lịch khám trên hệ thống MedFlow (kèm đường dẫn truy cập `#expert`). Đặc biệt, AI thông báo rõ cho bệnh nhân rằng **Báo cáo sơ loại lâm sàng AI (AI Triage Report)** bao gồm tóm tắt triệu chứng và chỉ số sẽ được tự động đính kèm trực tiếp vào hồ sơ đặt lịch để bác sĩ điều trị có thể xem xét trước!
  - **`TREATMENT Prompt` (Hướng xử lý & Sơ cứu)**: Cung cấp các lời khuyên chăm sóc ban đầu, biện pháp sơ cứu an toàn tại nhà. Bắt buộc **gợi ý chính xác Chuyên khoa thăm khám phù hợp nhất** từ danh sách chính thức của Bệnh viện MedFlow (Nội tổng hợp, Ngoại, Nhi, Sản-Phụ khoa, Da liễu, Tai-Mũi-Họng, Mắt, Răng-Hàm-Mặt, Cấp cứu 24/7).
  - **`CAUSE Prompt` (Căn nguyên bệnh lý)**: Phân tích cơ chế khoa học gây ra triệu chứng hoặc tác dụng phụ của thuốc, đưa ra các lời khuyên phòng tránh và định hướng chuyên khoa kiểm tra sâu.
  - **`SEVERITY Prompt` (Đánh giá mức độ nguy hiểm)**: Niêm yết danh sách các **Dấu hiệu Cờ Đỏ (Red-Flag Warnings)** đòi hỏi bệnh nhân phải đến phòng cấp cứu ngay lập tức, phân định rõ hoàn cảnh nào có thể theo dõi tại nhà và hoàn cảnh nào cần gọi xe cứu thương.
  - **`DIAGNOSIS Prompt` (Giải thích chẩn đoán)**: Giải thích ý nghĩa của các chỉ số xét nghiệm và triệu chứng, đồng thời tuân thủ nghiêm ngặt **tuyên bố miễn trừ trách nhiệm y khoa (Medical Disclaimer)**, nhấn mạnh AI chỉ hỗ trợ quyết định lâm sàng (CDSS) và hướng dẫn đặt lịch gặp bác sĩ.
  - **`OTHER Prompt` (Giao tiếp chung)**: Xử lý các câu hỏi giao tiếp thông thường với thái độ thấu cảm, ân cần và chuyên nghiệp của một trợ lý y tế.

---

### 2. Cloud-Native Managed RAG Engine (AWS Bedrock KB + Cohere Rerank)

Module `medflow-ai` được vận hành trên nền tảng kiến trúc Đám mây được quản lý (Managed Cloud Infrastructure) của Amazon Web Services nhằm tối ưu độ tin cậy và hiệu năng:

```text
[Văn bản CSV/PDF tại data/] 
       │ (src/upload_to_s3_bedrock.py)
       ▼
[Amazon S3 Bucket: medical-data/] ──(StartIngestionJob)──> [AWS Bedrock KB (Managed Vector Index)]
                                                                    │
                                                           (AmazonKnowledgeBasesRetriever)
                                                                    ▼
[Top 3 Passage Cô đọng] <──(ContextualCompressionRetriever / Cohere Rerank v3.0)<── [Top K=5 Raw Docs]
```

- **Đồng bộ hóa Amazon S3 & Bedrock Knowledge Bases**: Toàn bộ tài liệu phác đồ điều trị lâm sàng (.csv, .pdf) từ thư mục `data/` được đẩy lên kho lưu trữ S3 thông qua kịch bản `src/upload_to_s3_bedrock.py`. Kịch bản này tự động gọi API `StartIngestionJob` trên AWS Bedrock, kích hoạt tiến trình chia nhỏ văn bản (chunking) và lập chỉ mục vector nhúng quản lý bởi AWS.
- **Quy trình Truy xuất & Nén Ngữ cảnh 2 Giai đoạn (Hybrid Retrieval)**:
  - **Giai đoạn 1 (Khôi phục Ngữ cảnh & Truy xuất thô)**: Mô-đun `Contextualize Query Generator` biến đổi câu thoại hiện tại thành một câu hỏi tiếng Việt độc lập, đầy đủ chủ vị. Sau đó, `AmazonKnowledgeBasesRetriever` tìm kiếm và lấy về $k=5$ tài liệu thô có độ tương đồng cosine cao nhất từ Bedrock Knowledge Base.
  - **Giai đoạn 2 (Chấm điểm lại & Cô đọng tri thức)**: Đưa $k=5$ tài liệu thô qua bộ lọc `ContextualCompressionRetriever` tích hợp mô hình chấm điểm chuyên sâu **Cohere Rerank (`rerank-multilingual-v3.0`)**. Cohere đánh giá độ liên quan ngữ nghĩa đa ngữ sâu sắc và chỉ giữ lại **Top 3 đoạn văn bản (passages) chuẩn lâm sàng nhất**, triệt tiêu hoàn toàn thông tin nhiễu, tiết kiệm token tối đa trước khi đưa vào LLM sinh câu trả lời.

---
*Chuyển sang chuyên đề tiếp theo: **[4. Quản Lý Ngữ Cảnh, Streaming & Observability](../5.3.4-memory-streaming-observability/)**.*
