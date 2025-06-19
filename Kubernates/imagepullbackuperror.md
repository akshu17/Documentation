# 📦 Kubernetes `ImagePullBackOff` Error Cheat Sheet

## ✅ What is `ImagePullBackOff`?

`ImagePullBackOff` means Kubernetes tried to pull the image for your Pod but failed, and is now backing off (waiting and retrying).

---

## 🔑 Common Causes

| Reason                                    | Description                                    |
| ----------------------------------------- | ---------------------------------------------- |
| **Wrong image name or tag**               | Typo in image name or non-existing tag.        |
| **Image does not exist in registry**      | Image was deleted or never pushed.             |
| **Private registry, missing credentials** | Kubernetes needs a secret to authenticate.     |
| **Node has no network**                   | Node can't reach the registry.                 |
| **Rate limiting**                         | Too many pulls from Docker Hub can hit limits. |

---

## 🔍 How to Troubleshoot

1️⃣ **Describe the Pod to see details:**

```bash
kubectl describe pod <pod-name>
```

Check the `Events` section for specific pull errors.

---

2️⃣ **Verify the image manually:**

```bash
docker pull <image-name>
```

If this fails, fix the image name/tag.

---

3️⃣ **Check if registry is private:**

If yes, create an image pull secret:

```bash
kubectl create secret docker-registry my-registry-secret \
  --docker-username=<username> \
  --docker-password=<password> \
  --docker-email=<email> \
  --docker-server=<registry-url>
```

Reference it in your Deployment or Pod:

```yaml
spec:
  imagePullSecrets:
    - name: my-registry-secret
```

---

4️⃣ **Check node network:**

Ensure the Node has access to the internet and DNS resolution is working.

```bash
kubectl get nodes -o wide
kubectl describe node <node-name>
```

---

## 🗝️ Summary

✅ `ImagePullBackOff` = Pod can't pull image → fix typo, permissions, or network → Pod will auto-retry and recover!

---

## 📌 Related Commands

| Command                           | Purpose                           |
| --------------------------------- | --------------------------------- |
| `kubectl describe pod <pod-name>` | Check detailed events & errors.   |
| `kubectl get pods`                | See Pod status at a glance.       |
| `kubectl get events`              | Check cluster-wide recent events. |
| `docker pull <image>`             | Test image pull locally.          |

---

**Fix the cause → Kubernetes will pull the image and run the Pod automatically.** 🚀
