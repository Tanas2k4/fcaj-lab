---
title: "Tạo và chia sẻ EBS Snapshot"
date: 2026-07-08
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

Trong phần này, bạn sẽ thực hiện sao lưu ổ cứng EBS (chứa dữ liệu và mã nguồn ứng dụng Rookwork) ở tài khoản Nguồn và chia sẻ snapshot đó cho tài khoản Đích.

{{% notice warning %}}
⚠️ **Quan trọng:** Tất cả các lệnh trong chương này đều thực hiện với **Tài khoản Nguồn (Tài khoản A)**, do đó bạn phải chỉ định rõ tham số `--profile rookwork-source` ở cuối mỗi câu lệnh.
{{% /notice %}}

#### Bước 1: Dừng EC2 Instance của ứng dụng Rookwork

Để đảm bảo tính nhất quán dữ liệu (data consistency) và không bị lỗi ghi dở (dirty write) khi đang backup database, hãy dừng máy chủ ứng dụng Rookwork trước:

```bash
# Thay thế i-0123456789abcdef0 bằng Instance ID máy chủ Rookwork của bạn
aws ec2 stop-instances \
  --instance-ids i-0123456789abcdef0 \
  --profile rookwork-source
```

Đợi cho máy chủ chuyển hẳn sang trạng thái `stopped`.

#### Bước 2: Tạo EBS Snapshot từ Volume dữ liệu Rookwork

Liệt kê và tìm ID của EBS volume đang gắn vào máy chủ, sau đó tiến hành tạo snapshot:

```bash
# Tạo snapshot cho EBS Volume (ví dụ: vol-0abc123456789def0)
aws ec2 create-snapshot \
  --volume-id vol-0abc123456789def0 \
  --description "Rookwork Server Migration Backup" \
  --profile rookwork-source
```
*Ghi nhận lại ID của Snapshot được tạo ra ở kết quả trả về (ví dụ: `snap-0112233445566aabb`).*

Kiểm tra tiến độ tạo snapshot cho đến khi trạng thái chuyển sang `completed`:
```bash
aws ec2 describe-snapshots \
  --snapshot-ids snap-0112233445566aabb \
  --profile rookwork-source \
  --query "Snapshots[0].State"
```

#### Bước 3: Chia sẻ Snapshot sang tài khoản Đích

Sau khi snapshot được tạo thành công, tiến hành cấu hình quyền chia sẻ để cho phép tài khoản Đích (ví dụ ID: `987654321012`) có quyền truy cập:

```bash
aws ec2 modify-snapshot-attribute \
  --snapshot-id snap-0112233445566aabb \
  --attribute userIds \
  --operation-type add \
  --user-ids 987654321012 \
  --profile rookwork-source
```

*Lưu ý: Bạn cũng có thể khởi động lại máy chủ Rookwork ở tài khoản Nguồn sau khi snapshot hoàn tất.*
```bash
aws ec2 start-instances \
  --instance-ids i-0123456789abcdef0 \
  --profile rookwork-source
```
