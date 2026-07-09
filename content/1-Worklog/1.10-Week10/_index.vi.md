---
title: "Worklog Tuần 10"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

Trong phân công nhóm InboxIQ, tôi phụ trách ba mảng thường bị xem là "phụ" nhưng quyết định chất lượng sản phẩm cuối cùng: tài liệu (báo cáo Hugo mà cả nhóm sẽ nộp), kiểm thử (người dùng đầu tiên và khó tính nhất của mọi tính năng), và giám sát chi phí (đảm bảo cả dự án nằm trong Free Tier). Tuần này, trong khi các bạn dựng hệ thống, tôi dựng thứ song hành với hệ thống: nơi lưu giữ mọi quyết định, mọi bài học, mọi con số — để đến ngày nộp không ai phải ngồi nhớ lại "hồi đó mình làm gì".

- Khởi tạo repo báo cáo Hugo với theme workshop, cấu trúc chương mục song ngữ, quy ước đặt tên ảnh.
- Vẽ sơ đồ kiến trúc 5 layer chính thức trên draw.io từ bản phác thảo của buổi họp nhóm, đánh số từng luồng xử lý.
- Thiết lập quy trình ghi nhận: mọi quyết định thiết kế và sự cố của các thành viên đều được ghi lại trong tuần, không để dồn cuối kỳ.
- Kiểm thử phần backend đầu tiên: luồng Producer → SQS → Worker với message giả.
- Thiết lập nền nếp giám sát chi phí: Billing Dashboard, ước tính Free Tier cho từng dịch vụ đã chốt trong kiến trúc.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Họp nhóm chốt kiến trúc; nhận mảng tài liệu/kiểm thử/chi phí. <br> - Ghi biên bản buổi họp: phân công, ranh giới trách nhiệm, các "hợp đồng giao tiếp" giữa các phần (format message, endpoint) — tài liệu gốc cho mọi tranh luận sau này. | 22/06/2026 | 22/06/2026 | Nội bộ nhóm |
| 3 | - Khởi tạo repo Hugo với theme workshop: cấu trúc `content/` theo chương, hỗ trợ song ngữ (`.vi.md`/`.en.md`), thư mục `static/images/` theo quy ước từng mục. <br> - Chạy thử `hugo server`, xác nhận render đúng shortcode (`notice`, `children`). | 23/06/2026 | 23/06/2026 | https://gohugo.io/documentation/ |
| 4 | - Vẽ sơ đồ kiến trúc chính thức trên draw.io từ bản phác của bạn backend: 5 layer, đánh số 14 luồng xử lý, chú thích phân loại nét vẽ (luồng chính, retry, tuỳ chọn, observability). <br> - Lấy ý kiến cả nhóm, chỉnh sửa 2 vòng trước khi chốt. | 24/06/2026 | 24/06/2026 | https://app.diagrams.net |
| 5 | - Viết khung các chương báo cáo: giới thiệu, kiến trúc, các bước triển khai (đặt chỗ cho từng mảng), kiểm thử, chi phí. <br> - Thống nhất quy ước với cả nhóm: mỗi sự cố kỹ thuật phải có "hiện tượng → nguyên nhân → cách xử lý → bài học" để tôi viết lại thành tài liệu. | 25/06/2026 | 25/06/2026 | Nội bộ nhóm |
| 6 | - Lập bảng ước tính Free Tier cho từng dịch vụ trong kiến trúc: Lambda (1 triệu request/tháng), DynamoDB (25GB on-demand), SQS (1 triệu request), API Gateway, Secrets Manager (tính phí theo secret + lượt gọi). <br> - Xác định trước các "điểm nóng chi phí" cần theo dõi: lượt gọi OpenAI (ngoài AWS), Secrets Manager API calls. | 26/06/2026 | 26/06/2026 | https://aws.amazon.com/free/ |
| 7 | - Kiểm thử backend lần đầu cùng bạn backend: gửi message giả vào SQS, xác nhận Worker nhận và ghi kết quả vào DynamoDB đúng cấu trúc. <br> - Viết test case đầu tiên dạng checklist thủ công (chưa tự động hoá): các bước, dữ liệu vào, kết quả mong đợi. | 27/06/2026 | 27/06/2026 | Nội bộ dự án |
| CN | - Kiểm tra Billing Dashboard cuối tuần đầu: xác nhận chi phí bằng 0 (mọi dịch vụ trong Free Tier). <br> - Viết báo cáo tổng kết tuần và cập nhật tài liệu từ ghi nhận của 3 thành viên còn lại. | 28/06/2026 | 28/06/2026 | Nội bộ dự án InboxIQ |

---

### Kết quả đạt được tuần 10:

#### 1. Repo Hugo — nền móng của sản phẩm nộp cuối cùng

Sản phẩm nhóm nộp không phải là code mà là **báo cáo quá trình** — nên repo Hugo chính là "sản phẩm chính" của mảng tôi phụ trách. Cấu trúc được dựng chuẩn ngay từ đầu: chương mục theo `weight`, song ngữ bằng hậu tố `.vi.md`/`.en.md`, ảnh minh hoạ theo quy ước thư mục `/images/<chương>/<mục>/` để về sau ai chèn ảnh cũng nhất quán. Kinh nghiệm rút ra ngay tuần đầu: dựng quy ước sớm rẻ hơn nhiều so với dọn dẹp muộn — một repo tài liệu lộn xộn ở tuần cuối là ác mộng không thua gì code lộn xộn.

