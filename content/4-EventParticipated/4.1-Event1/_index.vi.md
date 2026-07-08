---
title: "Event 1"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Bài thu hoạch sự kiện "AWS Vietnam Community Day 2026"

### Mục Đích Của Sự Kiện

- Tiếp cận các xu hướng công nghệ mới nhất về Generative AI (GenAI), Multi-Agent, và tối ưu hóa hạ tầng đám mây AWS.
- Lắng nghe chia sẻ thực tế và học hỏi kinh nghiệm thiết kế giải pháp từ các kỹ sư, chuyên gia đầu ngành tại Việt Nam.
- Kết nối cộng đồng công nghệ, chia sẻ bài học kinh nghiệm về kỹ năng mềm, làm việc nhóm và định hướng nghề nghiệp trong kỷ nguyên AI.

### Danh Sách Diễn Giả & Các Chủ Đề

- **Tịnh Trương** – Platform Engineer tại GoTymeX
  * *Chủ đề:* Context Is Everything: Making AI Actually Work for You
- **Phạm Ng Hải Anh** – G-AsiaPacific Vietnam, AWS Community Builder
  * *Chủ đề:* Friendly AI Assistant w/ Amazon Q in QuickSight
- **Nguyễn Tuấn Thịnh** – DevOps Engineer, First Cloud AI Journey
  * *Chủ đề:* From Edge to Origin: CloudFront as Your Foundation
- **Team VIB** – LotusHacks 2026
  * *Chủ đề:* 36 hrs with LotusHacks: Building UTMorpho from Idea to Reality
- **Đức Đào** – Solution Architect tại Cloud Kinetics
  * *Chủ đề:* Non-Determinism of "Deterministic" LLM Settings
- **Vy Lâm** – Senior Business Systems Analyst tại VPBank
  * *Chủ đề:* Enterprise-Grade Multi-Agent System: The Case of Startup Credit Scoring

### Nội Dung Nổi Bật

#### 1. Quản lý Context trong Ứng dụng AI (Diễn giả Tịnh Trương)
- **Tầm quan trọng của Context**: AI chỉ thực sự hoạt động hiệu quả khi được cung cấp đầy đủ thông tin ngữ cảnh. Context chính là cầu nối giúp giảm thiểu lỗi ảo tưởng (hallucination) của LLM.
- **Phương pháp tối ưu**: Cách cấu trúc prompt, quản lý dung lượng cửa sổ ngữ cảnh (context window) và chiến lược truy xuất dữ liệu phù hợp để mô hình trả về kết quả chính xác nhất.

#### 2. Trợ lý ảo AI với Amazon Q trong QuickSight (Diễn giả Phạm Ng Hải Anh)
- **Tích hợp GenAI vào Business Intelligence**: Sử dụng Amazon Q trong QuickSight giúp tự động hóa quá trình phân tích dữ liệu, tự động tạo dashboard từ các truy vấn ngôn ngữ tự nhiên.
- **Tối ưu năng suất**: Giúp doanh nghiệp rút ngắn thời gian tạo báo cáo và đưa ra quyết định nhanh chóng thông vụ tương tác trực tiếp với dữ liệu bằng ngôn ngữ tự nhiên.

#### 3. Tối ưu hạ tầng với Amazon CloudFront (Diễn giả Nguyễn Tuấn Thịnh)
- **Giảm tải CPU cho EC2**: Sử dụng CloudFront để đảm nhận việc nén dữ liệu (giảm dung lượng truyền tải, giúp tiết kiệm lên đến 82% CPU load cho máy chủ gốc EC2) và xử lý quá trình TLS handshake.
- **Bảo mật mạnh mẽ tại Edge**: Tận dụng mạng lưới Edge toàn cầu của AWS để chặn đứng các cuộc tấn công DDoS và lọc traffic độc hại ngay tại biên trước khi chạm đến hệ thống gốc.

#### 4. Hành trình 36 giờ Hackathon LotusHacks chế tạo UTMorpho (Team VIB)
- **Dự án UTMorpho**: Xây dựng một AI Agent hỗ trợ tạo và chỉnh sửa trực tiếp giao diện người dùng trên canvas trực quan (WYSIWYG editor) từ mô tả ngôn ngữ tự nhiên, giải quyết triệt để lỗi thiết kế bị trôi khi re-prompt nhiều lần.
- **Bài học Hackathon**: Những ý tưởng thực tế nhất xuất phát từ khó khăn hàng ngày. Trong áp lực thời gian (36 giờ liên tục), sự ăn ý và phối hợp nhịp nhàng giữa các thành viên quan trọng hơn năng lực cá nhân đơn lẻ.

#### 5. Tính không xác định của LLM trong thực tế (Diễn giả Đức Đào)
- **Hiện tượng Non-Determinism**: Phân tích việc LLM có thể đưa ra các kết quả khác nhau cho cùng một câu lệnh đầu vào ngay cả khi đã cấu hình temperature bằng 0 (do sai số tính toán float của GPU và xử lý song song).
- **Giải pháp kiểm soát**: Đưa ra các kiến trúc hệ thống và chiến lược kiểm soát (như guardrails, cấu trúc hóa output) để giảm thiểu rủi ro phi xác định trong các ứng dụng doanh nghiệp đòi hỏi tính nhất quán cao.

