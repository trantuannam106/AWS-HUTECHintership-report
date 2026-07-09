---
title: "Worklog Tuần 12"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:

Tuần cuối của dự án, hệ thống đi vào giai đoạn tích hợp cuối và các thành viên khác dồn sức debug — còn tôi dồn sức vào việc đóng gói: chuyển ba tuần làm việc của cả nhóm thành một bộ báo cáo Hugo hoàn chỉnh mà người ngoài đọc vào hiểu được trọn vẹn quá trình. Ba đầu việc lớn: viết chương Flutter (bám sát các sự cố tích hợp đang diễn ra nóng hổi trong tuần), viết chương dọn dẹp tài nguyên, và tổng hợp phần "xương sống trí tuệ" của báo cáo — bảng tra cứu dịch vụ kèm số liệu chi phí thực tế.

- Tham gia các buổi test tích hợp end-to-end với vai trò ghi nhận: chụp lại bằng chứng từng sự cố (log, ảnh Console) phục vụ tài liệu.
- Viết trọn chương Flutter: mục cha và các mục con (setup, OAuth deep link, kiểm thử & xử lý sự cố WebSocket).
- Viết chương dọn dẹp tài nguyên song ngữ: hướng dẫn từng bước, phân biệt tài nguyên trong stack và ngoài stack.
- Rà soát toàn bộ dịch vụ đã dùng, lập bảng tra cứu (dịch vụ – vai trò – lý do chọn – rủi ro) — kiểm chứng trạng thái thật của từng tài nguyên thay vì tin tài liệu cũ.
- Chốt số liệu chi phí toàn dự án từ Billing Dashboard và OpenAI usage.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Hạng mục công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Tham dự buổi test tích hợp đầu tiên với vai trò ghi nhận: chụp ảnh hiện tượng "WebSocket chưa sẵn sàng" và log Forbidden — bằng chứng gốc cho mục troubleshooting sau này. | 06/07/2026 | 06/07/2026 | Nội bộ dự án |
| 3 | - Theo chân quá trình truy vết của bạn backend, chụp lại từng mốc bằng chứng: thông báo "Log group does not exist", Deployment history chỉ có bản cũ. <br> - Ghi nhận thô sự cố theo khung 4 phần ngay trong ngày. | 07/07/2026 | 07/07/2026 | Nội bộ dự án |
| 4 | - Viết mục cha chương Flutter: sơ đồ luồng từ bấm nút đến kết quả, điểm mấu chốt "push qua WebSocket thay vì polling REST" và cái giá phải trả về độ phức tạp. <br> - Viết mục con setup môi trường và kiến trúc app từ ghi nhận của bạn Flutter. | 08/07/2026 | 08/07/2026 | Nội bộ dự án |
| 5 | - Ghi nhận sự cố 410 Gone: chụp log Worker (GoneException, httpStatusCode 410) và bảng đối chiếu timestamp ba nguồn của bạn backend — chất liệu cho mục troubleshooting đắt giá nhất chương. <br> - Viết mục con OAuth deep link phía client (sự cố Chrome chặn redirect từ góc nhìn hai bạn Flutter/bảo mật). | 09/07/2026 | 09/07/2026 | Nội bộ dự án |
| 6 | - Hệ thống chạy trọn vẹn end-to-end — nhận bộ ảnh luồng hoàn chỉnh từ bạn Flutter, ghép vào tài liệu. <br> - Viết mục con "Kiểm thử end-to-end và xử lý sự cố WebSocket": 4 sự cố lớn theo khung hiện tượng → nguyên nhân → cách xử lý → bài học. | 10/07/2026 | 10/07/2026 | Nội bộ dự án |
| 7 | - Viết chương "Dọn dẹp tài nguyên" song ngữ Việt/Anh: `sam delete` cho stack chính, xoá riêng Cognito/Secrets (cả hai secret: OpenAI và Google), S3 artifact bucket, CloudWatch Logs còn sót — kèm vị trí ảnh minh hoạ "trước khi xoá". <br> - Ghi rõ bối cảnh: tài nguyên giữ nguyên đến hết đợt chấm điểm, chương này là hướng dẫn thực hiện sau đó. | 11/07/2026 | 11/07/2026 | https://docs.aws.amazon.com/serverless-application-model/ |
| CN | - Rà soát toàn hệ thống lập bảng tra cứu dịch vụ: mở từng resource trên Console kiểm chứng trạng thái thật — phát hiện bảng `inboxiq-processing-jobs` mới khai báo trong template, chưa có code ghi dữ liệu. <br> - Chốt số liệu chi phí: AWS trong Free Tier, OpenAI ở mức không đáng kể. Viết báo cáo tuần cuối và rà soát chéo toàn bộ báo cáo. | 12/07/2026 | 12/07/2026 | Nội bộ dự án InboxIQ |

---

### Kết quả đạt được tuần 12:

#### 1. Vai trò "người ghi sử" trong tuần debug — bằng chứng gốc quý hơn hồi tưởng

Tuần debug căng nhất của nhóm hoá ra là tuần thu hoạch lớn nhất của mảng tài liệu. Bằng cách có mặt tại các buổi test với vai trò ghi nhận, tôi chụp được bằng chứng gốc tại đúng khoảnh khắc: thông báo đỏ "Log group does not exist" (bằng chứng request chưa từng chạm Lambda), Deployment history trước và sau khi sửa, log GoneException với mã 410 đầy đủ. Những ảnh này không thể dựng lại sau khi sự cố đã sửa xong — muốn có, phải chụp ngay lúc đó. Mục troubleshooting của chương Flutter nhờ vậy có độ tin cậy của một biên bản hiện trường, không phải một bản kể lại.

#### 2. Chương Flutter — hai câu chuyện debug thành hai bài học phổ quát

