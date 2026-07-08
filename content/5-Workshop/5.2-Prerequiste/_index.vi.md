---
title: "Các bước chuẩn bị"
date: 2026-07-08
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

Để tiến hành sao lưu và di chuyển dữ liệu EBS Cross-Account từ máy trạm **Linux Fedora GNOME**, bạn cần chuẩn bị các thành phần sau:

#### 1. Cài đặt AWS CLI v2 trên Fedora GNOME

Mở Terminal của bạn trên Fedora (GNOME Terminal) và thực hiện các lệnh sau để tải và cài đặt phiên bản mới nhất của **AWS CLI v2**:

```bash
# Tải bộ cài đặt AWS CLI v2
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

# Giải nén
unzip awscliv2.zip

# Tiến hành cài đặt hệ thống (yêu cầu quyền sudo)
sudo ./aws/install

# Kiểm tra cài đặt thành công
aws --version
```

#### 2. Cấu hình Credentials cho cả 2 Tài khoản AWS

Để quản lý song song hai tài khoản AWS trên cùng một máy trạm, chúng ta cấu hình các Named Profiles trong file `~/.aws/credentials`.

Nhập lệnh sau để cấu hình cấu hình tài khoản Nguồn (Source - Tài khoản A):
```bash
aws configure --profile rookwork-source
```
Nhập các thông tin sau:
- **AWS Access Key ID**: [Access Key của tài khoản A]
- **AWS Secret Access Key**: [Secret Key của tài khoản A]
- **Default region name**: `ap-southeast-1` (hoặc region bạn đang chạy Rookwork)
- **Default output format**: `json`

Tiếp tục nhập lệnh sau để cấu hình tài khoản Đích (Target - Tài khoản B):
```bash
aws configure --profile rookwork-target
```
Nhập các thông tin tương tự tương ứng với tài khoản B.

{{% notice info %}}
**Lưu ý cực kỳ quan trọng về Account Profile:**
Trong suốt workshop này, chúng ta sẽ thực thi các câu lệnh AWS CLI từ máy trạm Fedora. Hãy **đặc biệt chú ý** đến tham số `--profile` ở cuối mỗi câu lệnh:
- `--profile rookwork-source`: Dành riêng cho **Tài khoản Nguồn (Tài khoản A)** nơi chứa máy chủ Rookwork cũ.
- `--profile rookwork-target`: Dành riêng cho **Tài khoản Đích (Tài khoản B)** nơi di chuyển máy chủ sang.
Việc chạy lệnh sai profile/tài khoản sẽ dẫn đến lỗi phân quyền (Access Denied) hoặc làm thay đổi nhầm tài nguyên ở tài khoản còn lại.
{{% /notice %}}

#### 3. Thu thập thông tin định danh tài khoản Đích

Để chia sẻ snapshot giữa hai tài khoản, bạn cần biết **AWS Account ID** của tài khoản Đích (B). Trên terminal, bạn có thể nhanh chóng lấy ID này bằng lệnh:

```bash
aws sts get-caller-identity --query "Account" --output text --profile rookwork-target
```
*(Kết quả ví dụ: `987654321012` - hãy ghi nhớ số tài khoản này cho bước tiếp theo).*

#### 4. Quyền IAM tối thiểu yêu cầu
Đảm bảo user IAM hoặc Role của bạn ở cả hai tài khoản có tối thiểu các quyền sau:
- **Source Account (A)**: `ec2:CreateSnapshot`, `ec2:DescribeSnapshots`, `ec2:ModifySnapshotAttribute`.
- **Target Account (B)**: `ec2:CopySnapshot`, `ec2:CreateVolume`, `ec2:AttachVolume`, `ec2:DescribeVolumes`.
