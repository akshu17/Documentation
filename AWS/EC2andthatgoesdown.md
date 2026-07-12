# AWS Interview Question: An EC2 Instance Goes Down – How Do You Resolve It?

## Interview Question

**You are working on an EC2 instance, and suddenly it goes down. How would you troubleshoot and resolve the issue?**

---

# Answer

The first thing I do is identify whether the issue is related to:

- The EC2 instance itself
- The Operating System
- Network connectivity
- Storage
- Application
- AWS infrastructure

I troubleshoot step by step instead of immediately rebooting the instance.

---

# Step 1: Check EC2 Instance Status

Go to:

**AWS Console → EC2 → Instances**

Verify the instance state.

Possible states:

- Running
- Stopped
- Stopping
- Pending
- Terminated

If the instance is **Stopped**, I start it.

If it's **Terminated**, it cannot be restarted, so I launch a new instance from an AMI or restore from backup.

---

# Step 2: Check Status Checks

AWS provides two health checks.

### System Status Check

Checks AWS infrastructure:

- Hardware
- Power
- Network
- Hypervisor

If this fails, it's an AWS infrastructure issue.

### Instance Status Check

Checks the guest operating system:

- OS boot
- File system
- Memory
- Network configuration

If this fails, it's an issue inside the EC2 instance.

Example:

```text
EC2 Instance

System Status  → Passed

Instance Status → Failed
```

This indicates the OS needs troubleshooting.

---

# Step 3: Verify Security Groups

Ensure the Security Group allows the required traffic.

For Linux:

```text
SSH → Port 22
```

For Windows:

```text
RDP → Port 3389
```

For Web Server:

```text
HTTP → Port 80
HTTPS → Port 443
```

---

# Step 4: Check Network ACLs

Ensure Network ACLs are not blocking traffic.

Verify:

- Inbound rules
- Outbound rules

---

# Step 5: Verify Route Table

Check that the subnet route table contains the correct routes.

For a public subnet:

```text
0.0.0.0/0 → Internet Gateway
```

For a private subnet:

```text
0.0.0.0/0 → NAT Gateway
```

---

# Step 6: Verify Public IP

For internet access:

The instance should have:

- Public IP
or
- Elastic IP

Without a public IP, SSH or browser access from the internet will not work.

---

# Step 7: Connect to the Instance

If SSH works:

```bash
ssh -i my-key.pem ec2-user@Public-IP
```

Check:

```bash
top
```

or

```bash
htop
```

Verify:

- CPU usage
- Memory usage

---

# Step 8: Check Disk Space

Run:

```bash
df -h
```

If disk usage is 100%, applications may stop working.

Free space by deleting unnecessary files or increase the EBS volume size.

---

# Step 9: Check Application Status

If EC2 is running but the application is unavailable:

Check services.

Example:

```bash
sudo systemctl status nginx
```

or

```bash
sudo systemctl status httpd
```

Restart if needed:

```bash
sudo systemctl restart nginx
```

---

# Step 10: Check Logs

Linux logs:

```bash
/var/log/messages

/var/log/syslog

/var/log/nginx/error.log

journalctl
```

These logs help identify:

- Application errors
- Boot issues
- Permission issues

---

# Step 11: Check CloudWatch

Review:

- CPU Utilization
- Memory (if CloudWatch Agent is installed)
- Disk usage
- Network traffic

CloudWatch alarms may indicate what caused the issue.

---

# Step 12: Recover the Instance

If the instance is unhealthy:

Possible actions:

- Reboot the instance
- Stop and Start the instance
- Recover the instance (if supported)
- Replace the instance using an Auto Scaling Group
- Restore from an AMI or EBS Snapshot

---

# If Auto Scaling Is Enabled

Suppose:

```text
Desired Capacity = 3
```

Running:

```text
EC2-1

EC2-2

EC2-3
```

EC2-2 becomes unhealthy.

Auto Scaling detects:

```text
Health Check Failed
```

AWS automatically:

- Terminates EC2-2
- Launches a new EC2 instance
- Registers it with the Load Balancer

The application continues running without manual intervention.

---

# Real-World Scenario

A production web server suddenly becomes unavailable.

Investigation:

- EC2 State → Running
- Status Checks → Passed
- SSH → Successful
- Disk Usage → 100%

Cause:

Application stopped because the disk was full.

Solution:

- Delete unnecessary log files
- Extend the EBS volume
- Restart the application
- Monitor disk usage using CloudWatch

Application is restored.

---

# Interview Answer (2–3 Minutes)

> "If an EC2 instance goes down, I first check whether the issue is with the instance state or AWS infrastructure. I verify the EC2 status checks to determine whether it's a System Status Check failure or an Instance Status Check failure. Then I review the Security Groups, Network ACLs, Route Tables, and ensure the instance has the correct public or Elastic IP if internet access is required. If I can connect via SSH, I check CPU, memory, disk space, and application services, and review system logs for errors. I also use CloudWatch metrics to identify resource bottlenecks. If the instance cannot be recovered, I reboot or replace it. In production environments, I use an Auto Scaling Group so unhealthy instances are automatically replaced, minimizing downtime."

---

# Common Interview Questions

## Q1. What is the difference between System Status Check and Instance Status Check?

**Answer:**

| System Status Check | Instance Status Check |
|----------------------|-----------------------|
| AWS infrastructure issue | Operating System issue |
| Hypervisor, hardware, network | OS boot, file system, memory |

---

## Q2. What if SSH is not working?

**Answer:**

Check:

- Security Group
- Network ACL
- Route Table
- Public IP/Elastic IP
- SSH service
- Instance reachability

---

## Q3. What if the instance is terminated?

**Answer:**

A terminated instance cannot be restarted.

Launch a new instance using:

- AMI
- Auto Scaling Group
- Infrastructure as Code (CloudFormation/Terraform)

---

## Q4. What if the root EBS volume is full?

**Answer:**

- Delete unnecessary files
- Extend the EBS volume
- Resize the file system
- Restart the application if needed

---

# Key Interview Points

- Check EC2 instance state.
- Review System and Instance Status Checks.
- Verify Security Groups, NACLs, and Route Tables.
- Check CPU, memory, and disk usage.
- Review application and system logs.
- Use CloudWatch for monitoring.
- Replace unhealthy instances using Auto Scaling.
- Restore from AMI or EBS snapshots if necessary.
