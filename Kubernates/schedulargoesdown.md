 What is the Scheduler?

The Kubernetes Scheduler is the control-plane component that:
Watches for unscheduled Pods
Decides which Node each Pod should run on
Binds the Pod to a Node by updating its spec
📌 If the Scheduler goes down:

What happens	Explanation
✅ Running Pods	Keep running normally! — once scheduled, the Scheduler is no longer involved.
✅ Cluster services (API, etcd)	Keep working (assuming other control-plane components are healthy).
⚠️ New Pods	Will not be scheduled! — they stay in Pending state because there is no Scheduler to assign them to Nodes.
⚠️ Rescheduling on failure	If a Node dies and its Pods need rescheduling on other Nodes — that won’t happen automatically because the Scheduler is down.
📌 Key point:

The Scheduler does not run or manage containers directly — it only assigns Pods to Nodes.
The Kubelet on each Node actually runs the containers.

✅ So, existing workloads stay up and serve traffic.

❌ New workloads or reschedules won’t happen.

📌 Example:

Scenario	What you see
Scheduler down	kubectl get pods shows existing Pods are Running
New Deployment	Pods stay in Pending
Node failure	Pods on dead Node do not move to healthy Nodes
📌 How to recover:

✅ Highly Available Scheduler:

Run multiple Scheduler replicas (HA control plane).
✅ Restart Scheduler:

Usually, it’s a Pod itself (if using kubeadm or managed cluster) — so it restarts automatically.
✅ Check health:

kubectl get componentstatuses
kubectl get pods -n kube-system
