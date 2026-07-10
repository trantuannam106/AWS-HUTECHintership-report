---
title: "Bản đề xuất"
date: 2026-07-04
weight: 2
chapter: false
pre: "  2.  "
---

# InboxIQ

## AI-powered email triage on Serverless AWS

### 1. Tổng quan dự án

InboxIQ là một trợ lý ảo thông minh giúp giải quyết tình trạng quá tải email cho người dùng hiện đại (sinh viên, nhân viên văn phòng). Ứng dụng di động (Flutter) kết nối an toàn với Gmail qua chuẩn OAuth 2.0, sử dụng mô hình trí tuệ nhân tạo (GPT-4o-mini) để tóm tắt nội dung, phân loại danh mục (work / personal / promo / notification) và đánh giá mức độ ưu tiên của từng email, sau đó đẩy kết quả về ứng dụng theo thời gian thực qua WebSocket. Toàn bộ backend vận hành trên kiến trúc Serverless Event-Driven của AWS (Region `us-east-1`), được xây dựng trong khuôn khổ chương trình thực tập First Cloud AI Journey (FCAJ) 2026.

### 2. Mục tiêu

- Xây dựng hệ thống hoàn chỉnh end-to-end: từ ứng dụng di động trên thiết bị thật, qua backend serverless, tới các dịch vụ AI/Gmail bên ngoài — được kiểm chứng với dữ liệu email thật.
- Áp dụng kiến trúc bất đồng bộ (Producer/Worker qua SQS) để phản hồi tức thì cho người dùng trong khi xử lý nặng chạy nền, kết hợp WebSocket push thay cho polling.
- Đảm bảo bảo mật nhiều tầng: xác thực người dùng bằng Cognito (JWT), uỷ quyền đọc Gmail bằng OAuth 2.0 với scope tối thiểu, mọi credential lưu trong Secrets Manager, IAM Role theo nguyên tắc Least Privilege.
- Vận hành toàn bộ dự án trong hạn mức AWS Free Tier, kiểm soát chặt chi phí AI bằng hạn mức cứng.
- Quản lý hạ tầng hoàn toàn bằng Infrastructure as Code (AWS SAM) và tài liệu hoá trọn quá trình — bao gồm cả các sự cố và bài học — thành báo cáo Hugo song ngữ.

### 3. Vấn đề cần giải quyết

Người dùng hiện đại thường nhận 50–100 email mỗi ngày, tiêu tốn nhiều thời gian lọc thông tin và dễ bỏ lỡ email quan trọng. Các giải pháp hiện có hoặc mang tính thủ công (bộ lọc theo từ khoá, nhãn tự gắn), hoặc là dịch vụ AI bên thứ ba có chi phí cao và tiềm ẩn rủi ro quyền riêng tư khi dữ liệu email được xử lý tập trung ngoài tầm kiểm soát.

Bài toán kỹ thuật đặt ra gồm ba thách thức chính: (1) truy cập hộp thư người dùng một cách an toàn và có sự đồng ý tường minh (OAuth, không lưu mật khẩu Gmail); (2) xử lý AI tốn thời gian (nhiều giây tới hàng chục giây) mà không bắt ứng dụng di động chờ nghẽn; (3) trả kết quả về đúng người dùng, đúng phiên, theo thời gian thực.

### 4. Kiến trúc giải pháp

Hệ thống tổ chức thành 5 tầng chức năng tách biệt theo mô hình Serverless Event-Driven:

```
LAYER 1 · USER         → Users, Mobile App (Flutter)
LAYER 2 · BACKEND      → Cognito, API Gateway (REST + WebSocket), Lambda (Producer + Worker + Authorizer)
LAYER 3 · WORKFLOW     → SQS (Main Queue + Dead-Letter Queue), EventBridge Scheduler (optional)
LAYER 4 · STORAGE      → DynamoDB (4 bảng, TTL tự dọn), Secrets Manager
LAYER 5 · MONITORING   → CloudWatch, X-Ray, IAM Role
EXTERNAL SERVICES      → Gmail API, OpenAI API (ngoài AWS Cloud)
```

**Luồng xử lý chính:** người dùng bấm "Check Gmail" trên app → REST API (xác thực JWT) → Lambda Producer đóng gói yêu cầu kèm `connectionId` đẩy vào SQS, trả `202 Accepted` ngay → Lambda Worker tiêu thụ message, đọc Gmail token từ DynamoDB (tự refresh khi hết hạn), gọi Gmail API lấy email chưa đọc, gọi GPT-4o-mini tóm tắt song song → lưu kết quả vào DynamoDB (kèm TTL 30 ngày) → push kết quả về app qua API Gateway WebSocket.

**Các dịch vụ AWS sử dụng:**

- **Amazon Cognito**: quản lý định danh, xác thực người dùng và cấp phát JWT.
- **Amazon API Gateway**: REST endpoint cho tác vụ đồng bộ; WebSocket endpoint (route `$connect`, `$disconnect`, `whoami`) cho kênh hai chiều thời gian thực, xác thực bằng Lambda Authorizer.
- **AWS Lambda**: các hàm xử lý độc lập — Authorizer, Producer, Worker, các hàm vòng đời WebSocket và luồng OAuth (init/callback), chia sẻ logic chung qua Lambda Layer.
- **Amazon SQS**: hàng đợi `inboxiq-main` (Partial Batch Response — chỉ retry message lỗi) và Dead-Letter Queue cô lập message thất bại sau 3 lần retry, kèm CloudWatch Alarm cảnh báo.
- **Amazon DynamoDB**: 4 bảng chuyên biệt (kết nối Gmail, tóm tắt email, phiên WebSocket, job xử lý) ở chế độ On-Demand, dùng TTL quản lý vòng đời dữ liệu.
- **AWS Secrets Manager**: lưu trữ bảo mật OpenAI API key và Google OAuth Client Secret, đọc kèm cache ở global scope của Lambda.
- **Amazon EventBridge Scheduler** (tuỳ chọn): lên lịch kiểm tra email định kỳ 30 phút.
- **CloudWatch & X-Ray**: log, metric, alarm và tracing end-to-end.

