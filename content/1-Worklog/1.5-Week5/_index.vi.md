---
title: "Worklog Tuần 5"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

- Nắm bắt bức tranh toàn cảnh về phương pháp vận hành ứng dụng FCJ Management kết hợp với sức mạnh của Auto Scaling Group.
- Hiểu rõ cơ chế tự động co giãn tài nguyên (tăng/giảm EC2 Instance) của Amazon EC2 Auto Scaling theo nhịp độ lưu lượng truy cập thực tế.
- Biết cách tích hợp bộ cân bằng tải Application Load Balancer (ALB) với ASG nhằm đảm bảo hệ thống luôn sẵn sàng và chống chịu lỗi xuất sắc.
- Tự tay thiết lập nền tảng mạng và máy chủ cốt lõi, bao gồm: VPC, các Subnet (Public/Private), hệ thống tường lửa Security Group, máy chủ EC2 và cơ sở dữ liệu RDS.
- Cài đặt và vận hành app FCJ Management trên môi trường EC2, thiết lập liên kết thành công với database RDS, đồng thời duy trì ứng dụng qua Node.js và trình quản lý PM2.
- Đóng gói cấu hình EC2 hoàn chỉnh thành AMI, từ đó xây dựng Launch Template làm khuôn mẫu chuẩn để "đúc" ra các instance mới sau này.
- Thiết lập Target Group cùng ALB để làm nhiệm vụ điều phối và chia đều traffic người dùng vào hệ thống các máy chủ EC2.
- Khởi tạo Auto Scaling Group, định mức các thông số giới hạn (Desired, Min, Max Capacity) và kết nối đồng bộ hệ thống này với Load Balancer.
- Trực tiếp kiểm thử và so sánh 4 kịch bản co giãn tài nguyên: Thủ công (Manual), Theo lịch trình (Scheduled), Động (Dynamic) và Theo dự đoán (Predictive).
- Giám sát các chỉ số hiệu năng thông qua nền tảng CloudWatch, phân tích hiệu quả của quá trình scaling và thực hiện dọn dẹp tài nguyên bài bản để tránh chi phí rác.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------------------------------------------------- |
| 2   | - Module 01: Introduction <br> - Module 02.1: Setup Network Infrastructure <br> - **Thực hành:** <br>&emsp;+ Khởi tạo VPC `AutoScaling-Lab` với 3 AZs <br>&emsp;+ Phân chia vùng Public/Private Subnet <br>&emsp;+ Cấu hình Security Group bảo mật cho cả luồng ứng dụng và database | 18/05/2026   | 18/05/2026      | https://000006.awsstudygroup.com/ |
| 3   | - Module 02.2: Launch EC2 Instance <br> - Module 02.3: Launch a Database Instance with RDS <br> - **Thực hành:** <br>&emsp;+ Dựng máy chủ EC2 `FCJ-Management` trên nền Amazon Linux 2023 <br>&emsp;+ Gom nhóm DB Subnet Group và khởi chạy RDS MySQL Instance <br>&emsp;+ Kết nối từ EC2 vào RDS, tạo cấu trúc database, lập bảng `user` | 19/05/2026   | 19/05/2026      | https://000006.awsstudygroup.com/ |
| 4   | - Module 02.4: Setup data for Database <br> - Module 02.5: Deploy Web Server <br> - Module 02.6: Prepare metric for Predictive Scaling <br> - **Thực hành:** <br>&emsp;+ Triển khai môi trường, kéo mã nguồn app FCJ Management từ GitHub <br>&emsp;+ Cài PM2, khởi động app bằng `npm start` và cấu hình tự động bật lại ứng dụng <br>&emsp;+ Chuẩn bị bộ dữ liệu metric ảo và đẩy lên CloudWatch | 20/05/2026   | 20/05/2026      | https://000006.awsstudygroup.com/ |
| 5   | - Module 03: Create Launch Template <br> - Module 04.1: Create Target Group <br> - **Thực hành:** <br>&emsp;+ Chụp bản ghi hệ thống tạo AMI từ máy EC2 đã chạy mượt mà ứng dụng <br>&emsp;+ Sử dụng AMI này để đúc ra Launch Template `FCJ-Management-template` <br>&emsp;+ Lập Target Group `FCJ-Management-TG` chạy giao thức HTTP port `5000` | 21/05/2026   | 21/05/2026      | https://000006.awsstudygroup.com/ |
| 6   | - Module 04.2: Create Load Balancer <br> - Module 05: Test <br> - **Thực hành:** <br>&emsp;+ Dựng Application Load Balancer `FCJ-Management-LB` dạng Internet-facing <br>&emsp;+ Trỏ luồng dữ liệu của Load Balancer thẳng vào Target Group <br>&emsp;+ Dùng địa chỉ DNS của Load Balancer truy cập web và test chức năng CRUD | 22/05/2026   | 22/05/2026      | https://000006.awsstudygroup.com/ |
| 7   | - Module 06: Create Auto Scaling Group <br> - Module 07.1: Test Manual Scaling Solution <br> - Module 07.2: Test Scheduled Scaling Solution <br> - **Thực hành:** <br>&emsp;+ Khởi tạo ASG `FCJ-Management-ASG` dựa trên nền tảng Launch Template <br>&emsp;+ Bấm nút chạy thử kịch bản Manual Scaling (rút số lượng máy) <br>&emsp;+ Lên lịch chạy thử Scheduled Scaling để đón tải giờ cao điểm | 23/05/2026   | 23/05/2026      | https://000006.awsstudygroup.com/ |
| CN  | - Module 07.3: Test Dynamic Scaling Solution <br> - Module 07.4: Read Metrics of Predictive Scaling Solution <br> - Module 08: Cleanup Resources <br> - **Thực hành:** <br>&emsp;+ Viết chính sách Dynamic Scaling tự động đẻ máy dựa trên lượng Request gửi vào ALB <br>&emsp;+ Thiết lập và phân tích Predictive Scaling Policy <br>&emsp;+ Tiến hành xóa sạch hệ thống (ASG, ALB, TG, Template, AMI, EC2, RDS) và soát lại Billing | 24/05/2026   | 24/05/2026      | https://000006.awsstudygroup.com/ |

