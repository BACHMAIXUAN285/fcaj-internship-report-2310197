---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Khởi tạo, tích hợp và triển khai hệ thống **RAG Pipeline (Retrieval-Augmented Generation)** tư vấn y tế ban đầu kết hợp giữa **AWS Bedrock Knowledge Base**, mô hình **ViMQ (Local Host)**, **GPT-4o-mini** và công cụ giám sát **Langfuse**.
* Lập trình bộ định tuyến **[LLM Intent Router]** trong NestJS Backend để phân luồng nhận câu hỏi từ Bệnh nhân, gửi trích xuất thực thể y tế qua ViMQ, tra cứu tri thức trên Bedrock KB và tổng hợp câu trả lời qua GPT-4o-mini theo thời gian thực.
* Xây dựng tính năng tự động tổng hợp nội dung trò chuyện thành tệp **Pre-consultation Report (PDF/JSON)** đẩy lên lưu trữ an toàn tại **Amazon S3** thông qua cơ chế Presigned URLs.
* Xây dựng kịch bản **Fallback an toàn** trong NestJS Backend: Khi kết nối tới dịch vụ LLM/Bedrock bị Timeout hoặc gián đoạn, hệ thống tự động điều hướng bệnh nhân sang màn hình Đặt lịch khám trực tiếp mà không gây ngắt đoạn trải nghiệm.
* Tích hợp **Langfuse** để giám sát chỉ số LLM (Token count, Latency, Prompt performance) và đồng bộ log về **AWS CloudWatch**.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu  |
| --- | --- | --- | --- | --- |
| 2   | - Thiết lập **AWS Bedrock Knowledge Base** chứa tài liệu y tế chuẩn hóa phục vụ tra cứu RAG. <br> - Cấu hình mô hình **ViMQ (Local Host)** cho bài toán trích xuất thực thể y tế (Medical NER) và chuẩn bị API **GPT-4o-mini**. | 29/06/2026 | 29/06/2026 | [Tại đây](<https://docs.aws.amazon.com/bedrock/>) |
| 3   | - Xây dựng Module **[LLM Intent Router]** trong NestJS Backend: Nhận câu hỏi từ người dùng -> Định tuyến trích xuất thực thể qua ViMQ -> Truy vấn tri thức RAG từ AWS Bedrock KB -> Gửi Prompt tổng hợp sang GPT-4o-mini trả về client. <br> - Kết nối **Langfuse** để ghi log giám sát LLM và đẩy chỉ số về **AWS CloudWatch**. | 30/06/2026 | 30/06/2026 | [Tại đây](<https://langfuse.com/docs>) |
| 4   | - Viết module tự động tổng hợp nội dung hội thoại tư vấn thành tệp **Pre-consultation Report (PDF/JSON)**. <br> - Gọi dịch vụ Amazon S3 để tải tệp báo cáo lên S3 Bucket và lưu trữ liên kết đường dẫn (S3 URI / Presigned URL) vào thông tin lịch hẹn dưới CSDL RDS PostgreSQL. | 01/07/2026 | 01/07/2026 | [Tại đây](<https://docs.aws.amazon.com/s3/>) |
| 5   | - Phát triển cơ chế **Global Exception Filter** & **Fallback Service** trong NestJS. <br> - Lập kịch bản Fallback an toàn: Khi các API LLM/Bedrock gặp sự cố nghẽn mạng -> tự động chuyển bệnh nhân sang giao diện Đặt lịch khám thủ công, đảm bảo luồng nghiệp vụ chính không bị gián đoạn. | 02/07/2026 | 02/07/2026 | [Tại đây](<https://docs.nestjs.com/exception-filters>) |
| 6   | - Kiểm thử toàn diện luồng hội thoại AI RAG Chatbot trên giao diện di động của Bệnh nhân; xác nhận file Pre-consultation Report được upload thành công lên Amazon S3. <br> - Kiểm thử màn hình Doctor Portal xem danh sách lịch hẹn và mở đọc file báo cáo tóm tắt cuộc trò chuyện của bệnh nhân trước ca khám. | 03/07/2026 | 03/07/2026 | [Tại đây](<https://cloudjourney.awsstudygroup.com/>) |


### Kết quả đạt được tuần 5:

* Triển khai thành công hệ thống **RAG Pipeline (AWS Bedrock KB + ViMQ + GPT-4o-mini)** đóng vai trò Trợ lý Chatbot AI giải đáp thắc mắc và tư vấn thông tin y tế ban đầu chuẩn xác cho bệnh nhân 24/7.
* Xây dựng hoàn chỉnh bộ định tuyến **[LLM Intent Router]** và tích hợp thành công **Langfuse** để theo dõi hiệu năng, token tiêu thụ và đẩy log hệ thống về **AWS CloudWatch**.
* Tự động hóa luồng tổng hợp và đóng gói dữ liệu trò chuyện thành file **Pre-consultation Report**, đẩy trực tiếp lên lưu trữ an toàn tại **Amazon S3**.
* Xây dựng hoàn chỉnh kịch bản **Fallback an toàn**, đảm bảo hệ thống tự động chuyển sang luồng đặt lịch khám thông thường nếu dịch vụ AI gặp sự cố gián đoạn.
* Hoàn thiện tính năng cho Doctor Portal: Bác sĩ dễ dàng tra cứu danh sách lịch hẹn trong ngày và mở xem file báo cáo tóm tắt câu hỏi của bệnh nhân từ S3.
* Chuẩn bị hạ tầng AI và dịch vụ phụ trợ hoàn chỉnh để sẵn sàng cho Tuần 6 tối ưu hệ thống giám sát **AWS CloudWatch** và tiến hành kiểm thử tải bài toán concurrency booking.


