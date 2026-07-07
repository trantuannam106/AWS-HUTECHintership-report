---
title: "Worklog Tuần 9"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu trọng tâm tuần 9:

- Khám phá tổng quan về công cụ giao diện dòng lệnh AWS Command Line Interface (AWS CLI).
- Nắm bắt được ưu điểm và vai trò của CLI trong việc tự động hóa, quản trị tài nguyên AWS thay thế cho giao diện web truyền thống.
- Trực tiếp triển khai cài đặt và thiết lập môi trường AWS CLI trên máy tính cá nhân.
- Luyện tập kỹ năng truy vấn thông tin và kiểm soát hệ thống hoàn toàn bằng các câu lệnh terminal.
- Ứng dụng AWS CLI để thao tác với dịch vụ lưu trữ Amazon S3 (quản lý bucket, object).
- Cấu hình và điều hướng dịch vụ thông báo Amazon SNS bằng dòng lệnh.
- Thao tác truy xuất và quản trị thông tin danh tính (IAM) thông qua AWS CLI.
- Định hình cách lấy thông tin và quản lý mạng ảo (Amazon VPC) bằng script.
- Triển khai khởi tạo, kiểm tra và gỡ bỏ máy chủ ảo Amazon EC2 không cần dùng chuột.
- Thực thi các tập lệnh dọn dẹp (Cleanup) sau khi hoàn tất lab để bảo vệ ngân sách AWS.

---

### Kế hoạch hành động chi tiết:

| Thứ | Nội dung công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Nghiên cứu tài liệu giới thiệu về AWS CLI <br> - Phân tích cơ chế gọi API thông qua dòng lệnh <br> - Chuẩn bị máy tính cá nhân và tài khoản thực hành | 15/06/2026 | 15/06/2026 | https://000011.awsstudygroup.com/1-introduction/ |
| 3 | - Tải và cài đặt gói phần mềm AWS CLI <br> - Thực thi `aws configure` để nạp Access Key và Region <br> - Xác thực kết nối tới tài khoản AWS | 16/06/2026 | 16/06/2026 | https://000011.awsstudygroup.com/2-prerequiste/ <br> https://000011.awsstudygroup.com/3-installation/ |
| 4 | - Dùng lệnh truy vấn để kiểm kê tài nguyên hiện có <br> - Làm quen với cấu trúc ngữ pháp cơ bản của CLI | 17/06/2026 | 17/06/2026 | https://000011.awsstudygroup.com/4-check-resource/ |
| 5 | - Vận hành Amazon S3 qua terminal <br> - Chạy script tạo Bucket mới <br> - Thực hiện lệnh copy, upload và download file | 18/06/2026 | 18/06/2026 | https://000011.awsstudygroup.com/5-cli-with-s3/ |
| 6 | - Tương tác với Amazon SNS bằng CLI <br> - Tạo chủ đề (Topic) thông báo <br> - Đăng ký email (Subscribe) và push tin nhắn test | 19/06/2026 | 19/06/2026 | https://000011.awsstudygroup.com/6-cli-with-sns/ |
| 7 | - Truy xuất thông tin IAM (User, Group) qua dòng lệnh <br> - Liệt kê chi tiết hạ tầng mạng (VPC, Subnet, SG) <br> - Dùng lệnh `run-instances` để cấp phát máy chủ EC2 | 20/06/2026 | 20/06/2026 | https://000011.awsstudygroup.com/7-cli-with-iam/ <br> https://000011.awsstudygroup.com/8-cli-with-vpc/ <br> https://000011.awsstudygroup.com/9-create-ec2/ |
| CN | - Rà soát chéo các tài nguyên đã khởi tạo <br> - Chạy lệnh gỡ bỏ (Cleanup) toàn bộ hạ tầng thực hành <br> - Viết báo cáo, đúc kết kinh nghiệm | 21/06/2026 | 21/06/2026 | https://000011.awsstudygroup.com/11-clean-up/ |

---

### Tổng kết kết quả thu hoạch:

#### Về mặt kiến thức

**Bản chất của AWS CLI**
- Hiểu được AWS CLI là một bộ công cụ mã nguồn mở, hoạt động như một lớp vỏ (wrapper) giao tiếp trực tiếp với AWS API.
- Đánh giá được sức mạnh của CLI trong việc giúp kỹ sư DevOps tối ưu hóa thời gian, dễ dàng tự động hóa các tác vụ lặp lại bằng shell script.
- Nắm vững quy trình quản lý thông tin xác thực an toàn trên môi trường local.

**Tiến trình Cài đặt & Cấu hình**
- Thành thạo việc setup file thực thi CLI trên hệ điều hành đang dùng.
- Hiểu rõ ý nghĩa của 4 tham số khi chạy `aws configure`: Access Key ID, Secret Access Key, Default Region và Default Output Format (thường là `json`).
- Biết dùng lệnh `aws sts get-caller-identity` để xác minh xem mình đang thao tác dưới danh tính nào.

**Quản trị Amazon S3 qua dòng lệnh**
- Sử dụng trơn tru họ lệnh `aws s3` để quản trị cấp độ cao (tạo bucket `mb`, đồng bộ `sync`, sao chép `cp`, xóa `rm`).
- Nắm được cách dọn dẹp sạch sẽ một bucket bằng các tham số ép buộc (force).

**Điều hướng Amazon SNS**
- Hiểu cách gọi lệnh để khởi tạo Topic mới và trích xuất Topic ARN.
- Biết cách thêm một Endpoint (như Email) vào Topic và kích hoạt gửi thử một Notification trực tiếp từ terminal.

**Quản trị Danh tính (IAM)**
- Biết cách dùng lệnh `aws iam` để liệt kê danh sách người dùng, hiển thị các nhóm và trích xuất quyền hạn (Policy) nhằm phục vụ công tác rà soát bảo mật (Audit).

