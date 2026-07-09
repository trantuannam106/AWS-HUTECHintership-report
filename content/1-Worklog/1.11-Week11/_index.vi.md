---
title: "Worklog Tuần 11"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

Tuần này hệ thống bắt đầu chạm dữ liệu thật: luồng OAuth của bạn bảo mật hoàn thành, Worker của bạn backend bắt đầu đọc Gmail và gọi OpenAI. Vai trò của tôi chuyển từ "người dựng khung" sang "người dùng đầu tiên" — chạy kiểm thử end-to-end phía server bằng công cụ dòng lệnh, và chính trong vai này, tôi là người đầu tiên chạm mặt sự cố lớn nhất tuần của cả nhóm. Song song, tôi viết chương tài liệu nhiều nội dung kỹ thuật nhất: tích hợp OAuth Gmail.

- Kiểm thử luồng OAuth end-to-end phía server: lấy token Cognito qua CLI, gọi endpoint init, hoàn tất consent, xác minh dữ liệu trong DynamoDB.
- Kiểm thử pipeline hoàn chỉnh với email thật: gọi `/check-gmail`, giám sát SQS/Worker, xác minh kết quả tóm tắt.
- Phát hiện và phối hợp truy vết sự cố Worker `403 Forbidden` — báo cáo triệu chứng chính xác cho bạn bảo mật xử lý.
- Giám sát hàng đợi lỗi: theo dõi Dead-Letter Queue và alarm CloudWatch trong suốt quá trình kiểm thử.
- Viết trọn chương tài liệu "Tích hợp OAuth Gmail" (mục cha + các mục con) từ ghi nhận sự cố của bạn bảo mật.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Chuẩn bị bộ công cụ kiểm thử phía server trên Windows: lấy ID Token qua `aws cognito-idp initiate-auth`, gọi API bằng `curl.exe` (không dùng alias `curl` của PowerShell vì đó là `Invoke-WebRequest` với cú pháp khác hẳn). <br> - Xử lý lỗi PowerShell nuốt dấu ngoặc kép trong JSON inline: chuyển sang ghi JSON ra file `-Encoding ascii` rồi trỏ `file://`. | 29/06/2026 | 29/06/2026 | https://docs.aws.amazon.com/cli/ |
| 3 | - Kiểm thử luồng OAuth: gọi `/auth/gmail/init` nhận consent URL, hoàn tất consent trên trình duyệt với tài khoản trong Test users, xác nhận trang callback báo thành công. <br> - Xác minh record trong bảng `inboxiq-gmail-connections`: đủ accessToken, refreshToken, gmailAddress, expiresAt. | 30/06/2026 | 30/06/2026 | Nội bộ dự án |
| 4 | - Kiểm thử pipeline hoàn chỉnh: gọi `/check-gmail`, nhận `202 Accepted` kèm jobId. Nhưng sau thời gian chờ, bảng `inboxiq-email-summaries` trống — không có kết quả nào. <br> - Thu thập triệu chứng có hệ thống: metric Lambda báo `Errors = 0` nhưng `Messages Deleted` của SQS bằng 0, message bị retry mỗi 5 phút đúng chu kỳ visibility timeout. Báo cáo đầy đủ cho bạn backend và bạn bảo mật. | 01/07/2026 | 01/07/2026 | Nội bộ dự án |
| 5 | - Hỗ trợ truy vết: cung cấp record DynamoDB cho bạn bảo mật đối chiếu — chính field `scope` thiếu `gmail.readonly` trong record tôi trích xuất là manh mối chốt hạ nguyên nhân (granular permissions). <br> - Gặp lỗi phụ khi trích dữ liệu: AWS CLI trên Windows không in được tiếng Việt (`charmap codec error`) kể cả với `chcp 65001` — chuyển sang xem qua DynamoDB Console. | 02/07/2026 | 02/07/2026 | Nội bộ dự án |
| 6 | - Kiểm thử lại sau khi bạn bảo mật xử lý (re-consent lấy đủ scope): pipeline chạy trọn vẹn, email thật được tóm tắt đúng cấu trúc summary/category/priority/action kèm TTL. <br> - Giám sát DLQ trong lúc test: các message lỗi của đợt 403 đã dồn vào Dead-Letter Queue đúng thiết kế (sau 3 lần retry), alarm `inboxiq-dlq-messages` chuyển "In alarm" — xác nhận cơ chế cảnh báo hoạt động. Purge DLQ sau khi sự cố xử lý xong. | 03/07/2026 | 03/07/2026 | https://docs.aws.amazon.com/sqs/ |
| 7 | - Viết chương tài liệu "Tích hợp OAuth Gmail": mục cha (vì sao cần mục riêng, sơ đồ luồng, điểm mấu chốt init có auth / callback không auth) và mục con về Lambda + Layer (từ ghi nhận của bạn bảo mật). | 04/07/2026 | 04/07/2026 | Nội bộ dự án |
| CN | - Viết mục con "Kiểm thử end-to-end và xử lý sự cố": toàn bộ quy trình test bằng CLI, sự cố granular permissions, bảng tổng hợp các lỗi khác đã gặp trong tuần. <br> - Kiểm tra Billing + OpenAI dashboard: chi phí AWS vẫn 0, chi phí OpenAI ở mức không đáng kể. Viết báo cáo tuần. | 05/07/2026 | 05/07/2026 | Nội bộ dự án InboxIQ |

---

### Kết quả đạt được tuần 10:

#### 1. Vai trò "người dùng đầu tiên" — và giá trị của việc báo cáo triệu chứng chính xác