#### 6. Hệ thống Multi-Agent cấp doanh nghiệp trong phê duyệt tín dụng (Diễn giả Vy Lâm)
- **Bài toán phê duyệt tín dụng startup**: Khắc phục sự bất đối xứng dữ liệu giữa mô hình quản trị truyền thống của ngân hàng và dữ liệu linh hoạt của startup.
- **Kiến trúc Multi-Agent**: Mô hình hóa quy trình hội đồng tín dụng ảo thành các agent chuyên biệt (Financial Agent, Compliance Agent, Risk Agent...).
- **Giá trị kinh doanh**: Tự động hóa các quy trình phân tích phức tạp, giúp tiết kiệm lên tới 95% thời gian và chi phí vận hành mà vẫn đảm bảo tính tuân thủ bảo mật và quản trị.

### Những Gì Học Được

#### Tư Duy Thiết Kế Ứng Dụng AI
- **Đặt nghiệp vụ lên hàng đầu (Business-first)**: Ứng dụng AI cần tập trung giải quyết bài toán thực tế của doanh nghiệp (như phê duyệt tín dụng hay phân tích dữ liệu tự động) thay vì chỉ chạy theo công nghệ.
- **Phối hợp đa tác nhân (Multi-Agent Paradigm)**: Chia nhỏ hệ thống lớn thành các tác nhân AI chuyên biệt có nhiệm vụ và ranh giới rõ ràng để quản lý sự phức tạp hiệu quả hơn.

#### Kiến Trúc Kỹ Thuật Đám Mây & AI
- **Xây dựng nền tảng từ Edge**: Tận dụng tối đa CDN (Amazon CloudFront) để tối ưu hiệu suất truyền tải dữ liệu và làm lá chắn bảo mật vững chắc cho ứng dụng.
- **Kiểm soát tính nhất quán**: Thiết kế các cơ chế ràng buộc output của mô hình ngôn ngữ lớn để đảm bảo ứng dụng hoạt động ổn định và tin cậy.

#### Kỹ năng mềm & Làm việc nhóm
- **Tầm quan trọng của giao tiếp**: Sự phối hợp nhịp nhàng, truyền thông rõ ràng giữa các bộ phận quyết định sự thành bại của dự án hơn là nỗ lực của một cá nhân riêng lẻ.

### Các Điểm Mấu Chốt Cho Báo Cáo

* **Về kinh doanh**: Ứng dung mô hình Multi-Agent giúp tự động hóa và cắt giảm tới 95% thời gian thẩm định hồ sơ tín dụng startup.
* **Về kỹ thuật**: Hiểu rõ bản chất phi xác định của LLM và tầm quan trọng của việc tối ưu hóa Context để nâng cao độ chính xác của AI.
* **Về hạ tầng**: Tích hợp CloudFront tại biên để tối ưu hóa chi phí đường truyền, giảm tải tới 82% CPU cho EC2 gốc và tăng cường khả năng chống DDoS.

### Ứng Dụng Vào Công Việc

- Áp dụng kỹ thuật tối ưu hóa Context để cải thiện độ chính xác cho chatbot và các ứng dụng AI trong dự án hiện tại.
- Triển khai cấu hình tối ưu hóa bộ nhớ đệm và bảo mật biên bằng Amazon CloudFront cho hệ thống máy chủ web của site project.
- Nghiên cứu mô hình Multi-Agent và các framework thiết kế để áp dụng cho bài toán tự động hóa quy trình nghiệp vụ phức tạp.

### Trải nghiệm trong event

Tham gia sự kiện **AWS Vietnam Community Day 2026** mang lại trải nghiệm vô cùng quý giá, giúp mở rộng góc nhìn từ lý thuyết đến thực tiễn triển khai các hệ thống AI và Cloud ở quy mô doanh nghiệp lớn:

#### Học hỏi từ chuyên gia hàng đầu
- Các diễn giả có chuyên môn cao từ VPBank, GoTymeX, Cloud Kinetics đã mang lại những bài học kinh nghiệm rất sâu sắc từ quá trình thiết kế hệ thống thực tế.

#### Trải nghiệm các giải pháp kỹ thuật mới
- Tiếp cận giải pháp BI thế hệ mới với Amazon Q in QuickSight, trực tiếp nhìn nhận bài toán phi xác định của LLM và học hỏi kiến trúc Multi-Agent của VPBank.

#### Kết nối cộng đồng
- Có cơ hội thảo luận trực tiếp cùng các AWS Community Builders, đồng nghiệp đến từ nhiều doanh nghiệp công nghệ lớn, mở rộng mạng lưới quan hệ và học hỏi phong cách làm việc chuyên nghiệp.

#### Bài học rút ra
- AI và Đám mây bổ trợ lẫn nhau; một ứng dụng AI tốt đòi hỏi nền tảng hạ tầng đám mây tối ưu, bảo mật từ biên và thiết kế hệ thống chặt chẽ để kiểm soát tính bất định của công nghệ mới.

#### Một số hình ảnh khi tham gia sự kiện

![Chị Ngọc Uyển làm speaker](/images/meetup-2305.jpg)
*Hình 1: Chị Ngọc Uyển chia sẻ tại sự kiện*

![Nhận giải Lucky Draw](/images/meetup-2305-3.jpg)
*Hình 2: Tôi may mắn nhận giải thưởng Lucky Draw tại sự kiện*

![AWS Vietnam Community Day 2026](/images/meetup-2305-2.jpg)
*Hình 3: Toàn cảnh sự kiện AWS Vietnam Community Day 2026*

> Tổng thể, sự kiện không chỉ cung cấp kiến thức kỹ thuật mà còn giúp tôi thay đổi cách tư duy về thiết kế ứng dụng, hiện đại hóa hệ thống và phối hợp hiệu quả hơn giữa các team.
