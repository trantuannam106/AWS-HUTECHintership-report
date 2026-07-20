---
title: "Worklog Tuần 6"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu đạt được trong tuần 6:

- Tiếp cận và nắm bắt bức tranh tổng quan về việc kiểm soát chi phí trên nền tảng AWS thông qua AWS Budgets.
- Định hình vai trò chủ chốt của AWS Budgets trong việc giám sát, quản lý và gửi cảnh báo khi có biến động chi phí hoặc mức tiêu thụ tài nguyên.
- Thực hành triển khai nhanh ngân sách bằng cách ứng dụng các Template (mẫu dựng sẵn) có sẵn từ hệ thống.
- Thiết lập Cost Budget nhằm theo dõi sát sao hạn mức chi tiêu dịch vụ AWS theo chu kỳ tháng.
- Khởi tạo Usage Budget phục vụ mục đích kiểm soát tần suất sử dụng tài nguyên, đặc biệt tập trung vào các dịch vụ tính phí dựa trên thời gian vận hành.
- Nghiên cứu cơ chế hoạt động của Reservation Budget để kiểm tra hiệu quả sử dụng của các Reserved Instances (RI).
- Tìm hiểu cách thức vận hành của Savings Plans Budget nhằm đo lường mức độ tối ưu hóa chi phí từ các gói cam kết linh hoạt.
- Cấu hình linh hoạt các ngưỡng báo động (alert thresholds) đi kèm email notification để nhận diện sớm nguy cơ vượt ngân sách.
- Thành thục kỹ năng rà soát lịch sử chi tiêu (Budget history), trạng thái vận hành (Budget health) cùng các cảnh báo đang kích hoạt.
- Thực hiện dọn dẹp (cleanup) các cấu hình thử nghiệm sau khi hoàn thành bài lab để giữ tài khoản gọn gàng.

---

### Kế hoạch hành động chi tiết:

| Thứ | Chi tiết công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Nghiên cứu tài liệu tổng quan bài thực hành Cost Management with AWS Budgets <br> - Đánh giá vai trò quản trị tài chính của dịch vụ <br> - Tiếp cận bảng điều khiển AWS Billing and Cost Management <br> - Làm quen các phân hệ chức năng trên giao diện Budgets | 25/05/2026 | 25/05/2026 | https://000007.awsstudygroup.com/1-create-budget/ |
| 3 | - Ứng dụng tính năng tạo ngân sách nhanh với Template <br> - Thiết lập cấu hình dạng Monthly cost budget <br> - Khai báo các thông tin: Tên ngân sách, hạn mức chi tiêu/tháng và mốc cảnh báo <br> - Xác minh trạng thái hiển thị của ngân sách và truy cập Budget history | 26/05/2026 | 26/05/2026 | https://000007.awsstudygroup.com/1-create-budget/ |
| 4 | - Tự cấu hình Cost Budget nâng cao thông qua chế độ Customize <br> - Lựa chọn phân loại ngân sách chi phí (Cost budget) <br> - Định hình các tham số: Chu kỳ (Period), thời hạn hiệu lực, phương thức tính toán ngân sách và số tiền giới hạn <br> - Khoanh vùng phạm vi áp dụng (Budget scope) cho toàn bộ dịch vụ với Unblended costs | 27/05/2026 | 27/05/2026 | https://000007.awsstudygroup.com/2-cost-budgets/ |
| 5 | - Cài đặt các ngưỡng kích hoạt cảnh báo cho Cost Budget vừa tạo <br> - Chỉ định các hòm thư điện tử đích để nhận thông báo tự động <br> - Kiểm tra, đối chiếu lại toàn bộ thông số thiết lập của Cost Budget <br> - Kích hoạt ngân sách tùy chỉnh và theo dõi trạng thái khởi tạo | 28/05/2026 | 28/05/2026 | https://000007.awsstudygroup.com/2-cost-budgets/ |
| 6 | - Triển khai Usage Budget nhằm quản lý dung lượng và thời gian chạy tài nguyên <br> - Khởi tạo với tùy chọn Usage budget tại mục loại ngân sách <br> - Khai báo nhóm đối tượng theo dõi cụ thể, ví dụ: EC2: ELB - Running Hours <br> - Đặt giới hạn về số giờ vận hành và thiết lập mức báo động đi kèm | 29/05/2026 | 29/05/2026 | https://000007.awsstudygroup.com/3-usage-budget/ |
| 7 | - Khảo sát cơ chế vận hành Reservation Budget dành riêng cho Reserved Instances <br> - Nghiên cứu tính năng Savings Plans Budget để tối ưu hóa cam kết sử dụng <br> - Xem các bài viết hướng dẫn cấu hình RI và Savings Plans Budget trên môi trường doanh nghiệp <br> - Tìm hiểu cách thiết lập các chỉ số bao phủ (coverage) và hiệu suất sử dụng (utilization) | 30/05/2026 | 30/05/2026 | https://000007.awsstudygroup.com/4-reservation-budget/ <br> https://000007.awsstudygroup.com/5-saving-plans-budget/ |
| CN | - Rà soát lại toàn bộ danh mục ngân sách đã cấu hình trong tuần <br> - Đánh giá sức khỏe và biểu đồ biến động của từng budget <br> - Tiến hành hủy (delete) các budget thử nghiệm để làm sạch môi trường học tập <br> - Tổng kết các bài học kinh nghiệm, nhận diện vướng mắc và đề xuất giải pháp xử lý | 31/05/2026 | 31/05/2026 | https://000007.awsstudygroup.com/6-clean-up/ |

