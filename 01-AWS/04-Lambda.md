## 🟢 **Basic AWS Lambda Interview Questions**

1. **What is AWS Lambda?**
   **Answer:** AWS Lambda is a serverless compute service that runs your code in response to events and automatically manages the compute resources for you.

2. **What languages does Lambda support?**
   **Answer:** Python, Node.js, Java, Go, Ruby, .NET (C#), and custom runtimes using Lambda Layers.

3. **What is the default timeout of a Lambda function?**
   **Answer:** 3 seconds (maximum is 15 minutes).

4. **What is the maximum size of deployment package?**
   **Answer:** 50 MB (compressed), 250 MB (uncompressed including layers).

---

## 🟡 **Intermediate Lambda Interview Questions**

1. **How can you invoke a Lambda function?**
   **Answer:**

   * API Gateway
   * EventBridge
   * S3 bucket trigger (on upload)
   * DynamoDB streams
   * SQS messages
   * Manual invocation via CLI/SDK

2. **How does Lambda handle concurrency?**
   **Answer:** Lambda automatically scales based on the number of incoming requests. Each request is handled in a new instance of the function (up to the account concurrency limit).

3. **What are Lambda Layers?**
   **Answer:** Layers are ZIP archives that contain libraries, dependencies, or custom runtimes and can be shared across multiple functions.

4. **How do you manage secrets in Lambda?**
   **Answer:**

   * Use **AWS Secrets Manager** or **SSM Parameter Store**.
   * Load values at runtime using the AWS SDK in your function.

---

## 🔴 **Advanced Lambda Interview Questions**

1. **How do you troubleshoot a slow-running Lambda?**
   **Answer:**

   * Check CloudWatch logs for cold start times.
   * Profile function with AWS X-Ray.
   * Optimize dependencies and code.
   * Reduce package size and enable provisioned concurrency.

2. **What is provisioned concurrency?**
   **Answer:**
   It pre-initializes a set number of Lambda instances to eliminate cold starts.

3. **How do you handle versioning and aliases in Lambda?**
   **Answer:**

   * Publish different versions of a function.
   * Use **aliases** (e.g., *dev*, *prod*, *blue/green*) to point to specific versions.

4. **How to implement CI/CD for Lambda using Terraform or CodePipeline?**
   **Answer:**

   * Use Terraform to deploy Lambda (via `aws_lambda_function`) and use GitHub/CodeCommit + CodePipeline/CodeBuild for automation.

---

## ⚙️ **Scenario-Based Questions**

### **Q1: How to deploy different Lambda versions for different environments (dev, qa, prod)?**

**Answer:**

* Use **aliases** to separate environments.
* Example:

  * `dev` → Lambda version 1
  * `qa` → version 2
  * `prod` → version 3
* Automate with **Terraform**, Helm for config storage (e.g., if Lambda is part of a bigger EKS deployment), or CodePipeline.

---

### **Q2: How to invoke Lambda from S3 and restrict to only a specific file type (e.g., .csv)?**

**Answer:**

* S3 Trigger + Use event name: `ObjectCreated`
* Filter `.csv` files using S3 trigger filter
* In code:

  ```python
  if key.endswith(".csv"):
      process_file()
  else:
      return "Unsupported file type"
  ```

---

### **Q3: A Lambda needs to access private resources in a VPC. What do you do?**

**Answer:**

* Attach the Lambda to the VPC with the correct subnets and security groups.
* Ensure there’s a **NAT Gateway** if Lambda needs internet access.

---

### **Q4: How to reduce cold start issues in Lambda?**

**Answer:**

* Use **provisioned concurrency**.
* Avoid heavy dependencies.
* Minimize initialization code.
* Use compiled languages like Go.

---
