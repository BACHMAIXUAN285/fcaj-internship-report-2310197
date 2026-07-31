---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# [FCAJ2026] AWS Cognito là gì? Tại sao đây là "mảnh ghép" không thể thiếu cho hệ thống Y tế số?

---

### Mở đầu

Trong quá trình phát triển hệ thống **Smart Healthcare Platform** (Nền tảng hỗ trợ sàng lọc y khoa AI và quản lý lịch hẹn), sau khi đã giải quyết xong bài toán đặt lịch chống trùng slot và tích hợp AI, mình tiếp tục đối mặt với một "cơn ác mộng" khác: **Quản lý định danh và phân quyền (Authentication & Authorization)**.  

Hệ thống của mình có 3 nhóm người dùng hoàn toàn riêng biệt với vai trò và quyền hạn khác nhau:  
1. **Bệnh nhân (Patient)**: Đăng ký/Đăng nhập, chat với AI, đặt lịch khám.
2. **Bác sĩ (Doctor)**: Xem lịch khám trong ngày, đọc báo cáo tóm tắt y khoa từ AI, kê đơn thuốc.
3. **Lễ tân (Receptionist)**: Quản lý quầy, check-in bệnh nhân qua mã QR, xuất hóa đơn và thu phí.  

Ban đầu, suy nghĩ đầu tiên của mình là tự viết một service Auth riêng trên Backend NestJS bằng JWT, 
PassportJS và lưu User/Password mã hóa bcrypt trong database PostgreSQL. Tuy nhiên, khi đối mặt với các yêu cầu khắt khe về bảo mật dữ liệu y tế (HIPAA compliance, mã hóa token, đổi mật khẩu tạm thời cho nhân viên y tế, hạn chế Brute-force), mình nhận ra việc **tự xây dựng hệ thống Auth từ đầu là một cái bẫy lớn**.  

Đó là lúc mình chuyển sang tìm hiểu và áp dụng **AWS Cognito**.  

---

### Tự xây dựng Auth System: Chi phí "ngầm" ít ai ngờ tới

Khi làm các dự án quy mô nhỏ, viết vài API `/login`, `/register` và trả về một JWT Token có vẻ rất đơn giản. Nhưng khi hệ thống đi vào thực tế với quy mô hàng ngàn lượt truy cập, hàng loạt bài toán phức tạp xuất hiện:  
* **Quản lý Session & Token Refresh**: Làm sao để refresh token an toàn mà không làm gián đoạn trải nghiệm người dùng?  
* **Phân quyền đa vai trò (RBAC)**: Cần đảm bảo Bệnh nhân tuyệt đối không thể truy cập vào Dashboard Bác sĩ hoặc API tạo đơn thuốc.  
* **Cấp phát tài khoản nội bộ**: Bệnh viện thêm bác sĩ mới thì cấp tài khoản thế nào? Phải tạo mật khẩu tạm thời (Temporary Password) và bắt buộc bác sĩ đổi mật khẩu ở lần đăng nhập đầu tiên.  
* **Bảo mật & Tuân thủ**: Mã hóa dữ liệu người dùng, chống tấn công Brute-force/DDoS vào API đăng nhập, gửi email khôi phục mật khẩu an toàn.  

Nếu tự code toàn bộ những tính năng này, mình sẽ phải tốn hàng tuần liền chỉ để chăm chút cho lớp Auth thay vì tập trung phát triển nghiệp vụ cốt lõi của dự án.  

---

### AWS Cognito là gì?

Theo tài liệu chính thức từ AWS, **Amazon Cognito** là dịch vụ quản lý định danh, xác thực và phân quyền truy cập người dùng (User Identity and Access Management) được quản lý toàn diện (Fully Managed). AWS Cognito cho phép bạn nhanh chóng thêm tính năng đăng ký, đăng nhập và kiểm soát truy cập vào các ứng dụng Web hoặc Mobile.  

Trong kiến trúc của AWS Cognito có 2 thành phần cốt lõi:  
1. **User Pools**: Nơi lưu trữ và quản lý thư mục người dùng (User Directory). Nó đảm nhận toàn bộ luồng đăng ký, đăng nhập, xác thực MFA, quên mật khẩu và trả về các mã **JWT Token (ID Token, Access Token, Refresh Token)**.  
2. **Identity Pools**: Cho phép phân quyền trực tiếp người dùng để họ có thể truy cập hợp lệ vào các tài nguyên AWS khác (như S3 Bucket, DynamoDB) dựa trên IAM Role.  

