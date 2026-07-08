---
title: "Sao chép Snapshot và tạo EBS Volume"
date: 2026-07-08
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

Trong phần này, bạn sẽ làm việc trên tài khoản Đích (Target Account) để sao chép snapshot được chia sẻ về tài khoản của mình nhằm sở hữu hoàn toàn bản sao lưu, sau đó tạo ổ cứng EBS Volume mới từ snapshot này.

{{% notice warning %}}
⚠️ **Quan trọng:** Tất cả các lệnh trong chương này đều thực hiện với **Tài khoản Đích (Tài khoản B)**, do đó bạn phải chỉ định rõ tham số `--profile rookwork-target` ở cuối mỗi câu lệnh.
{{% /notice %}}

#### Bước 1: Sao chép (Copy) Shared Snapshot về tài khoản Đích

Việc sao chép snapshot giúp bạn chuyển quyền sở hữu bản sao lưu về tài khoản Đích, cho phép bạn quản lý vòng đời (lifecycle), mã hóa bằng KMS key của tài khoản Đích và tạo volume thuận tiện.

Thực hiện lệnh sau trên GNOME Terminal:

```bash
# Thực hiện copy snapshot từ tài khoản Nguồn về tài khoản Đích
aws ec2 copy-snapshot \
  --source-region ap-southeast-1 \
  --source-snapshot-id snap-0112233445566aabb \
  --description "Copied Rookwork Backup from Source" \
  --profile rookwork-target
```
*Ghi nhận lại ID của Snapshot mới trong tài khoản Đích (ví dụ: `snap-0998877665544ccdd`).*

Kiểm tra tiến độ sao chép:
```bash
aws ec2 describe-snapshots \
  --snapshot-ids snap-0998877665544ccdd \
  --profile rookwork-target \
  --query "Snapshots[0].State"
```
Đợi cho đến khi trạng thái trả về là `completed`.

#### Bước 2: Tạo EBS Volume mới từ Snapshot đã sao chép

Khi tạo volume từ snapshot, bạn **bắt buộc** phải chọn cùng một **Availability Zone (AZ)** với máy chủ EC2 đích (ví dụ: `ap-southeast-1a`). Nếu tạo khác AZ, bạn sẽ không thể gắn (attach) volume vào máy chủ.

Nhập lệnh sau để tạo Volume:

```bash
# Tạo EBS Volume loại gp3 tại Availability Zone ap-southeast-1a
aws ec2 create-volume \
  --availability-zone ap-southeast-1a \
  --snapshot-id snap-0998877665544ccdd \
  --volume-type gp3 \
  --profile rookwork-target
```
*Ghi nhận lại Volume ID mới được tạo ra (ví dụ: `vol-0998877665544eeff`).*

Kiểm tra trạng thái của Volume cho đến khi chuyển sang `available`:
```bash
aws ec2 describe-volumes \
  --volume-ids vol-0998877665544eeff \
  --profile rookwork-target \
  --query "Volumes[0].State"
```
