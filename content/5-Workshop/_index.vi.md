---
title: "Workshop"
date: 2026-07-08
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Backup và Di chuyển dữ liệu EBS Cross-Account (Dự án Rookwork)

#### Tổng quan

Trong quá trình phát triển dự án **Rookwork** (ứng dụng quản lý làm việc nhóm), nhóm phát triển thường xuyên đối mặt với các vấn đề về cấu hình môi trường, xung đột thư viện hoặc nhu cầu nâng cấp phần cứng máy chủ. Để giải quyết, việc **chuyển máy chủ thường xuyên** là điều tất yếu.

Workshop này sẽ hướng dẫn chi tiết quy trình sử dụng **Amazon EBS Snapshot** để backup và di chuyển toàn bộ dữ liệu (cơ sở dữ liệu và file đính kèm) từ tài khoản AWS Nguồn (Source - Tài khoản A) sang tài khoản AWS Đích (Target - Tài khoản B) một cách nhanh chóng và an toàn. Mọi thao tác dòng lệnh được thực hiện từ máy trạm cục bộ của nhà phát triển sử dụng hệ điều hành **Linux Fedora GNOME**.

#### Nội dung

1. [Giới thiệu và Kiến trúc](5.1-Workshop-overview/)
2. [Chuẩn bị](5.2-Prerequiste/)
3. [Tạo và chia sẻ EBS Snapshot](5.3-Create-Share-Snapshot/)
4. [Sao chép Snapshot và tạo EBS Volume ở tài khoản đích](5.4-Copy-Snapshot-Create-Volume/)
5. [Khôi phục dữ liệu và Khởi động ứng dụng](5.5-Attach-Volume-Restore-App/)
6. [Dọn dẹp tài nguyên](5.6-Cleanup/)