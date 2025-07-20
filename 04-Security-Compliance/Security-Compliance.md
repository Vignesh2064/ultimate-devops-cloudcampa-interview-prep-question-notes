## ✅ **1. General Cloud Compliance Questions (All Frameworks)**

### Q1. What is cloud compliance?

**Answer:** Cloud compliance refers to the practice of ensuring that cloud computing services comply with regulatory standards and frameworks like PCI DSS, HIPAA, SOC 2, etc., by leveraging proper controls in data storage, access, encryption, monitoring, and audit logging.

### Q2. How does AWS help with regulatory compliance?

**Answer:** AWS provides tools like:

* **AWS Artifact** – On-demand access to AWS compliance reports (SOC, PCI, ISO, etc.)
* **AWS Config** – Track and audit configuration changes
* **AWS CloudTrail** – Records API calls for auditing
* **AWS Security Hub** – Central view of security & compliance status
* **AWS Organizations & SCPs** – Enforce guardrails for multi-account security

---

## 🔐 **2. PCI DSS (Payment Card Industry Data Security Standard)**

### Q1. How do you ensure PCI compliance on AWS?

**Answer:**

* Use **AWS PCI-compliant services** (listed in [AWS PCI Service List](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/))
* Encrypt cardholder data with **KMS**
* Enable **VPC** isolation, **security groups**, and **WAF**
* Log access via **CloudTrail**
* Use **AWS Shield** for DDoS protection

### Q2. Which AWS services are typically used in PCI workloads?

**Answer:** Amazon EC2, RDS (with encryption), ELB, Lambda, CloudHSM, AWS WAF, KMS, and CloudTrail.

### Q3. How do you secure sensitive cardholder data in transit and at rest?

**Answer:**

* **In transit**: TLS 1.2+, HTTPS, Secure API Gateway
* **At rest**: S3 server-side encryption (SSE), KMS-managed keys, or customer-managed keys

---

## 📜 **3. SOC 2 (System and Organization Controls Type 2)**

### Q1. What are the Trust Service Criteria in SOC 2?

**Answer:**

* Security
* Availability
* Processing Integrity
* Confidentiality
* Privacy

### Q2. How do AWS services support SOC 2?

**Answer:**

* **Security**: IAM, GuardDuty, Security Hub
* **Availability**: Auto Scaling, Route53 failover, CloudWatch
* **Confidentiality**: KMS, S3 bucket policies
* **Privacy**: IAM roles, access logs

### Q3. How do you implement logging and monitoring to support SOC 2?

**Answer:**

* **Enable CloudTrail + CloudWatch**
* Log management using **OpenSearch (ELK)** or **3rd party SIEM**
* **Config Rules** for compliance checks

---

## 🌐 **4. ISO/IEC 27001**

### Q1. What is ISO 27001 and how can AWS help?

**Answer:** ISO 27001 is an international standard for **Information Security Management Systems (ISMS)**. AWS provides:

* **Shared Responsibility Model**
* Pre-certified infrastructure
* Logging tools (CloudTrail, Config)
* Encryption services (KMS, HSM)
* Risk management and incident response frameworks

### Q2. How do you implement access control for ISO 27001 compliance?

**Answer:**

* IAM least-privilege policies
* MFA on all privileged accounts
* Central identity via **AWS SSO**
* Periodic review of IAM roles and policies

---

## 🇺🇸 **5. FISMA / FedRAMP**

### Q1. What is FedRAMP and how does AWS help?

**Answer:** FedRAMP is a U.S. government program that standardizes security assessments for cloud services. AWS GovCloud and many services have **FedRAMP Moderate/High** compliance.

### Q2. How to deploy FISMA-compliant workloads on AWS?

**Answer:**

* Use **GovCloud (US)** regions
* Encrypt data using **FIPS 140-2 compliant** modules
* Implement **audit trails**, **incident response**, and **boundary protection**

---

## 🏥 **6. HIPAA (Health Insurance Portability and Accountability Act)**

### Q1. How do you ensure HIPAA compliance on AWS?

**Answer:**

* Sign a **Business Associate Agreement (BAA)** with AWS
* Use **HIPAA-eligible AWS services** (S3, EC2, Lambda, RDS, etc.)
* Encrypt PHI data at rest and in transit using KMS
* Enable access auditing using CloudTrail
* Use **Amazon Macie** to detect and protect PHI data

### Q2. What services are commonly used for HIPAA workloads?

**Answer:** S3 (with SSE), RDS, EC2, Lambda, KMS, Shield, WAF, CloudTrail, GuardDuty, Macie

### Q3. How do you secure PHI data in AWS Lambda-based architecture?

**Answer:**

* Store PHI in **encrypted S3 or RDS**
* Encrypt environment variables
* Restrict access with IAM
* Enable logging and alarms with **CloudWatch**

---

## ✅ **7. Real-World Scenario-Based Questions**

### Q1. Your application handles card transactions and patient data. How will you ensure PCI + HIPAA compliance together on AWS?

**Answer:**

* Use **HIPAA-eligible and PCI DSS certified AWS services**
* Apply **encryption in transit and at rest** using KMS
* **Tokenize or mask** sensitive data where possible
* Enable **CloudTrail + Security Hub** for auditing
* Isolate environments with **VPC**, private subnets, and **IAM boundaries**

---

## 🔧 AWS Compliance Tooling for All Frameworks

| Tool               | Use                                         |
| ------------------ | ------------------------------------------- |
| AWS Artifact       | Download compliance reports (SOC, PCI, ISO) |
| AWS Config         | Continuous compliance monitoring            |
| AWS CloudTrail     | Auditing API activity                       |
| AWS Security Hub   | Central compliance dashboard                |
| AWS Macie          | Detect sensitive data like PII, PHI         |
| AWS GuardDuty      | Threat detection                            |
| AWS KMS / CloudHSM | Encryption and key management               |
| AWS Organizations  | Enforce account-level policies (SCPs)       |

---

