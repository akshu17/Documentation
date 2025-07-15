# 🛂 What is Kubernetes Admission Control?

Kubernetes Admission Controllers are plugins that intercept requests to the Kubernetes API server **after** authentication and authorization, but **before** the object is persisted in etcd. They allow you to validate, mutate, or reject requests based on custom or predefined policies.

---

## 🔄 Kubernetes Request Lifecycle

1. **Authentication** – Verifies identity.
2. **Authorization** – Checks permissions.
3. **Admission Control** ✅ – Mutate or validate request.
4. **etcd Persistence** – Saves the object.

---

## 🎯 Types of Admission Controllers

### 1. **Validating Admission Controllers**

* Inspect the object and can reject it.
* Example: Reject pods without resource limits.

### 2. **Mutating Admission Controllers**

* Modify or add fields to an object.
* Example: Inject sidecar containers or default labels.

---

## ⚙️ Common Built-in Admission Controllers

| Name                         | Purpose                                |
| ---------------------------- | -------------------------------------- |
| `NamespaceLifecycle`         | Prevents use of terminated namespaces  |
| `LimitRanger`                | Enforces resource limits               |
| `ServiceAccount`             | Automatically assigns service accounts |
| `PodSecurity`                | Enforces security policies             |
| `MutatingAdmissionWebhook`   | Allows external mutation               |
| `ValidatingAdmissionWebhook` | Allows external validation             |

---

## 🧰 Webhook-Based Admission Controllers

* Define custom logic using webhooks.
* Kubernetes sends admission requests to external HTTP services.

```yaml
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingWebhookConfiguration
...
```

---

## 🔐 Use Cases

* Enforcing image policies (e.g., no `latest` tag)
* Injecting monitoring/logging sidecars
* Validating required labels or annotations
* Blocking privileged containers

---

## ✅ Summary

* Admission controllers enforce policies at the API level.
* They help secure, validate, and customize object creation and updates.
* Use both built-in and custom webhook controllers to extend Kubernetes functionality.

Would you like an example webhook configuration or setup guide?
