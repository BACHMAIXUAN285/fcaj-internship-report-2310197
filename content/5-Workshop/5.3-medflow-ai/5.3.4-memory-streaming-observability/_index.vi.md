---
title: "Quản Lý Ngữ Cảnh, Streaming & Observability"
date: 2026-07-01
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

Để đáp ứng các tiêu chuẩn khắt khe nhất của một hệ thống y tế cấp sản xuất (Production-grade), module **`medflow-ai`** được xây dựng với kiến trúc quản lý bộ nhớ tự phục hồi, truyền tải bất đồng bộ độ trễ thấp và giám sát viễn trắc (telemetry) toàn diện 24/7.

---

### 1. Quản Lý Bộ Nhớ Bền Vững Tự Phục Hồi (`SafePostgresChatMessageHistory`)

Trong môi trường điện toán đám mây, kết nối tới cơ sở dữ liệu quan hệ (PostgreSQL / NeonDB) thường xuyên phải đối mặt với tình trạng ngắt kết nối đột ngột (network blips) hoặc hết hạn phiên làm việc (timeout). Nếu sử dụng driver thông thường, toàn bộ ngữ cảnh chẩn đoán y khoa của bệnh nhân sẽ bị mất trắng.

Module giải quyết triệt để vấn đề này bằng lớp bộ nhớ tùy biến `SafePostgresChatMessageHistory`:
- **Đấu Nối Bất Đồng Bộ (`Async psycopg`)**: Sử dụng trình điều khiển `psycopg` thế hệ mới hỗ trợ hoàn toàn I/O bất đồng bộ, giúp máy chủ gRPC không bị khóa luồng khi đọc/ghi lịch sử chat vào bảng `chat_history`.
- **Cơ Chế Tự Phục Hồi Kết Nối (Auto-reconnect)**: Lớp `SafePostgresChatMessageHistory` được ghi đè (override) các phương thức cốt lõi `aget_messages` và `aadd_messages`. Trước mỗi giao dịch đọc/ghi, hệ thống kiểm tra trạng thái `_aconnection.closed` hoặc bẫy ngoại lệ `OperationalError`. Nếu phát hiện kết nối đã rớt, module tự động khởi tạo lại một kết nối mới tới cơ sở dữ liệu NeonDB chỉ trong vài mili-giây, đảm bảo hội thoại tư vấn y khoa không bao giờ bị gián đoạn.

---

### 2. Vi Dịch Vụ gRPC Bi-directional Streaming (`LangGraphServicer`)

Để loại bỏ hoàn toàn độ trễ giao thức HTTP (cực kỳ quan trọng khi LLM mất 1-2 giây để suy luận toàn bộ câu trả lời), `medflow-ai` vận hành trên máy chủ **gRPC Microservice** tại cổng `50051`:

- **Đặc Tả Giao Thức Protobuf (`triage.proto`)**: Khung truyền tải dữ liệu giữa Cổng FastAPI Gateway và máy chủ AI được định nghĩa nhị phân nghiêm ngặt qua tệp `triage.proto`, tối ưu hóa băng thông mạng.
- **Truyền Phát Song Hướng (Bi-directional Streaming)**: Thông qua lớp dịch vụ `LangGraphServicer`, ngay khi bộ sinh (Generator) của LLM phát ra một từ mới, từ đó sẽ được đóng gói vào đối tượng `ChatChunk(token=...)` và đẩy ngược qua luồng gRPC về cho Client. Bệnh nhân có thể thấy câu trả lời xuất hiện mượt mà từng chữ theo thời gian thực (Real-time token streaming).
- **Khắc Phục Lỗi Event Loop trên Windows**: Mã nguồn tích hợp bộ quản lý luồng asyncio tùy biến, triệt tiêu hoàn toàn lỗi xung đột `ProactorEventLoop` thường gặp khi chạy các vi dịch vụ streaming bất đồng bộ trên môi trường máy chủ Windows.

---

### 3. Giám Sát Viễn Trắc Toàn Diện (Comprehensive Telemetry)

Một hệ thống AI y tế không thể vận hành như một "hộp đen". Chúng tôi áp dụng kiến trúc giám sát kép trên cả hai tầng hiệu năng AI và nhật ký hệ thống:

```text
[Luồng gRPC Server / LLM Generation]
          │
          ├──(1) LLM Callbacks ──> [Langfuse Cloud Platform] (Độ trễ TTFT, Token Cost, Tracing)
          │
          └──(2) System / Error Logs ──> [AWS CloudWatch Logs] (Group: med-chatbot | Stream: gRPC-Server)
```

1. **Giám Sát Mô Hình AI Với Langfuse (AI Observability)**:
   - Tích hợp trực tiếp `Langfuse Callback Handler` vào từng chuỗi RAG LangChain.
   - Bảng điều khiển Langfuse ghi nhận chi tiết cây thực thi (Execution Tree): đo lường độ trễ từ lúc nhận câu hỏi đến khi phát ra token đầu tiên (**Time-to-First-Token - TTFT** < 200ms), thời gian truy xuất AWS Bedrock, và tự động tính toán chi phí token (FinOps) cho từng ca tư vấn.

2. **Quản Trị Nhật Ký Hệ Thống Với AWS CloudWatch (`watchtower`)**:
   - Sử dụng thư viện `watchtower` chuyển tiếp tự động toàn bộ nhật ký hệ thống (System logs), cảnh báo bảo mật và các ngoại lệ gRPC (gRPC Exceptions) lên CloudWatch.
   - Các bản ghi được tập trung tại Log Group **`med-chatbot`** bên dưới luồng Log Stream **`gRPC-Server`**. Nhờ đó, đội ngũ kỹ sư có thể thiết lập các bộ cảnh báo CloudWatch Alarms để lập tức phát hiện các bất thường trong hạ tầng Cloud RAG.

---
*Chuyển sang chuyên đề tiếp theo: **[5. Điểm Nổi Bật & Giá Trị Độc Bản Của medflow-ai (USPs)](../5.3.5-unique-selling-points/)**.*
