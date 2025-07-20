
## 🚀 ArgoCD Interview Questions & Answers

---

### 🟢 **Basic Level Questions**

#### 1. **What is ArgoCD?**

**Answer:**
ArgoCD is a declarative GitOps continuous delivery tool for Kubernetes. It monitors Git repositories for Kubernetes manifest changes and automatically applies them to the cluster.

---

#### 2. **What are the core components of ArgoCD?**

**Answer:**

* `argocd-server`: UI, CLI, and API access
* `argocd-repo-server`: Clones Git repo and renders manifests
* `argocd-application-controller`: Reconciles desired and live states
* `argocd-dex-server`: Authentication (OIDC, LDAP, etc.)

---

#### 3. **What is an ArgoCD Application?**

**Answer:**
An `Application` is a Kubernetes custom resource that tells ArgoCD:

* Where the source (Git) is
* What tool to use (Helm, Kustomize, plain YAML)
* Where to deploy it (namespace/cluster)
* Sync policy (manual or automatic)

---

#### 4. **How do you install ArgoCD?**

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

---

### 🟡 **Intermediate Questions**

#### 5. **How does ArgoCD handle multi-environment deployments (dev/stage/prod)?**

**Answer:**
By using:

* Separate `Application` CRs for each env
* Helm/Kustomize overlays
* Branch-based or folder-based Git structure
  Example folders:

  ```
  ├── dev/
  ├── staging/
  ├── prod/
  ```

---

#### 6. **How does ArgoCD sync changes from Git?**

**Answer:**

* It compares the Git manifest (desired state) with the live state in the cluster.
* Sync is triggered:

  * Manually (via UI/CLI)
  * Automatically (auto-sync enabled)

---

#### 7. **What are ArgoCD sync policies?**

**Answer:**

* **Manual**: You manually trigger the sync.
* **Automated**:

  ```yaml
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
  ```

  * `prune`: delete resources not in Git
  * `selfHeal`: if drift occurs, auto fix it

---

#### 8. **How to configure authentication in ArgoCD?**

**Answer:**

* Dex-based: OIDC, LDAP
* SSO: GitHub, Google, Okta
* RBAC defined in `argocd-rbac-cm`

---

#### 9. **What is App of Apps pattern in ArgoCD?**

**Answer:**
An "App of Apps" is a parent ArgoCD application that deploys multiple child applications by pointing to their `Application` CRs in a single Git folder.

---

### 🔴 **Advanced Questions**

#### 10. **How to use Helm with ArgoCD for multi-environment deployment?**

**Folder Structure:**

```
helm-chart/
├── Chart.yaml
├── values/
│   ├── dev.yaml
│   ├── stage.yaml
│   └── prod.yaml
```

**Application YAML (dev):**

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: myapp-dev
spec:
  project: default
  source:
    repoURL: https://github.com/vignesh/myapp
    targetRevision: main
    path: helm-chart
    helm:
      valueFiles:
        - values/dev.yaml
  destination:
    server: https://kubernetes.default.svc
    namespace: dev
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

Repeat the same with `stage.yaml`, `prod.yaml`, etc.

---

#### 11. **How does ArgoCD handle Helm dependencies?**

**Answer:**
ArgoCD uses the `argocd-repo-server` to run `helm dependency build` internally when rendering charts. Make sure the `Chart.yaml` has correct dependencies listed.

---

#### 12. **How to manage secrets securely in ArgoCD?**

**Answer:**

* Use **Sealed Secrets**
* Use **SOPS** with Helm/Kustomize
* Integrate **Vault** with external secret manager
* Don't store plaintext secrets in Git

---

#### 13. **How to debug sync errors in ArgoCD?**

**Answer:**

* Use CLI:

  ```bash
  argocd app logs myapp
  argocd app get myapp
  ```
* Check:

  * Events: `kubectl describe application <name>`
  * Repo-server logs
  * Application Controller logs

---

#### 14. **How to do blue-green or canary deployments in ArgoCD?**

**Answer:**

* Use Argo Rollouts + ArgoCD
* Replace Deployment with Rollout kind
* Add canary steps:

```yaml
spec:
  strategy:
    canary:
      steps:
        - setWeight: 20
        - pause: {}
```

