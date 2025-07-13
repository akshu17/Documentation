# ✅ Verified Commands to Debug Kubernetes Service-to-Pod Connectivity

Use the following commands and explanations to ensure your Kubernetes Service is correctly routing traffic to the intended Pods.

---

## 1. 📦 List and Inspect Pods

```bash
kubectl get pods -o wide
```

**Why:**

* Shows Pod IPs, node information, and current status.
* Helps confirm Pods are running and where they are located.

---

## 2. 🌐 Get Basic Service Info

```bash
kubectl get service <service-name>
```

**Why:**

* Displays the ClusterIP, port mappings, and type of the service.

---

## 3. 📝 Detailed Service Inspection

```bash
kubectl describe service <service-name>
```

**Why:**

* Shows the Service's selectors, endpoints, events, and routing details.
* Useful to verify that endpoints are correctly populated.

---

## 4. 🏷️ Check Pod Labels

```bash
kubectl get pods --show-labels
```

**Why:**

* Ensures the Pod labels match the Service’s selector.

---

## 5. 🔍 Validate Service Endpoints

```bash
kubectl get endpoints <service-name>
```

**Why:**

* Confirms which Pods the service is routing traffic to.
* If this is empty, the service is not targeting any pods.

---

## 6. 🛡️ Check Network Policies

```bash
kubectl get networkpolicies
kubectl describe networkpolicy <policy-name>
```

**Why:**

* Ensures that the network policies allow communication between Services and Pods.

---

## 🧠 Summary

These commands help validate:

* Service selector accuracy
* Pod availability and labeling
* Endpoint connectivity
* Network policy openness

Would you like a visual diagram or YAML example to accompany this guide?
