---
title: "Event 2"
date: 2026-05-23
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch “FCAJ Community Day - May 2026 Edition”

### Mục Đích Của Sự Kiện

- Cập nhật xu hướng vĩ mô và định vị thị trường CNTT Việt Nam trong thời đại AI phát triển thần tốc.
- Chia sẻ phương pháp thiết kế cấu trúc Prompt tối ưu hóa ngữ cảnh (Context Optimization) và cách kiểm soát tính ngẫu nhiên (Randomness) của LLM.
- Giới thiệu giải pháp trợ lý phân tích dữ liệu doanh nghiệp thông qua Amazon Q Business (QuickSight/Q Desktop) kết hợp MCP server.
- Chia sẻ kinh nghiệm thực chiến từ cuộc thi Hackathon và cách thiết kế hệ thống Multi-Agent chuẩn Enterprise áp dụng trong tài chính - ngân hàng.

### Danh Sách Diễn Giả

- **Anh Nguyễn Gia Hưng** - Solutions Architect tại AWS Việt Nam & Founder của FCAJ (Chia sẻ về định hướng vĩ mô thị trường).
- **Anh Tịnh Trương** - Platform Engineer tại Gothamic X (Chia sẻ về Kỹ thuật tối ưu hóa ngữ cảnh và Randomness của LLM).
- **Anh Hải Anh** - Solutions Architect tại Pacific Việt Nam (Chia sẻ về Amazon Q Business & MCP).
- **Anh Nguyễn Hấn Thịnh** - DevOps Engineer (Chia sẻ về cơ chế Flat-rate Pricing và bảo mật nâng cao của Amazon CloudFront).
- **Bạn Uyển, Bạn Mách & Chị Thảo** - Nhóm Winner Hackathon (Chia sẻ về hành trình 36 giờ phát triển dự án UTMorpho).
- **Diễn giả cuối (Kỹ sư FinTech)** - Cố vấn giải pháp FinTech tại VPBank (Chia sẻ về kiến trúc Multi-Agent ứng dụng trong ngân hàng).

### Nội Dung Nổi Bật

#### 1. Định vị thị trường CNTT và Cơ hội nghề nghiệp mới trong thời đại AI
- **Nghịch lý "Đèn LED" và sự bùng nổ phần mềm**: Khi AI giúp việc viết mã trở nên rẻ hơn (tương tự như bóng đèn LED giúp chi phí chiếu sáng giảm đi 1/10), nhu cầu phát triển phần mềm trên thế giới sẽ không giảm đi mà tăng lên một cách khủng khiếp. Ngay cả những người không thuộc ngành IT (luật sư, bác sĩ) hiện nay cũng có thể thắng các giải Hackathon lớn của Anthropic.
- **Luồng gió công việc mới - Fix Code rác & Platform Engineering**: Do AI sinh code dễ dàng, thị trường sẽ xuất hiện một lượng lớn các sản phẩm MVP/đồ án bị lỗi hoặc không thể vận hành ổn định. Từ đó, nhu cầu tuyển dụng các kỹ sư đi "fix code rác", cải tiến hệ thống và các kỹ sư xây dựng nền tảng (Platform Engineering) để tự động hóa hạ tầng (IDP - Internal Developer Platform) cho các tổ chức lớn sẽ tăng rất mạnh trong dài hạn.
- **Thực tế tuyển dụng tại Việt Nam**: Các ông lớn trên thế giới vẫn đang liên tục mở các Technical Hub tại Việt Nam để tận dụng nhân tài. Do đó, các kỹ sư Việt cần tập trung nâng cao khả năng tự tin, trình độ tiếng Anh, kiến trúc nghiệp vụ thực tế (Domain knowledge) và sản phẩm thực tế (Production-ready) thay vì chỉ dừng lại ở các bài tập demo nhỏ lẻ.

