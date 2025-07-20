### ✅ **Basic to Advanced EBS Interview Questions with Answers**

---

### 🔹 **1. What is Amazon EBS?**

**Answer:**
Amazon Elastic Block Store (EBS) provides block-level storage volumes for use with EC2 instances. It’s like a virtual hard drive that persists independently from the EC2 instance lifecycle.

---

### 🔹 **2. What are the types of EBS volumes?**

**Answer:**

* **gp3 (General Purpose SSD)**
* **gp2 (General Purpose SSD)** — legacy
* **io2/io1 (Provisioned IOPS SSD)**
* **st1 (Throughput-Optimized HDD)**
* **sc1 (Cold HDD)**

---

### 🔹 **3. How do you increase the size of an EBS volume?**

**Answer:**
You can **modify** the volume using:

* AWS Console
* AWS CLI:

  ```bash
  aws ec2 modify-volume --volume-id vol-xxxxxxxx --size 100
  ```

---

### 🔹 **4. After modifying an EBS volume, what should be done on the instance?**

#### ✅ **For Linux:**

1. **Check new size:**

   ```bash
   lsblk
   ```
2. **Resize file system (ext4):**

   ```bash
   sudo growpart /dev/xvdf 1
   sudo resize2fs /dev/xvdf1
   ```

   For `xfs` file system:

   ```bash
   sudo xfs_growfs -d /
   ```

#### ✅ **For Windows:**

1. Use **Disk Management (diskmgmt.msc)**
2. Right-click the volume → **Extend Volume**
3. Follow the wizard to allocate the unallocated space.

---

### 🔹 **5. Is it possible to decrease the size of an EBS volume?**

**Answer:**
No. AWS doesn’t support reducing the size directly. Instead:

* Take a snapshot.
* Create a new smaller volume from the snapshot.
* Attach it and migrate data manually.

---

### 🔹 **6. What happens to data when you stop and start an instance using EBS?**

**Answer:**
Data in the root and attached EBS volumes is **retained** even after stopping or restarting the EC2 instance.

---

### 🔹 **7. What’s the difference between EBS and Instance Store?**

| EBS                         | Instance Store              |
| --------------------------- | --------------------------- |
| Persistent                  | Non-persistent              |
| Data retained on stop/start | Data lost on stop/terminate |
| Can take snapshots          | Cannot snapshot             |

---

### 🔹 **8. Can you attach the same EBS volume to multiple EC2 instances?**

**Answer:**
Only with **EBS Multi-Attach** using **io1/io2** volumes and **Amazon EBS-optimized** Nitro-based EC2 instances.

---

### 🔹 **9. How do you back up an EBS volume?**

**Answer:**
By creating a **snapshot**:

```bash
aws ec2 create-snapshot --volume-id vol-xxxxxxxx --description "Backup"
```

---

### 🔹 **10. How do you encrypt an unencrypted EBS volume?**

**Steps:**

1. Create a snapshot of the volume.
2. Copy the snapshot with encryption enabled.
3. Create a new volume from the encrypted snapshot.

---

### ✅ **Real-Time Scenario-Based Questions**

---

### 🔸 **Q1. You increased the EBS size from 30GB to 100GB, but EC2 shows still 30GB. What do you do?**

**Answer:**

* Confirm size with `lsblk`
* Resize the partition using `growpart`
* Resize file system with `resize2fs` or `xfs_growfs`

---

### 🔸 **Q2. EBS volume shows `100% full`, how do you fix?**

**Answer:**

* Stop large logging or rotating files
* Expand EBS volume
* Resize partition and file system

---

### 🔸 **Q3. How do you monitor EBS performance?**

**Answer:**

* Use **CloudWatch** metrics like:

  * `VolumeReadOps`, `VolumeWriteOps`
  * `VolumeQueueLength`
  * `BurstBalance`

---

### 🔸 **Q4. EBS volume becomes `stuck in-use`, what do you do?**

**Answer:**

* Detach forcefully:

  ```bash
  aws ec2 detach-volume --volume-id vol-xxxx --force
  ```

---
