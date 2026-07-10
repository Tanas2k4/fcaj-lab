---
title: "Các bài blogs đã dịch"
date: 2026-07-08
weight: 3
chapter: false
pre: " <b> 3. </b> "
---


Tại đây liệt kê và giới thiệu tóm tắt nội dung các bài blog công nghệ đã được dịch thuật trong quá trình thực tập:

###  [Blog 1 - Tự động hóa viễn thông quy mô hàng triệu thiết bị với Managed Red Hat AAP và ROSA trên AWS](3.1-Blog1/)
Blog này giới thiệu giải pháp tự động hóa viễn thông quy mô lớn trên AWS bằng cách kết hợp dịch vụ được quản lý AAP và cụm ROSA. Bạn sẽ tìm hiểu cách tách biệt hoàn toàn mặt điều khiển (Control Plane) và mặt thực thi (Execution Plane) để tối ưu hiệu năng và độ ổn định khi thao tác đồng loạt trên hàng triệu thiết bị (modem, router...). Bài viết cũng chia sẻ cơ chế tự động co giãn thực tế giúp tối ưu hóa chi phí đám mây theo thời gian thực và việc thu thập nhật ký log tập trung để đào tạo các mô hình AI vận hành.

###  [Blog 2 - Giới thiệu Dashboard Tổng quan Traffic của AWS WAF](3.2-Blog2/)
Blog này giới thiệu tính năng dashboard tổng quan traffic hoàn toàn miễn phí và có sẵn mặc định trên AWS WAF. Bạn sẽ tìm hiểu cách dashboard cung cấp cái nhìn realtime về lưu lượng request (allowed/blocked, bot/non-bot) để hỗ trợ SOC phát hiện hành vi bất thường. Bài viết cũng trình bày hai use case thực tế gồm phân tích pattern để săn lùng các đợt spike đột biến và tối ưu hóa cấu hình Bot Control thông qua cơ chế kiểm soát token.

###  [Blog 3 - Lối đi giữa Read-Write Separation (CQRS Prelude) cho Serverless API](3.3-Blog3/)
Blog này phân tích ưu nhược điểm của hai thái cực thiết kế API Serverless: Single Responsibility Lambda (chia nhỏ tối đa) và Lambda-lith (gộp tất cả). Từ đó, bài viết giới thiệu giải pháp trung hòa phân tách luồng Đọc và Ghi (Read-Write Separation) trong một Bounded Context thành 2 Lambda. Đây là bước chuẩn bị hoàn hảo giúp hệ thống dễ dàng tiến hóa lên mô hình CQRS hoàn chỉnh và kiến trúc hướng sự kiện khi tải tăng cao.