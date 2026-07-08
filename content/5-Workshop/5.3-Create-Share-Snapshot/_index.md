---
title: "Create & Share EBS Snapshot"
date: 2026-07-08
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

In this section, you will back up the EBS volume (containing Rookwork application database and files) in the Source account and share it with the Target account.

{{% notice warning %}}
⚠️ **Important:** All commands in this chapter must be executed on the **Source Account (Account A)**. Therefore, you must specify the `--profile rookwork-source` parameter at the end of each command.
{{% /notice %}}

#### Step 1: Stop the Rookwork EC2 Instance

To ensure file system and database transactional consistency (preventing dirty writes during backup), stop the Rookwork server instance first:

```bash
# Replace i-0123456789abcdef0 with your Rookwork Instance ID
aws ec2 stop-instances \
  --instance-ids i-0123456789abcdef0 \
  --profile rookwork-source
```

Wait until the instance state changes to `stopped`.

#### Step 2: Create EBS Snapshot from the Rookwork Volume

Identify your volume ID attached to the instance, and create the snapshot:

```bash
# Create a snapshot from the EBS Volume (e.g., vol-0abc123456789def0)
aws ec2 create-snapshot \
  --volume-id vol-0abc123456789def0 \
  --description "Rookwork Server Migration Backup" \
  --profile rookwork-source
```
*Note the returned Snapshot ID (e.g., `snap-0112233445566aabb`).*

Monitor the snapshot creation progress until the state changes to `completed`:
```bash
aws ec2 describe-snapshots \
  --snapshot-ids snap-0112233445566aabb \
  --profile rookwork-source \
  --query "Snapshots[0].State"
```

#### Step 3: Share the Snapshot with the Target Account

Once the snapshot state is `completed`, modify its permissions to share it with the Target Account (e.g., Target Account ID: `987654321012`):

```bash
aws ec2 modify-snapshot-attribute \
  --snapshot-id snap-0112233445566aabb \
  --attribute userIds \
  --operation-type add \
  --user-ids 987654321012 \
  --profile rookwork-source
```

*Note: You may now restart the Rookwork EC2 instance in the Source account if needed.*
```bash
aws ec2 start-instances \
  --instance-ids i-0123456789abcdef0 \
  --profile rookwork-source
```
