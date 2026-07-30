---
title: "Tóm Tắt Quy Trình Xử Lý Một Truy Vấn (End-to-End Execution Flow)"
date: 2026-07-01
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

Để hiểu rõ cách các thành phần công nghệ trong module **`medflow-ai`** phối hợp mượt mà với nhau từng mili-giây, hãy cùng mô phỏng chi tiết hành trình xử lý một ca lâm sàng thực tế từ một bệnh nhân đang gặp tình trạng sốt cao không đáp ứng thuốc hạ sốt.

---

### Tình Huống Lâm Sàng Mẫu (Patient Scenario)

Bệnh nhân gửi tin nhắn thoại qua ứng dụng MedFlow Client:
> *"Tôi bị đau đầu dữ dội kèm sốt cao 39 độ, uống paracetamol không đỡ, tôi phải làm sao?"*

---

### Chi Tiết 9 Bước Xử Lý Kỹ Thuật Thời Gian Thực

#### Bước 1: Tiếp Nhận Bản Tin gRPC tại Cổng `50051`
- **Hoạt động**: Cổng API Gateway nhận tin nhắn từ Client, đóng gói thành bản tin Protobuf `triage.ConsultationRequest(client_id="usr_882", query=...)` và truyền qua kênh gRPC streaming tới máy chủ AI đang lắng nghe ở cổng `50051`.
- **Độ trễ khởi tạo**: ~5ms (Không tốn overhead bắt tay HTTP).

#### Bước 2: Bóc Tách Thực thể Lâm Sàng với ViMQ NER (`ViMQNEREngine`)
- **Hoạt động**: Lớp `vimq_integration.py` đưa câu thoại vào mô hình học sâu cục bộ PhoBERT + BiLSTM + Biaffine Classifier. Mô hình nhận diện và xuất ra danh sách thực thể:
  - `SYMPTOM_AND_DISEASE`: `["đau đầu dữ dội", "sốt cao 39 độ"]`
  - `DRUG`: `["paracetamol"]`
- **Độ trễ inference cục bộ**: ~45ms.

#### Bước 3: Phân Loại Ý Định Lâm Sàng (`LLM Intent Router`)
- **Hoạt động**: Mô hình định tuyến nhanh (GPT-4o-mini) nhận vào câu hỏi và danh sách thực thể. Nó nhận diện bệnh nhân đang tìm kiếm biện pháp xử lý khi dùng thuốc không hạ sốt $\rightarrow$ Phân loại ý định vào nhãn **`TREATMENT`**.
- **Độ trễ định tuyến**: ~120ms.

#### Bước 4: Khôi Phục Ngữ Cảnh & Tạo Câu Hỏi Độc Lập (`Contextualize Query Generator`)
- **Hoạt động**: Bộ nhớ `SafePostgresChatMessageHistory` truy vấn bảng `chat_history` trên NeonDB để lấy các hội thoại trước đó. Mô-đun RAG tái cấu trúc ngữ cảnh thành câu truy vấn tìm kiếm độc lập: *"Hướng xử lý cho bệnh nhân bị đau đầu dữ dội và sốt cao 39 độ đã uống paracetamol nhưng không hạ sốt"*.
- **Độ trễ bộ nhớ DB**: ~15ms.

#### Bước 5: Truy Xuất Thô Trên Đám Mây AWS Bedrock Knowledge Base
- **Hoạt động**: `AmazonKnowledgeBasesRetriever` gọi API lên AWS Bedrock, thực hiện tìm kiếm tương đồng cosine trên vector index lưu tại Amazon S3. Hệ thống trả về Top $k=5$ tài liệu phác đồ điều trị sốt cao từ Bộ Y tế.
- **Độ trễ AWS Bedrock**: ~85ms.

#### Bước 6: Chấm Điểm Lại & Cô Đọng Tri Thức với Cohere Rerank v3.0
- **Hoạt động**: Bộ nén `ContextualCompressionRetriever` đưa 5 tài liệu qua mô hình `rerank-multilingual-v3.0`. Cohere chấm điểm ngữ nghĩa chuyên sâu và lọc ra **Top 3 đoạn văn bản (passages) chính xác nhất** hướng dẫn xử lý sốt cao liên tục không đáp ứng thuốc hạ sốt đơn thuần.
- **Độ trễ Reranking**: ~35ms.

#### Bước 7: Kích Hoạt Luồng `TREATMENT Prompt` & Sơ Loại Chuyên Khoa
- **Hoạt động**: Luồng RAG nạp 3 tài liệu cô đọng vào bộ Prompt `TREATMENT`. LLM (GPT-4o-mini) tổng hợp lời khuyên:
  - Hướng dẫn chườm mát tích cực vùng trán, nách, bẹn; bù nước điện giải Oresol.
  - Cảnh báo nguy cơ sốt xuất huyết hoặc viêm màng não khi có kèm đau đầu dữ dội.
  - **Chỉ định Sơ loại Chuyên khoa**: Đề xuất bệnh nhân lập tức tới **"Khoa Nội tổng hợp & Chuyên sâu"** hoặc **"Khoa Cấp cứu 24/7"** của Bệnh viện MedFlow để được xét nghiệm công thức máu ngay lập tức.

#### Bước 8: Đề Xuất Đặt Lịch Hẹn & Đính Kèm Báo Cáo Sơ Loại AI
- **Hoạt động**: Ở phần kết luận của câu trả lời, trợ lý AI ân cần chủ động đề xuất:
  > *"Anh/Chị có muốn MedFlow gửi đường link và hướng dẫn chi tiết các bước đặt lịch khám ngay tại chuyên khoa này không ạ? Toàn bộ các triệu chứng sốt cao và lịch sử dùng paracetamol vừa rồi của Anh/Chị đã được AI tự động tổng hợp thành Báo cáo Sơ loại Lâm sàng (AI Triage Report) đính kèm vào hồ sơ đặt lịch để bác sĩ tiếp nhận có thể đọc trước ngay khi Anh/Chị tới viện!"*

#### Bước 9: Phát Luồng gRPC Streaming & Ghi Nhận Telemetry
- **Hoạt động**: Từng token của câu trả lời trên được phát theo thời gian thực về Client qua luồng gRPC `ChatChunk(token=...)`. Ngay khi luồng streaming hoàn tất:
  - **Langfuse Callback Handler** ghi nhận toàn bộ cây thực thi Trace, xác nhận chỉ số **TTFT đạt 180ms**, tổng thời gian hoàn thành 1.4s, chi phí token `$0.0015`.
  - **AWS CloudWatch Logs** tự động lưu lại nhật ký thành công tại Log Group `med-chatbot`.

---

### Tổng Kết Kỹ Thuật

Qua 9 bước xử lý liên hoàn trên, module **`medflow-ai`** đã chứng minh sự vượt trội toàn diện của một kiến trúc AI Cloud-Native hiện đại: kết hợp sức mạnh nhận thức sắc bén của mô hình nội địa **ViMQ NER**, tri thức chính thống của **AWS Bedrock RAG**, và độ tin cậy tuyệt đối của giao thức **gRPC streaming** trong việc cứu chữa và chăm sóc bệnh nhân.

---
*Hoàn tất báo cáo chuyên đề `medflow-ai`. Vui lòng quay lại **[Mục Lục Workshop Chính](../../)** để xem các phần triển khai tiếp theo.*
