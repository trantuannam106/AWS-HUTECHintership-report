---
title: "Báo cáo Thực hành Tuần 8"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu trọng tâm tuần 8:

- Khám phá bức tranh toàn cảnh về dịch vụ AWS Identity and Access Management (IAM).
- Nhận thức sâu sắc vai trò cốt lõi của IAM trong việc kiểm soát danh tính và phân bổ quyền hạn trên môi trường điện toán đám mây.
- Triển khai các lớp bảo vệ tài khoản vững chắc thông qua cơ chế Xác thực đa yếu tố (MFA).
- Trực tiếp thực hành quy trình quản trị danh tính: khởi tạo IAM User, phân bổ Group, thiết lập Role và gắn Policy.
- Thấm nhuần và áp dụng triệt để nguyên tắc "Đặc quyền tối thiểu" (Principle of Least Privilege) trong bảo mật.
- Nghiên cứu tổng quan về kiến trúc mạng riêng ảo Amazon Virtual Private Cloud (Amazon VPC).
- Bóc tách và phân tích các node mạng cấu thành nên một hệ thống VPC hoàn chỉnh.
- Tự tay xây dựng hạ tầng mạng từ con số không: cấu hình VPC, phân hoạch Subnet, thiết lập bảng định tuyến (Route Table) và mở cổng ra Internet (Internet Gateway).
- Triển khai các chốt chặn an ninh mạng thông qua tường lửa Security Group và Network ACL.
- Củng cố tư duy thiết kế hạ tầng mạng an toàn, biệt lập và tối ưu trên nền tảng AWS.

---

### Kế hoạch hành động chi tiết:

| Thứ | Nội dung công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Đọc tài liệu hướng dẫn bài lab AWS IAM <br> - Đánh giá chức năng của IAM trong hệ sinh thái AWS <br> - Chuẩn bị tài khoản và môi trường thực hành an toàn | 08/06/2026 | 08/06/2026 | https://000009.awsstudygroup.com/ |
| 3 | - Phân biệt bản chất của các thực thể: IAM User, Group, Role và Policy <br> - Thao tác tạo mới người dùng và đưa vào nhóm tương ứng <br> - Cấp phát quyền bằng các chính sách có sẵn (Managed Policy) | 09/06/2026 | 09/06/2026 | https://000009.awsstudygroup.com/ |
| 4 | - Nghiên cứu cơ chế bảo vệ tài khoản bằng xác thực đa yếu tố (MFA) <br> - Kích hoạt MFA cho cả người dùng Root và IAM User <br> - Tìm hiểu sâu các tiêu chuẩn bảo mật trên đám mây | 10/06/2026 | 10/06/2026 | https://000009.awsstudygroup.com/ |
| 5 | - Chuyển sang chủ đề mạng ảo với Amazon VPC <br> - Phân tích sơ đồ kiến trúc và luồng dữ liệu trong mạng VPC <br> - Làm quen với các khái niệm mạng nền tảng | 11/06/2026 | 11/06/2026 | https://000010.awsstudygroup.com/ |
| 6 | - Khởi tạo một Virtual Private Cloud độc lập <br> - Phân hoạch dải mạng thành Public Subnet (vùng công khai) và Private Subnet (vùng kín) <br> - Gắn Internet Gateway và điều hướng traffic qua Route Table | 12/06/2026 | 12/06/2026 | https://000010.awsstudygroup.com/ |
| 7 | - Xây dựng các rào chắn bảo mật: Security Group và Network ACL <br> - Test thử luồng kết nối giữa các instance để xác minh cấu hình <br> - Tinh chỉnh và hoàn tất kiến trúc mạng | 13/06/2026 | 13/06/2026 | https://000010.awsstudygroup.com/ |
| CN | - Rà soát lại toàn bộ danh sách tài nguyên đã deploy <br> - Tiến hành dọn dẹp (Cleanup) môi trường để tránh phát sinh hóa đơn <br> - Tổng hợp kiến thức, ghi chép lỗi và viết báo cáo tuần | 14/06/2026 | 14/06/2026 | https://000009.awsstudygroup.com/ <br> https://000010.awsstudygroup.com/ |

---

### Tổng kết kết quả thu hoạch:

#### Về mặt kiến thức

**Quản trị danh tính AWS IAM**
- Hiểu sâu sắc IAM là trung tâm kiểm soát toàn bộ quyền "ai" được phép làm "gì" trên tài khoản AWS.
- Nắm vững vòng đời tạo lập và quản lý các nhóm thực thể: IAM User, Group, Role và Policy.
- Khắc sâu cốt lõi của nguyên tắc Đặc quyền tối thiểu (Least Privilege) nhằm ngăn chặn rủi ro rò rỉ dữ liệu.
- Phân định rõ ràng ranh giới giữa chính sách do AWS quản lý (AWS Managed Policy) và chính sách tự định nghĩa (Customer Managed Policy).
- Nắm được phương pháp quản lý an toàn thông tin đăng nhập và Access Keys.

**An ninh tài khoản AWS**
- Đánh giá cao vai trò của MFA như một "lớp khiên" thứ hai chống lại các cuộc tấn công chiếm đoạt tài khoản.
- Nắm bắt thao tác đồng bộ thiết bị để cấu hình MFA.
- Thấm nhuần quy tắc vàng trong bảo mật: Tuyệt đối không sử dụng tài khoản Root cho các tác vụ hàng ngày, thay vào đó phải tạo và sử dụng IAM User.

