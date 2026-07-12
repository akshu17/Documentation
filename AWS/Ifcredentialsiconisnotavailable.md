# AWS Interview Question

## Question

**If the "Security Credentials" option (or credentials icon) is not available, what will you do?**

---

# Answer

The first step is to identify **why the option is missing**. In AWS, missing credential options are usually caused by **permissions**, **IAM policies**, or because you're signed in with an IAM user instead of the root user.

I would troubleshoot the issue as follows.

---

# Step 1: Verify Which Account I'm Using

Check whether I'm logged in as:

- Root User
- IAM User
- IAM Role (for example, AWS IAM Identity Center/SSO)

Some credential options are available only to specific account types.

---

# Step 2: Check IAM Permissions

If I'm using an IAM user, I verify that I have the required permissions.

Example permissions:

```text
iam:GetUser
iam:ListAccessKeys
iam:CreateAccessKey
iam:DeleteAccessKey
iam:UpdateAccessKey
```

Without these permissions, the Security Credentials page may not display the expected options.

---

# Step 3: Check IAM Policies

Review the attached:

- IAM Policies
- Permission Boundaries
- Organizations SCPs (Service Control Policies)

These policies may explicitly deny IAM credential management.

Example:

```json
{
  "Effect": "Deny",
  "Action": "iam:*",
  "Resource": "*"
}
```

If such a policy exists, I would contact the AWS administrator.

---

# Step 4: Check AWS Organizations

If the account belongs to an AWS Organization, the administrator may have restricted IAM operations using **Service Control Policies (SCPs)**.

In that case, I would verify whether an SCP is preventing credential management.

---

# Step 5: Use IAM Roles Instead of Access Keys

If the goal is for an EC2 instance or Lambda function to access AWS services, I would avoid creating access keys altogether.

Instead, I would:

- Create an IAM Role.
- Attach the role to the EC2 instance or Lambda function.
- Let AWS automatically provide temporary credentials.

This is the recommended AWS best practice.

---

# Step 6: Contact the Administrator

If the option is still unavailable due to organizational security policies, I would raise a request with the AWS administrator to:

- Grant the required IAM permissions.
- Create an IAM role.
- Generate access keys if absolutely necessary.

---

# Real-World Scenario

Suppose you're a DevOps Engineer.

You log in as an IAM user and cannot find **Create Access Key**.

Investigation shows:

```text
IAM User
      |
No iam:CreateAccessKey Permission
      |
Security Credentials Option Missing
```

Solution:

The AWS administrator updates the IAM policy to grant the required permissions (or, preferably, provides an IAM role if access keys are not needed).

---

# Best Practices

- Use IAM Roles instead of long-term access keys.
- Grant only the minimum required IAM permissions.
- Enable MFA for IAM users.
- Avoid using the root account for daily work.
- Follow the Principle of Least Privilege.

---

# Interview Answer (Best Answer)

> "If the Security Credentials option is not available, I first verify whether I'm logged in as the root user, an IAM user, or through IAM Identity Center. Then I check whether my IAM user has the necessary permissions, such as `iam:CreateAccessKey` and `iam:ListAccessKeys`. I also review IAM policies, permission boundaries, and any Service Control Policies in AWS Organizations that might be restricting access. If the application needs AWS access, I prefer using an IAM Role instead of creating access keys. If the restriction is intentional, I would contact the AWS administrator to request the required permissions."

---

# Common Follow-up Questions

## Q1. Why might the Security Credentials option be missing?

**Answer:**

Possible reasons include:

- Insufficient IAM permissions
- Explicit deny in IAM policies
- Service Control Policies (SCPs)
- Using an IAM role or IAM Identity Center where long-term access keys are restricted
- Organization security policies

---

## Q2. Is creating an Access Key the recommended approach?

**Answer:**

No.

For AWS services like EC2, Lambda, ECS, and EKS, the recommended approach is to use **IAM Roles**, which provide temporary credentials.

---

## Q3. What if you don't have permission to create access keys?

**Answer:**

I would request the required permissions from the AWS administrator or use an IAM Role if appropriate.

---

# Key Interview Points

- Verify the account type (Root, IAM User, IAM Role).
- Check IAM permissions and attached policies.
- Review Permission Boundaries and SCPs.
- Prefer IAM Roles over Access Keys.
- Follow the Principle of Least Privilege.
- Contact the AWS administrator if additional permissions are required.