---

### Kết quả đạt được tuần 5:

#### Kiến thức

**Khái niệm Amazon EC2 Auto Scaling và ALB**
- Giới thiệu EC2 Auto Scaling như một công cụ thông minh giúp tự động bơm thêm hoặc rút bớt máy chủ EC2 hoàn toàn dựa theo áp lực tải thực tế.
- Đảm bảo hệ thống không bao giờ thiếu hụt tài nguyên nhờ cơ chế thay thế máy hỏng, giữ mốc instance mong muốn và giãn nở linh hoạt khi user truy cập đông.
- Nắm được đặc tính hoạt động ở Layer 7 của ALB, cực kỳ tối ưu cho các luồng HTTP/HTTPS giúp nhận request từ người dùng và phân chia đều cho các máy chủ EC2.
- ALB giúp bảo vệ hệ thống bằng cách che giấu IP Private và tránh việc người dùng nhìn thấy hay kết nối trực tiếp vào từng máy EC2 riêng lẻ.

**Cơ chế Target Group, AMI và Launch Template**
- Hiểu Target Group là điểm tập kết của các thiết bị đích, phân loại target theo `Instances`, chạy giao thức `HTTP` với cổng `5000` và tự động chặn luồng gửi đến các node bị lỗi (Unhealthy).
- Khái niệm AMI: Là bản sao chụp (image) chứa nguyên vẹn hệ điều hành, code ứng dụng và mọi thiết lập cấu hình của một máy chủ để phục vụ nhân bản.
- Launch Template đóng vai trò là "bản vẽ kỹ thuật" lưu trữ thông số cốt lõi (AMI, cấu hình máy, Key Pair, mạng, tường lửa) để ASG khởi tạo hàng loạt instance nhất quán.

**Amazon RDS và Kiến trúc mạng phân lớp**
- Ứng dụng mô hình chia lớp: gỡ bỏ hoàn toàn database ra khỏi EC2, chuyển xuống vùng private subnet của RDS nhằm giảm thiểu tối đa rủi ro bảo mật.
- Thiết kế mạng trải dài trên tối thiểu 3 Availability Zones để tăng tính sẵn sàng cao (High Availability) và loại bỏ điểm chết đơn lẻ.
- Thiết lập Security Group khắt khe: SG của Web App mở cổng ứng dụng (`5000`) ra ngoài; trong khi SG của Database chặn đứng mọi kết nối, chỉ chấp nhận port `3306` đi từ chính Security Group của ứng dụng.

