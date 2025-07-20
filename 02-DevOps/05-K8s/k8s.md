## 🚀 Kubernetes Interview Questions & Answers (With Troubleshooting)

---

### 🟢 **Basic (Conceptual) – Must-Know**

#### 1. **What is Kubernetes and why do we use it?**

**Answer:** Kubernetes is a container orchestration platform that automates deployment, scaling, and management of containerized applications.

#### 2. **What are Pods?**

**Answer:** The smallest deployable unit in K8s. A Pod can contain one or more containers sharing storage/network.

#### 3. **What is a ReplicaSet vs Deployment?**

**Answer:**

* **ReplicaSet** ensures the specified number of pod replicas are running.
* **Deployment** manages ReplicaSets and allows rolling updates and rollbacks.

#### 4. **Difference between ConfigMap and Secret?**

**Answer:**

* **ConfigMap** stores non-sensitive data in key-value pairs.
* **Secret** stores sensitive data (like passwords) base64 encoded.

#### 5. **What is a Service?**

**Answer:** A Kubernetes object that exposes a set of Pods as a network service. Types: ClusterIP, NodePort, LoadBalancer, ExternalName.

---

### 🟡 **Intermediate – Practical Usage**

#### 6. **How does Kubernetes handle storage?**

**Answer:**
Using Volumes, Persistent Volumes (PV), and Persistent Volume Claims (PVC). Supports dynamic provisioning via StorageClass.

#### 7. **What is a DaemonSet?**

**Answer:** Ensures a Pod runs on **every node** (or selected nodes). Example: Fluentd, Prometheus node exporter.

#### 8. **What is a StatefulSet? When do you use it?**

**Answer:**
For stateful apps like databases. Provides stable identities and persistent storage (e.g., for Cassandra, MongoDB).

#### 9. **Explain Liveness and Readiness Probes.**

**Answer:**

* **Liveness probe** checks if the app is alive; restarts if fails.
* **Readiness probe** checks if app is ready to serve traffic.

#### 10. **How do you roll back a deployment?**

```bash
kubectl rollout undo deployment <deployment-name>
```

---

### 🔴 **Advanced – Architecture & Internals**

#### 11. **How does the Kubernetes Scheduler work?**

**Answer:**
The Scheduler assigns pods to nodes based on constraints like CPU/memory availability, node selectors, affinity rules, taints/tolerations.

#### 12. **What is etcd?**

**Answer:**
A key-value store for all Kubernetes cluster data (state, configurations). It's the **single source of truth**.

#### 13. **Difference between Job and CronJob?**

* **Job**: One-time execution.
* **CronJob**: Scheduled job (e.g., backups every night).

#### 14. **How do you secure a Kubernetes cluster?**

* Role-Based Access Control (RBAC)
* Network Policies
* TLS everywhere
* PodSecurityPolicies (deprecated), use **OPA/Gatekeeper** or **Kyverno**

#### 15. **What is a ServiceAccount?**

**Answer:**
Provides an identity for processes in pods to interact with the Kubernetes API.

---

### ⚠️ **Troubleshooting & Real-Time Scenarios**

#### 16. **Pod is in `CrashLoopBackOff` — how do you debug?**

**Steps:**

```bash
kubectl describe pod <pod-name>   # check Events
kubectl logs <pod-name>           # view container logs
kubectl get events                # check error reasons (OOMKilled, ImagePullError)
```

**Common causes:**

* Misconfigured startup command
* App crash
* Failed readiness probe

---

#### 17. **Pod is stuck in `Pending` state — reasons?**

**Common reasons:**

* No nodes with sufficient resources
* NodeSelector or Taints blocking scheduling
* PVC not bound

Check:

```bash
kubectl describe pod <pod-name>
```

---

#### 18. **PVC is not getting bound — how to fix?**

* Check if the StorageClass exists
* Ensure volume size matches the provisioner

```bash
kubectl get pvc
kubectl describe pvc <name>
```

---

#### 19. **How do you troubleshoot failed deployments?**

```bash
kubectl rollout status deployment <name>
kubectl describe deployment <name>
kubectl get rs
kubectl get events
```

Check container image errors, init container issues, resource limits, etc.

---

#### 20. **Node is NotReady – how do you fix?**

```bash
kubectl describe node <node-name>
kubectl get nodes
journalctl -u kubelet        # check kubelet logs
systemctl status docker      # check Docker/containerd status
```

---

### 🔐 **Security & Best Practices – For Architect/Senior Roles**

* Use RBAC and restrict access
* Enforce Pod Security Standards (Kyverno/OPA)
* Use resource limits/requests for all pods
* Use **Network Policies** to isolate traffic
* Restrict image pull sources, use signed images
* Scan images for CVEs (Trivy, Clair)

---