#### 2. Kỹ thuật tối ưu hóa ngữ cảnh và Kiểm soát tính ngẫu nhiên (Randomness) của LLM
- **Lỗi đổi Context liên tục**: Sai lầm phổ biến của người dùng là nhồi nhét quá nhiều chủ đề khác nhau vào cùng một phiên chat (hỏi từ đi du lịch, sửa CV cho đến code phần mềm), điều này làm biến đổi Context Window liên tục và khiến AI nhanh chóng bị "ảo tưởng" (hallucination).
- **Cơ chế Temperature và điểm số Logit**: Bản chất của LLM là một "probabilistic engine" hoạt động bằng cách xếp hạng điểm số (logit) cho các từ vựng tiếp theo. Khi thiết lập `Temperature = 0`, AI sẽ chuyển từ cơ chế tính toán Softmax sang Argmax (luôn luôn chọn từ có điểm số cao nhất) để tạo ra câu trả lời mang tính định tính và nhất quán (consistent).
- **Sự khác biệt giữa API Cloud và Local Host**: Ngay cả khi đặt `Temperature = 0`, các API của OpenAI hay Amazon Bedrock vẫn cho ra các kết quả khác nhau giữa các lượt chạy. Nguyên nhân cốt lõi là do GPU tính toán song song làm lệch số thập phân khi làm tròn, và do các nhà cung cấp áp dụng kỹ thuật tối ưu hóa thương mại (Inference Optimization) - gộp nhiều câu Prompts ngắn của các user khác nhau thành một lượt xử lý để giảm cost. Nếu muốn kiểm soát tuyệt đối 100% độ nhất quán, kỹ sư phải tự host Model trên hạ tầng Local.

#### 3. Hệ sinh thái Amazon Q Business & Trợ lý phân tích dữ liệu thế hệ mới
- **Xây dựng cánh tay nối dài bằng MCP (Model Context Protocol)**: Khái niệm AI Agent ngày nay không chỉ dừng lại ở việc trả lời văn bản, mà phải có khả năng hành động (Action). Bằng cách cắm các cổng MCP, AI Agent có thể tương tác trực tiếp, đặt lịch họp, gửi mail tự động hoặc kết nối trực tiếp với hệ thống Jira, Confluence, Microsoft Cloud, Google Suite.
- **Trợ lý phân tích dữ liệu tự động**: Người dùng doanh nghiệp không có kiến thức về BI (Business Intelligence) chỉ cần đưa file dữ liệu Excel thô vào Amazon Q Business (hoặc QuickSight Desktop), hệ thống sẽ tự động phân tích và trực quan hóa thành một Dashboard hoàn chỉnh cực kỳ nhanh chóng.

#### 4. Case Study: Dự án UTMorpho thắng giải Hackathon trong 36 giờ liên tục
- **Ý tưởng giải quyết nỗi đau thực tế (Pain point)**: Thay vì chọn những ý tưởng vĩ mô, nhóm tập trung giải quyết việc tiết kiệm thời gian và Token cho các lập trình viên khi thiết kế giao diện (UI). Thông thường mỗi lần muốn chỉnh sửa một chi tiết nhỏ trên giao diện do AI tạo ra, ta phải yêu cầu AI gen lại từ đầu.
- **Kiến trúc Multi-Agent của UTMorpho**: Dự án sử dụng mô hình Serverless trên AWS phối hợp 3 con Agent chuyên biệt:
  - *Agent 1 (Vision Agent)*: Đọc hình ảnh/bản vẽ phác thảo từ camera của người dùng và bóc tách thành file cấu trúc JSON.
  - *Agent 2 (Layout Agent)*: Tiếp nhận file JSON và tiến hành tính toán cấu trúc CSS, bố cục layout và kích thước.
  - *Agent 3 (Design Agent)*: Nhận thông tin từ Agent 2 và biên dịch thành mã nguồn HTML/CSS hoàn chỉnh theo thời gian thực (Streaming UI).
- **Tính năng nổi bật**: Tích hợp một trình Editor trực quan cho phép lập trình viên trực tiếp kéo thả, thay đổi vị trí component ngay trên giao diện được hiển thị và xuất link HTML public để đồng nghiệp cùng review.

#### 5. Kiến trúc Multi-Agent chuẩn Enterprise cho nghiệp vụ Ngân hàng (VPBank Practice)
- **Bài toán Nghiệp vụ - Đánh giá tín dụng cho Startup**: Hệ thống phê duyệt khoản vay truyền thống đòi hỏi doanh nghiệp phải cung cấp báo cáo tài chính 3 năm liên tiếp và tài sản thế chấp vật lý. Điều này khiến các Startup (vốn chỉ có tài sản trí tuệ và mới vận hành từ 3-6 tháng) không thể tiếp cận nguồn vốn. Giải pháp là thiết kế hệ thống Multi-Agent để phân tích đa chiều các dữ liệu phi truyền thống.
- **Thiết kế Hệ thống Multi-Agent chuyên biệt**:
  - *Credit Committee Agent (Manager/Orchestrator)*: Đóng vai trò chủ tọa hội đồng, phân phối nhiệm vụ và tổng hợp báo cáo cuối cùng.
  - *Financial Analyst Agent*: Tập trung xử lý sâu về báo cáo tài chính ngắn hạn và dòng tiền doanh nghiệp.
  - *Market Research Agent*: Phân tích thị phần (Tam, Sam, Som), đối thủ cạnh tranh và xu hướng thị trường.
  - *Team Evaluator Agent*: Thu thập dữ liệu, đánh giá năng lực của các Founders dựa trên hồ sơ công nghệ, hoạt động trên Twitter(X), LinkedIn, Facebook.
  - *Risk Assessor Agent*: Đảm nhận vai trò quan trọng nhất - kiểm soát ranh giới hoạt động của các con Agent khác, lọc dữ liệu đầu ra và đầu vào (Input/Output filtering) để chống rò rỉ thông tin bảo mật và ngăn chặn tấn công Prompt Injection theo tiêu chuẩn nghiêm ngặt của Ngân hàng Nhà nước.

