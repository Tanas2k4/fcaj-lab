---
title: "Overview & Architecture"
date: 2026-07-08
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### About Amazon EBS Snapshot

**Amazon Elastic Block Store (EBS) Snapshots** provide block-level, incremental backups of your EBS volumes. 

In this lab, we will leverage Cross-Account Snapshot Sharing to copy the storage drive data of the **Rookwork** application server from the Source account to the Target account. This helps to:
- Securely back up application data outside the primary account.
- Fast-migrate application servers (Database, Uploaded Files) to a different environment without risking data inconsistency.

#### Migration Architecture

The operational workflow of the migration process is as follows:
1. **Source Account (Account A)**: Contains the running Rookwork application EC2 instance, attached to an EBS Volume hosting the databases and source files.
2. **Create Snapshot**: Stop the EC2 instance to ensure file system consistency (consistent snapshot), then create an EBS Snapshot of the volume.
3. **Share Snapshot**: Grant access permissions allowing the Target Account (Account B) to read the created Snapshot.
4. **Target Account (Account B)**: Copy the shared Snapshot into Account B to transfer ownership.
5. **Restore Volume & Launch**: Create a new EBS Volume from the copied Snapshot and attach it to a new EC2 instance in Account B to restart Rookwork.

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

#### Step-by-Step Sequence Flow (AWS Official Workflow):

![EBS Migration Architecture](/images/5-Workshop/ebs_migration_architecture.png)
