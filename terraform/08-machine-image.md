# Terraform Learning Log – Creating a Machine Image from an Instance

## Overview

In this exercise, Terraform was used to create a reusable machine image from an existing virtual machine.  
Machine images allow identical instances to be launched quickly without repeating configuration steps.

---

## Terraform Configuration

```hcl
resource "aws_instance" "ec2" {
  ami           = "ami-0c101f26f147fa7fd"
  instance_type = "t2.micro"

  vpc_security_group_ids = [
    "sg-d8cec8485e8d6529f"
  ]

  tags = {
    Name = "devops-ec2"
  }
}

resource "aws_ami_from_instance" "ec2_ami" {
  name               = "devops-ec2-ami"
  source_instance_id = aws_instance.ec2.id
}
```

---

## Terraform Workflow

Initialize Terraform:

```
terraform init
```

Preview infrastructure changes:

```
terraform plan
```

Apply configuration:

```
terraform apply
```

---

## Understanding Machine Images

A machine image is a snapshot of a server that includes:

- operating system
- installed software
- system configuration

Once an image is created, new instances can be launched from it.

Example workflow:

```
Configured Server
      │
      ▼
Create Machine Image
      │
      ▼
Launch Identical Servers
```

---

## Terraform Resource Dependency

Terraform automatically determines execution order.

Example:

```
aws_instance.ec2
       ↓
aws_ami_from_instance.ec2_ami
```

Because the AMI references the instance ID, Terraform ensures the instance is created first.

---

## Real World Usage

Machine images are commonly used in production infrastructure to ensure consistency.

Example workflow used in DevOps pipelines:

```
Base Server
   │
Install Application
   │
Create Image
   │
Deploy Multiple Servers from Image
```

This approach is part of **immutable infrastructure practices**.

---

## Key Takeaways

- Machine images allow rapid deployment of identical servers.
- Terraform can automate image creation from existing instances.
- Resource references create automatic dependency management.
- Infrastructure as Code ensures repeatable and consistent environments.