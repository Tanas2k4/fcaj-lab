---
title: "Khôi phục dữ liệu và Khởi động ứng dụng"
date: 2026-07-08
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

Trong phần này, bạn sẽ gắn (attach) EBS Volume mới tạo vào máy chủ EC2 đích, thực hiện mount ổ đĩa trong hệ điều hành Linux và khởi động lại ứng dụng **Rookwork** để xác minh dữ liệu đã được khôi phục thành công.

#### Bước 1: Gắn EBS Volume vào máy chủ EC2 đích

Trên máy trạm Fedora, chạy lệnh AWS CLI để gắn volume `vol-0998877665544eeff` vào máy chủ EC2 ở tài khoản Đích (ví dụ ID: `i-0998877665544aaaa`):

```bash
aws ec2 attach-volume \
  --volume-id vol-0998877665544eeff \
  --instance-id i-0998877665544aaaa \
  --device /dev/sdf \
  --profile rookwork-target
```

#### Bước 2: Truy cập SSH vào EC2 Instance đích

Sử dụng GNOME Terminal trên máy Fedora, thực hiện SSH vào máy chủ đích:

```bash
ssh -i ~/.ssh/rookwork-target-key.pem ec2-user@<IP_MÁY_CHỦ_ĐÍCH>
```

#### Bước 3: Mount ổ đĩa trên Linux

Khi kết nối vào máy chủ, kiểm tra danh sách ổ đĩa để tìm thiết bị mới gắn:
```bash
lsblk
```
*Bạn sẽ thấy thiết bị mới xuất hiện (ví dụ: `/dev/xvdf` hoặc `/dev/nvme1n1` đối với các dòng máy ảo nitro).*

Tạo thư mục để mount dữ liệu ứng dụng Rookwork:
```bash
sudo mkdir -p /var/www/rookwork
```

Thực hiện mount ổ đĩa vào thư mục vừa tạo (không cần format lại ổ cứng vì snapshot đã giữ nguyên định dạng file system từ trước):
```bash
sudo mount /dev/xvdf /var/www/rookwork
# Hoặc nếu là ổ đĩa NVMe:
# sudo mount /dev/nvme1n1 /var/www/rookwork
```

Kiểm tra thư mục để đảm bảo toàn bộ dữ liệu database và mã nguồn Rookwork đã có mặt:
```bash
ls -lh /var/www/rookwork
```

#### Bước 4: Khởi chạy ứng dụng Rookwork

Di chuyển vào thư mục dự án và tiến hành khởi động dịch vụ (ví dụ ứng dụng Rookwork chạy bằng Docker Compose):

```bash
cd /var/www/rookwork/app
sudo docker-compose up -d
```
Hoặc nếu chạy trực tiếp qua Systemd:
```bash
sudo systemctl restart rookwork
```

#### Bước 5: Xác minh từ trình duyệt

Mở trình duyệt Web (Firefox/Chromium) trên máy Fedora GNOME của bạn, truy cập địa chỉ IP công cộng của máy chủ đích:
`http://<IP_MÁY_CHỦ_ĐÍCH>:port`

Đăng nhập vào hệ thống quản lý làm việc nhóm Rookwork và kiểm tra xem danh sách các task, bảng phân chia công việc (boards) và tài liệu đính kèm có được giữ nguyên vẹn hay không. Nếu dữ liệu đầy đủ, quy trình di chuyển máy chủ đã thành công tốt đẹp!