**Kiểm soát Mạng (Amazon VPC)**
- Sử dụng hiệu quả lệnh `describe` để lấy thông tin chi tiết về các VPC ID, Subnet ID, và Security Group ID. Đây là bước đệm bắt buộc để khởi tạo EC2 bằng dòng lệnh.

**Triển khai Máy chủ ảo (Amazon EC2)**
- Nắm vững cú pháp phức tạp của lệnh `aws ec2 run-instances`.
- Hiểu rõ cần phải truyền đủ các tham số tối thiểu: Image ID (AMI), Instance Type, Subnet ID và Key Pair thì mới tạo được máy chủ thành công.

---

#### Về mặt thực hành trực quan

**Module 1 — Giới thiệu (Introduction)**
- Nghiên cứu kỹ tài liệu lý thuyết.
- Nắm bắt được logic cấu trúc một câu lệnh CLI chuẩn: `aws <command> <subcommand> [options and parameters]`.

**Module 2 — Cài đặt (Installation)**
- Download và cài đặt thành công AWS CLI v2.
- Nhập thông tin Access Key và cấu hình thành công profile mặc định.
- Chạy lệnh `aws --version` để kiểm tra cài đặt hợp lệ.

**Module 3 — Truy vấn tài nguyên (Check Resource)**
- Thực hành chạy các lệnh `describe` và `list` để quét các dịch vụ đang chạy trên tài khoản.
- Làm quen với cách đọc kết quả trả về dưới định dạng JSON.

**Module 4 — Thao tác với Amazon S3**
- Tạo thành công một Bucket mới toanh bằng lệnh `aws s3 mb`.
- Đẩy một file văn bản test từ máy tính lên cloud và kéo ngược xuống local thành công.
- Dùng lệnh `aws s3 rb` để xóa bucket hoàn tất lab S3.

**Module 5 — Thao tác với Amazon SNS**
- Khởi tạo thành công SNS Topic.
- Chạy lệnh subscribe để liên kết email cá nhân và xác nhận hộp thư.
- Dùng lệnh `publish` bắn một tin nhắn báo động giả lập và nhận được email phản hồi.

**Module 6 — Thao tác với IAM**
- Chạy lệnh `aws iam list-users` xuất danh sách user hiện tại.
- Truy vấn thành công các thông tin Group và Policy gắn liền với User đang thao tác.

**Module 7 — Thao tác với Amazon VPC**
- Thực hành bộ lệnh `aws ec2 describe-vpcs` và `describe-subnets`.
- Sao chép và lưu trữ các giá trị ID của hạ tầng mạng ra file nháp để chuẩn bị cho bước tạo EC2.

**Module 8 — Khởi tạo máy chủ (Create EC2)**
- Viết và thực thi thành công chuỗi lệnh dài khởi tạo EC2 Instance.
- Gọi lệnh kiểm tra trạng thái (Status) xác nhận máy chủ đã chuyển sang "running".
- Tiến hành chạy lệnh `terminate-instances` để tự tay tắt máy chủ từ xa.

**Module 9 — Giải phóng tài nguyên (Cleanup Resources)**
- Rà soát lại qua CLI để đảm bảo không còn EC2 nào đang chạy hay S3 Bucket nào bị bỏ quên.
- Tiết kiệm thời gian dọn dẹp bằng cách gõ lệnh thay vì phải click qua lại giữa các màn hình trên Console.

---

### Đánh giá kết quả tuần 9:

- Bước đầu chuyển đổi thành công tư duy vận hành từ giao diện đồ họa (GUI) sang giao diện dòng lệnh (CLI).
- Cài đặt, cấu hình và xác thực môi trường CLI hoạt động hoàn hảo.
- Vận dụng linh hoạt AWS CLI để xử lý các nhu cầu cơ bản với S3, SNS, IAM, VPC và EC2.
- Cảm nhận rõ rệt tốc độ thao tác được cải thiện đáng kể khi đã quen với cú pháp.
- Nâng cấp kỹ năng nền tảng vững chắc để hướng tới việc tự động hóa hoàn toàn quy trình DevOps trên AWS.

---

### Các trở ngại và thách thức đối mặt:

- Cú pháp lệnh khá dài, đặc biệt là ở module EC2, chỉ cần gõ sai một ký tự hoặc thiếu dấu cách là sẽ bị báo lỗi.
- Gặp khó khăn ban đầu khi phải đọc và bóc tách dữ liệu từ các khối JSON dài loằng ngoằng do CLI trả về.
- Việc thao tác tạo EC2 đòi hỏi tính tuần tự cao: phải dùng CLI lấy cho bằng được Subnet ID, AMI ID và Security Group ID thì mới lắp ghép thành câu lệnh chạy được.
- Đôi khi gặp lỗi `Access Denied` do tài khoản IAM User sử dụng để cấp Access Key không có đủ quyền (Policy) thực thi tác vụ.

---

### Phương án giải quyết và bài học rút ra:

- Thường xuyên đính kèm cờ `--help` vào sau câu lệnh để đọc hướng dẫn tích hợp sẵn, hoặc tra cứu trang AWS CLI Command Reference.
- Viết sẵn các câu lệnh dài ra phần mềm Note (như Notepad, VS Code), rà soát kỹ lưỡng các tham số ID trước khi copy/paste vào Terminal để chạy.
- Hình thành thói quen kiểm tra danh tính bằng lệnh `aws sts get-caller-identity` để chắc chắn mình đang dùng đúng profile có thẩm quyền.
- Để làm quen với JSON, có thể kết hợp thêm công cụ `jq` hoặc tính năng `--query` của AWS CLI để lọc kết quả hiển thị cho gọn gàng dễ nhìn hơn.
