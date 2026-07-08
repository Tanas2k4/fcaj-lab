---
title: "Clean up Resources"
date: 2026-07-08
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

After successfully migrating and verifying that the Rookwork application functions correctly on the target server, cleaning up temporary resources is essential to optimize operational costs on AWS (avoiding unnecessary snapshot storage fees).

#### 1. Delete Temporary Snapshots

Run the following commands in your GNOME Terminal on Fedora:

```bash
# Delete the original snapshot in the Source account (Account A)
aws ec2 delete-snapshot \
  --snapshot-id snap-0112233445566aabb \
  --profile rookwork-source

# Delete the copied snapshot in the Target account (Account B)
aws ec2 delete-snapshot \
  --snapshot-id snap-0998877665544ccdd \
  --profile rookwork-target
```

#### 2. Terminate the Old EC2 Instance in the Source Account

If the old server in the Source account is no longer needed for storage or redundancy, terminate the instance to stop computing charges:

```bash
aws ec2 terminate-instances \
  --instance-ids i-0123456789abcdef0 \
  --profile rookwork-source
```

*Note: This operation permanently deletes the old EC2 instance. Once terminated, its attached root EBS volume is automatically deleted if `DeleteOnTermination` was enabled.*

#### 3. Inspect and Delete Unused EBS Volumes

Identify and delete any EBS volumes that are in the `available` state (detached from any running instance) in both accounts:

```bash
# List unused volumes in the Target account
aws ec2 describe-volumes \
  --filters Name=status,Values=available \
  --query "Volumes[*].VolumeId" \
  --output text \
  --profile rookwork-target

# Delete an unused volume if list is not empty
aws ec2 delete-volume \
  --volume-id vol-xxxxxxxxxxxxxxxxx \
  --profile rookwork-target
```

> [!WARNING]
> **Important Note:** Do NOT delete the active EBS Volume (`vol-0998877665544eeff`) mounted on the new target server, as it contains your running Rookwork database and user data.
