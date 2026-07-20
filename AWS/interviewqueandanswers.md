# AWS DevOps Engineer Interview Questions and Answers

This file contains concise interview-ready AWS DevOps questions and answers.

## 1. What is AWS?
AWS is Amazon's cloud platform providing compute, storage, networking, databases, security, monitoring, and DevOps services on a pay-as-you-go model.

## 2. What is a VPC?
A logically isolated virtual network where AWS resources are deployed.

## 3. VPC Components
- VPC
- CIDR
- Public/Private Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs
- Elastic IP
- VPC Endpoints

## 4. Security Group vs NACL
- Security Group: Stateful, instance level, allow only.
- NACL: Stateless, subnet level, allow and deny.

## 5. EC2
Virtual server in AWS.

## 6. Auto Scaling
Automatically adds/removes EC2 instances based on demand.

## 7. S3
Object storage service.

## 8. Make S3 Bucket Private
- Enable Block Public Access
- Remove public bucket policies
- Remove public ACLs
- Use IAM roles/policies.

## 9. Cross-Region Replication
Replicates new objects to another region. Versioning required.

## 10. Read Replica
Read-only copy of an RDS database used for read scaling.

## 11. Lambda
Serverless compute service.

## 12. IAM
Identity and Access Management service.

## 13. Credential Management
- IAM Roles
- Secrets Manager
- Parameter Store
- STS
- Never hardcode credentials.

## 14. CloudWatch
Monitoring service.

## 15. CloudTrail
Auditing service for API activity.