**Kiến trúc mạng Amazon VPC**
- Nắm bắt được cách VPC tạo ra một không gian mạng biệt lập, định nghĩa bằng phần mềm trên cloud.
- Hiểu nguyên lý cấp phát dải IP (CIDR Block) và cách chia nhỏ chúng thành các Subnet phục vụ cho từng mục đích riêng biệt.
- Thấy được tầm quan trọng của Internet Gateway trong việc mở cổng ra Internet và cách Route Table đóng vai trò "người chỉ đường" cho các gói tin.
- Nhận diện sự khác biệt cốt lõi giữa Public Subnet (có đường ra Internet) và Private Subnet (hoàn toàn cách ly).

**Bảo mật hạ tầng mạng**
- Nắm vững cơ chế của Security Group: hoạt động như một tường lửa ảo có trạng thái (stateful) bảo vệ ở cấp độ EC2 Instance.
- Hiểu nguyên lý của Network ACL: đóng vai trò gác cổng không trạng thái (stateless) ở cấp độ mạng Subnet.
- Biết cách thiết lập các bộ quy tắc luồng dữ liệu vào (Inbound) và ra (Outbound) một cách chặt chẽ.
- Hoàn thiện tư duy thiết kế hệ thống mạng an toàn nhiều lớp.

---

#### Về mặt thực hành trực quan

**Module 1 — AWS IAM**
- Đăng nhập thành công vào console của IAM.
- Khởi tạo người dùng (User) và đưa vào các nhóm (Group) tương ứng.
- Đính kèm quyền hạn thông qua Managed Policy.
- Cấu hình thành công IAM Role cho các dịch vụ giả định.
- Kích hoạt thành công bảo mật 2 lớp (MFA).
- Đăng nhập thử bằng IAM User để kiểm thử ranh giới quyền hạn.

**Module 2 — Bảo mật AWS**
- Áp dụng các tiêu chuẩn bảo mật theo khuyến nghị của AWS.
- Vô hiệu hóa hoặc xóa bỏ các Access Key không cần thiết, ứng dụng triệt để Least Privilege.
- Xác minh lại cấu hình an toàn của tài khoản Root.

**Module 3 — Amazon VPC**
- Khởi tạo thành công VPC với dải mạng CIDR tùy chỉnh.
- Thiết lập hoàn chỉnh cấu trúc Public Subnet và Private Subnet.
- Khởi tạo và đính kèm Internet Gateway vào VPC.
- Định tuyến thành công traffic từ Public Subnet ra ngoài Internet thông qua Route Table.

**Module 4 — Cấu hình Security Mạng**
- Tạo và gắn Security Group cho phép các cổng giao tiếp cơ bản (SSH/HTTP).
- Cấu hình Network ACL để chặn/cho phép các dải IP theo kịch bản.
- Thực hiện ping test thành công để xác nhận mạng lưới thông suốt theo đúng thiết kế.
- Xác minh tính hiệu quả của các tường lửa ảo.

**Module 5 — Giải phóng tài nguyên (Cleanup)**
- Kiểm tra chéo toàn bộ VPC, Subnet, IGW, IAM User đã tạo trong bài thực hành.
- Thực hiện xóa và gỡ bỏ an toàn từng thành phần.
- Hoàn tất quá trình dọn dẹp, trả lại môi trường sạch cho tài khoản.

---

### Đánh giá kết quả tuần 8:

- Hoàn thành xuất sắc việc làm chủ công cụ IAM để quản lý quyền truy cập.
- Thao tác mượt mà trong việc tạo lập và phân quyền cho User, Group, Role và Policy.
- Kích hoạt thành công MFA, đảm bảo tài khoản ở mức an toàn cao nhất.
- Tự tay thiết kế, cấu hình và vận hành hoàn chỉnh một hệ thống mạng Amazon VPC cơ bản.
- Phân bổ chính xác các thành phần mạng: Public/Private Subnet, Route Table và IGW.
- Cấu hình thành công mạng lưới bảo vệ đa tầng bằng Security Group và Network ACL.
- Tự tin hơn hẳn trong việc hoạch định và triển khai hạ tầng an toàn trên AWS.

---

### Các trở ngại và thách thức đối mặt:

- Ở giai đoạn đầu, rất dễ nhầm lẫn khái niệm giữa IAM Role (dùng cho dịch vụ/ủy quyền tạm thời) và IAM User (dùng cho con người).
- Lúng túng khi phân biệt sự khác nhau giữa Managed Policy (chính sách độc lập) và Inline Policy (chính sách gắn cứng).
- Khái niệm tường lửa "stateful" (Security Group) và "stateless" (Network ACL) còn hơi trừu tượng và khó nắm bắt.
- Phải chật vật một thời gian để hiểu cách tính toán dải IP CIDR Block và logic định tuyến luồng dữ liệu của Route Table.
- Gặp lỗi Timeout không thể truy cập instance do quên mở port Inbound trong Security Group hoặc điều hướng sai Route Table.

---

### Phương án giải quyết và bài học rút ra:

- Đọc đi đọc lại các ví dụ (use-case) trong tài liệu của AWS để thấu hiểu bản chất sự khác biệt giữa Role và User.
- Trực tiếp thao tác tạo cả hai loại Policy để thấy rõ sự khác biệt về tính linh hoạt và khả năng tái sử dụng.
- Chủ động tự vẽ sơ đồ kiến trúc mạng ra giấy hoặc dùng công cụ (như draw.io) để nhìn rõ luồng đi của gói tin (từ IGW -> Route Table -> NACL -> Subnet -> SG -> Instance).
- Hình thành thói quen đối chiếu kỹ lưỡng từng quy tắc Inbound/Outbound khi tiến hành gỡ lỗi mạng (Troubleshooting).
- Kiên định áp dụng tư duy "chỉ mở những cổng thực sự cần thiết" thay vì chọn cách dễ dàng là mở All Traffic (0.0.0.0/0).
