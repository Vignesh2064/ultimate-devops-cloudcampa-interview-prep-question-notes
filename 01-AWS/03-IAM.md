### ⚙️ **Intermediate IAM Interview Questions**

5. **How is IAM different from Cognito?**
   IAM manages AWS resource permissions; Cognito manages app users (authentication and authorization).

6. **What are managed vs. inline policies?**

   * **Managed**: Standalone, reusable.
   * **Inline**: Embedded directly into a user/group/role.

7. **How do IAM roles help in cross-account access?**
   Role is created in Account A with trust for Account B. IAM user from B can assume the role to access A's resources.

8. **Can an IAM role be assumed by an EC2 instance? How?**
   Yes. Attach the IAM role to the EC2 instance using an instance profile.

9. **Difference between IAM role and service-linked role?**

   * IAM Role: Can be assumed by users, apps, services.
   * Service-linked Role: Automatically created and managed by AWS services.

---

### 🚀 **Advanced IAM Interview Questions**

10. **How would you restrict access to an S3 bucket to a specific VPC?**
    Use VPC endpoint policies or condition like `aws:SourceVpc` in the bucket policy.

11. **How do you audit IAM changes?**

* Use AWS CloudTrail for monitoring changes.
* Enable AWS Config for compliance checks.

12. **What are IAM Access Analyzer and Credential Reports?**

* IAM Access Analyzer: Detects unintended access to resources.
* Credential Reports: Shows credential usage details for each IAM user.

13. **How can you restrict IAM user actions by IP address?**
    Add a condition in the policy like:

```json
"Condition": {
  "IpAddress": {
    "aws:SourceIp": "203.0.113.0/24"
  }
}
```

14. **What is a permission boundary in IAM?**
    It's an advanced feature that limits the maximum permissions a role or user can have, regardless of attached policies.

---

### 📘 **Scenario-Based IAM Questions**

15. **Scenario:** You have multiple DevOps teams across AWS accounts. How do you allow them temporary access to deploy in a shared production account securely?

**Answer:**

* Create IAM roles in the production account.
* Grant each team the `sts:AssumeRole` permission for the production roles.
* Use session policies and MFA to restrict further.

16. **Scenario:** You notice an EC2 instance accessing unauthorized resources. How to investigate?

**Answer:**

* Check the instance role.
* Use CloudTrail logs to trace API calls.
* Use IAM Access Analyzer to review external access.
* Audit the policies attached to the instance role.

17. **Scenario:** You need to rotate IAM user credentials across 100 users. How do you handle this?

**Answer:**

* Enforce IAM password policies with automatic rotation.
* Use automation (Python + Boto3) to rotate access keys programmatically.
* Prefer IAM roles or federated identities over long-term credentials.

---

### 🧰 IAM Best Practices

* Always **use IAM roles** instead of access keys for services.
* Apply **least privilege principle**.
* Enable **MFA for root and privileged users**.
* Use **IAM groups** to assign permissions to multiple users.
* Regularly **review IAM policies** and use **IAM Access Analyzer**.

---