Viết lại hai sự cố lớn (route chưa publish, connectionId chết) từ ghi nhận của hai thành viên dạy tôi kỹ năng cốt lõi của người viết tài liệu kỹ thuật: tách **bài học phổ quát** ra khỏi **chi tiết cụ thể**. "Route whoami trả Forbidden" là chi tiết của dự án này; "CloudFormation tạo route thành công không đồng nghĩa route được publish lên stage" là bài học mọi người dùng API Gateway đều cần. Mỗi mục troubleshooting được kết bằng phần bài học viết ở tầng phổ quát — đó là phần người chấm và người đọc sau này thực sự mang đi được.

#### 3. Chương dọn dẹp — tưởng đơn giản, hoá ra cần nhiều quyết định biên tập

Chương "Dọn dẹp tài nguyên" đặt ra loạt câu hỏi biên tập không hiển nhiên: viết ở thì nào khi tài nguyên chưa thể xoá thật (hệ thống phải sống đến hết đợt chấm điểm)? Giải quyết: viết dạng hướng dẫn từng bước với ảnh minh hoạ "trạng thái trước khi xoá", ghi rõ bối cảnh thời điểm thực hiện. Liệt kê gì? Phải bao phủ cả tài nguyên **ngoài** stack SAM (Cognito tạo tay, cả hai secret — OpenAI lẫn Google, S3 artifact bucket do SAM CLI tự tạo) — những thứ `sam delete` không đụng tới và cũng không xuất hiện trên sơ đồ kiến trúc, nhưng vẫn âm thầm tồn tại trong tài khoản. Bản tiếng Anh được dịch song song ngay khi bản Việt chốt, tránh lệch nội dung giữa hai ngôn ngữ.

#### 4. Bảng tra cứu dịch vụ — và nguyên tắc "kiểm chứng tận Console"

Phần việc cuối cùng và nghiêm ngặt nhất: rà từng dịch vụ trong kiến trúc, mở tận Console kiểm chứng trạng thái thật thay vì tin tài liệu các tuần trước. Nguyên tắc này lập tức có kết quả: phát hiện bảng `inboxiq-processing-jobs` mới chỉ tồn tại trong SAM template, **chưa có dòng code nào ghi dữ liệu vào** — nếu cứ viết vào báo cáo như một tính năng hoạt động sẽ là điểm trừ nặng khi bị hỏi sâu. Trạng thái thật của từng tài nguyên (đang dùng / mới khai báo / dự phòng) được ghi tường minh.

Số liệu chi phí chốt: toàn bộ dịch vụ AWS nằm trong Free Tier suốt ba tuần phát triển; chi phí OpenAI (GPT-4o-mini) ở mức không đáng kể so với hạn mức — kèm ghi chú các "chi phí ẩn" đã chủ động né từ đầu (cache secret giảm lượt gọi Secrets Manager, trần 10 email/lần chặn chi phí OpenAI đột biến).

---

### Đánh giá kết quả tuần 12:

- Bộ báo cáo Hugo hoàn chỉnh: chương kiến trúc, OAuth, Flutter (kèm troubleshooting mức "biên bản hiện trường"), dọn dẹp song ngữ, chi phí.
- Bảng tra cứu dịch vụ với trạng thái kiểm chứng tận Console — bao gồm phát hiện trung thực về bảng chưa dùng.
- Toàn bộ bằng chứng sự cố được lưu giữ có hệ thống, sẵn sàng cho phần bảo vệ báo cáo.
- Số liệu chi phí ba tuần được chốt với kết luận rõ ràng: trong Free Tier + OpenAI không đáng kể.

---

### Khó khăn gặp phải:

- Viết tài liệu trong lúc sự cố đang diễn ra nghĩa là nội dung thay đổi liên tục — có mục phải viết lại hai lần vì chẩn đoán ban đầu của nhóm hoá ra chưa phải nguyên nhân gốc.
- Cân bằng giữa độ chi tiết kỹ thuật (đủ để tái hiện) và độ dài báo cáo (người chấm còn đọc nổi) là bài toán biên tập không có đáp án tuyệt đối.
- Việc ghi trung thực các điểm chưa hoàn thiện (bảng chưa dùng, secret cần rotate, các hạng mục bảo trì) cần sự đồng thuận của cả nhóm — may mắn là văn hoá minh bạch đã được thống nhất từ đầu.

---

### Hướng khắc phục và Best Practices đúc kết được:

- Với tài liệu troubleshooting, chụp bằng chứng ngay tại thời điểm sự cố — không có cơ hội thứ hai sau khi lỗi được sửa.
- Kết mỗi mục sự cố bằng bài học viết ở tầng phổ quát, tách khỏi chi tiết dự án — đó là giá trị bền của tài liệu.
- Trước khi chốt báo cáo, kiểm chứng trạng thái thật của mọi tài nguyên tận Console; không tin bất kỳ ghi chú nào cũ hơn một tuần.
- Báo cáo trung thực về giới hạn (kèm kế hoạch xử lý) thuyết phục hơn báo cáo "hoàn hảo" — và an toàn hơn nhiều khi bị hỏi sâu.

---

### Định hướng sau dự án:

- Hoàn thiện nốt phần chụp ảnh minh hoạ cho chương dọn dẹp (các trang Console "trước khi xoá") và hỗ trợ nhóm thực hiện dọn dẹp thật sau đợt chấm điểm.
- Cập nhật báo cáo lần cuối với ảnh Billing sát ngày nộp để số liệu chi phí phản ánh trọn vòng đời dự án.
- Tổng hợp bộ "bài học phổ quát" từ các mục troubleshooting thành một trang riêng — di sản tri thức của nhóm cho các khoá sau.