---

### Luồng vận hành của AWS Cognito trong Dự án Y tế

Trong hệ thống **Smart Healthcare Platform**, AWS Cognito đã hoàn toàn giải phóng Backend NestJS khỏi nhiệm vụ quản lý người dùng: 
```text 
[ Patient / Doctor / Receptionist ]  
    |  
    v (1. Credentials / Auth Request)  
[ AWS Cognito User Pool ]  
    |  
    v (2. Issue Signed JWT Tokens - RBAC Groups)  
[ Web App / Next.js ]  
    |  
    v (3. Request API + JWT Token)  
[ NestJS Backend Service ] ---> Verified by Cognito Public Key 
``` 
1. **Khởi tạo & Phân quyền User Group**: On-boarding tài khoản mượt mà.  
   * **Bệnh nhân**: Đăng ký trực tiếp trên Web App Next.js, Cognito tự động gán role `Patient`.  
   * **Bác sĩ / Lễ tân**: Quản trị viên (Admin) tạo tài khoản qua Cognito API. Cognito tự động gửi Email kèm Mật khẩu tạm thời. Ở lần đăng nhập đầu tiên trên Portal Bác sĩ, Cognito bắt buộc người dùng đổi mật khẩu mới rồi mới cấp Token chính thức.  
2. **Xác thực JWT Token tại Backend**: Backend NestJS không cần lưu trữ bất kỳ mật khẩu nào của người dùng. Mỗi Request gửi lên kèm theo Bearer JWT Token, NestJS Middleware chỉ cần verify chữ ký của Token này thông qua Public Key của AWS Cognito.  
3. **Bảo mật dữ liệu nhạy cảm**: Cognito kết hợp cùng chiến lược mã hóa UUID giúp ẩn danh hoàn toàn ID người dùng gốc, đảm bảo tính riêng tư cho hồ sơ bệnh án theo tiêu chuẩn bảo mật y tế.  

---

### Vì sao AWS Cognito là "mảnh ghép" hoàn hảo?

Sau khi tích hợp thành công Cognito vào dự án, đây là 3 giá trị lớn nhất mà mình nhận được:  
1. **Tiết kiệm chi phí vận hành & Thời gian phát triển**: Thay vì mất 2-3 tuần để dựng Auth Service, mình chỉ mất 1 ngày để tích hợp AWS Cognito SDK vào NestJS và Next.js.
2. **Chuẩn hóa Phân quyền (RBAC)**: Thông qua thuộc tính `cognito:groups` đính kèm trong JWT Token, việc Guard/Middleware trên NestJS phân quyền xem Báo cáo y khoa hay Tạo đơn thuốc trở nên cực kỳ gọn nhẹ và chính xác.
3. **Chi phí tối ưu tuyệt đối (Free Tier cực rộng)**: AWS Cognito cung cấp hạn mức miễn phí lên tới **50,000 MAU (Monthly Active Users)** mỗi tháng. Điều này giúp dự án khởi chạy giai đoạn MVP gần như với **chi phí 0 USD** cho riêng hạ tầng Auth!

---

### Lời kết

Sử dụng các dịch vụ Cloud Native như **AWS Cognito** chính là tư duy cốt lõi khi thiết kế hệ thống hiện đại. Thay vì "tái chế lại cái bánh xe" cho những bài toán kinh điển như Authentication, hãy nhường gánh nặng bảo mật và vận hành hạ tầng đó cho AWS, để bạn có thể dồn 100% năng lượng vào việc tối ưu sản phẩm và giải quyết bài toán nghiệp vụ cho người dùng!

---

### Tài liệu tham khảo

1. AWS. *"Amazon Cognito Developer Guide"*. (<https://docs.aws.amazon.com/cognito/>)
2. NestJS Documentation. *"Authentication with JWT & External Providers"*. (<https://docs.nestjs.com/security/authentication>)

Xem bài viết trên Facebook [Tại đây](<https://www.facebook.com/groups/awsstudygroupfcj/permalink/2228021697962790/?rdid=MLFJXbxXfs8sMMKH#>)
