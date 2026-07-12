# AWS Interview Question: What is an RDS Read Replica?

## Interview Question

**What is a Read Replica in AWS RDS? Why do we use it?**

---

# What is a Read Replica?

A **Read Replica** is a **read-only copy** of an Amazon RDS database.

It is created from a primary (master) database and is used to **offload read traffic** from the primary database, improving application performance and scalability.

The primary database continues to handle **read and write operations**, while the Read Replica handles **read-only queries**.

---

# Example Architecture

```text
                    Users
                      |
               Web Application
                      |
             -------------------
             |                 |
      Read/Write          Read Queries
             |                 |
      Primary RDS       Read Replica
```

- **Primary RDS:** Handles INSERT, UPDATE, DELETE, and SELECT.
- **Read Replica:** Handles only SELECT (read) queries.

---

# Why Do We Use Read Replicas?

Read Replicas help to:

- Improve application performance
- Handle large numbers of read requests
- Reduce the load on the primary database
- Scale applications horizontally
- Improve user response time

---

# Real-Time Example

Suppose you have an **E-commerce Application**.

The application receives:

- Customers browsing products
- Customers searching products
- Customers viewing order history

These operations generate many **read requests**.

Instead of sending all requests to the primary database:

```text
               Web Application
                     |
        -------------------------
        |                       |
   Primary Database       Read Replica
   (Writes + Reads)        (Reads Only)
```

The application sends:

- INSERT/UPDATE/DELETE → Primary RDS
- SELECT Queries → Read Replica

This improves database performance.

---

# How Does Read Replica Work?

1. A write operation occurs on the **Primary Database**.
2. Amazon RDS copies the changes to the Read Replica.
3. Replication is **Asynchronous**.

Example:

```text
Application
      |
      | Write
      |
Primary Database
      |
Asynchronous Replication
      |
Read Replica
```

Because replication is asynchronous, there may be a slight delay before new data appears on the Read Replica.

---

# How to Create a Read Replica

### Step 1

Open the **Amazon RDS Console**.

### Step 2

Select the primary database.

### Step 3

Click **Actions**.

### Step 4

Select **Create Read Replica**.

### Step 5

Choose:

- Region
- Instance class
- Storage
- Multi-AZ (optional)

### Step 6

Click **Create Read Replica**.

AWS automatically configures replication.

---

# Can We Write Data to a Read Replica?

**No.**

A Read Replica is **read-only**.

Allowed:

- SELECT

Not Allowed:

- INSERT
- UPDATE
- DELETE

---

# Can a Read Replica Be Promoted?

**Yes.**

If the primary database fails or if you want an independent database, you can **promote the Read Replica**.

After promotion:

- It becomes a standalone database.
- It accepts both read and write operations.
- Replication with the original primary stops.

---

# Advantages

- Improves read performance
- Handles high read traffic
- Reduces load on the primary database
- Supports horizontal scaling
- Can be promoted for disaster recovery if needed

---

# Limitations

- Replication is asynchronous.
- Slight replication lag is possible.
- Read Replica does not automatically replace the primary database during failure.
- Additional charges apply for replica instances.

---

# Read Replica vs Multi-AZ

| Feature | Read Replica | Multi-AZ |
|----------|--------------|-----------|
| Purpose | Improve read performance | High availability and failover |
| Read Operations | Yes | No (standby is not used for reads) |
| Write Operations | No | No |
| Replication | Asynchronous | Synchronous |
| Automatic Failover | No | Yes |
| Can Be Promoted | Yes | No |

---

# Real-World Scenario

A shopping website receives:

- 20,000 product searches per minute
- 500 orders per minute

Without Read Replica:

```text
Application
      |
Primary Database
```

The primary database handles both reads and writes.

With Read Replica:

```text
              Application
                    |
        ------------------------
        |                      |
 Primary Database        Read Replica
  (Writes)                (Reads)
```

Result:

- Faster product searches
- Better user experience
- Reduced load on the primary database

---

# Interview Answer (2 Minutes)

> "A Read Replica is a read-only copy of an Amazon RDS database used to improve read performance and scale read traffic. The primary database handles both read and write operations, while the Read Replica serves only read requests. Replication from the primary to the replica is asynchronous, so there may be a slight delay before changes appear on the replica. To create a Read Replica, I select the primary RDS instance in the AWS Console and choose 'Create Read Replica.' Read Replicas are commonly used in applications with heavy read traffic, such as e-commerce or reporting systems. If needed, a Read Replica can also be promoted to become a standalone database."

---

# Common Interview Questions

## Q1. Can we write to a Read Replica?

**Answer:**

No. Read Replicas are read-only.

---

## Q2. Is replication synchronous?

**Answer:**

No.

Read Replicas use **asynchronous replication**.

---

## Q3. Can Read Replicas improve write performance?

**Answer:**

No.

They improve **read performance** by offloading read queries.

---

## Q4. Can we create multiple Read Replicas?

**Answer:**

Yes.

A primary RDS instance can have multiple Read Replicas (the supported number depends on the database engine and AWS limits).

---

## Q5. What happens if the primary database fails?

**Answer:**

Read Replicas do **not** fail over automatically.

You must **promote** a Read Replica to become a standalone primary database.

For automatic failover, use **Multi-AZ** deployment.

---

# Key Interview Points

- Read Replica is a **read-only copy** of an RDS database.
- Used to **improve read performance**.
- Uses **asynchronous replication**.
- Primary handles **read and write** operations.
- Replica handles **read-only** queries.
- Can be **promoted** to a standalone database.
- Does **not** provide automatic failover.
- Different from **Multi-AZ**, which is designed for high availability.
```