**Hệ thống Giám sát và 4 Giải pháp Co giãn Tài nguyên**
- Nhận biết CloudWatch là bảng điều khiển giám sát hiệu năng (CPU Utilization, Request Count) hiển thị số liệu trực quan giúp hỗ trợ các quyết định điều hướng.
- **Manual Scaling:** Điều chỉnh tay mốc mong muốn trực tiếp trên Console, dễ kiểm soát nhưng người quản trị phải túc trực và phản ứng chậm với bão traffic bất ngờ.
- **Scheduled Scaling:** Lập trình sẵn thời khóa biểu tăng dung lượng máy chủ phục vụ các dịch vụ có chu kỳ tải dễ đoán trước (giờ cao điểm, mùa sale).
- **Dynamic Scaling:** Kịch bản co giãn tự động dựa trên tải thực tế, áp dụng mô hình Target Tracking Policy theo sát lượng request gửi vào Target Group.
- **Predictive Scaling:** Tận dụng thuật toán Machine Learning học hỏi dữ liệu quá khứ, giúp chủ động chuẩn bị máy trước một bước khi bão traffic thực sự đổ bộ.

---

#### Thực hành

**Module 2 — Thiết lập hạ tầng Mạng và Triển khai Database:**
- Khởi tạo VPC `AutoScaling-Lab` (CIDR `10.0.0.0/16`) phân chia cấu trúc mạng gồm 3 public subnets và 3 private subnets trải rộng trên 3 AZs khác nhau.
- Setup tường lửa Security Group cho ứng dụng (`FCJ-Management-SG`) mở cổng 22, 80, 443, 5000 và Database SG chỉ chấp nhận port 3306 từ Application SG.
- Dựng cụm DB Subnet Group làm bệ đỡ khởi chạy hệ thống cơ sở dữ liệu RDS MySQL Instance chuẩn Production hỗ trợ Multi-AZ.
- SSH vào máy chủ EC2 mồi, cài đặt Git, MariaDB client, đăng nhập xuyên dải mạng vào RDS endpoint để nạp cấu trúc bảng và dữ liệu mẫu cho bảng `user`.

- 📸 ![Ảnh minh chứng: Hệ thống cơ sở dữ liệu RDS MySQL đã tạo thành công ở trạng thái Available](/aws-intership-report/images/1-Worklog/1.5-Week5/rds-mysql-available.png)

**Module 3 & 4 — Vận hành Web Server, đóng gói AMI và tạo Cân bằng tải:**
- Triển khai môi trường Node.js 20, kéo code từ GitHub, cấu hình file biến môi trường `.env` kết nối trực tiếp với Endpoint của RDS Database.
- Cài đặt trình quản lý PM2 global để duy trì ứng dụng chạy nền ở port 5000, đồng thời chạy lệnh bảo hiểm `pm2 startup` và `pm2 save` để tự khởi động lại app khi máy chủ reboot.
- Chụp ảnh trạng thái EC2 thành `FCJ-Management-AMI`, xây dựng Launch Template `FCJ-Management-template` chuẩn hóa toàn bộ phần cứng và mạng.
- Thiết lập Target Group `FCJ-Management-TG` (Port 5000) và triển khai bộ cân bằng tải Application Load Balancer `FCJ-Management-LB` dạng Internet-facing.

- 📸 ![Ảnh minh chứng: Giao diện ứng dụng FCJ Management load thành công và CRUD mượt mà qua DNS của Load Balancer](/aws-intership-report/images/1-Worklog/1.5-Week5/alb-dns-crud-success.png)

**Module 6 & 7 — Thực hành cấu hình và kiểm thử các giải pháp Auto Scaling:**
- Khởi tạo Auto Scaling Group `FCJ-Management-ASG` gắn vào khuôn Launch Template với quy mô giới hạn (Min: 1, Desired: 1, Max: 3) và bật ELB Health Checks.
- Bắn thử công cụ Load testing cường độ cao vào link DNS của ALB, thực hiện kịch bản **Manual Scaling** hạ Desired về 0 để xem ASG terminate instance tự động.
- Lập lịch **Scheduled Action** tên `Rush hour` múi giờ `Asia/Ho_Chi_Minh` tăng dung lượng máy chủ, kiểm chứng log thực thi chính xác trên tab Activity.
- Viết chính sách **Dynamic Scaling** (Target Tracking) dựa trên chỉ số `ALB Request Count Per Target` ở ngưỡng 500 request để kiểm tra tự co giãn động.
- Dùng cấu hình AWS CLI nạp tệp mock data JSON (CPU và instance metrics) lên CloudWatch, tạo lập **Predictive Scaling Policy** dựa trên custom metric pair và đọc đồ thị dự báo thông minh của AI.

