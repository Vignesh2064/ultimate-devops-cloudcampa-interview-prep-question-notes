### 🟢 **Basic EKS Interview Questions**

1. **What is EKS?**

   * AWS EKS is a managed Kubernetes service to run Kubernetes on AWS without installing your own control plane or nodes.

2. **How do you create a Kubernetes cluster in EKS?**

   * Using `eksctl`, AWS Console, or Terraform.
   * Example:

     ```bash
     eksctl create cluster --name my-cluster --region us-west-2 --nodes 3
     ```

3. **What are the core components in an EKS cluster?**

   * Control Plane (Managed by AWS)
   * Worker Nodes (EC2/managed node groups)
   * VPC, Subnets, Security Groups

4. **What is `eksctl`?**

   * A CLI tool to create and manage EKS clusters easily.

5. **Difference between EKS and self-managed Kubernetes?**

   * EKS: AWS manages control plane, auto-scaling, integration.
   * Self-managed: You manage everything yourself (Kubeadm, Kops, etc.).

---

### 🟡 **Intermediate EKS Interview Questions**

6. **How do you connect `kubectl` to an EKS cluster?**

   * Using AWS CLI:

     ```bash
     aws eks update-kubeconfig --name <cluster_name> --region <region>
     ```

7. **How does EKS manage authentication?**

   * IAM roles and AWS IAM Authenticator.
   * `aws-auth` ConfigMap used to map IAM roles to Kubernetes RBAC.

8. **What is an EKS Node Group?**

   * A group of EC2 instances in your cluster with a common configuration.

9. **Can you use Fargate with EKS?**

   * Yes, for serverless pod deployment (no EC2 nodes required).

10. **How does autoscaling work in EKS?**

    * Cluster Autoscaler (for nodes)
    * Horizontal Pod Autoscaler (for pods)
    * Karpenter (next-gen autoscaler by AWS)

---

### 🔴 **Advanced EKS Interview Questions**

11. **How do you implement multi-AZ EKS architecture?**

    * Spread nodes across subnets in different AZs.
    * Enable high availability by setting subnet mappings in `eksctl` or Terraform.

12. **How do you secure communication in EKS?**

    * Use TLS, security groups, NACLs, and mutual TLS for internal services.
    * RBAC for authorization.

13. **How to handle logging and monitoring in EKS?**

    * Use CloudWatch Container Insights, Prometheus, Grafana.
    * Fluentd/Fluentbit for log forwarding.

14. **How do you upgrade your EKS cluster?**

    * Step 1: Upgrade control plane via Console or CLI.
    * Step 2: Upgrade node groups (create new AMIs, drain old nodes).

15. **How do you use service meshes like Istio in EKS?**

    * Install Istio via Helm.
    * Inject sidecars for services and configure mesh policies.

---

### 💼 **Scenario-Based & Real-World EKS Questions**

16. **Scenario: How would you deploy an app in 4 environments (dev, qa, stage, prod) using EKS and Helm?**

* Use separate namespaces or clusters.
* Helm values files per environment.
* Example structure:

  ```
  helm install app -f values-dev.yaml
  helm install app -f values-prod.yaml
  ```

17. **Scenario: Pods are in `Pending` state. How do you troubleshoot?**

* Check `kubectl describe pod`.
* Look for node resource issues.
* Check if node groups are in correct subnets.

18. **Scenario: Node group not scaling even with HPA active. What to check?**

* Verify Cluster Autoscaler is deployed and has IAM permissions.
* Ensure instance limits not hit.
* Check taints and labels match pods.

19. **Scenario: EKS API access is denied for a new user. Why?**

* IAM user not added to `aws-auth` ConfigMap.
* RBAC roles not mapped.

20. **Scenario: You need zero-downtime deployment in EKS. How?**

* Use `RollingUpdate` strategy in Deployment spec.
* Use readiness/liveness probes.

---

### ⚙️ **EKS Terraform Block Example**

```hcl
resource "aws_eks_cluster" "example" {
  name     = "my-eks-cluster"
  role_arn = aws_iam_role.eks_cluster.arn

  vpc_config {
    subnet_ids = [aws_subnet.public1.id, aws_subnet.public2.id]
  }

  depends_on = [aws_iam_role_policy_attachment.eks_cluster_AmazonEKSClusterPolicy]
}
```

---
