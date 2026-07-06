---
title: "Các bài blogs đã dịch"
date: 2026-07-02
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

###  [Blog 1 - Accessing Amazon S3 Privately from a VPC using a VPC Endpoint](3.1-Blog1/)
Blog này hướng dẫn cách thiết kế mô hình truy cập Amazon S3 riêng tư từ bên trong một VPC mà không cần sử dụng Public IP, Internet Gateway hay NAT Gateway. Bạn sẽ tìm hiểu bối cảnh bài toán khi triển khai các dịch vụ nội bộ (backend, data processing) trong private subnet, cách thức hoạt động của Gateway VPC Endpoint kết hợp với Route table để định tuyến traffic an toàn trong mạng nội bộ AWS. Bài viết cũng nhấn mạnh tư duy bảo mật nhiều lớp (defense-in-depth) thông qua việc kết hợp giữa IAM Role, Endpoint policy và Bucket policy theo nguyên tắc đặc quyền tối thiểu (least privilege) để hệ thống vừa vận hành mượt mà, vừa đảm bảo an toàn thông tin.
###  [Blog 2 - Amazon CloudFront – Tăng tốc phân phối nội dung từ Edge đến Origin](3.2-Blog2/)
Bài blog này giới thiệu cách sử dụng Amazon CloudFront để giải quyết vấn đề tốc độ tải trang không ổn định và độ trễ cao khi người dùng truy cập ứng dụng web từ nhiều khu vực địa lý khác nhau. Bạn sẽ tìm hiểu lý do tại sao mạng phân phối nội dung (CDN) của AWS lại quan trọng trong việc lưu trữ bộ đệm (cache) cho đa dạng nội dung (file tĩnh, video, API), cách nó giúp giảm tải đáng kể cho máy chủ gốc (như Amazon S3 hay EC2), cũng như khả năng tăng cường bảo mật khi kết hợp với AWS WAF. Bài viết cũng hướng dẫn bạn các bước thực hành cơ bản để khởi tạo CloudFront Distribution, cấu hình origin, tùy chỉnh cache behavior và kiểm tra tốc độ tải trang thực tế.
###  [Blog 3 - ...](3.3-Blog3/)
Blog này giới thiệu cách bắt đầu xây dựng data lake trong lĩnh vực y tế bằng cách áp dụng kiến trúc microservices. Bạn sẽ tìm hiểu vì sao data lake quan trọng trong việc lưu trữ và phân tích dữ liệu y tế đa dạng (hồ sơ bệnh án điện tử, dữ liệu xét nghiệm, thiết bị IoT y tế…), cách microservices giúp hệ thống linh hoạt, dễ mở rộng và dễ bảo trì hơn. Bài viết cũng hướng dẫn các bước khởi tạo môi trường, tổ chức pipeline xử lý dữ liệu, và đảm bảo tuân thủ các tiêu chuẩn bảo mật & quyền riêng tư như HIPAA.
