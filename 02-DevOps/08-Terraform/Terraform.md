## ✅ **Terraform Interview Questions and Answers**

---

## 🔹 **Basic Level (0–2 years)**

### 1. ❓ What is Terraform?

**✅ Answer:**
Terraform is an open-source **Infrastructure as Code (IaC)** tool by HashiCorp used to provision, manage, and version cloud infrastructure using a declarative configuration language.

---

### 2. ❓ What is the difference between Terraform and CloudFormation?

**✅ Answer:**

| Feature    | Terraform       | CloudFormation      |
| ---------- | --------------- | ------------------- |
| Vendor     | Multi-cloud     | AWS-only            |
| Language   | HCL             | JSON/YAML           |
| State Mgmt | Maintains state | Managed by AWS      |
| Modules    | Yes             | Limited reusability |

---

### 3. ❓ What are providers in Terraform?

**✅ Answer:**
Providers are plugins that interact with APIs of cloud platforms (like AWS, Azure, GCP). Each provider is configured in the `.tf` file.

```hcl
provider "aws" {
  region = "us-east-1"
}
```

---

### 4. ❓ What is the use of `terraform init`?

**✅ Answer:**
Initializes the working directory by:

* Downloading provider plugins
* Preparing the backend (for remote state)

---

### 5. ❓ Difference between `terraform apply` and `terraform plan`?

* `terraform plan`: Shows **what will change** without applying.
* `terraform apply`: **Executes the changes** defined in the plan.

---

### 6. ❓ What is `terraform state`?

**✅ Answer:**
Terraform state keeps track of the infrastructure resources it manages. It can be stored:

* Locally (default)
* Remotely (S3, etcd, Terraform Cloud)

---

### 7. ❓ What are input variables?

**✅ Answer:**
They allow parameterizing Terraform configurations.

```hcl
variable "region" {
  default = "us-east-1"
}
```

---

## 🔸 **Intermediate Level (2–5 years)**

### 8. ❓ How do you manage multiple environments (dev, prod)?

**✅ Answer:**

* Use workspaces (`terraform workspace new dev`)
* Separate directories with separate `*.tfvars` files
* Use separate state files per environment

---

### 9. ❓ What is a Terraform module?

**✅ Answer:**
A reusable collection of `.tf` files used across projects.

```hcl
module "vpc" {
  source = "./modules/vpc"
  cidr_block = "10.0.0.0/16"
}
```

---

### 10. ❓ What are data sources in Terraform?

**✅ Answer:**
Data sources allow Terraform to **read existing infrastructure** (not create).

```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
  owners = ["099720109477"]
  filter {
    name = "name"
    values = ["ubuntu/images/*"]
  }
}
```

---

### 11. ❓ How do you manage sensitive data like secrets?

**✅ Answer:**

* Use `sensitive = true` for variables
* Store secrets in Vault or AWS SSM
* Avoid committing `.tfstate` to Git
* Use remote backends with encryption

---

### 12. ❓ What is a backend? What types are available?

**✅ Answer:**
Backend stores Terraform state remotely (e.g., S3, Azure Blob, Terraform Cloud). It also handles state locking and team collaboration.

---

### 13. ❓ How do you handle resource dependencies?

**✅ Answer:**
Terraform automatically infers dependencies. But you can use `depends_on` for explicit control.

```hcl
resource "aws_instance" "web" {
  depends_on = [aws_vpc.main]
}
```

---

## 🔺 **Advanced / Real-time Scenarios (5–10+ years)**

### 14. ❓ How do you manage Terraform at scale in teams?

**✅ Answer:**

* Use remote state backends with locking
* Use modules for reusability
* Store Terraform code in Git
* Implement CI/CD pipelines (GitHub Actions, Jenkins, GitLab CI)
* Use Sentinel (in Terraform Enterprise) for policy enforcement

---

### 15. ❓ How do you implement blue/green or canary deployments in Terraform?

**✅ Answer:**
Terraform alone is not ideal for blue/green. You combine Terraform with:

* Application Load Balancer (ALB) target groups
* Launch templates with weighted traffic
* Separate environments for blue/green, then switch traffic

---

### 16. ❓ How do you manage module versioning?

**✅ Answer:**

* Use `git tags` or release versions in the `source` attribute:

```hcl
module "vpc" {
  source = "git::https://github.com/org/vpc-module.git?ref=v1.2.0"
}
```

---

### 17. ❓ How do you debug Terraform errors?

**✅ Answer:**

* Use `terraform plan -out=plan.out`
* Enable verbose logging: `TF_LOG=DEBUG terraform apply`
* Validate code: `terraform validate`
* Format files: `terraform fmt`

---

### 18. ❓ How do you use dynamic blocks?

**✅ Answer:**
Useful when creating repeated nested blocks.

```hcl
dynamic "ingress" {
  for_each = var.ingress_rules
  content {
    from_port = ingress.value.from
    to_port = ingress.value.to
    protocol = ingress.value.protocol
    cidr_blocks = ingress.value.cidr
  }
}
```

---

### 19. ❓ How do you import existing resources into Terraform?

**✅ Answer:**

```bash
terraform import aws_instance.my_instance i-12345678
```

Then manually write the config to match the imported resource.

---

### 20. ❓ How do you use `count` vs `for_each`?

* **`count`**: Used when number of resources is based on a number.
* **`for_each`**: Used when iterating over maps or sets.

```hcl
resource "aws_instance" "example" {
  count = var.instance_count
  ...
}
```

```hcl
resource "aws_security_group_rule" "example" {
  for_each = var.rules
  ...
}
```