### Những Gì Học Được

#### Tư Duy Thiết Kế
- **Tư duy hướng nghiệp vụ thực tế (Business-Driven Mindset)**: Khi thiết kế bất kỳ một giải pháp công nghệ nào trong doanh nghiệp lớn, phải luôn trả lời được 4 câu hỏi cốt lõi: Ai xài? Xài cái gì? Tại sao người ta phải xài? Khi nào là lúc thích hợp để triển khai?
- **Tư duy phân tách trách nhiệm (Separation of Concerns)**: Mỗi con AI Agent chỉ nên đảm nhận đúng một vai trò chuyên môn duy nhất dựa trên Backstory và System Prompt rõ ràng để tránh quá tải Context Window và tối ưu hóa phân phối sự chú ý (Attention) của mô hình.

#### Kiến Trúc Kỹ Thuật
- Nắm vững **Cơ chế kiểm soát tính định tính (Determinism)** của mô hình LLM thông qua việc cấu hình các tham số `Temperature`, `Top P`, và `Repeat Penalty` tùy thuộc vào định dạng đầu ra (Văn bản sáng tạo hay mã JSON/Code).
- Hiểu sâu về kiến trúc hạ tầng mạng nội bộ **AWS Backbone & PoP (Points of Presence)** của CloudFront: Cách CDN gộp các request đa tầng để bảo vệ Origin Server khỏi các đợt tấn công volumetric DDoS hoặc Syn Flush bằng tính năng Syn Proxy.
- Hiểu được tầm quan trọng của việc quản lý hạ tầng bằng mã nguồn thông qua **Terraform (Infrastructure as Code)** để quản lý các phiên bản tài nguyên và khả năng tái lập (Reproduce) hệ thống trên nhiều Region khác nhau của AWS.

#### Chiến Lược Hiện Đại Hóa
- **Chiến lược đo lường ROI (Return on Investment)**: Một dự án AI muốn được ban lãnh đạo Enterprise phê duyệt cần phải chứng minh bằng những con số cụ thể (Numbers speak louder than words), ví dụ như tính toán được chu kỳ hoàn vốn (Payback period) và số tiền tiết kiệm được cho doanh nghiệp hàng năm thay vì chỉ đưa ra bản demo công nghệ.
- **Chiến lược kiểm thử liên tục (Testing, Testing, Testing)**: Để một hệ thống AI có thể Production-ready trong môi trường khắt khe, các kỹ sư cần phải thực hiện các bài test động, test sâu ở tầng downstream services để đảm bảo hệ thống có thể handle được mọi trường hợp khi AI sinh lỗi format.

### Ứng Dụng Vào Công Việc

- **Cấu hình tham số Temperature mindful hơn**: Đặt `Temperature = 0` hoặc `0.1` khi cần AI sinh các định dạng cấu trúc chuẩn như JSON/HTML cho dự án hiện tại nhằm giảm tỷ lệ sai lệch cấu trúc dấu ngoặc, dấu phẩy.
- **Áp dụng kiến trúc Multi-Agent phòng ngừa lỗi**: Thay vì bắt một khung chat xử lý toàn bộ quy trình, tôi sẽ chia nhỏ bài toán ra thành các sub-agents hoạt động độc lập (theo mô hình dự án UTMorpho) và dùng một Agent quản lý để kiểm tra chéo kết quả.
- **Nâng cao tính bảo mật cho ứng dụng**: Triển khai các lớp lọc dữ liệu nhạy cảm (Input/Output filtering) bằng AWS Lambda trước khi truyền dữ liệu qua các mô hình ngôn ngữ lớn nhằm tuân thủ quy định bảo mật của tổ chức.
- **Chuyển đổi sang quản lý hạ tầng bằng Terraform**: Bắt đầu viết mã nguồn Terraform cho các dịch vụ AWS CloudFront, S3 của hệ thống để thay thế việc cấu hình thủ công (Click engineering) trên AWS Console, giúp dễ dàng quản lý và rotate các API Keys/Access Keys định kỳ.
- **Tập trung vào kiến thức Backend nền tảng**: Rèn luyện tư duy kỹ nghệ phần mềm cốt lõi (Software Engineering), master cấu trúc dữ liệu và API contract vì AI chỉ là công cụ hỗ trợ xây dựng sản phẩm nhanh hơn, tư duy hệ thống của lập trình viên vẫn là yếu tố quyết định.

