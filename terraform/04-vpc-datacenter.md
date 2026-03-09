# Terraform Learning Log – Custom VPC Creation

## Overview

In this exercise, Terraform was used to create a Virtual Private Cloud (VPC) with a specific IPv4 CIDR block.  
A VPC provides an isolated network environment in the cloud where infrastructure components such as application servers, databases, and internal services can run securely.

By defining the network configuration using Terraform, the infrastructure can be provisioned automatically and managed as code.

---

# Objective

Create a Virtual Private Cloud with:

- A specific IPv4 CIDR block
- A descriptive name tag
- Deployment through Terraform in the cloud environment

---

# Terraform Configuration

```hcl
resource "aws_vpc" "datacenter_vpc" {
  cidr_block = "192.168.0.0/24"

  tags = {
    Name = "datacenter-vpc"
  }
}
```

---

# Terraform Commands Used

Initialize Terraform:

```
terraform init
```

Preview infrastructure changes:

```
terraform plan
```

Create the infrastructure:

```
terraform apply
```

---

# Understanding VPC

A Virtual Private Cloud is a **private network inside a cloud provider**.  
It allows organizations to define their own networking environment for deploying resources.

Inside a VPC, teams can create:

- Subnets
- Application servers
- Databases
- Load balancers
- Network security rules

Example architecture:

```
Cloud Environment
        │
        ▼
Virtual Private Cloud
        │
 ┌──────────────┐
 │ App Servers  │
 └──────────────┘
        │
 ┌──────────────┐
 │ Databases    │
 └──────────────┘
```

The VPC acts as the foundational network layer for cloud infrastructure.

---

# CIDR Block Explanation

The VPC uses the CIDR block:

```
192.168.0.0/24
```

CIDR notation defines the IP address range available inside the network.

This range provides:

```
192.168.0.0 – 192.168.0.255
```

Total available addresses:

```
256 IP addresses
```

CIDR blocks allow organizations to control how large their internal network should be.

---

# Why VPCs Are Important

VPCs provide:

- Network isolation
- Custom IP addressing
- Secure communication between resources
- Control over routing and connectivity

Most cloud architectures start by designing the VPC because it becomes the **foundation of the entire infrastructure**.

---

# Real World Example

Imagine deploying an internal company platform.

The infrastructure might include:

```
Internet
   │
   ▼
Load Balancer
   │
   ▼
Application Servers
   │
   ▼
Database
```

All these components run inside the same VPC so they can communicate securely within a private network.

---

# Terraform Concepts Practiced

This exercise reinforced several Infrastructure as Code principles:

- Defining network infrastructure using Terraform
- Automating cloud resource creation
- Managing infrastructure through configuration files
- Using tags for resource identification

---

# Key Takeaways

- A VPC is the foundation of cloud networking.
- CIDR blocks define the IP address range inside the network.
- Terraform can automate the creation of cloud network infrastructure.
- Infrastructure as Code enables consistent and repeatable deployments.