---

### Tổng kết kết quả thu hoạch:

#### Về mặt kiến thức

> **Bản chất của AWS Budgets**
> - Là công cụ đắc lực giúp theo dõi dòng tiền, đo lường năng suất sử dụng tài nguyên và kiểm tra hiệu quả của các cam kết giảm giá trên AWS.
> - Hỗ trợ thiết lập linh hoạt các mốc giới hạn theo chu kỳ Ngày, Tháng, Quý hoặc Năm.
> - Cung cấp khả năng gửi email thông báo chủ động ngay khi hệ thống phát hiện chi phí thực tế hoặc dự báo vượt ngưỡng cho phép.
> - Đóng vai trò như một "tấm khiên" bảo vệ ví tiền của người học, ngăn ngừa rủi ro phát sinh hóa đơn lớn ngoài tầm kiểm soát.
> - **Lưu ý cốt lõi:** AWS Budgets chỉ hoạt động như một hệ thống giám sát và phát tín hiệu cảnh báo; dịch vụ này hoàn toàn không tự động tắt hay can thiệp vào trạng thái hoạt động của tài nguyên đang chạy.

**Bảng điều khiển AWS Billing and Cost Management**
- Thành thạo việc tìm kiếm và truy cập trung tâm quản lý tài chính từ AWS Console.
- Hiểu rõ đây là nơi tập trung toàn bộ dữ liệu về hóa đơn, phân tích dòng tiền, thiết lập hạn mức và quản lý các quy tắc cảnh báo chi tiêu.
- Biết cách sử dụng menu điều hướng Budgets để quản lý vòng đời của một ngân sách (Tạo - Sửa - Theo dõi - Xóa).

**Phương thức tạo Ngân sách qua Mẫu (Template)**
- Hiểu được lợi ích của việc dùng mẫu thiết lập sẵn giúp tối giản hóa quy trình và tiết kiệm thời gian.
- Biết cách chọn chế độ "Use a template" cho các nhu cầu cơ bản.
- Áp dụng thành công cấu hình "Monthly cost budget" để nhanh chóng có một bộ khung quản lý chi phí hàng tháng kèm email thông báo.
- Nắm được cách xem lịch sử dữ liệu (Budget history) để phục vụ việc đánh giá xu hướng chi tiêu sau này.

**Cấu hình Ngân sách Chi phí (Cost Budget)**
- Hiểu rõ bản chất Cost Budget là thước đo tập trung vào số tiền (đơn vị USD) phát sinh khi sử dụng dịch vụ.
- Biết cách cấu hình chuyên sâu với chế độ Customize sang dạng Cost budget.
- Phân biệt được hai loại hình áp dụng chu kỳ:
  - *Recurring Budget:* Tự động làm mới và lặp lại khi sang chu kỳ kế tiếp.
  - *Expiring Budget:* Hạn mức có ngày hết hạn cố định và chỉ có hiệu lực một lần duy nhất.
