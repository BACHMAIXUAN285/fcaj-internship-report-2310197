---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# [FCAJ2026] AWS Bedrock Knowledge Bases là gì? Tại sao đây là "mảnh ghép" hoàn hảo cho kiến trúc Serverless RAG?

---

### Mở đầu

Sau khi tìm hiểu cách xây dựng các hệ thống Trợ lý AI y khoa bằng phương pháp RAG (Retrieval-Augmented Generation) từ đầu, mình bắt đầu đối mặt với hàng loạt khó khăn trong việc tự xây dựng đường ống dữ liệu (Data Pipeline). Điều khiến mình bất ngờ là khi đọc các tài liệu và giải pháp mẫu của AWS, hầu hết kiến trúc đều sử dụng "AWS Bedrock Knowledge Bases" thay vì hướng dẫn tự triển khai các Vector Database độc lập.

Điều này khiến mình đặt ra một câu hỏi: "Nếu việc tự thiết lập chunking và vector database là cách làm tiêu chuẩn của RAG, tại sao AWS lại sinh ra Bedrock Knowledge Bases?"

Sau khi đọc tài liệu chính thức và trực tiếp triển khai dịch vụ này cho một dự án trợ lý y khoa, mình nhận ra rằng Bedrock Knowledge Bases không chỉ là một "nơi lưu trữ vector" mà là một dịch vụ quản lý toàn bộ quy trình RAG, biến mọi công đoạn phức tạp thành Serverless.

---

### Tự quản lý hạ tầng RAG - Nỗi ám ảnh vận hành

Trước đây, mình nghĩ việc xây dựng một hệ thống RAG chủ yếu xoay quanh việc tự viết script. Chẳng hạn, để hệ thống có thể đọc hàng chục ngàn trang tài liệu PDF hay CSV y khoa, mình phải tự viết code để cắt gọt văn bản (chunking), gọi API của các mô hình embedding để chuyển đổi văn bản, và sau đó tự host một Vector Database như Milvus hay Qdrant.

Cách làm này khá thú vị khi làm các dự án nhỏ. Tuy nhiên, khi khối lượng dữ liệu y khoa tăng lên, việc quản lý hạ tầng này trở nên khó khăn. Việc duy trì một Vector Database ổn định hay viết cronjob/Airflow để đồng bộ dữ liệu liên tục sinh ra rất nhiều vấn đề về vận hành (Ops).

Đó là lý do các hệ thống đám mây hiện đại khuyến khích sử dụng các dịch vụ Managed Serverless - phương pháp giao phó toàn bộ việc quản lý hạ tầng cơ sở cho nhà cung cấp đám mây.

---

### AWS Bedrock Knowledge Bases là gì?

Theo tài liệu chính thức của AWS, "Knowledge bases for Amazon Bedrock" là một khả năng được quản lý toàn diện (fully managed) giúp kết nối các mô hình nền tảng (Foundation Models) với các nguồn dữ liệu nội bộ của doanh nghiệp để thực hiện RAG.

Nói cách khác, AWS Bedrock Knowledge Bases tự động hóa hoàn toàn quy trình xử lý dữ liệu. Thay vì phải tự tay làm từng bước, dịch vụ này sẽ đảm nhận:

1. **Tự động Chunking**: Phân tách ngữ nghĩa các tài liệu y khoa phức tạp.
2. **Tự động Embedding**: Biến đổi văn bản thành vector thông qua các mô hình như Amazon Titan hay Cohere.
3. **Tự động Indexing**: Lưu trữ và lập chỉ mục trong một Vector Database Serverless ẩn dưới nền (như Amazon OpenSearch Serverless).

Đây là điểm khiến mình thay đổi cách nhìn về việc xây dựng ứng dụng AI. Trước đây, mình nghĩ kỹ sư AI phải tự tay kiểm soát từng bước của Data Pipeline. Tuy nhiên, sau khi sử dụng Bedrock Knowledge Bases, mình nhận ra "phần việc vận hành hạ tầng nên được tự động hóa để tập trung vào logic ứng dụng".

---

### Quy trình làm việc với AWS Bedrock Knowledge Bases

Trong quá trình xây dựng hệ thống, quy trình tích hợp và vận hành trở nên vô cùng đơn giản:

**Tải dữ liệu lên Amazon S3**
*Tác dụng*: Amazon S3 đóng vai trò là nguồn dữ liệu gốc (Data Source). Các tài liệu lâm sàng, phác đồ điều trị chỉ cần được thả vào một S3 Bucket.

**Start Ingestion Job (Đồng bộ dữ liệu)**
*Tác dụng*: Chỉ cần một cú click chuột trên AWS Console hoặc một lệnh gọi API, hệ thống sẽ tự động đồng bộ tài liệu mới từ S3, xử lý chunking và embedding để cập nhật kiến thức cho AI mà không gây ra downtime.

**Tích hợp qua LangChain**
*Tác dụng*: Cho phép ứng dụng Python truy xuất ngữ cảnh dễ dàng. Thay vì viết code kết nối database phức tạp, mình chỉ cần sử dụng `AmazonKnowledgeBasesRetriever` kết hợp với ID của Knowledge Base để truy vấn (bao gồm cả Hybrid Search).

---

### Vai trò của Amazon S3 trong kiến trúc

Ban đầu, mình chỉ xem Amazon S3 như một nơi lưu trữ file tĩnh. Tuy nhiên, khi kết hợp với Bedrock Knowledge Bases, mình nhận ra S3 chính là "cửa ngõ" kiến thức của toàn bộ hệ thống. Bất cứ khi nào bệnh viện ban hành danh mục thuốc hoặc phác đồ mới, quản trị viên chỉ cần đẩy file lên S3. Không cần can thiệp vào code, không cần deploy lại ứng dụng, hệ thống AI vẫn lập tức có được kiến thức mới nhất.

Có thể nói, Amazon S3 kết hợp cùng Bedrock Knowledge Bases tạo ra một luồng cập nhật tri thức tự động và vô hạn.

---

### Vì sao AWS Bedrock Knowledge Bases là "chân ái" cho kỹ sư AI?

Đây là điều mình đúc kết được sau khi hoàn thiện dự án. Điểm khác biệt lớn nhất nằm ở sự giải phóng nguồn lực.

Nếu tự xây dựng RAG, kỹ sư sẽ phải đóng vai trò của cả một đội ngũ DevOps: loay hoay với hạ tầng, xử lý lỗi pipeline, và giám sát Vector Database. Ngược lại, Bedrock Knowledge Bases đưa toàn bộ gánh nặng đó về phía AWS. Dịch vụ này xử lý mọi tác vụ ngầm định phức tạp và trả lại cho chúng ta những API sạch sẽ, đơn giản nhất.

Chính vì vậy, AWS Bedrock Knowledge Bases giúp các nhóm kỹ sư tiết kiệm hàng tuần làm việc, cho phép họ dồn toàn bộ sự tập trung vào việc tối ưu hóa business logic lâm sàng và cải thiện trải nghiệm của bệnh nhân.

---

### Tài liệu tham khảo

1. AWS. "Knowledge bases for Amazon Bedrock". ([https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html))
2. LangChain. "Amazon Knowledge Bases Integrations". ([https://python.langchain.com/docs/integrations/retrievers/bedrock/](https://python.langchain.com/docs/integrations/retrievers/bedrock/))

---

Xem bài viết trên Facebook [Tại đây](<https://www.facebook.com/groups/awsstudygroupfcj/permalink/2227962487968711/?rdid=DpIlk8AoW652AXKC#>)
