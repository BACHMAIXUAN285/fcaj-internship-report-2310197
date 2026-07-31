---
title : "Các bước Thực hiện"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2.1. </b> "
---

#### Bước 1: Khởi tạo User Pool (Kho lưu trữ người dùng)

1. Truy cập **AWS Management Console**, tìm kiếm và chọn dịch vụ **Amazon Cognito**.
2. Bấm **Create user pool** và cấu hình các thuộc tính:
   * **User pool name**: `healthcare`
   * **Sign-in options**: Tích chọn phương thức đăng nhập chính bằng **Email**.
   * **Password policy**: Thiết lập chính sách mật khẩu tuân thủ tiêu chuẩn an toàn dữ liệu y tế (Tối thiểu 8 ký tự, bắt buộc chứa chữ hoa, chữ thường, chữ số và ký tự đặc biệt).

![Figure 3](/images/5-Workshop/5.2.1-Step-to-do/Cognito.png)

##### Phân tích Kỹ thuật & Bảo mật (JWT & RSA Encryption):

* **Xác nhận hạ tầng thực tế**: Thông tin `Estimated number of users: 9` minh chứng hệ thống Auth đã vận hành thực tế, tiếp nhận các lượt đăng ký/đăng nhập thử nghiệm thành công.
* **Chuẩn mã hóa bất đối xứng**: Đường link `Token signing key URL` (**JWKS Endpoint**) cung cấp các Public Keys cho phép Backend NestJS giải mã chữ ký JWT Token (RSA) một cách hoàn toàn tự động. Nhờ đó, Backend không cần lưu trữ bất kỳ mật khẩu nào của người dùng.

#### Bước 2: Phân quyền đa vai trò (RBAC - Role-Based Access Control)

1. Truy cập vào User Pool `healthcare` --> chọn tab **Group management**.
2. Khởi tạo 3 nhóm người dùng đại diện cho các vai trò trong hệ thống:
   * `Admin`: Quản trị viên hệ thống & Lễ tân.
   * `Doctor`: Bác sĩ khám chữa bệnh.
   * `Patient`: Bệnh nhân đặt lịch & xem hồ sơ.
3. Khi người dùng đăng nhập, Cognito tự động nhúng thông tin nhóm vào Claim `cognito:groups` bên trong **JWT Access Token**. Backend NestJS dựa vào trường này để phân quyền truy cập API bằng Guard.

![Figure 4](/images/5-Workshop/5.2.1-Step-to-do/Cognito.png)

##### Phân tích Chuyên sâu về An toàn Dữ liệu Y tế (Data Privacy):

* **Ẩn danh hóa bằng UUID (Anonymization)**: Ở cột `User name`, hệ thống cấp phát chuỗi định danh duy nhất (UUID - ví dụ: `395ee448...`) thay vì dùng Email hay tên thật. Các bảng dữ liệu bệnh án dưới Database chỉ lưu UUID này, đảm bảo quyền riêng tư tuyệt đối cho bệnh nhân.
* **Tự động hóa luồng Email Verification**: Cột `Confirmation status` thể hiện rõ hai trạng thái `Confirmed` và `Unconfirmed`, chứng minh hệ thống đã tích hợp thành công luồng tự động gửi OTP/Link xác thực qua Email ngay khi có tài khoản mới đăng ký.
* **Quản lý tập trung đa vai trò**: Việc xuất hiện tài khoản quản trị (`superadminbkmed@gmail.com`) cùng các email người dùng thông thường minh chứng hạ tầng Cognito đang điều phối trơn tru luồng RBAC cho toàn bộ hệ thống.

#### Bước 3: Cấu hình Ứng dụng khách (App Client cho Next.js)

1. Tại mục **App integration**, chọn **Create app client**.
2. Đặt tên App Client (ví dụ: `healthcare-nextjs-web`).
3. Cấu hình các tham số OAuth 2.0:
   * **Grant types**: Chọn `Authorization code grant` hoặc `Implicit grant`.
   * **Disable Client Secret**: Bắt buộc vô hiệu hóa **Client Secret**. Vì Frontend Next.js chạy trên trình duyệt (Single Page App - SPA), việc không dùng Client Secret sẽ loại bỏ hoàn toàn rủi ro lộ khóa bí mật ở client.

#### Bước 4: Tích hợp Giải mã JWT vào Backend (NestJS)

1. Trích xuất **JWKS Endpoint** từ trang tổng quan User Pool:  
   ```bash
   https://cognito-idp.<region>.amazonaws.com/<user-pool-id>/.well-known/jwks.json
   ```
2. Trong dự án NestJS, cấu hình `JwtStrategy` (sử dụng thư viện `jwks-rsa`):
   ```bash
   // Minh họa cấu hình JwtStrategy kết nối JWKS của Cognito
   passportJwt.Strategy({
       jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
       secretOrKeyProvider: jwksRsa.passportJwtSecret({
           jwksUri: `https://cognito-idp.ap-southeast-2.amazonaws.com/ap-southeast-2_xxxxxx/.well-known/jwks.json`,
       }),
       algorithms: ['RS256'],
   });
   ```
3. Mỗi khi User gửi Request đính kèm Bearer Token, NestJS tự động tải Public Key từ Cognito về để verify Token mà không tốn chi phí gọi API ngược lại AWS.

#### Tóm tắt Kết quả Triển khai
Sau khi hoàn tất 4 bước triển khai AWS Cognito:
1. **Xây dựng hệ thống Auth chuẩn Enterprise**: Đăng nhập an toàn qua Email, tự động xác thực OTP và bảo mật mật khẩu tuân thủ tiêu chuẩn y tế.
2. **Triển khai phân quyền đa vai trò (RBAC)**: Định danh người dùng qua **UUID ẩn danh** và cấp quyền bằng `cognito:groups` đính kèm trong JWT.
3. **Tối ưu hóa hiệu năng & Bảo mật Backend**: Backend NestJS giải mã Token bằng thuật toán bất đối xứng RSA (qua JWKS) trực tiếp trên bộ nhớ máy chủ, vừa tăng tốc độ xử lý Request vừa đảm bảo an toàn tối đa.
