# AWS Interview Question: Where Will You Set the Route Table?

## Question

**Where will you set the Route Table?**

---

## Short Answer

A **Route Table is associated with a subnet**, **not** with an EC2 instance or directly with the VPC.

---

# Explanation

When you create a VPC, AWS automatically creates a **Main Route Table**.

You can:

- Use the Main Route Table
- Create Custom Route Tables

These Route Tables are then **associated with one or more subnets**.

---

# Example

```text
VPC (10.0.0.0/16)

├── Public Subnet (10.0.1.0/24)
│
│── Associated with
│
└── Public Route Table

├── Private App Subnet (10.0.11.0/24)
│
│── Associated with
│
└── Private Route Table

└── Private DB Subnet (10.0.21.0/24)
     │
     │── Associated with
     │
     └── Database Route Table
```

Every subnet uses its associated Route Table.

---

# Public Route Table

Associated with:

- Public Subnet 1
- Public Subnet 2

Routes

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 0.0.0.0/0 | Internet Gateway |

### Purpose

Allows internet access for:

- Application Load Balancer
- NAT Gateway
- Bastion Host

---

# Private Application Route Table

Associated with:

- Private App Subnet 1
- Private App Subnet 2

Routes

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 0.0.0.0/0 | NAT Gateway |

### Purpose

Allows private EC2 instances to:

- Download updates
- Install packages
- Access AWS APIs

The internet **cannot** initiate connections to these instances.

---

# Database Route Table

Associated with:

- Database Subnet 1
- Database Subnet 2

Routes

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |

No Internet Gateway.

No NAT Gateway.

This keeps the database isolated from the internet.

---

# AWS Console Steps

1. Open the VPC Console.
2. Click **Route Tables**.
3. Create a Route Table.
4. Add Routes.
5. Open **Subnet Associations**.
6. Associate the Route Table with the required subnet.

---

# Production Architecture

```text
                  Internet
                      |
              Internet Gateway
                      |
             Public Route Table
                      |
                Public Subnet
                      |
          Application Load Balancer
                      |
-------------------------------------------------
                      |
            Private Route Table
                      |
          Private Application Subnet
                      |
                  EC2 Instances
                      |
-------------------------------------------------
                      |
            Database Route Table
                      |
             Private Database Subnet
                      |
                 Amazon RDS
```

---

# Why Associate Route Tables with Subnets?

Because every resource inside a subnet automatically follows that subnet's Route Table.

Example:

- EC2 in Public Subnet → Uses Public Route Table
- EC2 in Private Subnet → Uses Private Route Table
- RDS in Database Subnet → Uses Database Route Table

You **cannot** attach a Route Table directly to an EC2 instance.

---

# Interview Answer

> "A Route Table is configured within a VPC and associated with subnets, not with EC2 instances. In a production environment, I create separate Route Tables for public, private application, and database subnets. The public Route Table has a default route (`0.0.0.0/0`) pointing to the Internet Gateway. The private application Route Table points to the NAT Gateway for outbound internet access. The database Route Table contains only the local route, ensuring the database remains isolated from the internet."

---

# Common Follow-up Question

### Can one Route Table be associated with multiple subnets?

**Answer:** Yes.

A single Route Table can be associated with multiple subnets if they require the same routing behavior.

Example:

- Public Subnet AZ-1
- Public Subnet AZ-2

Both can use the same Public Route Table.
