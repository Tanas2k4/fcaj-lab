---
title: "Prerequisites"
date: 2026-07-08
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

To perform cross-account EBS snapshot backup and migration from a **Linux Fedora GNOME** local workstation, you need to prepare the following components:

#### 1. Install AWS CLI v2 on Fedora GNOME

Open GNOME Terminal on your Fedora workstation and execute the following commands to download and install the latest version of the **AWS CLI v2**:

```bash
# Download the AWS CLI package
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

# Unzip the installer
unzip awscliv2.zip

# Run the system installer (requires sudo privileges)
sudo ./aws/install

# Verify installation success
aws --version
```

#### 2. Configure Credentials for Both AWS Accounts

To manage two AWS accounts side-by-side on your workstation, configure Named Profiles in your `~/.aws/credentials` file.

Enter the following command to configure the Source account (Account A):
```bash
aws configure --profile rookwork-source
```
Enter the requested details:
- **AWS Access Key ID**: [Access Key for Account A]
- **AWS Secret Access Key**: [Secret Key for Account A]
- **Default region name**: `ap-southeast-1` (or the region where Rookwork is currently hosted)
- **Default output format**: `json`

Configure the Target account (Account B) by entering:
```bash
aws configure --profile rookwork-target
```
Provide the credentials associated with Account B.

{{% notice info %}}
**Crucial Warning on Account Profiles:**
Throughout this workshop, we will execute AWS CLI commands from your Fedora workstation. Pay **extreme attention** to the `--profile` parameter at the end of each command:
- `--profile rookwork-source`: Used strictly for the **Source Account (Account A)** hosting the original Rookwork server.
- `--profile rookwork-target`: Used strictly for the **Target Account (Account B)** where the server is being migrated.
Running a command with the wrong profile will lead to permission issues (Access Denied) or accidentally modify resources in the wrong account.
{{% /notice %}}

#### 3. Retrieve Target Account ID

To share the snapshot across accounts, you will need the **AWS Account ID** of the Target account (B). From the terminal, quickly retrieve this ID by running:

```bash
aws sts get-caller-identity --query "Account" --output text --profile rookwork-target
```
*(Example output: `987654321012` - save this number for the next steps).*

#### 4. Required Minimum IAM Permissions
Ensure your IAM Users or Roles in both accounts possess at least these permissions:
- **Source Account (A)**: `ec2:CreateSnapshot`, `ec2:DescribeSnapshots`, `ec2:ModifySnapshotAttribute`.
- **Target Account (B)**: `ec2:CopySnapshot`, `ec2:CreateVolume`, `ec2:AttachVolume`, `ec2:DescribeVolumes`.
