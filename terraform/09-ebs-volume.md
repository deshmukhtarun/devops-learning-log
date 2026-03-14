# Terraform Learning Log – Creating Block Storage

## Overview

In this exercise, Terraform was used to create a block storage volume in the cloud environment.  
Block storage volumes provide persistent storage that can be attached to virtual machines.

This type of storage behaves like a physical hard drive attached to a server.

---

## Objective

Provision a block storage volume that:

- Uses a specific storage type
- Has a defined capacity
- Is tagged for identification
- Is created using Infrastructure as Code

---

## Terraform Configuration

```hcl
resource "aws_ebs_volume" "storage_volume" {
  availability_zone = "us-east-1a"
  size              = 2
  type              = "gp3"

  tags = {
    Name = "storage-volume"
  }
}
```

---

## Terraform Commands Used

Initialize Terraform:

```
terraform init
```

Preview planned changes:

```
terraform plan
```

Create the storage volume:

```
terraform apply
```

---

## Understanding Block Storage

Block storage volumes act like virtual hard drives that can be attached to virtual machines.

Example architecture:

```
Virtual Machine
      │
      ▼
Block Storage Volume
```

The operating system sees the volume as a disk and can use it to store files, databases, or application data.

---

## Storage Type

The configuration uses the storage type:

```
gp3
```

This stands for **General Purpose SSD** and provides:

- high performance
- low latency
- balanced cost

This type is commonly used for application workloads.

---

## Volume Size

The storage capacity defined:

```
2 GiB
```

This represents the maximum storage space available for data on the volume.

Volumes can later be attached to instances and formatted with file systems.

---

## Real World Example

A typical application server might use block storage for:

```
Application logs
Database files
Uploaded content
Persistent application data
```

Even if the server is replaced, the storage volume can be detached and attached to another instance.

---

## Terraform Concepts Practiced

This exercise reinforced several Infrastructure as Code concepts:

- provisioning persistent storage
- defining infrastructure using Terraform
- automating resource creation
- organizing infrastructure with tags

---

## Key Takeaways

- Block storage volumes provide persistent disk storage for servers.
- Terraform can automate the creation of storage infrastructure.
- Storage resources can be attached or detached from instances.
- Infrastructure as Code ensures consistent infrastructure deployment.