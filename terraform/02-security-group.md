# Terraform Learning Log – Security Group Configuration

## Overview

In this exercise, I practiced using Terraform to create and configure a network security group in a cloud environment.  
Security groups act as virtual firewalls that control inbound and outbound traffic to cloud resources such as virtual machines.

Using Infrastructure as Code (IaC), the security group and its rules were defined declaratively and provisioned automatically using Terraform.

---

# Objective

Create a security group with rules that allow:

- HTTP traffic on port **80**
- SSH access on port **22**

Both rules allow connections from any IP address.

---

# Terraform Configuration

```hcl
resource "aws_security_group" "app_sg" {
  name        = "xfusion-sg"
  description = "Security group for Nautilus App Servers"

  ingress {
    description = "Allow HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "Allow SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

---

# Terraform Commands Used

Initialize the Terraform working directory:

```
terraform init
```

Preview the infrastructure changes:

```
terraform plan
```

Create the infrastructure:

```
terraform apply
```

---

# Understanding Security Groups

A security group acts like a **firewall for cloud resources**.

It controls which network traffic is allowed to reach the resource.

Example architecture:

```
Internet
   │
   ▼
Security Group (Firewall Rules)
   │
   ▼
Virtual Machine / Application Server
```

If traffic matches an allowed rule, it can reach the server.  
Otherwise, it is blocked.

---

# Inbound Rules Explained

Two inbound rules were created.

## HTTP Rule

```
Port: 80
Protocol: TCP
Source: 0.0.0.0/0
```

Meaning:

Allow web traffic from any IP address.

This is required for applications that serve web pages or APIs.

Example request:

```
User → Browser → http://server-ip
```

---

## SSH Rule

```
Port: 22
Protocol: TCP
Source: 0.0.0.0/0
```

Meaning:

Allow remote login access to the server.

Example:

```
ssh user@server-ip
```

This is commonly used by engineers to manage servers remotely.

---

# CIDR Block Explanation

The rule uses the CIDR block:

```
0.0.0.0/0
```

This means:

Allow traffic from **any IP address on the internet**.

While this is acceptable for learning environments, production environments usually restrict SSH access to trusted IP ranges.

Example:

```
203.0.113.10/32
```

---

# Default Security Behavior

Security groups follow a **default deny model**.

Meaning:

```
All traffic is blocked by default
```

Only traffic that matches defined rules is allowed.

In this configuration, only the following traffic is permitted:

```
HTTP (80)
SSH (22)
```

All other ports remain blocked.

---

# Real World Example

Consider a web application running on a cloud server.

Users need to access the application through their browser:

```
HTTP → Port 80
```

Engineers need secure access to maintain the server:

```
SSH → Port 22
```

The security group ensures:

- Users can access the web application
- Engineers can manage the server
- All other traffic remains blocked

---

# Terraform Concepts Practiced

This exercise helped reinforce several core Infrastructure as Code concepts:

- Cloud networking fundamentals
- Security groups as virtual firewalls
- Terraform resource configuration
- Declarative infrastructure definitions
- Infrastructure automation

---

# Key Takeaways

- Security groups act as network firewalls for cloud resources.
- Terraform can automate the creation and configuration of network security rules.
- The standard Terraform workflow is:

```
init → plan → apply
```

- Infrastructure defined in code can be version controlled, reviewed, and reused.