- Phân biệt hai phương pháp đặt hạn mức (Budgeting method):
  - *Fixed:* Đặt một con số cố định, bằng nhau cho mọi tháng.
  - *Planned:* Linh hoạt điều chỉnh số tiền giới hạn tăng hoặc giảm theo từng tháng cụ thể.
- Biết cách định cấu hình phạm vi giám sát tổng thể (All AWS services) và lựa chọn cách tổng hợp chi phí gốc chưa gộp (Unblended costs).

**Cấu hình Ngân sách Sử dụng (Usage Budget)**
- Nhận diện bản chất Usage Budget là theo dõi khối lượng hoặc thời gian tiêu thụ của tài nguyên thay vì nhìn vào số tiền.
- Phân biệt rõ ràng: Cost Budget quản lý áp lực về "Tiền", còn Usage Budget quản lý áp lực về "Tần suất/Thời gian vận hành".
- Biết cách cấu hình bộ lọc theo nhóm loại hình sử dụng (Usage type groups), điển hình là kiểm soát số giờ chạy của Load Balancer (`EC2: ELB - Running Hours`).
- Nhận thức được Usage Budget cực kỳ hữu ích cho việc giám sát các tài nguyên chạy ngầm dễ gây lãng phí theo thời gian như NAT Gateway, EC2, ELB.

**Hiểu biết về Reservation & Savings Plans Budgets**
- Nắm bắt được lý thuyết về Reservation Budget (quản lý RI) và Savings Plans Budget (quản lý gói tiết kiệm compute).
- Hiểu rằng hai loại hình này giúp doanh nghiệp đo lường chỉ số bao phủ (coverage) và mức độ tận dụng (utilization) của các khoản đầu tư trả trước hoặc cam kết dài hạn nhằm tránh lãng phí.
- Ý thức được đây là các tính năng nâng cao, thường áp dụng trong môi trường sản xuất thực tế (Production), không tự ý kích hoạt mua gói thật trong tài khoản cá nhân để tránh phát sinh chi phí cam kết dài hạn.

**Cơ chế Ngưỡng báo động (Alert Threshold) & Giám sát sức khỏe**
- Biết cách thiết lập các nấc cảnh báo dựa trên hai tiêu chí: Chi phí thực tế (Actual) hoặc Chi phí dự báo (Forecasted).
- Thiết lập được các bộ quy tắc đa tầng (ví dụ: phát cảnh báo khi chạm 50%, nhắc nhở nghiêm trọng ở mức 80% và báo động đỏ ở mức 100%).
- Hiểu cách hoạt động của Budget health để nhanh chóng sàng lọc ra các ngân sách nào đang nằm trong vùng an toàn hoặc vùng nguy hiểm.
- Hiểu rõ cơ chế trễ dữ liệu (data latency) của AWS Billing để không hoang mang khi số liệu chưa đồng bộ ngay lập tức.

**Tầm quan trọng của Cleanup**
- Nhận thức được việc dọn dẹp (Cleanup) sau mỗi bài thực hành là một kỹ năng bắt buộc để duy trì hạ tầng sạch và tránh nhiễu thông báo.
- Nắm chắc nguyên lý: Xóa cấu hình AWS Budgets chỉ là hủy bỏ các quy tắc kiểm tra và gửi email, hoàn toàn không gây ảnh hưởng hay làm gián đoạn các dịch vụ đang phân phối ứng dụng trong tài khoản.

---

#### Về mặt thực hành trực quan

**Module 1 — Triển khai nhanh Budget bằng Mẫu**
- Đăng nhập hệ thống AWS Management Console thành công.
- Chuyển hướng đến bảng quản trị AWS Billing and Cost Management và chọn phân hệ Budgets.
- Khởi động trình tạo bằng cách nhấn vào nút `Create a budget`.
- Lựa chọn phương án khởi tạo nhanh: `Use a template (simplified)`.
- Áp dụng mẫu `Monthly cost budget`, điền các thông tin định danh và số tiền hạn mức theo tài liệu lab.
- Chỉ định email đích nhận thông báo và hoàn tất quy trình bằng lệnh `Create budget`.
- Xác minh sự xuất hiện của ngân sách trên danh bạ và mở tab Budget history để khảo sát giao diện lịch sử.


