## ✅ Kubernetes Labels and Selectors — Cheat Sheet

### 📌 **What are Labels?**

* **Definition:** Key-value pairs attached to Kubernetes objects (Pods, Deployments, Services, etc.).
* **Purpose:** Organize, categorize, and identify objects for querying and selection.
* **Do not affect object behavior directly.**

**Example:**

```yaml
labels:
  app: nginx
  environment: production
  version: v1
```

---

### 📌 **Label Rules**

| Rule               | Label Key                                           | Label Value                          |
| ------------------ | --------------------------------------------------- | ------------------------------------ |
| Case-sensitive     | ✅ Yes (no uppercase)                                | ✅ Yes (uppercase allowed but avoid)  |
| Allowed characters | lowercase letters, numbers, `-`, `_`, `.`           | letters, numbers, `-`, `_`, `.`, `:` |
| Length             | Max 63 chars (key); prefix up to 253 chars          | Max 63 chars                         |
| Can be empty       | ❌ No                                                | ✅ Yes                                |
| Prefix             | Optional (`myteam.com/`); `kubernetes.io/` reserved | —                                    |

👉 **Check labels:**
`kubectl get <object_type> <object_name> --show-labels`

---

### 📌 **What are Selectors?**

* **Definition:** Queries that match objects based on their labels.
* **Purpose:** Find and operate on groups of resources.
* **Used by:** Services, ReplicaSets, Deployments, `kubectl`.

**Example:**

```yaml
selector:
  matchLabels:
    app: nginx
```

---

### 📌 **Types of Selectors**

✅ **Equality-based:**

```yaml
selector:
  matchLabels:
    app: nginx
```

Matches if `app=nginx`.

✅ **Set-based:**

```yaml
selector:
  matchExpressions:
    - key: environment
      operator: In
      values:
        - dev
        - qa
```

Matches if `environment` is `dev` or `qa`.

---

### 📌 **How They Work Together**

* **Labels:** Attached to objects.
* **Selectors:** Used to find objects with matching labels.
* **Example:**

  * Pods: `labels: app: nginx`
  * Service: `selector: app: nginx` → connects to matching Pods.

---

### 📌 **Practical Commands**

* List Pods with a label:
  `kubectl get pods -l app=nginx`

* Show labels:
  `kubectl get pods --show-labels`

* Apply a label:
  `kubectl label pod nginx-pod tier=frontend`

* Remove a label:
  `kubectl label pod nginx-pod tier-`

---

### 📌 **Common Label Examples**

| Key           | Example Values           |
| ------------- | ------------------------ |
| `release`     | stable, canary           |
| `environment` | dev, qa, production      |
| `tier`        | frontend, backend, cache |
| `app`         | nginx, redis, api        |

---

✅ **One-liner summary:**

> **Labels describe resources. Selectors find and operate on groups of resources with matching labels.**

---

**Use them wisely for flexible, powerful Kubernetes configurations! 🚀✨**
