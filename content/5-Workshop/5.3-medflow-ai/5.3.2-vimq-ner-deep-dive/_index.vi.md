---
title: "Chuyên Sâu Về Mô Hình ViMQ: Kiến Trúc, Dữ Liệu & Thuật Toán Huấn Luyện"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

Điểm khác biệt cốt lõi giúp module **`medflow-ai`** vượt trội hơn các hệ thống AI y tế thông thường là việc sở hữu một **Mô hình Nhận dạng Thực thể Có tên (NER - Named Entity Recognition)** nội địa hóa chuyên sâu, được thiết kế và tối ưu riêng cho ngữ cảnh lâm sàng tiếng Việt.

---

### 1. Kiến Trúc Tổng Quan Mô Hình ViMQ

Mô hình ViMQ áp dụng cách tiếp cận **Span-based NER kết hợp bộ phân loại Biaffine**, giúp giải quyết hiệu quả bài toán nhận diện các từ ghép chuyên ngành y khoa, từ viết tắt và các thực thể có ranh giới lồng nhau trong tiếng Việt:

```text
[Câu thoại lâm sàng đầu vào]
            │
            ├──(1) Subword Tokenization (PhoBERT Base Embeddings)
            │
            └──(2) Character Embedding (BiLSTM / Conv Layer)
                                │
                                ▼
                       [Word Representation Layer]
                                │
                                ▼
                     [3-Layer BiLSTM Contextual Net]
                                │
                   ┌────────────┴────────────┐
                   ▼                         ▼
         [feedStart (MLP Layer)]   [feedEnd (MLP Layer)]
                   │                         │
                   └────────────┬────────────┘
                                ▼
                   [Biaffine Classifier Layer]
                                │
                                ▼
                [Dự đoán Ranh giới & Nhãn Thực thể]
```

- **Đặc trưng Ngữ nghĩa Sâu**: Mô hình sử dụng `vinai/phobert-base` làm bộ trích xuất đặc trưng ngôn ngữ, kết hợp với các vector nhúng ở cấp độ ký tự (Character-level Embeddings). Nhờ sự bổ trợ này, hệ thống duy trì khả năng nhận dạng mạnh mẽ ngay cả khi bệnh nhân sử dụng từ viết tắt y khoa, tên thuốc nước ngoài hoặc gõ sai chính tả.
- **Học Ngữ cảnh Tuần tự**: Mạng LSTM hai chiều (BiLSTM) 3 lớp giúp mô hình liên kết chặt chẽ ý nghĩa giữa các cụm từ trước và sau trong lời khai bệnh sử.
- **Phân loại Ranh giới Thực thể**: Bộ đôi mạng MLP (`feedStart` và `feedEnd`) kết hợp cùng lớp phân loại Biaffine tính toán xác suất cao nhất cho điểm bắt đầu và kết thúc của mỗi thực thể, chỉ định chính xác thuật ngữ y tế trong câu.

---

### 2. Chuẩn Hóa Bộ Dữ Liệu Lâm Sàng (Dataset)

Dữ liệu huấn luyện của ViMQ được cấu trúc hóa theo tiêu chuẩn nghiêm ngặt, chia thành các tập huấn luyện (`train.json`), đánh giá (`dev.json`) và kiểm thử (`test.json`):

- **Phân loại Nhãn Thực thể Lâm sàng (`entity_set.txt`)**: 
  - `SYMPTOM_AND_DISEASE`: Triệu chứng tự kể và biểu hiện bệnh lý (ví dụ: *đau đầu*, *sốt cao*, *tiểu đường type 2*).
  - `DRUG`: Tên biệt dược, hoạt chất điều trị (ví dụ: *paracetamol*, *aspirin*, *insulin*).
  - `MEDICAL_PROCEDURE`: Thủ thuật thăm khám, chẩn đoán hình ảnh và xét nghiệm (ví dụ: *nội soi*, *chụp MRI*, *xét nghiệm máu*).
- **Từ điển Ký tự (`char2index.json`)**: Bộ ánh xạ chuẩn hóa toàn bộ các ký tự tiếng Việt, hỗ trợ mô hình xử lý linh hoạt các biến thể văn bản thực tế.

---

### 3. Quy Trình Tự Huấn Luyện & Bồi Đắp Nhãn (Self-Training Workflow)

Khác với các mô hình gán nhãn tĩnh truyền thống, ViMQ tích hợp chiến lược **Huấn luyện lặp tự cập nhật nhãn (Iterative Bootstrapping & Self-Training)** nhằm liên tục nâng cao vốn từ vựng lâm sàng:

1. **Cơ chế Tiêm Nhiễu Chủ Động (Active Data Noising)**:  
   Trong quá trình huấn luyện, hệ thống chủ động tạo ra các vi dịch chuyển nhỏ trên ranh giới nhãn thực thể gốc. Kỹ thuật này ngăn chặn hiện tượng mô hình học vẹt ranh giới từ cứng nhắc, tăng khả năng thích ứng với văn bản nói tắt hoặc ngữ pháp tự do từ bệnh nhân.

2. **Bầu Chọn Đa Số & Tự Đồng Hóa Nhãn (Major Vote Pseudo-Labeling)**:  
   Để khắc phục những thiếu sót trong các bộ dữ liệu y khoa gán nhãn thủ công, hệ thống áp dụng cơ chế tự dự đoán và bầu chọn đa số qua nhiều chu kỳ huấn luyện. Những từ vựng y tế mới xuất hiện nhiều lần với độ tự tin cao sẽ được hệ thống tự động xác nhận và bồi đắp ngược lại vào tập huấn luyện cho chu kỳ kế tiếp.

3. **Nghiệm Thu Khắt Khe**:  
   Hiệu năng mô hình được nghiệm thu theo tiêu chuẩn `IOB` với các chỉ số đánh giá toàn diện về Độ chuẩn xác (Precision), Độ phủ (Recall) và Điểm F1.

{{% notice note %}}
**Tài liệu Tham khảo Mở rộng:** Để tìm hiểu sâu hơn về mã nguồn triển khai, cấu trúc ma trận hàm mất mát Biaffine và cấu trúc siêu tham số (hyperparameters), vui lòng tham khảo tại repository chính thức của mô hình: [ViMQ NER Official Repository](https://github.com/tadeephuy/vimq).
{{% /notice %}}

---
*Chuyển sang chuyên đề tiếp theo: **[3. Kiến Trúc Định Tuyến & RAG Engine Tiên Tiến](../5.3.3-routing-rag-engine/)**.*
