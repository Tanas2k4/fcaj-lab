---
title: "Restore Data & Launch Application"
date: 2026-07-08
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

In this section, you will attach the newly created EBS Volume to the target EC2 instance, mount the volume in the Linux OS, and restart the **Rookwork** application to verify that the data has been successfully restored.

#### Step 1: Attach EBS Volume to the Target EC2 Instance

On your Fedora workstation, run the AWS CLI command to attach volume `vol-0998877665544eeff` to the EC2 instance in the Target account (e.g., ID: `i-0998877665544aaaa`):

```bash
aws ec2 attach-volume \
  --volume-id vol-0998877665544eeff \
  --instance-id i-0998877665544aaaa \
  --device /dev/sdf \
  --profile rookwork-target
```

#### Step 2: Access the Target EC2 Instance via SSH

Use GNOME Terminal on your local Fedora machine to SSH into the target server:

```bash
ssh -i ~/.ssh/rookwork-target-key.pem ec2-user@<TARGET_SERVER_IP>
```

#### Step 3: Mount the Volume in Linux

Once connected, list the block devices to verify the new volume is recognized:
```bash
lsblk
```
*You will see the newly attached volume (e.g., `/dev/xvdf` or `/dev/nvme1n1` for Nitro-based instances).*

Create a mount point directory for Rookwork application data:
```bash
sudo mkdir -p /var/www/rookwork
```

Mount the volume to the directory (do not format the drive, as the snapshot retains its existing filesystem):
```bash
sudo mount /dev/xvdf /var/www/rookwork
# Or if it is an NVMe drive:
# sudo mount /dev/nvme1n1 /var/www/rookwork
```

List directory contents to verify that databases and source files are present:
```bash
ls -lh /var/www/rookwork
```

#### Step 4: Launch the Rookwork Application

Navigate to the project folder and launch services (e.g., if Rookwork runs via Docker Compose):

```bash
cd /var/www/rookwork/app
sudo docker-compose up -d
```
Or if running directly via systemctl:
```bash
sudo systemctl restart rookwork
```

#### Step 5: Verify via Web Browser

Open a Web Browser (Firefox/Chromium) on your Fedora GNOME machine and enter the public IP of the target server:
`http://<TARGET_SERVER_IP>:port`

Log in to the Rookwork workspace and confirm that task boards, discussions, and attachments are fully restored. If all workspaces are intact, your server migration was a success!