#### 2. Sơ đồ kiến trúc — từ bản phác lên "ngôn ngữ chung"

Bản phác trên giấy của buổi họp nhóm được chuyển thành sơ đồ draw.io chính thức: 5 layer (User, Auth, API, Compute, Async Workflow, Storage, Observability), 14 luồng xử lý đánh số, và một bảng chú giải phân loại nét vẽ — luồng chính nét liền, retry nét đứt đỏ, tuỳ chọn nét cam, observability nét xám. Chi tiết tưởng hình thức nhưng có tác dụng thật: khi bạn backend giải thích luồng whoami hay bạn Flutter hỏi về đường đi của kết quả push, cả nhóm chỉ vào cùng một con số trên cùng một sơ đồ thay vì mô tả bằng lời mỗi người một kiểu.

Một nguyên tắc được chốt khi vẽ: sơ đồ chỉ chứa những gì thuộc **luồng chạy của ứng dụng** — các tài nguyên phục vụ deploy (như S3 bucket chứa artifact của SAM) không vẽ vào, dù chúng tồn tại thật trong tài khoản. Ranh giới "kiến trúc ứng dụng" và "hạ tầng công cụ" được ghi rõ để tránh tranh luận lại sau này.

#### 3. Quy ước "ghi ngay trong tuần" — chống lại trí nhớ con người

Bài học từ các dự án môn học trước: đến tuần cuối, không ai nhớ nổi vì sao mình chọn phương án A thay vì B ở tuần đầu. Quy ước được cả nhóm đồng ý: mỗi sự cố hoặc quyết định thiết kế phải ghi lại theo khung 4 phần (hiện tượng → nguyên nhân → cách xử lý → bài học) ngay trong tuần xảy ra, dù chỉ vài dòng thô — tôi chịu trách nhiệm biên tập lại thành tài liệu hoàn chỉnh. Đây là lý do các mục troubleshooting trong báo cáo cuối có độ chi tiết cao: chúng được viết khi sự việc còn nóng, không phải hồi tưởng.

#### 4. Kỷ luật chi phí từ ngày đầu

Bảng ước tính Free Tier hoàn thành trước cả khi hệ thống có traffic thật, với hai "điểm nóng" được đánh dấu theo dõi đặc biệt: chi phí OpenAI (nằm ngoài AWS, có dashboard riêng) và Secrets Manager (tính phí theo lượt gọi API — chính là lý do bạn backend cache secret ở global scope). Kiểm tra Billing cuối tuần: chi phí bằng 0 đúng dự kiến. Nền nếp "xem Billing mỗi Chủ nhật" được thiết lập từ tuần này.

---

### Đánh giá kết quả tuần 10:

- Hạ tầng tài liệu (Hugo song ngữ, quy ước ảnh, khung chương) sẵn sàng nhận nội dung từ mọi thành viên.
- Sơ đồ kiến trúc chính thức được cả nhóm phê duyệt, trở thành ngôn ngữ chung khi trao đổi kỹ thuật.
- Quy ước ghi nhận sự cố 4 phần được thống nhất — khoản đầu tư quan trọng nhất cho chất lượng báo cáo cuối.
- Luồng backend với message giả được kiểm thử đạt; kỷ luật giám sát chi phí đi vào nền nếp.

---

### Khó khăn gặp phải:

- Theme Hugo workshop có nhiều shortcode và quy ước ngầm (cấu trúc `pre`, `weight`, children) phải mò qua ví dụ vì tài liệu chính thức mỏng.
- Vẽ sơ đồ cho hệ thống chưa xây xong đòi hỏi cập nhật liên tục khi thiết kế thay đổi — phải chấp nhận sơ đồ là tài liệu "sống", không phải vẽ một lần là xong.
- Thuyết phục các thành viên ghi lại sự cố ngay trong tuần không dễ khi ai cũng đang cuốn vào việc chính — phải chủ động "phỏng vấn" từng người cuối tuần thay vì chờ họ tự viết.

---

### Hướng khắc phục và Best Practices đúc kết được:

- Với theme/framework tài liệu mỏng docs, đọc thẳng source của theme và các site mẫu thay vì chỉ tìm tài liệu chính thức.
- Chấp nhận sơ đồ kiến trúc có phiên bản: lưu từng bản chốt theo mốc, ghi ngày — vừa phản ánh quá trình tiến hoá thiết kế (chi tiết hay cho báo cáo), vừa tránh tranh cãi "sơ đồ nào mới nhất".
- Chủ động thu thập thông tin từ thành viên theo lịch cố định (cuối tuần) thay vì chờ đợi — vai trò tài liệu là vai trò chủ động, không phải thụ động nhận bài.

---

### Định hướng cho tuần tiếp theo:

- Kiểm thử luồng OAuth và pipeline hoàn chỉnh với email thật khi bạn phụ trách bảo mật hoàn thành — vai "người dùng đầu tiên" của tính năng quan trọng nhất.
- Bắt đầu viết mục tài liệu đầu tiên có chiều sâu: tích hợp OAuth Gmail, dựa trên ghi nhận sự cố của bạn bảo mật.
- Theo dõi sát chi phí OpenAI khi hệ thống bắt đầu gọi API thật.
