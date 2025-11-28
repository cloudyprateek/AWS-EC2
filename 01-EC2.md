
 
 #  Elastic Compute Cloud (EC2)

Amazon EC2 (Elastic Compute Cloud) is a web service that allows you to run virtual servers in the cloud. It provides scalable, secure, and cost‑efficient compute capacity, allowing you to deploy applications without buying physical hardware.

### Why the name “EC2”?

* **Elastic** – You can increase or decrease the number or size of servers anytime.
* **Compute** – It provides processing power for applications.
* **Cloud** – All resources run on AWS cloud infrastructure.

### What is an EC2 Instance?

An **EC2 instance** is simply a virtual machine (VM) that runs on AWS. You can select the OS, hardware configuration, and storage type based on your needs.

---

#  Amazon Machine Image (AMI)

An **Amazon Machine Image (AMI)** is a pre-configured template used to create EC2 instances.

### What does an AMI include?

* Operating system (Ubuntu, Amazon Linux, Windows, etc.)
* Default software/applications
* Architecture (x86_64 / ARM)
* Storage mappings
* Launch permissions

### Key Points:

* You **must** choose an AMI when launching an instance.
* You can launch multiple identical instances from one AMI.
* You can also use different AMIs for different configurations.

---

#  Types of EC2 Instances

AWS categorizes EC2 instances based on CPU, memory, storage, and networking needs.

## 1️ General Purpose Instances

Balanced compute, memory, and storage.

**Best for:** Web apps, microservices, small databases.

**Examples:** t2, t3, t4g, m5, m6

---

## 2️ Compute Optimized Instances

Designed for high‑performance CPU operations.

**Best for:** Gaming servers, scientific modeling, batch processing.

**Examples:** c4, c5, c6

---

## 3️ Memory Optimized Instances

High RAM relative to CPU.

**Best for:** Large databases, caching servers, in‑memory analytics.

**Examples:** r4, r5, x1

---

## 4️ Storage Optimized Instances

Fast I/O performance + large storage capacity.

**Best for:** Big data, file storage, log processing.

**Examples:** i3, d3, h1

---

## 5️ Accelerated Computing Instances

Use specialized hardware like GPUs or FPGAs.

**Best for:** Machine learning, video rendering, 3D processing.

**Examples:** g4, p4, f1

---

#  Key Pair (SSH Keys)

A **key pair** is used to securely connect to EC2 instances without a password.

### Key pair consists of:

* **Public key** – stored on the instance
* **Private key (.pem)** – kept by the user

### Public Key

Acts like a “lock” installed on the server.

### Private Key

You use this to unlock and log in securely.

  Never share private key.

---

#  Security Group

A **security group** acts as a virtual firewall for your instance.

### Two types of rules:

* **Inbound rules:** control incoming traffic
* **Outbound rules:** control outgoing traffic

### Example:

* Allow SSH (port 22) from your IP
* Block all unknown traffic

Security groups help ensure only trusted sources can connect.

---

## A) Launching an EC2 Instance (AWS Management Console)

1. **Login to AWS Console**: Go to [AWS Console](https://aws.amazon.com/console/).  
2. **Navigate to EC2 Service**: Search for **EC2** in the search bar and select it.  
3. **Launch Instance**:
   - Click **Launch Instances**.
   - Choose an **Amazon Machine Image (AMI)** (e.g., Amazon Linux 2 Macos, ubantu).  
   - Select **Instance Type** (e.g., t2.micro for free tier).  
   - Configure **Instance Details** (default VPC and subnet is fine for basic setup).  
   - Add **Storage**: By default, root volume is attached. You can add additional EBS volumes here.  
   - Add **Tags** (optional) to identify your instance.  
   - Configure **Security Group**: Allow SSH (port 22) access from your IP.  
   - Click **Launch**, then select an existing key pair or create a new one. Download the `.pem` file.  

4. **Connect to EC2 Instance**:
```bash
ssh -i "your-key.pem" ec2-user@<EC2-Public-IP>
```
---

#  EC2 Instance States

| State             | Meaning                                             |
| ----------------- | --------------------------------------------------- |
| **Pending**       | Instance is being created and initialized           |
| **Running**       | Instance is active and ready to use                 |
| **Stopping**      | Shutting down process has started                   |
| **Stopped**       | Instance is off but can restart; no compute charges |
| **Starting**      | Restarting from “Stopped” state                     |
| **Shutting‑down** | Instance is being terminated                        |
| **Terminated**    | Instance deleted permanently                        |
| **Hibernating**   | Instance RAM saved to EBS for fast resume           |

---

#  EC2 Pricing Models

AWS provides various cost options depending on flexibility and usage.

## 1️ On‑Demand

* Pay per hour/second
* No commitment
* Good for testing or unpredictable workloads

## 2️ Reserved Instances

* 1 or 3‑year commitment
* Up to **75% cheaper** than On‑Demand
* Payment options:

  * All upfront
  * Partial upfront
  * No upfront

## 3️ Savings Plans

* Commit to a fixed $/hour usage
* More flexible than Reserved Instances
* Works across regions & instance families

## 4️ Spot Instances

* Use unused AWS capacity at **up to 90% discount**
* Can be interrupted anytime
* Best for flexible, fault‑tolerant workloads

## 5️ Dedicated Hosts

* A full physical EC2 server dedicated to your account
* Useful for license‑specific workloads (Windows, SQL)

---

#  Remote Access: SSH vs RDP

##  SSH (Linux)

* Uses **port 22**
* Command‑line interface
* Technically advanced but powerful
* Example:

```
ssh -i mykey.pem ec2-user@<public-ip>
```

##  RDP (Windows)

* Uses **port 3389**
* Full graphical interface (GUI)
* Good for beginners

---
###  Common Ports

| Purpose | Port |
| ------- | ---- |
| SSH     | 22   |
| HTTP    | 80   |
| HTTPS   | 443  |
| RDP     | 3389 |


## B)  Amazon Machine Image (AMI)

An AMI defines the template used to launch EC2 instances. It acts like a snapshot of your machine that can be reused.

###  AMI Contains:

* Root OS image
* Software packages
* Boot instructions
* Block device mapping
* Permissions for launching

###  Types of AMIs

* AWS Provided AMIs
* Marketplace AMIs
* Custom AMIs (created from your running server)
* Community AMIs

## . Creating an AMI Image from an EC2 Instance (GUI)

1. Go to **EC2 → Instances** and select the instance you want to create an image from.  
2. Click **Actions → Image → Create Image**.  
3. Fill in the details:
   - **Image Name:** e.g., `MyEC2Backup`  
   - **Image Description:** Optional, e.g., "Backup before updates"  
   - **No Reboot:** Check if you do not want the instance to reboot during image creation  
4. Click **Create Image**.  
5. The AMI will appear under **Images → AMIs**.  
6. You can use this AMI to launch new instances with the same configuration as the original instance.

---



