# Create a Markdown file for the troubleshooting scenario: traffic goes to only one Pod

content = """
# 🐳 Kubernetes Troubleshooting: Traffic Goes to Only One Pod

## ✅ Scenario
- You created a Deployment.
- It created **2 Pods**.
- Both Pods show as **Running**.
- But your Service sends traffic to only one Pod.

---

## ✅ Possible Causes

| Cause | Explanation |
| --- | --- |
| **1️⃣ Readiness probe failing** | If a Pod's readiness probe fails, it won't receive traffic even if `Running`. |
| **2️⃣ Missing Endpoints** | The Service Endpoints may list only one Pod IP. |
| **3️⃣ Network Policy or firewall** | Could block traffic to a specific Pod. |
| **4️⃣ Pod unhealthy** | Pod may be Running but app inside may be broken. |
| **5️⃣ Session Affinity** | Service uses `sessionAffinity: ClientIP`, so same client always talks to the same Pod. |
| **6️⃣ Local traffic policy** | Service is configured to send traffic only to Pods on the same Node (`externalTrafficPolicy: Local`). |

---

## ✅ How to Troubleshoot

### 1️⃣ Check Pod readiness
```bash
kubectl get pods -o wide
kubectl describe pod <pod-name>
