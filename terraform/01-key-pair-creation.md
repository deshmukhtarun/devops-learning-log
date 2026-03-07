# Terraform Learning Log – Day 1
## Automating Secure Access with Key Pairs

## Overview

In this exercise, I learned how to automate the creation of a cryptographic key pair using Terraform.  
The public key is registered with a cloud provider, while the private key is securely stored on the local system.

This demonstrates how infrastructure tasks that are normally manual can be automated using Infrastructure as Code (IaC).

---

# Infrastructure as Code (IaC)

Infrastructure as Code means managing infrastructure using code instead of manual configuration.

Instead of creating resources through web consoles or manual commands, we define them in configuration files.

Benefits:

- Automation
- Consistency
- Version control
- Reproducibility
- Easier collaboration

Example idea:

```
Without IaC

Engineer logs into console
Creates infrastructure manually
Configuration may vary each time
```

```
With IaC

Engineer writes configuration file
Terraform creates infrastructure automatically
Same result every time
```

---

# What Was Implemented

This setup performs three main tasks:

1. Generate an RSA key pair
2. Register the public key with the cloud infrastructure
3. Store the private key locally

The process is fully automated using Terraform.

---

# Terraform Configuration Used

The Terraform configuration file used in this exercise:

```hcl
resource "tls_private_key" "key" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

resource "aws_key_pair" "key_pair" {
  key_name   = "example-key"
  public_key = tls_private_key.key.public_key_openssh
}

resource "local_file" "private_key" {
  content         = tls_private_key.key.private_key_pem
  filename        = "/home/user/example-key.pem"
  file_permission = "0400"
}
```

This configuration defines three Terraform resources.

---

# Terraform Resource Breakdown

## 1. Generating the RSA Key

Terraform generates a private key using the TLS provider.

```
resource "tls_private_key"
```

Key details:

- Algorithm: RSA
- Key size: 4096 bits

This produces:

- Public key
- Private key

---

## 2. Creating the Cloud Key Pair

The public key generated earlier is uploaded as a key pair.

```
resource "aws_key_pair"
```

This allows virtual machines to trust the public key and allow secure access.

---

## 3. Saving the Private Key Locally

The private key is written to a local file using:

```
resource "local_file"
```

Important security practice:

Private keys must never be committed to version control systems.

File permissions are restricted to ensure only the owner can read the key.

```
0400
```

Meaning:

```
Owner: read
Group: no access
Others: no access
```

---

# Terraform Execution Workflow

Terraform follows a three-step workflow.

## Step 1 – Initialize

```
terraform init
```

Purpose:

- Download required providers
- Prepare the working directory

---

## Step 2 – Plan

```
terraform plan
```

Purpose:

- Shows what Terraform will create
- Allows reviewing changes before applying

---

## Step 3 – Apply

```
terraform apply
```

Purpose:

- Executes the plan
- Creates the infrastructure resources

---

# Terraform Dependency Flow

Terraform automatically determines resource dependencies.

Execution order:

```
Generate private key
        ↓
Extract public key
        ↓
Create cloud key pair
        ↓
Save private key locally
```

Terraform builds this dependency graph automatically.

---

# Real World DevOps Scenario

In real environments, engineers must access servers securely.

Older systems relied on passwords, which are insecure.

Modern systems use SSH key authentication.

Example connection:

```
ssh -i private-key.pem user@server-ip
```

How authentication works:

```
Private Key → kept by user
Public Key → stored on server
```

When connecting, the server verifies the key pair.

If they match, access is granted.

---

# Why Automation Matters

Imagine provisioning 100 servers manually.

Steps would include:

- Generate keys
- Upload keys
- Configure access
- Repeat multiple times

Using Terraform:

```
terraform apply
```

The entire setup is automated.

This improves reliability and scalability.

---

# Key Takeaways

- Infrastructure can be automated using Terraform.
- RSA key pairs provide secure SSH authentication.
- Terraform resources represent infrastructure components.
- Terraform automatically handles resource dependencies.
- The standard workflow is:

```
init → plan → apply
```

- Sensitive data such as private keys must be handled securely.

---

# Skills Practiced

- Infrastructure as Code fundamentals
- Terraform resource configuration
- Key-based authentication
- Secure credential handling
- Terraform workflow
- Automation of infrastructure tasks