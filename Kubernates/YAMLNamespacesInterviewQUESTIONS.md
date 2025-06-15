## YAML & Namespaces - Interview Questions and Answers

### ✅ YAML Syntax Questions

**1️⃣ What is YAML and what is it used for?**
YAML (YAML Ain’t Markup Language) is a human-readable data serialization format used for configuration files and data exchange.

---

**2️⃣ Explain the basic syntax rules of YAML.**

* Use spaces for indentation (no tabs).
* Lists use `-` (dash).
* Key-value pairs use `:` (colon).
* Strings don’t need quotes unless special characters are used.
* Comments use `#`.

**Example:**

```yaml
name: John Doe
age: 30
hobbies:
  - reading
  - cycling
```

---

**3️⃣ How do you define nested objects in YAML?**
Use indentation:

```yaml
person:
  name: Alice
  address:
    street: 123 Main St
    city: Wonderland
```

---

**4️⃣ How are lists defined in YAML?**

```yaml
fruits:
  - apple
  - banana
  - mango
```

Or inline: `fruits: [apple, banana, mango]`

---

**5️⃣ How do you write multi-line strings in YAML?**
`|` preserves line breaks, `>` folds lines:

```yaml
description: |
  This is a multi-line
  string with line breaks.

summary: >
  This is a multi-line
  string folded into one line.
```

---

**6️⃣ How do you include comments in a YAML file?**
Use `#`:

```yaml
# This is a comment
name: Bob  # Inline comment
```

---

### ✅ Namespaces Questions (Kubernetes Context)

**1️⃣ What is a namespace and why is it used?**
A namespace is a logical partition to group and isolate resources. In Kubernetes, it helps organize environments, apply quotas, and avoid name conflicts.

---

**2️⃣ How do you create a namespace in Kubernetes using YAML?**

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
```

---

**3️⃣ How do you apply a resource to a specific namespace?**
Add `namespace` in `metadata`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  namespace: my-namespace
```

Or use CLI:

```bash
kubectl apply -f pod.yaml -n my-namespace
```

---

**4️⃣ What happens if you don’t specify a namespace?**
It is created in the `default` namespace.

---

**5️⃣ How do you list all namespaces?**

```bash
kubectl get namespaces
```

---

**6️⃣ How can namespaces help with resource management and security?**

* Apply quotas (limit CPU, memory).
* Use RBAC for access control.
* Use network policies to restrict traffic.

---

### ✅ Mock Interview Quick Practice

**Q1.** What does YAML stand for?
**A1.** YAML Ain’t Markup Language.

**Q2.** How does YAML handle data structure?
**A2.** Indentation for nesting, `:` for key-values, `-` for lists.

**Q3.** Define a list of users with name and age:

```yaml
users:
  - name: Alice
    age: 28
  - name: Bob
    age: 32
```

**Q4.** How to write a comment?
**A4.** `# This is a comment`

**Q5.** Multi-line string preserving line breaks:

```yaml
text: |
  Line 1
  Line 2
```

**Q6.** What is a namespace?
**A6.** A way to isolate resources and manage them.

**Q7.** Default namespace?
**A7.** `default`

**Q8.** List namespaces:
**A8.** `kubectl get namespaces`

**Q9.** YAML to create `dev` namespace:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

**Q10.** Apply a Pod to `dev` namespace:

```bash
kubectl apply -f pod.yaml -n dev
```

**Q11.** Two benefits of namespaces:
**A11.** Isolation and resource limits/quotas.

---

✅ **Tip:** Practice 5 random questions in 1 minute each to build confidence!
