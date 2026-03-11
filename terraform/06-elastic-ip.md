# Terraform Learning Log – Allocating a Static Public IP

## Overview

In this exercise, Terraform was used to allocate a static public IP address in the cloud environment.  
Unlike regular public IP addresses that can change when resources restart, an Elastic IP provides a persistent public address that can be reassigned to different resources when needed.

This allows infrastructure to maintain stable network endpoints even if the underlying resources change.

---

# Objective

Allocate a static public IP address that:

- Can be associated with cloud resources
- Remains persistent even if the instance stops or restarts
- Is created using Infrastructure as Code

---

# Terraform Configuration

```hcl
resource "aws_eip" "public_ip" {
  domain = "vpc"

  tags = {
    Name = "nautilus-eip"
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

# Understanding Elastic IP

An Elastic IP is a **static public IPv4 address** allocated for use within a cloud environment.

Normally, when a server is stopped and restarted, its public IP address may change.

Elastic IPs solve this problem by providing a **persistent public address** that can be reassigned.

Example concept:

```
Internet
   │
   ▼
Elastic IP
   │
   ▼
Virtual Machine
```

Even if the server is replaced, the same public IP can be attached to another instance.

---

# Why Static IPs Are Important

Static IP addresses are useful for:

- Hosting public web services
- DNS records pointing to infrastructure
- External integrations
- Failover systems

Because the IP remains constant, external systems can reliably connect to the service.

---

# Real World Example

Imagine a production web application.

Users access the application through a fixed public IP address.

```
User Browser
      │
      ▼
Static Public IP
      │
      ▼
Application Server
```

If the server fails, a new server can be launched and the same Elastic IP can be reassigned to it.  
This ensures the application remains accessible without requiring DNS updates.

---

# Terraform Concepts Practiced

This exercise reinforced several Infrastructure as Code concepts:

- Allocating public network addresses
- Managing infrastructure resources with Terraform
- Using tags to organize cloud resources
- Automating network infrastructure provisioning

---

# Key Takeaways

- Elastic IP addresses provide persistent public connectivity.
- Static IPs are useful for applications that require stable endpoints.
- Terraform can automate the allocation and management of network resources.
- Infrastructure as Code ensures consistent and repeatable infrastructure provisioning.