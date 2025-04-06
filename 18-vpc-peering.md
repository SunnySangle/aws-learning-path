Sure Sunny! Here's a **step-by-step guide to creating VPC Peering** and connecting two EC2 instances (in different VPCs) via Internet Gateway, Subnets, and Route Tables.

---

### ✅ **Project Objective**
To connect **two VPCs** using **VPC Peering**, allowing **EC2 instances** in both VPCs to communicate **privately**.

---

## 🌐 STEP 1: Create Two VPCs

### VPC 1 - "VPC-A"
- CIDR block: `10.0.0.0/16`

### VPC 2 - "VPC-B"
- CIDR block: `192.168.0.0/16`

> Go to **VPC Dashboard > Your VPCs > Create VPC**

---

## 🛤️ STEP 2: Create Subnets

### Subnet in VPC-A
- Name: `Subnet-A`
- CIDR block: `10.0.1.0/24`
- Availability Zone: Select any

### Subnet in VPC-B
- Name: `Subnet-B`
- CIDR block: `192.168.1.0/24`

> Go to **Subnets > Create Subnet** and choose the VPC during setup.

---

## 🌐 STEP 3: Create Internet Gateways (Optional, for Internet access)

### IGW for VPC-A
- Name: `IGW-A`
- Attach to VPC-A

### IGW for VPC-B
- Name: `IGW-B`
- Attach to VPC-B

> Go to **Internet Gateways > Create Internet Gateway > Attach to VPC**

---

## 📑 STEP 4: Create Route Tables and Add Routes

### For VPC-A
- Route Table Name: `RT-A`
- Associate with Subnet-A
- Add route: `0.0.0.0/0` → Target: `IGW-A`

### For VPC-B
- Route Table Name: `RT-B`
- Associate with Subnet-B
- Add route: `0.0.0.0/0` → Target: `IGW-B`

---

## 🖥️ STEP 5: Launch EC2 Instances

### EC2 in VPC-A
- Subnet: Subnet-A
- AMI: Amazon Linux 2
- Security Group: Allow ICMP (ping) and SSH from anywhere or your IP

### EC2 in VPC-B
- Subnet: Subnet-B
- Security Group: Same as above

---

## 🔗 STEP 6: Create VPC Peering Connection

> Go to **VPC Dashboard > Peering Connections > Create Peering Connection**

- **Name tag**: `Peer-A-B`
- **Requester VPC**: VPC-A
- **Accepter VPC**: VPC-B (in same region)

After creation:
- Click **Actions > Accept Request** (in VPC-B)

---

## 📑 STEP 7: Update Route Tables for Peering

### In Route Table of VPC-A (RT-A)
- Add Route:
  - Destination: `192.168.0.0/16`
  - Target: Peering Connection `Peer-A-B`

### In Route Table of VPC-B (RT-B)
- Add Route:
  - Destination: `10.0.0.0/16`
  - Target: Peering Connection `Peer-A-B`

---

## 🔒 STEP 8: Update EC2 Security Groups

Allow incoming traffic from the **other VPC's CIDR block**:

- VPC-A SG: Allow ICMP, SSH from `192.168.0.0/16`
- VPC-B SG: Allow ICMP, SSH from `10.0.0.0/16`

---

## ✅ STEP 9: Test VPC Peering

1. SSH into EC2 of VPC-A
2. Ping the **private IP** of EC2 in VPC-B

```bash
ping 192.168.1.x

or ```

curl  192.168.1.x

If ping works — VPC Peering is successfully established 🎉

---






##user data script
#!/bin/bash
sudo apt update -y
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
echo "<h1>Server $(hostname) - VPC Peering Test Page</h1>" > /var/www/html/index.html

