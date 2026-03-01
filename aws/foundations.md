# AWS Foundations
This document captures my current understanding of core AWS services based on hands-on practice and task-based learning.
It serves as a basekine before maintaining daily learning logs.

---

## Compute (EC2)
- Launched EC2 instances using AWS Console
- Understood instance lifecycle: start, stop, reboot, terminate
- Worked with instance types (t2.micro, t3.micro)
- Changed instance type by stopping and restarting instances
- Enabled stop protection and termination protection
- Created AMIs from EC2 instances and verified available state
- Launched instances from custom AMIs

---

## Storage - Block (EBS)
- Created EBS volumes and attached them to EC2 instances
- Attached volumes using specific device names (e.g. /dev/sdb)
- Learned that linux may map devices as /dev/xvd*
- Created EBS snapshots
- Understood snapshots as point-in-time backups
- Used snapshots to support AMI creation

---

## Storage - Object (S3)
- Created S3 buckets with unique names
- Enabled and verified bucket versioning
- Upload files to S3 using AWS CLI
- Downloaded bucket contents using recursive copy
- Deleted S3 buckets after emptying contents
- Understood S3 as object storage, not file system storage

---

## Identity and Access Management (IAM)

- Learned IAM core concepts: users, groups, roles, policies
- Created IAM users and attached policies
- Created IAM policies using:
  - Visual policy editor
  - JSON editor
- Built read-only EC2 policies using Describe permissions
- Created IAM roles for EC2 with attached policies
- Understood role-based access vs access keys
- Learned IAM is a global service

---

## Networking Basics

- Understood VPC as a private network
- Worked with subnets and CIDR blocks
- Learned rules for subnet CIDR:
  - Must be inside VPC CIDR
  - Cannot overlap
- Differentiated Security Groups and NACLs
- Created and attached Elastic IPs
- Attached Elastic Network Interfaces (ENIs) to EC2 instances

---
