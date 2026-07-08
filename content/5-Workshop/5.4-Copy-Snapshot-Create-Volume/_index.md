---
title: "Copy Snapshot & Create EBS Volume"
date: 2026-07-08
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

In this section, you will work in the Target account to copy the shared snapshot (to transfer ownership of the backup) and then create a new EBS Volume from it.

{{% notice warning %}}
⚠️ **Important:** All commands in this chapter must be executed on the **Target Account (Account B)**. Therefore, you must specify the `--profile rookwork-target` parameter at the end of each command.
{{% /notice %}}

#### Step 1: Copy the Shared Snapshot to the Target Account

Copying the shared snapshot gives the Target account ownership of the snapshot, allowing you to manage its lifecycle, encrypt it with target KMS keys, and provision volumes.

Execute this command on your GNOME Terminal:

```bash
# Copy the snapshot from the source region to the target account region
aws ec2 copy-snapshot \
  --source-region ap-southeast-1 \
  --source-snapshot-id snap-0112233445566aabb \
  --description "Copied Rookwork Backup from Source" \
  --profile rookwork-target
```
*Note the new Snapshot ID in the target account (e.g., `snap-0998877665544ccdd`).*

Check copy progress:
```bash
aws ec2 describe-snapshots \
  --snapshot-ids snap-0998877665544ccdd \
  --profile rookwork-target \
  --query "Snapshots[0].State"
```
Wait until the query output returns `completed`.

#### Step 2: Create a New EBS Volume from the Copied Snapshot

When creating a volume from a snapshot, you **must** select the same **Availability Zone (AZ)** where your target EC2 instance is located (e.g., `ap-southeast-1a`). If you create it in a different AZ, you cannot attach it to the EC2 instance.

Enter the following command to create the volume:

```bash
# Create a gp3 EBS Volume in Availability Zone ap-southeast-1a
aws ec2 create-volume \
  --availability-zone ap-southeast-1a \
  --snapshot-id snap-0998877665544ccdd \
  --volume-type gp3 \
  --profile rookwork-target
```
*Note the returned Volume ID (e.g., `vol-0998877665544eeff`).*

Verify the volume status until it becomes `available`:
```bash
aws ec2 describe-volumes \
  --volume-ids vol-0998877665544eeff \
  --profile rookwork-target \
  --query "Volumes[0].State"
```
