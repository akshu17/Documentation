# How You Will Set Up a VPC (AWS Interview Answer)

## Interview Question

**How would you set up a VPC for an application?**

## Step 1: Create the VPC

Create a VPC with a CIDR block such as `10.0.0.0/16`.

**Why?** - Provides an isolated private network. - Gives enough IP
addresses for future growth. - Can be divided into multiple subnets.

------------------------------------------------------------------------

## Step 2: Create Availability Zones

Deploy resources across at least **two Availability Zones (AZs)**.

**Why?** - High availability - Fault tolerance

------------------------------------------------------------------------

## Step 3: Create Subnets

### Public Subnets

Used for: - Application Load Balancer (ALB) - NAT Gateway

Example: - `10.0.1.0/24` - `10.0.2.0/24`

### Private Application Subnets

Used for: - EC2 - ECS - EKS

Example: - `10.0.11.0/24` - `10.0.12.0/24`

### Private Database Subnets

Used for: - Amazon RDS - Amazon Aurora

Example: - `10.0.21.0/24` - `10.0.22.0/24`

------------------------------------------------------------------------

## Step 4: Attach an Internet Gateway

Attach an Internet Gateway (IGW) to the VPC so resources in public
subnets can access the internet.

------------------------------------------------------------------------

## Step 5: Create a NAT Gateway

Deploy a NAT Gateway in a public subnet.

Purpose: - Allow private instances to download updates. - Prevent
inbound internet access to private instances.

------------------------------------------------------------------------

## Step 6: Configure Route Tables

### Public Route Table

-   Local
-   `0.0.0.0/0 → Internet Gateway`

### Private Application Route Table

-   Local
-   `0.0.0.0/0 → NAT Gateway`

### Database Route Table

-   Local only

------------------------------------------------------------------------

## Step 7: Configure Security Groups

-   ALB: Allow HTTP/HTTPS from the internet.
-   EC2: Allow traffic only from the ALB.
-   RDS: Allow database access only from the EC2 Security Group.

------------------------------------------------------------------------

## Step 8: Configure Network ACLs

Use subnet-level stateless firewall rules for additional protection.

------------------------------------------------------------------------

## Step 9: Deploy the Application

Deploy EC2 instances behind an Application Load Balancer.

------------------------------------------------------------------------

## Step 10: Deploy the Database

Deploy Amazon RDS in private database subnets with Multi-AZ enabled.

------------------------------------------------------------------------

## Step 11: Enable Monitoring

-   Amazon CloudWatch
-   AWS CloudTrail
-   VPC Flow Logs

------------------------------------------------------------------------

## Step 12: Configure VPC Endpoints

Create VPC Endpoints for Amazon S3, Systems Manager, CloudWatch, and
other AWS services to keep traffic on the AWS network.

------------------------------------------------------------------------

# Architecture

``` text
                         Internet
                             |
                     Internet Gateway
                             |
                --------------------------
                |                        |
        Public Subnet AZ-1      Public Subnet AZ-2
                |                        |
       Application Load Balancer (ALB)
                |
        --------------------------
        |                        |
   Private App AZ-1        Private App AZ-2
        |                        |
      EC2 Instance          EC2 Instance
        |                        |
        --------------------------
                |
        Private Database Subnets
                |
      Amazon RDS (Multi-AZ)
```

# Interview Answer

> For a production application, I start by creating a VPC with a CIDR
> block such as `10.0.0.0/16`. I then create public, private
> application, and private database subnets across at least two
> Availability Zones to ensure high availability. I attach an Internet
> Gateway to the VPC, deploy a NAT Gateway in a public subnet for
> outbound internet access from private instances, configure route
> tables, Security Groups, and Network ACLs, deploy an Application Load
> Balancer in the public subnets, application servers in private
> subnets, and Amazon RDS in private database subnets with Multi-AZ
> enabled. Finally, I enable CloudWatch, CloudTrail, VPC Flow Logs, and
> VPC Endpoints for monitoring, auditing, and secure connectivity.
