# 🐳 Dangling Image in Docker

## 🔍 What is a Dangling Image?

A **dangling image** is an image in Docker that:

* Is an **intermediate image layer**.
* **Has no name or tag** (its tag appears as `<none>`).
* Is **not used** by any container.
* Is usually **left behind** after rebuilding or updating images.

---

## 🧠 Why Do Dangling Images Exist?

When you build or rebuild Docker images:

* Docker creates intermediate layers to optimize builds.
* If you rebuild an image, the new layers may no longer reference the old ones.
* These **unreferenced layers become dangling images**.

---

## 🔧 How to See Dangling Images

Use the following command:

```bash
docker images -f dangling=true
```

Example output:

```plaintext
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
<none>              <none>              abc123456789        2 days ago          130MB
```

---

## 🧹 How to Remove Dangling Images

To remove them and free up disk space:

```bash
docker image prune
```

To skip confirmation:

```bash
docker image prune -f
```

---

## ⚠️ Important Notes

* Dangling images **are not always useless** — they may be reused internally by Docker.
* If you're not actively using them, it's usually **safe to prune** them.

---

Would you like a visual diagram or example showing how dangling images are created and removed?