You're right — to **crack high-paying Kubernetes (K8s) interviews**, especially targeting **senior or architect-level roles (e.g., 40 LPA+ in India)**, you'll need a **combination of in-depth, hands-on, scenario-based, troubleshooting-focused** questions and answers. Here's how to **level up** from what you've already covered:

---

## 🔹 Additional **Kubernetes Scenario-Based & Advanced Interview Questions** with Answers

### ✅ 1. **A pod is stuck in `CrashLoopBackOff`. How will you troubleshoot it?**

**Answer:**

* Check pod logs:
  `kubectl logs <pod-name> --previous`
* Describe pod:
  `kubectl describe pod <pod-name>`
  → Look for `Events` like failed mounts, missing secrets, bad probes, etc.
* Check init containers and probes.
* Validate config files, secrets, or image issues.
* Use `kubectl get events --sort-by=.metadata.creationTimestamp` for chronological event analysis.

---

### ✅ 2. **You deployed a Service but can't access it via NodePort. How do you debug it?**

**Answer:**

* Check if the service exists:
  `kubectl get svc <service-name>`
* Confirm node IP and port:
  `kubectl describe svc <service-name>`
* Validate if `targetPort` matches the container's actual port.
* Check firewall rules and security groups (if on cloud).
* Run `curl <node-ip>:<nodePort>` from a VM outside cluster.

---

### ✅ 3. **How to roll back a failed deployment?**

**Answer:**

* View revision history:
  `kubectl rollout history deployment <deployment-name>`
* Roll back:
  `kubectl rollout undo deployment <deployment-name>`

---

### ✅ 4. **How do you debug when a pod is not scheduled (in `Pending`)?**

**Answer:**

* `kubectl describe pod <pod-name>` → Check `Events`:

  * Not enough CPU/memory
  * No matching nodeSelector, taints/tolerations
  * Node affinity issues
* Use `kubectl get nodes -o wide` to compare available resources.

---

### ✅ 5. **How do you handle application versioning during blue-green or canary deployment?**

**Answer:**

* Use **labels and selectors** for different versions.
* Canary: Route small traffic to a new version using `weight` in ingress.
* Blue-Green: Maintain 2 deployments, shift the service selector.
* Tools: Argo Rollouts, Flagger.

---

### ✅ 6. **Troubleshooting DNS issues inside the cluster?**

**Answer:**

* Run a debug pod with `dnsutils`:

  ```bash
  kubectl run -it --rm dns-test --image=busybox --restart=Never -- sh
  nslookup <service-name>
  ```
* Check `coredns` logs:
  `kubectl logs -n kube-system <coredns-pod>`
* Verify kube-dns service:
  `kubectl get svc -n kube-system`

---

### ✅ 7. **A node is `NotReady`. What steps do you take?**

**Answer:**

* `kubectl describe node <node-name>` → Review conditions and messages.
* Check kubelet logs on the node.
* Use `kubectl get events` for cluster-wide errors.
* Possible issues:

  * Disk pressure
  * Network not ready
  * Kubelet crashed or stuck

---

### ✅ 8. **How do you monitor and scale workloads automatically in Kubernetes?**

**Answer:**

* **Horizontal Pod Autoscaler**:
  `kubectl autoscale deployment <name> --cpu-percent=50 --min=2 --max=5`
* Integrate **custom metrics** with Prometheus + Adapter.
* Use **KEDA** for event-based scaling (SQS, Kafka, etc.).

---

### ✅ 9. **What’s the difference between readinessProbe and livenessProbe?**

| Probe     | Purpose                                |
| --------- | -------------------------------------- |
| Liveness  | Restarts pod if app is stuck or dead   |
| Readiness | Controls if pod should receive traffic |

**Tip:** Misconfigured probes are a major cause of CrashLoopBackOff.

---

### ✅ 10. **Kubernetes storage scenario: PVC is not getting bound. What next?**

**Answer:**

* Check StorageClass availability:
  `kubectl get sc`
* Validate PVC and PV specs match:

  * `accessModes`, `storage`, `storageClassName`
* Use:
  `kubectl describe pvc <name>`

---

### ✅ 11. **What happens when you delete a deployment vs a pod?**

**Answer:**

* **Pod**: If part of Deployment/ReplicaSet, it gets recreated.
* **Deployment**: All pods and the ReplicaSet will be deleted.

---

### ✅ 12. **How do you implement security best practices in K8s?**

**Answer:**

* Use **RBAC** to control access.
* **PodSecurityContext**: Run as non-root, drop capabilities.
* Use **network policies**.
* Scan images with tools like Trivy.
* Integrate with **Kyverno**, **OPA/Gatekeeper** for policy enforcement.

---

### ✅ 13. **Have you implemented K8s in production? Describe a real-world problem you solved.**

**Answer Template:**

> “Yes, in one project, our app pods were frequently restarting. Upon investigation, we found the readiness probes were misconfigured with very short timeout and delay values. We modified them, increased `initialDelaySeconds`, and stabilized the deployments.”

---