---

### 🧠 **Real-Time Scenario Questions**

#### 15. **Scenario:** “You pushed a faulty Helm value to prod. ArgoCD deployed it and broke prod. How do you fix it?”

**Answer:**

* Roll back via Git (revert commit)
* ArgoCD detects Git change → syncs automatically
* Use `argocd app history <app>` and `app rollback <id>` if needed

---

#### 16. **Scenario:** “One of your ArgoCD apps is stuck in `OutOfSync` despite matching Git state.”

**Answer:**

* Check for:

  * Drift: Resources deleted manually
  * Errors in `argocd app diff`
  * Cluster connection issues
* Use `argocd app refresh <app>` to force re-evaluation

---

#### 17. **Scenario:** “Your dev and prod ArgoCD apps are using same chart but different configs. How do you structure it?”

**Answer:**

* Use `values/dev.yaml`, `values/prod.yaml`
* Single Helm chart → parametrize via `Application` resource
* GitOps-friendly branching or folder-based config

---

### 🛠️ Bonus: ArgoCD CLI Cheatsheet

```bash
argocd login <host> --username admin
argocd app list
argocd app get myapp
argocd app sync myapp
argocd app delete myapp
argocd app history myapp
argocd app rollback myapp <revision>
argocd app diff myapp
```

---

### ✅ **Must-Know Advanced ArgoCD Interview Topics (with CRDs, Helm, Multi-Env)**

#### 1. **CRDs in ArgoCD**

* **Q:** What CRDs are created when you install ArgoCD?

* **A:** ArgoCD creates several CRDs like:

  * `applications.argoproj.io`
  * `appprojects.argoproj.io`
  * These CRDs are used to define and manage GitOps resources declaratively.

* **Q:** How does `Application` CRD work in ArgoCD?

* **A:** The `Application` CRD is the core ArgoCD object that defines:

  * Git repo source
  * Path in repo
  * Target cluster & namespace
  * Sync policies (auto/manual)
  * Helm/Kustomize settings

#### 2. **ArgoCD with Helm in Multi-Environment Setup**

* **Q:** How do you manage `dev`, `qa`, `staging`, and `prod` using ArgoCD and Helm?

* **A:**

  * Use a **single Helm chart** with separate `values-dev.yaml`, `values-qa.yaml`, etc.
  * In your `Application` YAML:

    ```yaml
    spec:
      source:
        helm:
          valueFiles:
            - values-dev.yaml
      destination:
        namespace: dev
        server: https://kubernetes.default.svc
    ```

* **Q:** How do you structure Git repositories for multiple environments?

* **A:** Either:

  * **Mono repo**: One repo with folders for `env/dev`, `env/prod`, etc.
  * **Multi repo**: One repo per environment, referenced via different Argo Applications.

#### 3. **Important ArgoCD CRD Interview Scenarios**

* **Q:** Can you sync a Helm-based Application on changes in Git only?

* **A:** Yes. Enable auto-sync with:

  ```yaml
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
  ```

  This syncs any Git change without manual action.

* **Q:** How do you restrict developers from deploying to production using ArgoCD?

* **A:** Use `AppProject` CRDs with RBAC:

  * Define allowed `sourceRepos`, `destinations`, and `clusterResourceWhitelist`.

#### 4. **ArgoCD Troubleshooting**

* **Q:** ArgoCD app stuck in “OutOfSync” — how do you fix?

* **A:**

  * Check logs of `argocd-repo-server` and `argocd-application-controller`
  * Validate if Helm values are mismatched or drifted
  * Try manual sync and check diff

* **Q:** How to debug Helm template rendering in ArgoCD?

* **A:** Use:

  ```bash
  helm template ./path --values values-prod.yaml
  ```

  Compare rendered output with what's deployed.

---

### 📌 Summary — Is This Enough?

To **crack 30LPA+ interviews**, ensure you cover:

* ✅ CRD deep dive (`Application`, `AppProject`)
* ✅ Multi-env setup using Helm & ArgoCD
* ✅ GitOps flow: push to Git → ArgoCD deploys → sync & self-heal
* ✅ RBAC & permission strategies
* ✅ Troubleshooting real issues (OutOfSync, failed syncs, Helm bugs)

---




