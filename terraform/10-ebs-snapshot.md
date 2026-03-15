# Terraform Learning Log – Creating a Storage Snapshot

## Overview

In this exercise, Terraform was used to create a snapshot of a block storage volume.  
Snapshots are backups of storage volumes that capture the state of the disk at a specific point in time.

They allow infrastructure teams to restore data or recreate storage volumes if needed.

---

## Terraform Configuration

```hcl
resource "aws_ebs_volume" "k8s_volume" {
  availability_zone = "us-east-1a"
  size              = 5
  type              = "gp2"

  tags = {
    Name = "xfusion-vol"
  }
}

resource "aws_ebs_snapshot" "volume_snapshot" {
  volume_id   = aws_ebs_volume.k8s_volume.id
  description = "Xfusion Snapshot"

  tags = {
    Name = "xfusion-vol-ss"
  }
}
```

---

## Terraform Commands Used

Initialize Terraform:

```
terraform init
```

Preview changes:

```
terraform plan
```

Apply infrastructure changes:

```
terraform apply
```

---

## Understanding Storage Snapshots

A snapshot is a backup of a storage volume taken at a specific moment.

Example process:

```
Storage Volume
      │
      ▼
Create Snapshot
      │
      ▼
Restore Volume Later
```

Snapshots store the data needed to recreate the volume in the future.

---

## Why Snapshots Are Important

Snapshots are commonly used for:

- backups
- disaster recovery
- creating new volumes
- cloning environments

They allow infrastructure teams to restore systems quickly in case of failure.

---

## Terraform Resource Dependency

Terraform automatically determines the order of resource creation.

Example:

```
aws_ebs_volume.k8s_volume
         ↓
aws_ebs_snapshot.volume_snapshot
```

Because the snapshot references the volume ID, Terraform ensures the volume exists before creating the snapshot.

---

## Real World Example

A database server may store important application data on a block storage volume.

To prevent data loss, snapshots can be taken regularly.

```
Database Server
       │
       ▼
Block Storage Volume
       │
       ▼
Scheduled Snapshots
```

If the server fails, the volume can be recreated from the snapshot.

---

## Terraform Concepts Practiced

- creating storage resources
- creating infrastructure backups
- referencing resources in Terraform
- automated infrastructure workflows

---

## Key Takeaways

- Snapshots provide point-in-time backups of storage volumes.
- Terraform can automate the creation of storage snapshots.
- Resource references create automatic dependency ordering.
- Infrastructure as Code helps maintain reliable backup processes.