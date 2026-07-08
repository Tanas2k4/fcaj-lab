---
title: "Workshop"
date: 2026-07-08
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# EBS Snapshot Cross-Account Backup and Migration (Rookwork Project)

#### Overview

During the development and testing of the **Rookwork** team collaboration application, the development team frequently encounters environment setup challenges, software conflicts, or infrastructure upgrade requirements. Consequently, **frequent server migrations** are an absolute necessity to resolve these issues.

This workshop provides a step-by-step guide on how to use **Amazon EBS Snapshots** to back up and migrate entire application state datasets (including active databases and uploaded attachments) from a Source AWS account (Account A) to a Target AWS account (Account B) securely and efficiently. All command-line operations in this guide are executed from the developer's local workstation running **Linux Fedora GNOME**.

#### Content

1. [Overview & Architecture](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequiste/)
3. [Create and Share EBS Snapshot](5.3-Create-Share-Snapshot/)
4. [Copy Snapshot & Create EBS Volume in Target Account](5.4-Copy-Snapshot-Create-Volume/)
5. [Restore Data & Launch Application](5.5-Attach-Volume-Restore-App/)
6. [Clean up Resources](5.6-Cleanup/)