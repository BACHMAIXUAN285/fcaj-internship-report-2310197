---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# [FCAJ2026] AWS S3 Bucket: "Mảnh ghép" lưu trữ chuẩn Cloud-Native cho Hệ thống Y tế số

---

### Mở đầu

Trong quá trình phát triển hệ thống Y tế số (Nền tảng hỗ trợ tư vấn y khoa AI và quản lý lịch hẹn), sau khi đã giải quyết xong bài toán đặt lịch chống trùng slot, tích hợp mô hình AI và dựng luồng xác thực người dùng, mình tiếp tục đối mặt với một vấn đề nhức nhối khác: **Quản lý và lưu trữ dữ liệu tệp tin (File Storage)**.

Hệ thống của mình liên tục phát sinh rất nhiều loại dữ liệu tệp tin khác nhau:  
* **Bệnh nhân**: Ảnh đại diện (Avatar), file báo cáo tóm tắt y khoa/đơn thuốc dạng PDF.
* **Bác sĩ & Nhân viên**: Bằng cấp chuyên môn, chứng chỉ hành nghề y tế.
* **Mô hình AI**: Các file trọng số huấn luyện (`.pt`, `.bin`) có dung lượng lên tới vài trăm MB và dữ liệu log hội thoại tư vấn.  

Ban đầu, thói quen tiện tay nhất khi làm local là mình quăng trực tiếp các file chứng chỉ, avatar vào thư mục uploads/ của server Backend NestJS, còn file trọng số AI thì commit thẳng vào Git. Tuy nhiên, khi chuẩn bị đưa hệ thống lên Production, mình nhận ra đây là một "thảm họa" về mặt bảo mật và khả năng mở rộng (Scalability): Repo Git trở nên quá nặng, server Backend bị gánh nặng lưu trữ file (Stateful), và nguy cơ rò rỉ các tệp y tế cá nhân là cực kỳ cao.  

Đó là lúc mình chuyển sang tìm hiểu và ứng dụng **Amazon S3 (Simple Storage Service)**.  

---

### Ứng dụng thực tế trong dự án

Thay vì biến máy chủ Backend thành nơi "chứa rác" lưu trữ, mình đã tái cấu trúc lại toàn bộ hệ thống để đẩy tất cả tài nguyên dạng tệp tin lên S3 Bucket. Cụ thể các vị trí ứng dụng chiến lược bao gồm:  
* **Bảo mật chứng chỉ hành nghề Bác sĩ**: Bằng cấp y khoa là dữ liệu cá nhân nhạy cảm, tuyệt đối không được để public. Mình tạo một **Private S3 Bucket** để chứa các file này. Khi Admin cần kiểm duyệt hồ sơ bác sĩ, Backend NestJS sẽ tạo ra một **S3 Presigned URL** có thời gian hết hạn ngắn. Hết thời hạn, URL đó tự động vô hiệu hóa, bảo mật tuyệt đối.
* **Quản lý Trọng số Mô hình AI**: Các file trọng số (`model.pt`) được tách biệt hoàn toàn khỏi mã nguồn. Toàn bộ file trọng số và checkpoints huấn luyện được lưu trên S3. Khi container service AI khởi chạy, script Python sẽ tự động kéo bản weights mới nhất từ S3 về bộ nhớ để nạp mô hình. Việc quản lý phiên bản cho mô hình AI trở nên cực kỳ nhẹ nhàng.
* **Xuất Báo cáo Y tế & Lưu trữ Log Chat**: Mỗi khi bệnh nhân hoàn thành buổi tư vấn hoặc khám bệnh, hệ thống tự động xuất file PDF báo cáo và ghi nhận nhật ký log hội thoại từ AI Service. Các file này được đẩy thẳng lên S3 Bucket để phục vụ việc tải về hoặc lưu trữ lâu dài.  

---

### Những giá trị vượt trội khi chuyển sang Amazon S3

Sau khi tích hợp thành công S3 Bucket vào hệ thống, đây là những giá trị lớn nhất mà dự án nhận được:  
1. **Giải phóng Backend về trạng thái "Stateless"**: Server Backend NestJS giờ đây chỉ thuần túy xử lý logic nghiệp vụ và API. Việc gỡ bỏ toàn bộ file tĩnh giúp server nhẹ hơn hẳn, dễ dàng nhân bản (scale-out) ra nhiều instance mà không lo bị lệch dữ liệu file lưu trữ.
2. **Bảo mật tuyệt đối dữ liệu y tế nhạy cảm**: Không còn rủi ro lộ đường dẫn file trực tiếp. Việc kiểm soát truy cập thông qua IAM Role và Presigned URL giúp đảm bảo chỉ đúng người, đúng thời điểm mới có thể tiếp cận được tài liệu y khoa.
3. **Độ tin cậy & Chi phí tối ưu tuyệt đối**: S3 cam kết độ bền vững dữ liệu lên tới 99.999999999% (11 số 9). Bên cạnh đó, AWS cấp sẵn 5GB lưu trữ miễn phí trong 12 tháng đầu. Kết hợp với việc cài đặt **Lifecycle Rules** (tự động xóa log tạm hoặc chuyển file cũ sang lưu trữ giá rẻ Glacier), chi phí duy trì hạ tầng lưu trữ cho dự án gần như bằng 0.

---

### Lời kết

Ứng dụng các dịch vụ Cloud-Native như Amazon S3 để quản lý tệp tin chính là tư duy cốt lõi giúp chuẩn hóa kiến trúc hệ thống hiện đại. Thay vì biến server Backend thành một "kho chứa" cồng kềnh và đối mặt với hàng loạt rủi ro bảo mật, hãy nhường gánh nặng lưu trữ và quản lý tài nguyên đó cho AWS S3.  

Điều này không chỉ giúp dự án của bạn trở nên chuyên nghiệp, linh hoạt hơn mà còn giúp bạn dồn trọn tâm trí vào việc phát triển các tính năng nghiệp vụ cốt lõi.  

---

### Tài liệu tham khảo

1. **AWS**. *"Amazon Simple Storage Service (S3) User Guide"*. (<https://docs.aws.amazon.com/AmazonS3/latest/userguide/>)
2. **AWS**. *"Amazon S3 Product Overview"*. (<https://aws.amazon.com/s3/>)

---

Xem bài viết trên Facebook [Tại đây](<https://www.facebook.com/groups/awsstudygroupfcj/permalink/2229299597835000/?rdid=53JdldxFDjYrRw5Q#>)