---

## 🧠 Bonus Questions (Asked at Top Companies)

### 21. ❓ What is `terraform taint` and when do you use it?

Marks a resource for recreation in the next apply.

```bash
terraform taint aws_instance.db
```

---

### 22. ❓ How do you avoid resource drift?

* Use `terraform plan` regularly
* Enable **auto remediation**
* Use `terraform refresh` or `terraform state show`

---

### 23. ❓ Can Terraform manage Kubernetes resources?

**✅ Answer:**
Yes, using the **Kubernetes provider**, you can manage ConfigMaps, Deployments, Services, etc.

---

### 24. ❓ Explain `terraform workspace` and use-case?

**✅ Answer:**
Allows managing multiple instances of a configuration.

```bash
terraform workspace new dev
terraform workspace select prod
```

Useful for managing environments from a single config set.

---

### 25. ❓ How do you ensure security best practices in Terraform?

* Use separate IAM roles for Terraform
* Store state remotely with encryption
* Never hardcode secrets
* Review plans before apply
* Use linting tools like `tflint`, `checkov`

---

### ✅ **Terraform Interview Questions and Answers**

---

## 🟢 **Basic Level**

1. **What is Terraform and why is it used?**
   Terraform is an Infrastructure as Code (IaC) tool by HashiCorp used to provision and manage cloud infrastructure in a declarative way using `.tf` files.

2. **What are providers in Terraform?**
   Providers are plugins to interact with cloud platforms like AWS, Azure, GCP, Kubernetes, etc.

3. **What is a Terraform module?**
   A module is a container for multiple resources that can be reused. It simplifies your code for repeat deployments.

4. **Difference between `terraform init`, `plan`, `apply`, and `destroy`?**

   * `init`: Initializes working directory
   * `plan`: Shows what will be changed
   * `apply`: Applies the changes
   * `destroy`: Tears down infrastructure

5. **What is the use of `terraform.tfstate` file?**
   It maintains the mapping of Terraform configuration to real-world infrastructure.

---

## 🟡 **Intermediate Level**

1. **What is remote backend in Terraform? Why use it?**
   Stores the `.tfstate` file remotely (like S3, Azure Blob) to support team collaboration and locking.

2. **What is `terraform workspace`?**
   It allows you to manage different environments like dev, stage, prod using the same codebase.

3. **How do you manage secrets in Terraform?**

   * Use `terraform.tfvars` (don't commit)
   * Use Vault or AWS Secrets Manager
   * Environment variables

4. **How do you import existing infrastructure into Terraform?**
   `terraform import <resource> <resource_id>`

5. **How does Terraform handle dependencies between resources?**
   Automatically with its dependency graph, or explicitly using `depends_on`.

---

## 🔴 **Advanced Level**

1. **Explain `terraform plan -out=tfplan` and `apply tfplan`**

   * Helps pre-review infrastructure changes
   * Allows controlled rollout
   * Used in CI/CD pipelines

2. **How do you avoid hardcoding values?**

   * Use variables and locals
   * Use environment-specific `tfvars` files
   * Use `terraform.workspace` for dynamic lookups

3. **Scenario: How do you design multi-account or multi-region deployments?**

   * Use multiple providers
   * Alias each provider
   * Use modules and workspaces
   * Example:

     ```hcl
     provider "aws" {
       region = var.region
     }

     provider "aws" {
       alias  = "prod"
       region = "us-east-1"
     }
     ```

4. **How do you manage drift in infrastructure?**

   * Run `terraform plan` regularly
   * Use `terraform refresh`
   * Automate drift detection in CI/CD

5. **How do you structure Terraform code for a large team?**

   * Use modules
   * Separate state files per environment
   * Store state in remote backend
   * Locking with DynamoDB (AWS) or blob locking (Azure)

---

## 🧠 **Scenario-Based Questions**

1. **You apply a change and only half of your resources are created. What do you do?**

   * Check `.tfstate`
   * Re-run `terraform apply`
   * Use `-target` to isolate failures

2. **How do you deploy separate environments using the same code?**

   * Create separate workspace or directory
   * Use `terraform.workspace`
   * Use `.tfvars` files

3. **How do you manage dynamic resource creation (e.g., create N subnets)?**
   Use `count`, `for_each` and dynamic blocks
   Example:

   ```hcl
   resource "aws_subnet" "example" {
     count = length(var.subnet_list)
     cidr_block = var.subnet_list[count.index]
   }
   ```

4. **You accidentally deleted a resource from the cloud, what next?**

   * Run `terraform apply`
   * Terraform recreates the resource if it’s still in the `.tfstate`
   * Or use `import` to reattach

5. **How do you rollback infrastructure changes?**

   * Use version control to revert `.tf` files
   * Re-run `terraform apply`
   * No native rollback; must be manually managed

---

## 🔧 **CI/CD Integration Questions**

1. **How do you integrate Terraform in Jenkins pipeline?**

   * Install Terraform CLI in Jenkins agents
   * Use steps like:

     ```sh
     terraform init
     terraform plan -out=tfplan
     terraform apply tfplan
     ```

2. **How do you enforce policy checks before apply?**

   * Use `terraform plan` with output
   * Integrate with `OPA`, `TFLint`, `Checkov`

---

## 📁 **Project Structure Example (Multi-Env)**

```
terraform/
├── modules/
│   └── vpc/
│       └── main.tf
├── dev/
│   ├── main.tf
│   ├── terraform.tfvars
├── prod/
│   ├── main.tf
│   ├── terraform.tfvars
```

---