### Trải nghiệm trong event

Được hòa mình vào workshop **“FCAJ Community Day”** lần này là một trải nghiệm bùng nổ về mặt tư duy. Không còn gói gọn trong các kiến thức học thuật sách vở, sự kiện đã mang đến những câu chuyện "xương máu" từ môi trường doanh nghiệp thực tế. Một số trải nghiệm nổi bật:

#### Học hỏi từ các diễn giả có chuyên môn cao
- Các diễn giả từ AWS Việt Nam, VPBank, VIB và Gothamic X mang lại những bài học vô giá về sự khác biệt giữa làm dự án cá nhân ở nhà và làm sản phẩm thật cho hàng triệu khách hàng trong ngành Ngân hàng (nơi bảo mật thông tin và tính tuân thủ luôn được đặt lên hàng đầu).

#### Trải nghiệm kỹ thuật thực tế
- Được khai phá về mặt tư duy khi chứng kiến cách các AI Agent phối hợp theo mô hình Multi-Agent, tự động phân tích thị trường toàn diện từ chỉ số tài chính, dữ liệu mạng xã hội cho đến chân dung nhà sáng lập doanh nghiệp.
- Hiểu được thực tế khốc liệt đằng sau các thuật toán tối ưu chi phí của các nhà cung cấp Cloud lớn và lý do tại sao AI vẫn có sự ngẫu nhiên dù cấu hình nhiệt độ bằng không.

#### Ứng dụng công cụ hiện đại
- Trực quan hóa dữ liệu chỉ bằng một vài câu lệnh tiếng Việt đơn giản qua bản demo của Amazon Q Business và QuickSight. Cách ứng dụng giao thức MCP (Model Context Protocol) mở ra một kỷ nguyên mới giúp các kỹ sư có thể tạo ra những "cánh tay nối dài" thực sự cho trí tuệ nhân tạo.

#### Kết nối và trao đổi
- Ban tổ chức đã tạo điều kiện kết nối rất tuyệt vời giữa các tầng (bao gồm cả các bạn ở tầng 36 thông qua hệ thống Lucky Draw). Sự kiện thúc đẩy tinh thần chủ động bắt chuyện, tìm kiếm cộng sự và truyền cảm hứng làm việc nhóm cực kỳ mạnh mẽ cho các bạn sinh viên trẻ.

#### Bài học rút ra
- AI đang làm cho việc phát triển phần mềm ngày một rẻ hơn, nhu cầu thị trường sẽ bùng nổ và mở ra cơ hội khổng lồ cho những ai có tư duy hệ thống tốt để đi làm các bài toán lớn.
- Đừng bao giờ lạm dụng AI theo kiểu sao chép nguyên văn (Ctrl+C & Ctrl+V) mà không hiểu bản chất mã nguồn, vì hậu quả trên môi trường Production của doanh nghiệp là vô cùng lớn.
- Xây dựng một hệ thống công nghệ, điều quan trọng nhất không phải là nó chạy được, mà là nó phải chạy một cách **an toàn**, **đáng tin cậy** và thực sự **mang lại giá trị cho người dùng**.

#### Một số hình ảnh khi tham gia sự kiện

![Ảnh minh chứng: tham gia event](</images/4-EventParticipated/Event2/event2(0).jpg>)

> Tổng thể, sự kiện không chỉ cung cấp những kiến thức kỹ thuật chuyên sâu về Prompt Engineering và mô hình phát triển phần mềm thời đại AI, mà quan trọng hơn hết là truyền ngọn lửa đam mê, kỷ luật tự học và định hình một tư duy nghề nghiệp đúng đắn cho thế hệ kỹ sư công nghệ tương lai.