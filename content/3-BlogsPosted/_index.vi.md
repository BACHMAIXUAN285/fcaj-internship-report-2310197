---
title: "Các bài blogs đã đăng"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Tại đây sẽ là phần liệt kê, giới thiệu các blogs đã đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj):

###  [Blog 1 - AWS COGNITO LÀ GÌ? TẠI SAO ĐÂY LÀ "MẢNH GHÉP" KHÔNG THỂ THIẾU CHO HỆ THỐNG Y TẾ SỐ?](3.1-Blog1/)
Blog này giải thích lý do lựa chọn AWS Cognito thay vì tự phát triển hệ thống xác thực (Auth) từ đầu cho nền tảng Smart Healthcare Platform. Bài viết phân tích sâu các thách thức về phân quyền đa vai trò (RBAC cho Bệnh nhân, Bác sĩ, Lễ tân), quy trình quản lý định danh an toàn với JWT Token, cũng như cách AWS Cognito giúp tối ưu thời gian phát triển và tiết kiệm chi phí vận hành nhờ hạn mức miễn phí 50,000 MAU.

###  [Blog 2 - AWS BEDROCK KNOWLEDGE BASES LÀ GÌ? TẠI SAO ĐÂY LÀ "MẢNH GHÉP" HOÀN HẢO CHO KIẾN TRÚC SERVERLESS RAG?](3.2-Blog2/)
Blog này chia sẻ trải nghiệm thực tế trong việc giải quyết bài toán Data Pipeline cho hệ thống Trợ lý AI Y tế bằng AWS Bedrock Knowledge Bases. Bài viết phân tích lý do thay thế các Vector Database tự host cồng kềnh bằng giải pháp Fully-Managed Serverless. Qua đó, dịch vụ tự động hóa toàn bộ quy trình Chunking, Embedding và Indexing, kết hợp linh hoạt với Amazon S3 và LangChain để giúp kỹ sư tập trung tối ưu logic lâm sàng thay vì vận hành hạ tầng.

###  [Blog 3 - AWS S3 BUCKET: "MẢNH GHÉP" LƯU TRỮ CHUẨN CLOUD-NATIVE CHO HỆ THỐNG Y TẾ SỐ](3.3-Blog3/)
Blog này giải thích lý do lựa chọn Amazon S3 thay vì tự lưu trữ tệp tin trên máy chủ Backend cho nền tảng Y tế số. Bài viết phân tích chi tiết cách loại bỏ rủi ro bảo mật và thói quen lưu file thủ công bằng việc ứng dụng Private S3 Bucket cùng S3 Presigned URL để bảo mật hồ sơ bác sĩ, tách biệt file trọng số AI (.pt), và tự động xuất - lưu trữ báo cáo y tế PDF. Qua đó, dịch vụ giúp đưa Backend về trạng thái Stateless nhẹ nhàng, nâng cao tính khả mở và tối ưu chi phí vận hành.
