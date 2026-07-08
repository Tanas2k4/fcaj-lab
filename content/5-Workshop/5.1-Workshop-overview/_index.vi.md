---
title: "Giới thiệu và Kiến trúc"
date: 2026-07-08
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Giới thiệu về Amazon EBS Snapshot

**Amazon Elastic Block Store (EBS) Snapshots** là phương pháp sao lưu dạng block-level, có tính chất lũy kế (incremental backup) của các EBS volume. 

Trong bài lab này, chúng ta sẽ tận dụng khả năng chia sẻ snapshot giữa các tài khoản AWS (Cross-Account Snapshot Sharing) để sao sao chép dữ liệu đĩa cứng của máy chủ chạy ứng dụng **Rookwork** từ tài khoản Source sang tài khoản Target. Điều này giúp:
- Sao lưu dự phòng dữ liệu ứng dụng một cách an toàn ngoài tài khoản gốc.
- Di chuyển máy chủ ứng dụng (Database, Uploaded Files) nhanh chóng sang môi trường khác mà không làm mất tính nhất quán của dữ liệu.

#### Kiến trúc di chuyển (Migration Architecture)

Mô hình hoạt động của quy trình di chuyển như sau:
1. **Source Account (Tài khoản A)**: Chứa máy chủ ứng dụng Rookwork chạy trên EC2 instance, gắn EBS Volume lưu trữ database và mã nguồn.
2. **Tạo Snapshot**: Tiến hành dừng EC2 instance để đảm bảo tính nhất quán dữ liệu (consistent snapshot), sau đó tạo EBS Snapshot từ EBS Volume này.
3. **Chia sẻ Snapshot**: Thiết lập quyền truy cập cho phép Target Account (Tài khoản B) đọc được Snapshot vừa tạo.
4. **Target Account (Tài khoản B)**: Thực hiện sao chép (copy) Snapshot đã được chia sẻ về tài khoản của mình nhằm chuyển quyền sở hữu (owner).
5. **Khôi phục Volume & Khởi chạy**: Tạo một EBS Volume mới từ bản sao Snapshot và gắn vào máy chủ EC2 mới trong tài khoản B để tiếp tục vận hành Rookwork.

```mermaid
graph TD
    subgraph Source Account A
        EC2_A[Rookwork EC2 Instance] -->|Stop Instance| Vol_A[(EBS Volume)]
        Vol_A -->|Create Snapshot| Snap_A[EBS Snapshot]
        Snap_A -->|Share Permissions| Snap_A_Shared[Shared Snapshot]
    end

    subgraph Target Account B
        Snap_A_Shared -->|Copy Snapshot| Snap_B[Owned EBS Snapshot]
        Snap_B -->|Create Volume| Vol_B[(Restored EBS Volume)]
        Vol_B -->|Attach & Mount| EC2_B[New Rookwork EC2 Instance]
    end

    Dev[Local Client: Fedora GNOME] -->|AWS CLI| Source_Account_A
    Dev -->|AWS CLI| Target_Account_B
```

#### Sơ đồ trình tự các bước thực hiện (AWS Official Workflow):

![EBS Migration Architecture](/images/5-Workshop/ebs_migration_architecture.png)
