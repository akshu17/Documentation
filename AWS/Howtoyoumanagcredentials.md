# AWS Interview Question: How Do You Manage Credentials in AWS?

## Interview Question

**How do you manage credentials in AWS?**

---

# Answer

Managing credentials securely is one of the most important AWS security best practices. Instead of hardcoding usernames, passwords, or access keys in applications, AWS provides services such as **IAM Roles**, **AWS Secrets Manager**, and **AWS Systems Manager Parameter Store** to securely manage credentials.

---

# 1. IAM Roles (Best Practice)

The preferred way to provide AWS service permissions is by using **IAM Roles** instead of storing AWS Access Keys.

### Example

```text
          EC2 Instance
                |
         IAM Role Attached
                |
      Access Amazon S3 Bucket
```

The EC2 instance automatically receives temporary security credentials from the IAM Role.

### Benefits

- No Access Keys to manage
- Temporary credentials
- Automatic credential rotation
- More secure

---

# 2. AWS Secrets Manager

Use **AWS Secrets Manager** to store sensitive information like:

- Database usernames
- Database passwords
- API Keys
- OAuth Tokens
- Third-party credentials

Example:

```text
Application
      |
AWS Secrets Manager
      |
Database Password
```

Instead of storing passwords in the application code, the application retrieves them securely from Secrets Manager.

### Benefits

- Encrypted using AWS KMS
- Automatic secret rotation
- Fine-grained IAM access control
- Audit access using CloudTrail

---

# 3. AWS Systems Manager Parameter Store

Parameter Store securely stores:

- Configuration values
- Database connection strings
- API URLs
- Environment variables
- Passwords (SecureString)

Example:

```text
Application
      |
Parameter Store
      |
Database URL
```

### Difference from Secrets Manager

| Parameter Store | Secrets Manager |
|-----------------|-----------------|
| Stores configuration and secrets | Designed specifically for secrets |
| Supports SecureString | Supports automatic secret rotation |
| Lower cost | More advanced features |

---

# 4. IAM Users (For Humans)

IAM Users are created for:

- Developers
- Administrators
- DevOps Engineers

Each user receives:

- Username
- Password (Console Access)
- Access Keys (if CLI/API access is required)

### Best Practices

- Enable Multi-Factor Authentication (MFA)
- Grant least-privilege permissions
- Rotate Access Keys regularly
- Avoid using the root account

---

# 5. Temporary Credentials (STS)

AWS Security Token Service (STS) provides temporary credentials.

Example:

```text
Developer
      |
Assume IAM Role
      |
Temporary Credentials
```

Used for:

- Cross-account access
- Federated users
- Temporary application access

---

# 6. AWS KMS (Key Management Service)

AWS KMS manages encryption keys.

Used to encrypt:

- Secrets Manager secrets
- S3 objects
- EBS volumes
- RDS databases
- Parameter Store SecureStrings

---

# What Should You Avoid?

❌ Hardcoding credentials in:

```java
password = "Admin123"
```

or

```python
AWS_ACCESS_KEY_ID = "AKIAxxxxxxxx"
AWS_SECRET_ACCESS_KEY = "xxxxxxxx"
```

This is insecure because anyone with access to the code can retrieve the credentials.

---

# Real-World Example

Suppose you have a Java application running on an EC2 instance.

```text
          EC2 Instance
                |
         IAM Role Attached
                |
        AWS Secrets Manager
                |
        Database Credentials
                |
          Amazon RDS
```

- The EC2 instance uses an IAM Role to access Secrets Manager.
- Secrets Manager stores the database username and password.
- The application retrieves the credentials securely at runtime.
- No credentials are stored in the source code.

---

# Best Practices

- Use IAM Roles instead of Access Keys for AWS services.
- Store secrets in AWS Secrets Manager.
- Use Parameter Store for configuration values.
- Enable MFA for IAM Users.
- Rotate secrets and access keys regularly.
- Follow the Principle of Least Privilege.
- Never commit credentials to Git repositories.
- Encrypt secrets using AWS KMS.

---

# Interview Answer (2 Minutes)

> "I manage credentials in AWS by following security best practices. For AWS services like EC2 and Lambda, I use IAM Roles instead of hardcoding access keys. For sensitive information such as database passwords, API keys, and tokens, I use AWS Secrets Manager, which securely stores and encrypts secrets using AWS KMS and supports automatic rotation. For application configuration values, I use AWS Systems Manager Parameter Store. IAM Users are created only for human users, with MFA enabled and least-privilege permissions. I also avoid storing credentials in source code or Git repositories and use temporary credentials through AWS STS whenever possible."

---

# Common Interview Questions

## Q1. Where do you store database passwords?

**Answer:**

AWS Secrets Manager.

---

## Q2. Do you store AWS Access Keys inside your application?

**Answer:**

No.

I use IAM Roles to provide temporary credentials.

---

## Q3. What is the difference between Secrets Manager and Parameter Store?

| Secrets Manager | Parameter Store |
|-----------------|-----------------|
| Stores secrets | Stores configuration values and secrets |
| Automatic secret rotation | No automatic rotation |
| Better for passwords and API keys | Better for configuration parameters |

---

## Q4. Why are IAM Roles better than Access Keys?

**Answer:**

- Temporary credentials
- Automatic rotation
- No hardcoded secrets
- More secure
- Easier to manage

---

## Q5. What service encrypts your secrets?

**Answer:**

AWS Key Management Service (AWS KMS).

---

# Key Interview Points

- Use **IAM Roles** for AWS service authentication.
- Store passwords and API keys in **AWS Secrets Manager**.
- Store configuration values in **AWS Systems Manager Parameter Store**.
- Encrypt secrets with **AWS KMS**.
- Use **STS** for temporary credentials.
- Enable **MFA** for IAM Users.
- Never hardcode credentials in code or store them in Git repositories.
- Follow the **Principle of Least Privilege**.
