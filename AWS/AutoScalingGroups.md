# AWS Scenario-Based Interview Question

## Question

Suppose you create an **Auto Scaling Group (ASG)** and configure:

- Desired Capacity = 3
- Minimum Capacity = 3
- Maximum Capacity = 6

All 3 EC2 instances are running at **100% CPU utilization**.

- Will the application fail?
- Will AWS automatically launch new instances?

---

# Answer

**It depends on whether a scaling policy is configured.**

Simply creating an Auto Scaling Group with 3 instances **does not automatically launch more instances** when CPU usage reaches 100%.

AWS launches additional instances **only if you configure an Auto Scaling policy** (such as a Target Tracking, Step Scaling, or Simple Scaling policy).

---

# Scenario 1: No Scaling Policy Configured

Configuration:

```text
Minimum = 3
Desired = 3
Maximum = 6
```

Current Status:

```text
EC2-1 → 100% CPU
EC2-2 → 100% CPU
EC2-3 → 100% CPU
```

Result:

- AWS keeps only 3 instances running.
- No new instances are launched.
- Response time increases.
- Users may experience slow performance.
- If the load continues to increase, the application may eventually fail or become unavailable.

---

# Scenario 2: Scaling Policy Configured

Example Target Tracking Policy:

```text
Target CPU Utilization = 60%
Maximum Instances = 6
```

Current Status:

```text
EC2-1 → 100%
EC2-2 → 100%
EC2-3 → 100%
```

CloudWatch detects high CPU usage.

↓

Auto Scaling triggers.

↓

AWS launches additional instances.

```text
EC2-4
EC2-5
```

After the new instances become healthy, the **Application Load Balancer (ALB)** starts routing traffic to them.

Result:

- CPU usage is distributed across more instances.
- Performance improves.
- The application continues running smoothly.

---

# Will the Application Fail?

### If there is NO Scaling Policy

Possibly yes.

Since all instances are overloaded:

- Response times increase.
- Requests may time out.
- Users experience errors.
- Eventually, the application may become unavailable if demand exceeds capacity.

---

### If Scaling Policy Exists

No.

AWS automatically launches additional EC2 instances (up to the configured **Maximum Capacity**) to handle the increased load.

---

# Does AWS Automatically Create New Instances?

**Yes, but only if:**

- An Auto Scaling policy is configured.
- CloudWatch alarms or Target Tracking detect that scaling conditions are met.
- The Auto Scaling Group has not reached its **Maximum Capacity**.

AWS does **not** add instances based only on high CPU unless scaling policies are configured.

---

# Real-Time Example

Configuration:

```text
Minimum Capacity = 2
Desired Capacity = 3
Maximum Capacity = 6

Target CPU = 60%
```

Current Load:

```text
EC2-1 → 95%
EC2-2 → 90%
EC2-3 → 98%
```

CloudWatch reports high CPU.

↓

Auto Scaling launches:

```text
EC2-4
EC2-5
```

ALB distributes traffic across five instances.

Average CPU drops to around 50–60%.

---

# What Happens if an EC2 Instance Fails?

Example:

```text
Desired Capacity = 3

Running:

EC2-1
EC2-2
EC2-3

EC2-2 crashes.
```

Auto Scaling Health Check detects:

```text
EC2-2 = Unhealthy
```

AWS automatically:

- Terminates the unhealthy instance.
- Launches a replacement EC2 instance.
- Registers the new instance with the Load Balancer (after passing health checks).

The desired capacity of **3 instances** is maintained automatically.

---

# Interview Answer (Best Answer)

> "If I create an Auto Scaling Group with a desired capacity of three instances, AWS will initially launch three EC2 instances. If all three instances reach 100% CPU utilization, AWS will **not** automatically launch new instances unless an Auto Scaling policy is configured. If a Target Tracking or Step Scaling policy is in place—for example, scaling out when CPU exceeds 60%—CloudWatch detects the high utilization, and the Auto Scaling Group launches additional instances up to the configured maximum capacity. If no scaling policy exists, the application may become slow or unavailable under heavy load. Also, if one of the EC2 instances becomes unhealthy, the Auto Scaling Group automatically replaces it to maintain the desired capacity."

---

# Key Interview Points

- Auto Scaling Group **maintains the desired number of instances**.
- High CPU **alone does not trigger scaling**.
- A **Scaling Policy** is required.
- **CloudWatch** monitors metrics and triggers scaling actions.
- The **Maximum Capacity** limits how many instances can be launched.
- If an instance becomes **unhealthy**, Auto Scaling automatically replaces it.
- An **Application Load Balancer** distributes traffic to healthy instances.
