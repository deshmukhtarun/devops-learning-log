# Terraform Learning Log – Creating a VPC with IPv6 Support

## Overview

In this exercise, Terraform was used to create a Virtual Private Cloud (VPC) with both an IPv4 network range and an automatically assigned IPv6 address range.

Modern cloud infrastructure increasingly supports IPv6 to accommodate the growing number of internet-connected devices. Terraform allows enabling IPv6 during VPC creation while still maintaining the required IPv4 network.

---

# Objective

Provision a VPC that:

- Uses a defined IPv4 CIDR range
- Automatically receives an IPv6 CIDR block from the cloud provider
- Is tagged for easier identification
- Is created using Infrastructure as Code

---

# Terraform Configuration

```hcl
resource "aws_vpc" "network_vpc" {
  cidr_block                       = "10.20.0.0/16"
  assign_generated_ipv6_cidr_block = true

  tags = {
    Name = "network-vpc"
  }
}
```

---

# Terraform Commands Used

Initialize Terraform:

```
terraform init
```

Preview planned changes:

```
terraform plan
```

Create the infrastructure:

```
terraform apply
```

---

# Understanding IPv4 and IPv6

Cloud networks traditionally use **IPv4 addresses**, but due to address exhaustion, **IPv6** was introduced.

Example IPv4 address:

```
192.168.1.10
```

Example IPv6 address:

```
2001:db8:abcd:0012::1
```

IPv6 provides a dramatically larger address space compared to IPv4.

---

# Why an IPv4 CIDR Block Is Still Required

When creating a VPC, an IPv4 CIDR block must always be defined.

This IPv4 network becomes the internal address range used by servers, databases, and other services inside the network.

IPv6 support can then be added on top of the IPv4 configuration.

Example structure:

```
Virtual Private Cloud
│
├── IPv4 Network → 10.20.0.0/16
│
└── IPv6 Network → Automatically generated
```

---

# CIDR Block Explanation

The IPv4 range used in the configuration:

```
10.20.0.0/16
```

CIDR notation defines the size of the network.

This network provides approximately:

```
65,536 IP addresses
```

This range can later be divided into smaller networks called **subnets**.

---

# Real World Example

Imagine deploying a multi-tier application in the cloud.

Infrastructure components might include:

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
Database Servers
```

All these components operate inside the same VPC, allowing them to communicate securely through private network addresses.

IPv6 support ensures the architecture can scale globally.

---

# Terraform Concepts Practiced

This exercise reinforced several Infrastructure as Code principles:

- Creating cloud networks using Terraform
- Enabling IPv6 support in cloud environments
- Understanding CIDR block configuration
- Automating infrastructure provisioning
- Using tags for infrastructure organization

---

# Key Takeaways

- A VPC forms the foundation of cloud networking.
- IPv4 CIDR blocks are required when creating VPCs.
- IPv6 can be enabled alongside IPv4 for future scalability.
- Terraform allows network infrastructure to be defined and managed as code.