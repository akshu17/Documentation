# AWS Interview Question: Cross-Region Replication (CRR)

## Interview Question

**What is Cross-Region Replication (CRR)? How do you configure it? Will it copy objects automatically?**

---

# What is Cross-Region Replication (CRR)?

**Cross-Region Replication (CRR)** is an Amazon S3 feature that automatically replicates objects from a **source bucket** in one AWS Region to a **destination bucket** in another AWS Region.

It is mainly used for:

- Disaster Recovery (DR)
- High Availability
- Compliance requirements
- Low latency for global users
- Backup across AWS Regions

---

# Example

```text
              Upload Object
                    |
        Source Bucket (Mumbai)
         Region: ap-south-1
                    |
                    |  Cross-Region Replication
                    |
        Destination Bucket (Singapore)
       Region: ap-southeast-1
```

Whenever a new object is uploaded to the source bucket, Amazon S3 automatically replicates it to the destination bucket.

---

# Prerequisites

Before enabling CRR, ensure:

- Both source and destination buckets exist.
- Buckets are in **different AWS Regions**.
- **Versioning is enabled** on both buckets.
- An IAM role with replication permissions is available.

---

# How to Configure Cross-Region Replication

## Step 1: Create Two S3 Buckets

Example:

**Source Bucket**

- Region: Mumbai (`ap-south-1`)

**Destination Bucket**

- Region: Singapore (`ap-southeast-1`)

> The buckets must be in different AWS Regions.

---

## Step 2: Enable Versioning

Enable versioning on both buckets.

### Why?

Cross-Region Replication works only when **Versioning** is enabled.

Without versioning, replication cannot be configured.

---

## Step 3: Create an IAM Role

Amazon S3 requires permission to replicate objects.

The IAM role should have permissions to:

- Read objects from the source bucket
- Replicate objects to the destination bucket

AWS can create this role automatically during setup if you choose that option.

---

## Step 4: Configure the Replication Rule

1. Open the **Amazon S3 Console**.
2. Select the **source bucket**.
3. Go to the **Management** tab.
4. Choose **Replication Rules**.
5. Click **Create Replication Rule**.
6. Select:
   - Source bucket
   - Destination bucket
   - IAM Role
7. Save the rule.

Replication is now enabled.

---

# Will It Copy Automatically?

## Yes, for New Objects

After CRR is enabled:

```text
Upload image.jpg
        |
Source Bucket
        |
Automatic Replication
        |
Destination Bucket
```

New objects uploaded to the source bucket are automatically copied to the destination bucket.

---

## Existing Objects

**No. Existing objects are NOT copied automatically.**

Example:

Before enabling CRR:

```text
image1.jpg
backup.zip
logs.tar
```

After enabling CRR:

These existing files **remain only in the source bucket**.

To replicate existing objects, use:

- **S3 Batch Replication**
- Or manually copy the objects

---

# What Gets Replicated?

By default, CRR replicates:

- New objects
- Object metadata
- Object tags
- Object ACLs (if enabled)
- Delete markers (optional)
- Encrypted objects (when configured correctly)

---

# What Does Not Replicate Automatically?

- Existing objects (unless Batch Replication is used)
- Objects uploaded before CRR was configured

---

# Real-World Example

Suppose your production application runs in Mumbai.

```text
             Users
               |
      Application (Mumbai)
               |
        S3 Source Bucket
               |
      Cross-Region Replication
               |
       S3 Backup Bucket
          (Singapore)
```

If the Mumbai Region experiences an outage, the replicated data in Singapore can be used for disaster recovery.

---

# Advantages of Cross-Region Replication

- Disaster recovery
- High availability
- Compliance with regional data requirements
- Reduced latency for users in different geographic regions
- Automatic replication of new objects

---

# Limitations

- Existing objects are not automatically replicated.
- Versioning must be enabled.
- Replication may incur additional storage and data transfer costs.
- Replication is asynchronous, so there can be a slight delay before objects appear in the destination bucket.

---

# Best Practices

- Enable Versioning on both buckets.
- Encrypt data using SSE-KMS if required.
- Monitor replication status using Amazon CloudWatch.
- Enable replication metrics for visibility.
- Use S3 Batch Replication to replicate existing objects if needed.

---

# Interview Answer (2–3 Minutes)

> "Amazon S3 Cross-Region Replication (CRR) automatically replicates objects from a source bucket in one AWS Region to a destination bucket in another AWS Region. It is commonly used for disaster recovery, compliance, and improving data availability. To configure CRR, I first create source and destination buckets in different AWS Regions, enable Versioning on both buckets, create or use an IAM role with replication permissions, and configure a replication rule on the source bucket. Once CRR is enabled, any new objects uploaded to the source bucket are automatically replicated to the destination bucket. However, existing objects are not copied automatically. To replicate existing data, I use S3 Batch Replication."

---

# Common Interview Questions

## Q1. Is replication automatic?

**Answer:**
Yes. After CRR is configured, **newly uploaded objects** are automatically replicated.

---

## Q2. Are existing objects copied automatically?

**Answer:**
No. Existing objects are not replicated automatically. Use **S3 Batch Replication** to copy them.

---

## Q3. What is mandatory before enabling CRR?

**Answer:**

- Versioning enabled on both buckets
- Buckets in different AWS Regions
- IAM role with replication permissions
- Replication rule configured on the source bucket

---

## Q4. Can CRR replicate encrypted objects?

**Answer:**
Yes. Objects encrypted with SSE-S3 or SSE-KMS can be replicated if the required permissions and KMS key access are configured.

---

## Q5. What is the difference between CRR and SRR?

| Feature | Cross-Region Replication (CRR) | Same-Region Replication (SRR) |
|---------|---------------------------------|-------------------------------|
| Destination | Different AWS Region | Same AWS Region |
| Purpose | Disaster recovery, compliance | Data redundancy, log aggregation, compliance within a Region |
