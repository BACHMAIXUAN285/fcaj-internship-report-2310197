---
title: "Tích Hợp RAG, Langfuse Tracing & CloudWatch Logging"
date: 2026-07-01
weight: 4
chapter: false
pre: " <b> 5.3.4. </b> "
---

Phần này hướng dẫn các bước lập trình tích hợp luồng RAG, cài đặt công cụ Tracing với Langfuse và cấu hình đẩy log hệ thống lên AWS CloudWatch.

---

### Tích Hợp Luồng Xử Lý RAG & Tracing Với Langfuse

* **Mục đích**: Tích hợp dữ liệu từ ViMQ NER, tra cứu Bedrock KB, sinh câu trả lời bằng GPT-4o-mini và đẩy trace về Langfuse.
* **Các bước thực hiện**:
  1. Tích hợp SDK `langchain-aws` vào mã nguồn để truy vấn Bedrock KB:
     ```python
     from langchain_aws import AmazonKnowledgeBasesRetriever

     retriever = AmazonKnowledgeBasesRetriever(
         knowledge_base_id="YOUR_BEDROCK_KB_ID",
         retrieval_config={"vectorSearchConfiguration": {"numberOfResults": 3}}
     )
     ```
  2. Cấu hình Langfuse Callback để theo dõi chi tiết luồng gọi LLM và độ trễ:
     ```python
     from langfuse.callback import CallbackHandler

     langfuse_handler = CallbackHandler(
         public_key="pk-lf-...",
         secret_key="sk-lf-...",
         host="[https://cloud.langfuse.com](https://cloud.langfuse.com)"
     )
     ```
  3. Xây dựng luồng hoàn chỉnh trong `grpc_server.py`:
     * Bóc tách từ khóa qua ViMQ - Định tuyến ý định - Query Bedrock KB lấy ngữ cảnh - Gọi LLM tổng hợp phản hồi - Stream token về gRPC Client.

---

### Cấu hình Giám sát Logs trên AWS CloudWatch

* **Mục đích**: Ghi nhận toàn bộ System Log, Error Log và nhật ký hoạt động của gRPC Server lên CloudWatch.
* **Các bước thực hiện**:
  1. Truy cập **Amazon CloudWatch Console**. Mục **Logs**. Chọn **Log groups**.
  2. Nhấn **Create log group** với tên: `/aws/medflow/med-chatbot`.
  3. Trong mã nguồn `grpc_server.py`, cấu hình thư viện `watchtower` hoặc `boto3` để tự động đẩy log khi ứng dụng vận hành:
     ```python
     import logging
     import watchtower

     logging.basicConfig(level=logging.INFO)
     logger = logging.getLogger("MedFlowAI")
     logger.addHandler(watchtower.CloudWatchLogHandler(log_group="/aws/medflow/med-chatbot"))
     ```

![Langfuse](/images/5-Workshop/5.3-medflow-ai/langfuse%20tracing%20router.png)
---