**Module 2 — Thiết lập Cost Budget tùy chỉnh nâng cao**
- Tại mục Budgets, kích hoạt tiến trình tạo mới và chuyển đổi sang chế độ thiết lập nâng cao `Customize`.
- Chỉ định phân loại `Cost budget` và tiến sang bước tiếp theo.
- Khai báo tên định danh cho ngân sách là `Monthly`.
- Cài đặt tần suất là `Monthly`, lựa chọn hình thức lặp lại `Recurring Budget` và áp dụng phương thức đặt hạn mức cố định `Fixed`.
- Nhập số tiền giới hạn cho phép chi tiêu.
- Thu hẹp hoặc mở rộng phạm vi áp dụng tại mục Budget scope với lựa chọn `All AWS services` kết hợp cùng `Unblended costs`.
- Thiết lập quy tắc báo động (`Add an alert threshold`) ở mức mong muốn (ví dụ 80% chi phí thực tế) và điền địa chỉ email quản trị.
- Rà soát lại tổng thể các thông số tại trang Summary trước khi nhấn nút xác nhận khởi tạo hệ thống.


**Module 3 — Khởi tạo Usage Budget theo dõi dung lượng tiêu thụ**
- Thực hiện các bước tạo ngân sách tùy chỉnh (`Customize`) nhưng lựa chọn phân loại là `Usage budget`.
- Đặt tên phân biệt cho Usage Budget.
- Tại khu vực bộ lọc đặc tính tiêu thụ (`Budget against`), chọn `Usage type groups`.
- Tìm kiếm và chỉ định đúng nhóm tài nguyên mong muốn, cụ thể ở đây là `EC2: ELB - Running Hours`.
- Cài đặt thời gian giám sát, chọn kiểu hạn mức thích hợp và điền số giờ tối đa mà dịch vụ Load Balancer được phép chạy trong chu kỳ.
- Chuyển tiếp sang mục cấu hình Alert, thiết lập mức phần trăm cảnh báo dựa trên dung lượng tiêu thụ thực tế và nhập thông tin email nhận thư.
- Hoàn tất khởi tạo và tiến hành rà soát chỉ số `Budget health` để đánh giá mức độ tiêu thụ hiện hành của Load Balancer.


**Module 4 & 5 — Nghiên cứu Reservation & Savings Plans Budget dưới dạng mô phỏng**
- Tiến hành thực hiện các bước khởi tạo tùy chỉnh dành riêng cho `Reservation budget` và `Savings Plans budget`.
- Đặt tên tường minh cho từng loại ngân sách để phục vụ công tác quản lý.
- Cấu hình chỉ số `Coverage threshold` (đối với RI) và `Utilization threshold` (đối với gói tiết kiệm) theo các kịch bản thực tế được hướng dẫn trong tài liệu workshop.
- Điền thông tin email nhận cảnh báo hiệu suất tại phần thiết lập Alert setting.
- Nhấn tạo để trải nghiệm quy trình thiết lập chuẩn doanh nghiệp.
- *Lưu ý quan trọng ghi nhận trong lab:* Do đặc thù tài khoản cá nhân/thực hành, sinh viên thực hiện thao tác ở mức độ tìm hiểu giao diện và cấu hình mô phỏng, không thực hiện mua gói cam kết thật để tránh phát sinh hóa đơn tài chính ngoài ý muốn.


**Module 6 — Giải phóng môi trường thực hành (Clean Up)**
- Truy cập vào danh mục quản lý tập trung các Budgets trong AWS Billing.
- Tiến hành tích chọn các ngân sách thử nghiệm đã khởi tạo xuyên suốt bài thực hành.
- Mở menu điều hướng `Actions` nằm ở góc trên bên phải và chọn lệnh `Delete`.
- Xác nhận lại quyết định xóa tại cửa sổ thông báo pop-up để hệ thống gỡ bỏ hoàn toàn cấu hình.
- Thực hiện tương tự cho đến khi danh sách trở lại trạng thái ban đầu, đảm bảo không còn các quy tắc gửi mail thừa thãi.


