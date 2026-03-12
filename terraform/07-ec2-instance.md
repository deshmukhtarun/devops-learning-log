# Terraform Learning Log – Launching a Virtual Machine

## Overview

In this exercise, Terraform was used to provision a virtual machine in the cloud along with a newly generated SSH key pair.  
This demonstrates how compute resources can be deployed automatically using Infrastructure as Code.

The configuration includes the creation of a cryptographic key, registration of that key with the cloud provider, and launching a virtual machine that uses the key for secure access.

---

# Objective

Provision a virtual machine that:

- Uses a specific machine image
- Runs on a small instance type
- Uses a newly generated RSA key for authentication
- Uses the default network security configuration
- Is tagged for identification

---

# Terraform Configuration

```hcl
resource "tls_private_key" "instance_key" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

resource "aws_key_pair" "generated_key" {
  key_name   = "example-key"
  public_key = tls_private_key.instance_key.public_key_openssh
}

data "aws_security_group" "default_sg" {
  name = "default"
}

resource "aws_instance" "vm_instance" {
  ami           = "ami-0c101f26f147fa7fd"
  instance_type = "t2.micro"
  key_name      = aws_key_pair.generated_key.key_name

  vpc_security_group_ids = [
    data.aws_security_group.default_sg.id
  ]

  tags = {
    Name = "example-instance"
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

# Key Concepts Learned

## Virtual Machine Provisioning

Cloud providers allow servers to be created on demand.  
These servers are commonly referred to as virtual machines or instances.

Example architecture:

```
User
 │
 ▼
Internet
 │
 ▼
Virtual Machine
```

Terraform automates the process of provisioning these compute resources.

---

## Machine Images

Machine images are templates used to create virtual machines.

They contain:

- operating system
- default packages
- boot configuration

Example:

```
Linux server image
```

Every time an instance launches, it starts from this image.

---

## Instance Type

Instance types define the hardware capacity of the server.

Example:

```
CPU
Memory
Network performance
```

Small instance types are commonly used for testing or lightweight workloads.

---

## Key Pair Authentication

Instead of passwords, servers use cryptographic keys for authentication.

Two components exist:

```
Private key → kept by the user
Public key → stored on the server
```

When connecting:

```
ssh -i private-key.pem user@server-ip
```

The server verifies the key pair and allows access.

---

## Security Groups

Security groups act as virtual firewalls controlling traffic to instances.

Example structure:

```
Internet
   │
   ▼
Security Group
   │
   ▼
Virtual Machine
```

They determine which network ports are allowed.

---

## Data Sources

Terraform can read existing infrastructure using data sources.

Example:

```
data "aws_security_group"
```

Instead of creating a new security group, Terraform references an existing one.

---

# Real World Example

A typical application environment might include:

```
Internet
   │
   ▼
Load Balancer
   │
   ▼
Application Server
   │
   ▼
Database
```

Application servers run as virtual machines inside the cloud environment.  
Terraform automates the creation and configuration of these servers.

---

# Terraform Concepts Practiced

- Infrastructure as Code
- Cloud compute provisioning
- Key pair authentication
- Data sources for existing infrastructure
- Resource dependencies
- Automated infrastructure deployment

---

# Key Takeaways

- Terraform can automate the provisioning of compute resources.
- Virtual machines are launched using machine images and instance types.
- Key pairs enable secure SSH access.
- Data sources allow Terraform to reference existing infrastructure.
- Infrastructure defined in code can be version controlled and reused.