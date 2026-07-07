---
title: "Báo cáo Công việc Tuần 7"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu trọng tâm tuần 7:

- Nắm bắt bức tranh toàn cảnh về dịch vụ giám sát Amazon CloudWatch.
- Đánh giá tầm quan trọng của CloudWatch trong công tác quản lý, theo dõi "sức khỏe" tài nguyên và ứng dụng trên môi trường AWS.
- Trực tiếp thao tác với CloudWatch Metrics nhằm đo lường và đánh giá hiệu năng của hệ thống.
- Làm quen với các cú pháp nâng cao: Search Expressions (tìm kiếm), Math Expressions (tính toán số liệu) và Dynamic Labels (nhãn động).
- Phân tích nhật ký hoạt động thông qua CloudWatch Logs và bộ công cụ truy vấn chuyên sâu CloudWatch Logs Insights.
- Thiết lập bộ lọc (Metric Filters) để trích xuất số liệu trực tiếp từ dữ liệu log.
- Cài đặt hệ thống cảnh báo tự động (CloudWatch Alarms) để phát hiện sớm và xử lý sự cố.
- Thiết kế bảng điều khiển (CloudWatch Dashboards) nhằm tập trung hóa và trực quan hóa các chỉ số giám sát.
- Thực hiện quy trình dọn dẹp (Cleanup) để giải phóng tài nguyên sau bài lab.
- Trau dồi và nâng cấp kỹ năng vận hành, giám sát hạ tầng đám mây.

---

### Kế hoạch hành động chi tiết:

| Thứ | Chi tiết công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Nghiên cứu tài liệu tổng quan bài lab Amazon CloudWatch <br> - Phân tích vai trò và kiến trúc giám sát của CloudWatch <br> - Cấu hình và chuẩn bị môi trường tài khoản AWS | 01/06/2026 | 01/06/2026 | https://000008.awsstudygroup.com/1-introduction/ |
| 3 | - Khám phá chức năng của CloudWatch Metrics <br> - Đọc, phân tích các chỉ số tài nguyên hiện có <br> - Thực hành lệnh lọc dữ liệu với Search Expressions | 02/06/2026 | 02/06/2026 | https://000008.awsstudygroup.com/3-cloud-watch-metric/ |
| 4 | - Ứng dụng Math Expressions để thực hiện phép toán trên số liệu <br> - Triển khai Dynamic Labels để biểu đồ hiển thị rõ ràng hơn <br> - Tinh chỉnh đồ thị trực quan cho Metrics | 03/06/2026 | 03/06/2026 | https://000008.awsstudygroup.com/3-cloud-watch-metric/ |
| 5 | - Vận hành hệ thống lưu trữ CloudWatch Logs <br> - Viết cú pháp truy vấn nhật ký thông qua Logs Insights <br> - Cấu hình Metric Filters để đếm số lượng lỗi từ Logs | 04/06/2026 | 04/06/2026 | https://000008.awsstudygroup.com/4-cloud-watch-logs/ |
| 6 | - Khởi tạo các bộ quy tắc CloudWatch Alarms <br> - Tích hợp dịch vụ Amazon SNS để nhận thông báo tự động (qua email) <br> - Mô phỏng sự cố để kiểm tra khả năng kích hoạt của Alarms | 05/06/2026 | 05/06/2026 | https://000008.awsstudygroup.com/5-cloud-watch-alarm/ |
| 7 | - Xây dựng giao diện CloudWatch Dashboards chuyên nghiệp <br> - Lồng ghép các biểu đồ Metrics và trạng thái Alarms vào chung một khung nhìn <br> - Quan sát luồng dữ liệu biến động theo thời gian thực | 06/06/2026 | 06/06/2026 | https://000008.awsstudygroup.com/6-cloud-watch-dashboard/ |
| CN | - Rà soát lại toàn bộ hệ thống đã cấu hình <br> - Tiến hành xóa bỏ tài nguyên (Cleanup) để tránh rủi ro chi phí <br> - Đúc kết kinh nghiệm và hoàn thành báo cáo tuần | 07/06/2026 | 07/06/2026 | https://000008.awsstudygroup.com/7-clean-up/ |

---

### Tổng kết kết quả thu hoạch:

#### Về mặt kiến thức

**Bản chất của Amazon CloudWatch**
- Định hình CloudWatch như một "trung tâm điều khiển" giúp quan sát toàn diện hệ sinh thái AWS.
- Nắm rõ luồng thu thập dữ liệu: từ việc lấy thông số (Metrics) đến việc lưu trữ nhật ký (Logs).
- Hiểu sâu sắc lý do vì sao việc giám sát chủ động lại là yếu tố sống còn để đảm bảo uptime cho ứng dụng.

**Hệ thống CloudWatch Metrics**
- Thuần thục việc tìm kiếm và bóc tách các chỉ số đo lường hiệu suất.
- Biết cách dùng công cụ Search Expressions để rà soát lượng lớn dữ liệu một cách nhanh chóng.
- Ứng dụng thành công Math Expressions để tổng hợp hoặc tính toán các chỉ số phái sinh.
- Hiểu cách dán nhãn thông minh (Dynamic Labels) để đồ thị tự động cập nhật tên hiển thị, thân thiện với người dùng.