---

### Các trở ngại và thách thức đối mặt:

- Bảng điều khiển Billing and Cost Management tích hợp rất nhiều công cụ phân tích (Bills, Cost Explorer, Budgets, v.v.) khiến quá trình tiếp cận ban đầu dễ bị nhầm lẫn giữa các tính năng.
- Ranh giới lý thuyết giữa Cost Budget và Usage Budget đôi khi dễ bị đánh tráo nếu không bám sát vào đơn vị đo lường (Tiền USD và Sản lượng/Giờ chạy).
- Danh mục `Usage type groups` có bộ lọc rất rộng, yêu cầu phải đọc kỹ và tìm kiếm chính xác từ khóa `EC2: ELB - Running Hours` để không chọn nhầm sang các dịch vụ khác.
- Do cơ chế cập nhật không đồng thời (Data Latency) của AWS, các chỉ số tiền và biểu đồ lịch sử không hiển thị thay đổi ngay lập tức sau khi tạo, gây khó khăn cho việc kiểm tra kết quả tức thời.
- Các kiến thức nâng cao liên quan đến RI và Savings Plans tương đối trừu tượng do sinh viên chưa có cơ hội va chạm với các bài toán tối ưu chi phí quy mô lớn trên thực tế.
- Nếu không kiểm tra kỹ cú pháp email hoặc quên không xác thực, hệ thống cảnh báo có thể không gửi được thư về hộp inbox như mong đợi.

---

### Phương án giải quyết và bài học rút ra:

- Luôn duy trì thói quen đọc kỹ từng chỉ dẫn kỹ thuật trong tài liệu hướng dẫn trước khi bấm chọn trên giao diện AWS Console.
- Hệ thống hóa lại bản chất các công cụ bằng sơ đồ tư duy ngắn gọn:
  - *Cost Budget:* Quản lý túi tiền.
  - *Usage Budget:* Quản lý giờ chạy/dung lượng tài nguyên.
  - *Reservation / Savings Plans Budget:* Giám sát hiệu quả các gói cam kết trả trước.
- Đặt các ngưỡng thông báo thông minh (từ thấp đến cao) để tạo ra các mốc đệm, giúp bản thân có thời gian can thiệp xử lý tài nguyên trước khi chạm mức 100%.
- Tuyệt đối tuân thủ nguyên tắc an toàn tài khoản: Không bấm mua hoặc kích hoạt bất kỳ gói cam kết RI/Savings Plans thật nào khi đang làm bài lab học tập.
- Thực hiện dọn dẹp triệt để các cấu hình thử nghiệm ngay khi kết thúc bài lab để giữ cho môi trường học tập luôn chuẩn hóa.
- Kết hợp việc dùng AWS Budgets với việc rà soát thủ công Billing Dashboard định kỳ sau mỗi buổi học để sớm phát hiện các chi phí ẩn.

---

### Kế hoạch và lộ trình cho tuần tiếp theo:

- Tiếp tục đào sâu các phân hệ bổ trợ trong hệ sinh thái AWS Billing and Cost Management.
- Chuyển dịch trọng tâm sang nghiên cứu **AWS Cost Explorer** để học cách bóc tách, phân tích sâu chi phí theo các chiều tag, dịch vụ và thời gian.
- Tìm hiểu cách thức theo dõi các hạn mức miễn phí thông qua **AWS Free Tier Dashboard**.
- Tiếp cận giải pháp phát hiện chi phí bất thường bằng công nghệ học máy với **AWS Cost Anomaly Detection**.
- Tìm hiểu mô hình quản lý tập trung tài chính cho chuỗi nhiều tài khoản thông qua dịch vụ **AWS Organizations**.
- Duy trì và rèn luyện thói quen kiểm tra Billing Dashboard định kỳ để nâng cao tư duy tối ưu hóa chi phí (FinOps) trên đám mây.
