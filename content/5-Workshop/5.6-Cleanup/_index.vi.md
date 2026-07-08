---
title: "Dọn dẹp tài nguyên"
date: 2026-07-08
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

Sau khi di chuyển thành công và xác minh hệ thống Rookwork hoạt động ổn định trên máy chủ đích, việc dọn dẹp các tài nguyên tạm thời là vô cùng quan trọng để tối ưu hóa chi phí vận hành trên AWS (tránh phí lưu trữ snapshot dư thừa).

#### 1. Xóa các Snapshot tạm thời

Chạy các lệnh sau trên GNOME Terminal từ máy trạm Fedora của bạn:

```bash
# Xóa snapshot gốc tại tài khoản Nguồn (Tài khoản A)
aws ec2 delete-snapshot \
  --snapshot-id snap-0112233445566aabb \
  --profile rookwork-source

# Xóa snapshot bản sao tại tài khoản Đích (Tài khoản B)
aws ec2 delete-snapshot \
  --snapshot-id snap-0998877665544ccdd \
  --profile rookwork-target
```

#### 2. Dọn dẹp máy chủ EC2 cũ ở tài khoản Nguồn

Nếu máy chủ cũ ở tài khoản Nguồn không còn giá trị lưu trữ hoặc không cần chạy dự phòng, bạn nên chấm dứt (terminate) instance để tránh phát sinh chi phí tính toán:

```bash
aws ec2 terminate-instances \
  --instance-ids i-0123456789abcdef0 \
  --profile rookwork-source
```

*Lưu ý: Thao tác này sẽ xóa máy ảo EC2 cũ. Sau khi instance bị hủy, EBS Volume gốc được gắn với máy ảo đó cũng sẽ tự động bị xóa nếu cấu hình thuộc tính `DeleteOnTermination` được bật.*

#### 3. Kiểm tra các EBS Volume thừa

Kiểm tra xem có bất kỳ EBS volume nào ở trạng thái `available` (không gắn vào máy ảo nào) ở cả hai tài khoản và tiến hành xóa chúng:

```bash
# Liệt kê các volume không dùng ở tài khoản Đích
aws ec2 describe-volumes \
  --filters Name=status,Values=available \
  --query "Volumes[*].VolumeId" \
  --output text \
  --profile rookwork-target

# Xóa volume thừa nếu có
aws ec2 delete-volume \
  --volume-id vol-xxxxxxxxxxxxxxxxx \
  --profile rookwork-target
```

> [!WARNING]
> **Chú ý quan trọng:** Tuyệt đối không xóa EBS Volume đang hoạt động (`vol-0998877665544eeff`) đang được mount vào máy chủ đích mới, vì đây là nơi lưu trữ toàn bộ dữ liệu hiện tại của ứng dụng Rookwork.