Sự cố `403 Forbidden` của tuần là bài học lớn nhất về vai trò kiểm thử. Tôi không phải người tìm ra nguyên nhân (đó là chuyên môn của bạn bảo mật), nhưng là người **phát hiện** và — quan trọng hơn — **báo cáo triệu chứng đủ chính xác để người khác truy vết được**: không chỉ nói "không có kết quả", mà chỉ ra bộ ba dữ kiện then chốt: Lambda `Errors = 0` (Worker không crash — nó bắt lỗi bên trong), `Messages Deleted = 0` (message không được xử lý xong), chu kỳ retry 5 phút khớp visibility timeout (SQS đang đẩy lại). Chính record DynamoDB tôi trích xuất — với field `scope` thiếu `gmail.readonly` — trở thành manh mối chốt hạ.

Bài học nghề nghiệp: một báo cáo lỗi tốt là một nửa lời giải. "Hệ thống không chạy" là lời phàn nàn; "Worker không crash nhưng message không được xoá khỏi queue, và đây là dữ liệu thực tế" là đầu vào cho chẩn đoán.

#### 2. Bộ công cụ kiểm thử trên Windows — những bẫy không có trong tài liệu nào

Kiểm thử API trên PowerShell dạy tôi ba bẫy môi trường tốn thời gian bậc nhất: `curl` trên PowerShell là alias của `Invoke-WebRequest` (cú pháp khác hẳn, phải gõ `curl.exe` tường minh); tham số JSON inline bị nuốt dấu ngoặc kép (giải pháp: ghi ra file `-Encoding ascii` rồi trỏ `file://`); và AWS CLI bản Windows không in được tiếng Việt (`charmap codec error`) bất kể `chcp 65001` — dữ liệu có dấu phải xem qua DynamoDB Console. Cả ba được ghi thành mục "lưu ý môi trường" trong tài liệu để người sau không mất thời gian như tôi.

#### 3. Xác nhận cơ chế chịu lỗi hoạt động đúng thiết kế — bằng một sự cố thật

Sự cố 403 vô tình trở thành bài kiểm thử thực chiến cho toàn bộ cơ chế chịu lỗi mà bạn backend dựng: message lỗi được retry đúng 3 lần rồi chuyển vào Dead-Letter Queue thay vì kẹt mãi ở hàng đợi chính, và alarm `inboxiq-dlq-messages` chuyển trạng thái "In alarm" đúng lúc — nghĩa là nếu đây là môi trường thật, đội vận hành đã được cảnh báo. Ít có cách nào xác nhận thiết kế chịu lỗi thuyết phục hơn một sự cố thật diễn ra đúng kịch bản đã lường trước. Sau khi sự cố xử lý xong, tôi purge DLQ và ghi chú theo dõi alarm quay về trạng thái OK.

#### 4. Chương tài liệu OAuth — viết khi sự việc còn nóng

Chương "Tích hợp OAuth Gmail" hoàn thành ngay trong tuần sự cố xảy ra, với mục troubleshooting chi tiết đến từng metric — điều không thể có nếu viết hồi tưởng sau một tháng. Quy ước "ghi ngay trong tuần" thiết lập từ tuần trước phát huy đúng lúc: ghi nhận thô của bạn bảo mật (nguyên nhân, cách xử lý) cộng dữ liệu kiểm thử của tôi (triệu chứng, metric, record) ghép thành một mục tài liệu hoàn chỉnh có đủ hai góc nhìn.

---

### Đánh giá kết quả tuần 11:

- Pipeline hoàn chỉnh với email thật được kiểm thử đạt sau sự cố — bao gồm xác minh đúng cấu trúc dữ liệu và cơ chế TTL.
- Đóng vai trò phát hiện và cung cấp dữ kiện then chốt cho sự cố lớn nhất tuần của nhóm.
- Cơ chế chịu lỗi (DLQ, alarm) được xác nhận hoạt động đúng thiết kế qua sự cố thật.
- Chương tài liệu OAuth Gmail hoàn thành với chất lượng troubleshooting cao nhờ viết ngay khi sự việc còn nóng.

---

### Khó khăn gặp phải:

- Ba bẫy môi trường Windows/PowerShell (curl alias, JSON escaping, charmap codec) ngốn thời gian đáng kể trước khi vào được việc kiểm thử thật.
- Ranh giới vai trò trong sự cố 403 ban đầu chưa rõ: tôi phát hiện nhưng không đủ chuyên môn OAuth để truy vết, phải học cách "bàn giao triệu chứng" hiệu quả thay vì cố tự sửa hoặc chỉ báo chung chung.
- Viết tài liệu kỹ thuật từ ghi nhận thô của người khác đòi hỏi hỏi lại nhiều vòng để không diễn giải sai bản chất kỹ thuật.

---

### Hướng khắc phục và Best Practices đúc kết được:

- Chuẩn hoá "mẫu báo cáo lỗi" cho kiểm thử: hiện tượng, các metric liên quan, dữ liệu trích xuất, các bước tái hiện — áp dụng cho mọi sự cố về sau.
- Ghi mọi bẫy môi trường vào một mục "lưu ý vận hành" dùng chung, tách khỏi nội dung kỹ thuật chính.
- Khi viết tài liệu từ ghi nhận của người khác, gửi bản nháp cho chính người đó soát lại trước khi chốt — người sửa lỗi là người duy nhất xác nhận được bản chất đúng hay sai.

---

### Định hướng cho tuần tiếp theo:

- Kiểm thử end-to-end trên thiết bị thật cùng cả nhóm khi app Flutter ghép vào hệ thống — dự kiến là tuần nhiều sự cố tích hợp nhất.
- Viết chương tài liệu Flutter và chương dọn dẹp tài nguyên.
- Tổng hợp số liệu chi phí toàn dự án và bảng tra cứu dịch vụ cho báo cáo cuối.