**Quản lý CloudWatch Logs**
- Hiểu cơ chế phân nhóm và duy trì vòng đời của log (Log Groups và Log Streams).
- Biết cách sử dụng cú pháp truy vấn đặc thù trong Logs Insights để bới tìm nguyên nhân gốc rễ (root cause) của lỗi.
- Nắm được kỹ thuật dùng Metric Filters để biến các chuỗi text vô tri trong log thành các con số có thể báo động được (ví dụ: đếm từ khóa "ERROR").

**Cơ chế CloudWatch Alarms**
- Hiểu rõ 3 trạng thái của một cảnh báo: *OK, ALARM, INSUFFICIENT_DATA*.
- Nắm vững cách thiết lập các ngưỡng kích hoạt (threshold) dựa trên dữ liệu tĩnh hoặc dữ liệu bất thường (Anomaly Detection).
- Nắm bắt quy trình kết nối với Amazon SNS để định tuyến thông báo đến đội ngũ vận hành.

**Trực quan hóa với CloudWatch Dashboards**
- Tư duy được cách sắp xếp các Widget trên không gian Dashboard sao cho hợp lý.
- Hiểu rằng việc gom nhóm Metrics và Alarms vào một nơi giúp tiết kiệm thời gian chẩn đoán lỗi hệ thống.

---

#### Về mặt thực hành trực quan

**Module 1 — Giới thiệu (Introduction)**
- Truy cập thành công vào bảng điều khiển Amazon CloudWatch.
- Làm quen với menu điều hướng và kiểm tra các điều kiện tiên quyết của bài lab.
- Khởi động môi trường thử nghiệm tài nguyên an toàn.

**Module 2 — Triển khai CloudWatch Metrics**
- Điều hướng đến giao diện Metrics của các dịch vụ AWS đang chạy.
- Viết và thực thi thành công các cú pháp Search Expressions.
- Áp dụng các hàm toán học (Math Expressions) lên đồ thị đường.
- Cấu hình và kiểm tra sự thay đổi tên hiển thị qua Dynamic Labels.

**Module 3 — Thao tác CloudWatch Logs**
- Khởi tạo thành công Log Groups mới.
- Đổ dữ liệu mẫu vào và tiến hành chạy lệnh lọc bằng Logs Insights.
- Thiết lập Metric Filters nhận diện từ khóa cụ thể và đối chiếu kết quả.

**Module 4 — Cấu hình CloudWatch Alarms**
- Tạo mới một quy tắc cảnh báo dựa trên chỉ số CPU hoặc số lượng lỗi đã lọc.
- Thiết lập chủ đề SNS (SNS Topic) và thêm email đăng ký nhận tin.
- Kích hoạt sự kiện để ép chỉ số vượt ngưỡng và xác nhận email báo động đã được gửi về hòm thư.

**Module 5 — Thiết kế CloudWatch Dashboards**
- Tạo một bảng không gian làm việc mới (Dashboard).
- Bổ sung các Widget dạng biểu đồ cột, biểu đồ đường đại diện cho Metrics.
- Gắn Widget trạng thái của Alarms để theo dõi tình trạng báo đỏ/báo xanh.

**Module 6 — Giải phóng tài nguyên (Cleanup Resources)**
- Truy cập vào từng phân hệ: Alarms, Dashboards, Logs để dọn dẹp các mục đã tạo.
- Đảm bảo môi trường trả về trạng thái sạch sẽ.
- Hoàn tất rà soát không còn dịch vụ nào chạy ngầm nhằm hạn chế hóa đơn phát sinh.

---

### Các trở ngại và thách thức đối mặt:

- Bị ngợp ở giai đoạn đầu do chưa phân định rạch ròi chức năng giữa Metrics (số liệu đo lường), Logs (nhật ký văn bản) và Metric Filters (cầu nối giữa hai bên).
- Cú pháp của Search Expressions và Math Expressions khá đặc thù, dễ viết sai cấu trúc nếu không xem kỹ tài liệu.
- Ngôn ngữ truy vấn của Logs Insights khá giống SQL nhưng có nhiều điểm khác biệt, tốn thời gian để làm quen các hàm như `stats`, `parse`.
- Quá trình cấu hình luồng thông báo SNS đôi khi bị gián đoạn do quên bấm xác nhận đăng ký (Confirm subscription) trong email.

---

### Phương án giải quyết và bài học rút ra:

- Nghiên cứu sâu hơn vào các tài liệu chuẩn (AWS Documentation) song song với việc đọc hướng dẫn lab.
- Ghi chép lại các mẫu cú pháp truy vấn (Queries) để tái sử dụng cho các lần cấu hình sau.
- Luôn kiểm tra kỹ hộp thư đến và thư mục spam để đảm bảo SNS endpoint đã được xác minh trước khi tiến hành test luồng Alarms.
- Chủ động tìm kiếm các video thực tế hoặc bài viết Use-case của AWS để hiểu rõ logic chuyển đổi dữ liệu của nền tảng.
