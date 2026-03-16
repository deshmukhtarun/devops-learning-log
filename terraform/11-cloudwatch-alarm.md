# Terraform Learning Log – Creating a CloudWatch Alarm

## Overview

In this exercise, Terraform was used to configure monitoring for compute infrastructure.  
A CloudWatch alarm was created to monitor CPU utilization of a virtual machine. Monitoring systems help detect abnormal behavior and allow engineers to respond before performance issues affect users.

This setup automatically triggers an alarm if the server CPU usage exceeds a defined threshold.

---

# Objective

Provision monitoring infrastructure that:

- Tracks CPU utilization of a virtual machine
- Triggers an alarm when CPU usage exceeds **80%**
- Evaluates the metric over a **5-minute period**
- Uses a single evaluation period
- Is fully defined using Infrastructure as Code

---

# Terraform Configuration

```hcl
# Create EC2 instance
resource "aws_instance" "monitor_instance" {
  ami           = "ami-0c101f26f147fa7fd"
  instance_type = "t2.micro"

  tags = {
    Name = "monitor-instance"
  }
}

# Create CloudWatch alarm
resource "aws_cloudwatch_metric_alarm" "cpu_alarm" {
  alarm_name          = "xfusion-alarm"
  comparison_operator = "GreaterThanThreshold"
  evaluation_periods  = 1
  metric_name         = "CPUUtilization"
  namespace           = "AWS/EC2"
  period              = 300
  statistic           = "Average"
  threshold           = 80

  dimensions = {
    InstanceId = aws_instance.monitor_instance.id
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

Apply the configuration:

```
terraform apply
```

---

# Understanding Cloud Monitoring

Monitoring systems track infrastructure performance metrics and trigger alerts when abnormal conditions occur.

Example architecture:

```
Application Server
       │
       ▼
Monitoring System
       │
       ▼
Alarm Triggered
```

This allows operations teams to detect performance issues early.

---

# CPU Utilization Metric

CPU utilization represents how much processing power a server is currently using.

Example ranges:

```
0%   → idle
40%  → moderate workload
80%  → high workload
100% → fully utilized
```

Monitoring CPU helps identify when servers are overloaded.

---

# Alarm Trigger Condition

The alarm is configured with the following condition:

```
CPUUtilization > 80%
```

If the average CPU usage exceeds **80% during the evaluation period**, the alarm changes state.

---

# Evaluation Period

The metric evaluation window is:

```
300 seconds (5 minutes)
```

With **one evaluation period**, the alarm triggers immediately when the threshold is exceeded.

---

# Resource Dependency

Terraform automatically determines the order in which resources are created.

Example dependency:

```
aws_instance.monitor_instance
           ↓
aws_cloudwatch_metric_alarm.cpu_alarm
```

The alarm references the instance ID, so Terraform ensures the instance is created before the alarm.

---

# Real World Example

A web application server may occasionally experience high traffic.

```
Users
  │
  ▼
Application Server
  │
  ▼
Monitoring System
```

If CPU usage exceeds the safe limit, the monitoring system can trigger alerts or automated actions such as scaling additional servers.

---

# Terraform Concepts Practiced

This exercise reinforced several Infrastructure as Code principles:

- infrastructure monitoring
- metric-based alerting
- resource dependency management
- automated operational visibility

---

# Key Takeaways

- Monitoring is essential for maintaining reliable systems.
- CloudWatch alarms track infrastructure metrics and trigger alerts.
- Terraform can automate monitoring configuration alongside infrastructure.
- Infrastructure and monitoring can be managed together using code.