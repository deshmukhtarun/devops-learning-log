# Terraform Learning Log – VPC Creation

## Overview

In this exercise, Terraform was used to create a Virtual Private Cloud (VPC).  
A VPC is a logically isolated network in the cloud where infrastructure resources such as servers, databases, and applications can run securely.

Using Infrastructure as Code (IaC), the network configuration was defined in a Terraform file and deployed automatically.

---

# Objective

Create a Virtual Private Cloud with:

- A custom IPv4 CIDR block
- A descriptive name tag
- Deployment through Terraform

---

# Terraform Configuration

```hcl
resource "aws_vpc" "main_vpc" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "xfusion-vpc"
  }
}
```

---

# Terraform Commands Used

Initialize Terraform:

```
terraform init
```

Preview changes:

```
terraform plan
```

Create the infrastructure:

```
terraform apply
```

---

# Understanding VPC

A Virtual Private Cloud is essentially a **private network in the cloud**.

It allows organizations to define:

- IP address ranges
- Subnets
- Routing rules
- Network security policies

Example architecture:

```
Cloud Provider
      │
      ▼
Virtual Private Cloud
      │
 ┌───────────────┐
 │ Application   │
 │ Servers       │
 └───────────────┘
      │
 ┌───────────────┐
 │ Databases     │
 └───────────────┘
```

Everything inside the VPC runs in an isolated network environment.

---

# CIDR Block Explanation

The VPC was created with the CIDR block:

```
10.0.0.0/16
```

CIDR blocks define the IP address range available inside the network.

Example:

```
10.0.0.0 – 10.0.255.255
```

This provides **65,536 private IP addresses** for resources inside the VPC.

Private IP ranges are commonly used for internal infrastructure communication.

---

# Real World Example

Consider a company deploying a web application.

The infrastructure may include:

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

All of these components run inside the same VPC so they can communicate securely.

The VPC acts as the **foundation of the cloud network**.

---

# Terraform Resource Used

This configuration uses:

```
aws_vpc
```

This resource allows Terraform to create and manage virtual networks.

Attributes defined include:

- `cidr_block` → Defines the network range
- `tags` → Adds metadata for identification

---

# Terraform Concepts Practiced

This exercise reinforced several Infrastructure as Code concepts:

- Creating cloud network infrastructure
- Defining resources using Terraform
- Automating infrastructure provisioning
- Managing cloud networking through code

---

# Key Takeaways

- A VPC is the foundational network layer for cloud infrastructure.
- CIDR blocks define the available IP address range inside a network.
- Terraform can automate network creation and configuration.
- Infrastructure defined in code can be version controlled and reused.