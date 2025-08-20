
# ⚡ Amazon EC2 – Interview Notes
### 1. What is EC2?
**Answer:**
* EC2 = **Elastic Compute Cloud**.
* AWS service that provides **resizable virtual servers (instances)** in the cloud.
* Pay-as-you-go model.
### 2. Why EC2?
**Answer:**
* Avoids cost of physical servers.
* Can **upgrade/downgrade easily** (change instance types).
* **Automatic updates/patches** possible.
* Security handled with **Security Groups & IAM roles**.
* Can scale from **1 to 1000+ servers** (auto scaling).
* Reduces **maintenance overhead** vs on-prem hardware.
### 3. Types of EC2 Instances
**Answer:**
1. **General Purpose** – Balanced CPU, memory, networking (e.g., `t2`, `t3`, `m5`).
   * Use case: Web servers, dev/test, small DB.
2. **Compute Optimized** – High CPU (e.g., `c5`).
   * Use case: High-performance computing, batch processing.
3. **Memory Optimized** – Large RAM (e.g., `r5`, `x1`).
   * Use case: In-memory DB, caching.
4. **Storage Optimized** – High IOPS & throughput (e.g., `i3`, `d2`).
   * Use case: Data warehousing, NoSQL DB, analytics.
5. **Accelerated Computing** – GPU/FPGA (e.g., `p3`, `f1`).
   * Use case: ML/AI, graphics rendering, scientific computing.
### 4. What are **Regions** and **Availability Zones (AZs)**?
**Answer:**
* **Region** = Geographical area (e.g., `us-east-1`, `ap-south-1`).
* **AZs** = Isolated data centers **within a region**.
* Example: `ap-south-1a`, `ap-south-1b` in Mumbai region.
### 5. What is **Latency**?
**Answer:**
* Time taken for a request to travel from **client → server → back to client**.
* Lower latency = faster response.
* Choosing nearest region reduces latency.
### 6. Why Availability Zones?
**Answer:**
* Provide **high availability & fault tolerance**.
* If one AZ fails, traffic can shift to another.
* Used in **load balancing** and **disaster recovery**.
### 7. Steps to Create an EC2 Instance
1. Go to **EC2 Console** → Launch Instance
2. Choose **AMI** (Amazon Machine Image – e.g., Ubuntu, Amazon Linux)
3. Select **Instance Type** (t2.micro, m5.large, etc.)
4. Create/choose **Key Pair** (used for SSH login)
   * **Public Key** stored in AWS
   * **Private Key (.pem)** stored locally
   * Use `chmod 600 mykey.pem` → restricts permissions so SSH works securely
5. Configure **Security Group** (firewall rules – e.g., allow port 22 for SSH, 80/443 for web)
6. Launch instance
### 8. Server Setup (Inside EC2)

1. **Update server**

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
2. **Install Java (for Jenkins)**

   ```bash
   sudo apt install openjdk-11-jdk -y
   java -version
   ```
3. **Install Jenkins**

   ```bash
   curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
     /usr/share/keyrings/jenkins-keyring.asc > /dev/null
   echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
     https://pkg.jenkins.io/debian binary/ | sudo tee \
     /etc/apt/sources.list.d/jenkins.list > /dev/null
   sudo apt update
   sudo apt install jenkins -y
   sudo systemctl enable --now jenkins
   ```
4. **Update Security Group**

   * Add inbound rule for **Port 8080** (Jenkins UI).
   * Keep SSH (22) restricted.
---