- 📸 ![Ảnh minh chứng: Biểu đồ Load và Capacity thể hiện năng lực dự đoán tải đón đầu tương lai của Predictive Scaling](/aws-intership-report/images/1-Worklog/1.5-Week5/asg-predictive-metrics-chart.png)

**Module 8 — Quy trình dọn dẹp hệ thống (Clean up):**
- Thực hiện tháo dỡ tài nguyên bài bản theo đúng thứ tự: Xóa ASG -> Gỡ bỏ ALB -> Xóa Target Group -> Xóa Launch Template -> Deregister AMI -> Terminate máy EC2 mồi -> Xóa RDS Database và DB Subnet Group để tránh phát sinh chi phí.

---

#### Khó khăn và cách giải quyết

**Khó khăn:**
- Ứng dụng chạy trên cổng `5000` nhưng Application Load Balancer liên tục báo lỗi kết nối và không hiển thị giao diện do người dùng quên mở port này trên Security Group.
- Khi cấu hình RDS MySQL, hệ thống không thể kết nối hoặc phân tách lớp mạng do nhầm lẫn chọn nhầm dải VPC công cộng hoặc DB Subnet Group chứa public subnet.
- Hệ thống Auto Scaling Group báo lỗi đỏ lòm và từ chối khởi tạo máy mới do người dùng cấu hình Launch Template liên kết với một bản chụp AMI đang ở trạng thái `Pending` (chưa chuyển sang `Available`).
- Nguy cơ phát sinh hóa đơn chi phí chạy ngầm rất lớn từ các tài nguyên tính phí cố định theo giờ khổng lồ như Multi-AZ RDS và Application Load Balancer nếu lỡ quên gỡ bỏ sau khi hoàn thành.

**Cách giải quyết:**
- Tiến hành rà soát lại Inbound rules của Security Group, mở rộng cổng TCP 5000 rộng rãi và áp dụng cấu hình bảo mật chỉ cho phép RDS nhận port 3306 từ ID của Application SG.
- Hệ thống hóa sơ đồ luồng đi của dữ liệu ra giấy trước khi làm, gom chính xác các subnet ẩn vào DB Subnet Group và giấu hoàn toàn RDS dưới dải mạng Private Subnet.
- Kiên nhẫn luyện chữ "Nhẫn", chờ đợi thanh tiến độ đóng gói AMI trên EC2 Console chuyển hẳn sang màu xanh lá cây hoàn toàn mới tiến hành nhúng vào Launch Template.
- Thiết lập bảng checklist kiểm tra dọn dẹp rác đám mây kỹ lưỡng từ ngọn xuống gốc (bao gồm cả các tài nguyên ẩn như EBS Snapshot và CloudWatch Logs) và soát lại Billing Dashboard.

---

#### Bài học rút ra

- Thấu hiểu sâu sắc kiến trúc 3 lớp kinh điển (ALB điều phối - EC2 ứng dụng - RDS lưu trữ) giúp hệ thống triệt tiêu điểm chết đơn lẻ và đạt độ bảo mật tối đa.
- Luôn tin dùng quản gia PM2 bọc ngoài ứng dụng Node.js phối hợp lệnh lưu cấu hình hệ thống (`pm2 startup`) để bảo hiểm cho việc server lỡ bị reset đột ngột.
- Nhận thức tầm quan trọng của việc phối hợp Dynamic Scaling hành trình song song với Predictive Scaling để hệ thống vừa phản ứng linh hoạt theo tải nóng vừa chủ động đi trước một bước đón bão traffic.
- Tư duy thiết kế hệ thống Cloud chất lượng luôn đòi hỏi người làm phải đặt cả bài toán tối ưu hóa chi phí (Cost Optimization) và an toàn bảo mật lên bàn cân ngay từ những bước vạch sơ đồ đầu tiên.