Do tài khoản trong khuôn khổ chương trình bị giới hạn quyền truy cập Amazon Bedrock, giải pháp lựa chọn OpenAI API, thiết kế theo hướng trừu tượng hoá AI provider để có thể chuyển sang Bedrock trong tương lai.

### 5. Timeline

Dự án triển khai trong 3 tuần với 4 thành viên, phân công theo mảng chuyên trách (backend/kiến trúc, Flutter, OAuth/bảo mật, tài liệu/kiểm thử/chi phí):

- **Tuần 1 — Nền móng**: chốt kiến trúc và phân công; dựng tầng lưu trữ (DynamoDB, SQS + DLQ) và lớp danh tính (Cognito, IAM Role, Secrets Manager); viết Lambda Producer/Worker, tích hợp OpenAI; khởi tạo Google Cloud project và OAuth consent screen; dựng repo tài liệu Hugo, thiết lập kỷ luật giám sát chi phí.
- **Tuần 2 — Tích hợp lõi**: hoàn thành luồng OAuth Gmail (Lambda init/callback, Lambda Layer refresh token); dựng API Gateway WebSocket kèm Authorizer và route `whoami`; ghép Gmail thật vào Worker; xây dựng phía client Flutter (xác thực Cognito, deep link OAuth, WebSocket service); kiểm thử pipeline với email thật.
- **Tuần 3 — Tích hợp cuối và hoàn thiện**: test end-to-end trên thiết bị Android thật, xử lý các sự cố tích hợp; tối ưu Worker (xử lý song song, chịu lỗi từng phần tử); hoàn thiện giao diện Material 3; rà soát bảo mật; tổng hợp tài liệu, số liệu chi phí và hướng dẫn dọn dẹp tài nguyên.

### 6. Ngân sách

Hạ tầng thiết kế theo mô hình On-Demand để tận dụng triệt để AWS Free Tier:

| Hạng mục | Ước tính hàng tháng | Ghi chú |
| --- | --- | --- |
| AWS Lambda | 0,00 USD | Trong hạn mức 1 triệu request/tháng |
| Amazon SQS & API Gateway | ~0,00 USD | Lượng request MVP nhỏ hơn nhiều so với Free Tier |
| Amazon DynamoDB | 0,00 USD | Chế độ On-Demand, dữ liệu nhỏ |
| Secrets Manager, CloudWatch, X-Ray | ~0,00 USD | Mức dùng thử nghiệm; cache secret giảm lượt gọi API |
| OpenAI API (GPT-4o-mini) | ~1,00 – 2,00 USD | Khối lượng test 50–100 email/ngày; trần 10 email/lần gọi |

Cơ chế kiểm soát rủi ro tài chính: AWS Budgets cảnh báo qua email theo các mốc chi phí; hạn mức cứng (Hard Limit) **5,00 USD/tháng** trên OpenAI Platform; giới hạn `maxResults = 10` email mỗi lần xử lý để chặn chi phí đột biến khi hộp thư có quá nhiều email chưa đọc.

### 7. Rủi ro

**Ma trận rủi ro:**

| Rủi ro | Ảnh hưởng | Xác suất |
| --- | --- | --- |
| Gmail OAuth token mất hiệu lực hoặc thiếu scope (người dùng không cấp đủ quyền trên màn consent) | Cao | Trung bình |
| Kết nối WebSocket rớt âm thầm khiến kết quả không về được app | Cao | Trung bình |
| Throttling từ OpenAI hoặc Secrets Manager khi gọi dồn dập | Trung bình | Thấp |
| Phát sinh chi phí AWS/OpenAI ngoài tầm kiểm soát | Cao | Thấp |
| Ứng dụng chỉ dùng được với tài khoản trong danh sách Test users (consent screen chế độ Testing) | Trung bình | Chắc chắn (giới hạn đã biết) |

**Chiến lược giảm thiểu:**

- **Token Gmail**: lưu trạng thái token trong DynamoDB, kiểm tra hiệu lực trước mỗi lần gọi, tự động refresh qua Lambda Layer dùng chung; kiểm tra field `scope` thực nhận trong token response thay vì tin vào việc luồng consent chạy trót lọt.
- **WebSocket**: client xác minh `connectionId` tại thời điểm sử dụng (không tin giá trị đã cache) và tự kết nối lại khi phát hiện kết nối đã rớt; phía Worker bọc lời gọi push trong xử lý lỗi riêng để thất bại push không làm hỏng cả batch.
- **Throttling**: cache API key ở global scope của Lambda; xử lý email song song bằng cơ chế chịu lỗi từng phần tử (một email lỗi không kéo sập cả mẻ); SQS Partial Batch Response chỉ retry đúng message thất bại.
- **Chi phí**: AWS Budgets cảnh báo nhiều mốc; hạn mức cứng OpenAI; trần số email mỗi lần xử lý; rà soát Billing Dashboard định kỳ hàng tuần.
- **Giới hạn Test users**: chấp nhận như phạm vi của đồ án (quy trình Google verification cho scope Gmail vượt khuôn khổ thực tập), ghi rõ vào phần Limitations của báo cáo kèm quy trình thêm tài khoản test khi cần demo.
