## 🟢 **Basic AWS Load Balancer Questions**

### 1. **What is an AWS Load Balancer?**
**Answer:** AWS Load Balancer distributes incoming traffic across multiple targets (like EC2 instances, containers, IPs) to ensure high availability and fault tolerance.

---

### 2. **What are the types of Load Balancers in AWS?**
**Answer:**
- **Application Load Balancer (ALB)** – Layer 7, supports content-based routing.
- **Network Load Balancer (NLB)** – Layer 4, handles TCP/UDP traffic at high performance.
- **Gateway Load Balancer (GWLB)** – Used for third-party virtual appliances.

---

### 3. **Which Load Balancer supports WebSocket?**
**Answer:** Application Load Balancer (ALB) supports WebSocket.

---

### 4. **What is a Target Group?**
**Answer:** A target group routes requests to one or more registered targets (EC2 instances, IPs, Lambda functions).

---

## 🟡 **Intermediate AWS Load Balancer Questions**

### 5. **What is the default timeout for ALB?**
**Answer:** 60 seconds for idle timeout (can be modified).

---

### 6. **How does health check work in ALB/NLB?**
**Answer:** Load balancers periodically ping a target (via HTTP or TCP) to check its health. If a target fails X number of health checks, it’s marked unhealthy and traffic is rerouted.

---

### 7. **What is the difference between ALB and NLB?**
| Feature | ALB | NLB |
|--------|-----|-----|
| Layer | 7 (HTTP/HTTPS) | 4 (TCP/UDP) |
| SSL Termination | Yes | Yes |
| WebSocket Support | Yes | Limited |
| Sticky Sessions | Yes (via cookies) | Yes (via source IP) |
| Static IP | No | Yes |

---

### 8. **Can ALB route traffic based on hostname or URL path?**
**Answer:** Yes, ALB supports host-based and path-based routing.

---

### 9. **What are sticky sessions?**
**Answer:** Sessions that allow a client to consistently reach the same backend target using a cookie or source IP.

---

## 🔴 **Advanced AWS Load Balancer Questions**

### 10. **How do you implement blue/green deployments using ALB?**
**Answer:**  
- Use two target groups (blue and green).  
- Register both with the same ALB.  
- Shift traffic from blue to green using weighted target groups or swapping.

---

### 11. **Can ALB integrate with AWS WAF?**
**Answer:** Yes, ALB can integrate with AWS Web Application Firewall (WAF) to protect against web exploits.

---

### 12. **How to secure traffic between ALB and backend instances?**
**Answer:**
- Use **HTTPS** listeners on ALB.
- Use **SSL certificates** on target instances.
- Enable **end-to-end encryption**.

---

### 13. **What is cross-zone load balancing?**
**Answer:** Distributes traffic evenly across all registered targets in all AZs. Enabled by default for ALB, disabled by default for NLB.

---

### 14. **How can you use Load Balancer with Lambda?**
**Answer:** ALB supports Lambda targets via HTTP/HTTPS. You can directly route HTTP requests to a Lambda function.

---

### 15. **What’s the difference between Gateway Load Balancer and NLB?**
**Answer:** GWLB is used to deploy, scale, and manage third-party virtual appliances (firewalls, IDS/IPS) in a transparent way, while NLB handles TCP/UDP connections with ultra-low latency.

---

## 🧩 **Scenario-Based Questions**

### 16. **Scenario: Your website experiences latency. How do you troubleshoot ALB?**
**Answer:**
- Check **CloudWatch metrics**: Latency, TargetResponseTime.
- Check **ALB access logs** for slow URLs.
- Verify **target health checks**.
- Ensure **backend EC2 instances** are properly configured and performant.

---

### 17. **Scenario: Some users report intermittent access failures. What would you check?**
**Answer:**
- **Cross-zone load balancing** (may be disabled).
- **Health check thresholds and path**.
- **Subnet configuration** (public/private).
- **Security group rules** and **NACLs**.

---

### 18. **Scenario: You want to expose services on TCP port 8080 with static IPs.**
**Answer:** Use **NLB** with TCP listener on port 8080. NLB provides static IPs.

---

### 19. **Scenario: Need to terminate SSL at load balancer and forward HTTP to backend.**
**Answer:**
- Set up **HTTPS listener on ALB**.
- Attach **SSL certificate** (ACM or IAM).
- Forward traffic to HTTP backend via target group.

---

### 20. **Scenario: How do you deploy a multi-environment app using Load Balancers?**
**Answer:**
- Use **separate target groups** for dev/stage/prod.
- Create **host-based routing** rules in ALB (e.g., dev.app.com, stage.app.com).
- Assign proper **security groups** per environment.

---
