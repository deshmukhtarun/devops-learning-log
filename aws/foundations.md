# AWS Foundations

This document captures my current understanding of core AWS services based on hands-on practice and task-based learning.
It serves as a baseline before maintaining daily learning logs.

---

## Compute (EC2)

- Launched EC2 instances using AWS Console
- Launched EC2 instances using AWS CLI under default VPC
- Understood EC2 instance lifecycle: start, stop, reboot, terminate
- Worked with instance types (t2.micro, t3.micro, t2.nano)
- Changed instance type by stopping and restarting instances
- Modified EC2 instance attributes using AWS CLI
- Enabled stop protection and termination protection
- Created AMIs from EC2 instances and verified available state
- Launched EC2 instances from custom AMIs
- Terminated EC2 instances using AWS CLI and verified terminated state

---

## Storage – Block (EBS)

- Created EBS volumes and attached them to EC2 instances
- Attached volumes using specific device names (e.g. /dev/sdb)
- Learned that Linux may map devices as /dev/xvd*
- Created EBS snapshots
- Understood snapshots as point-in-time backups
- Used EBS snapshots to support AMI creation

---

## Storage – Object (S3)

- Created S3 buckets with unique names
- Created S3 buckets using AWS CLI
- Enabled and verified S3 bucket versioning
- Uploaded files to S3 using AWS CLI
- Downloaded bucket contents using recursive copy
- Deleted S3 buckets after emptying contents
- Blocked all public access to S3 buckets using Block Public Access
- Verified bucket access configuration using AWS CLI
- Understood S3 as object storage, not file system storage

---

## Identity and Access Management (IAM)

- Learned IAM core concepts: users, groups, roles, and policies
- Created IAM users and attached policies
- Created IAM policies using:
  - Visual policy editor
  - JSON editor
- Built read-only EC2 policies using Describe permissions
- Created IAM roles for EC2 with attached policies
- Understood role-based access vs access keys
- Learned IAM is a global service
- Understood how IAM permissions affect AWS CLI operations

---

## Databases (RDS)

- Created Amazon RDS MySQL instances using Full configuration
- Understood the difference between Aurora and RDS
- Worked with MySQL engine version 8.4.x
- Configured db.t3.micro RDS instances
- Configured RDS storage using gp2
- Created both publicly accessible and private RDS instances
- Enabled deletion (termination) protection for RDS instances
- Took manual RDS snapshots while the instance was running
- Deleted RDS instances after disabling deletion protection
- Verified RDS instance and snapshot states (Available, Deleting)

---

## Networking Basics

- Understood VPC as a private network
- Created a VPC using AWS Console
- Defined IPv4 CIDR blocks while creating a VPC
- Enabled IPv6 addressing for a VPC using Amazon-provided CIDR
- Understood that IPv6 CIDR blocks are assigned automatically by AWS
- Worked with subnets and CIDR blocks
- Learned rules for subnet CIDR:
  - Must be inside VPC CIDR
  - Cannot overlap
- Differentiated Security Groups and NACLs
- Attached default security groups to EC2 instances
- Created and attached Elastic IPs
- Attached Elastic Network Interfaces (ENIs) to EC2 instances
- Learned that a VPC must have no dependencies before deletion
- Deleted a VPC after ensuring all associated resources were removed

