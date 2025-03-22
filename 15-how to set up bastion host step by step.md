## **How to Set Up a Bastion Host in AWS (Step-by-Step Guide)**  
A **Bastion Host** is a secure EC2 instance that acts as a gateway to access private instances in your **private subnet** via SSH.  

---

## **🚀 Step 1: Create a VPC with Public and Private Subnets**
1. Go to **AWS Console** → **VPC Dashboard** → Click **Create VPC**.
2. **Enter VPC Name** (e.g., `My-Bastion-VPC`).
3. Set up **IPv4 CIDR Block** (e.g., `10.0.0.0/16`).
4. Click **Create**.

---

## **🛜 Step 2: Create Two Subnets**
### **1️⃣ Public Subnet (For Bastion Host)**
1. **Go to VPC** → **Subnets** → **Create Subnet**.
2. Select **My-Bastion-VPC**.
3. **Subnet Name**: `Public-Subnet`
4. **CIDR Block**: `10.0.1.0/24`
5. Click **Create Subnet**.

### **2️⃣ Private Subnet (For Private EC2 Instances)**
1. Click **Create Subnet** again.
2. **Subnet Name**: `Private-Subnet`
3. **CIDR Block**: `10.0.2.0/24`
4. Click **Create Subnet**.

---

## **🌐 Step 3: Set Up Internet Gateway (For Public Subnet)**
1. **Go to VPC** → **Internet Gateway** → **Create Internet Gateway**.
2. **Name it**: `Bastion-IGW`.
3. Click **Attach to VPC** → Select `My-Bastion-VPC` → **Attach**.

---

## **📌 Step 4: Configure Route Tables**
### **1️⃣ Public Route Table**
1. **Go to VPC** → **Route Tables** → **Create Route Table**.
2. **Name it**: `Public-RT`.
3. Select `My-Bastion-VPC`.
4. Click **Create**.
5. Click **Edit Routes** → **Add Route**:
   - **Destination**: `0.0.0.0/0`
   - **Target**: `Bastion-IGW`
6. Click **Save Routes**.
7. Go to **Subnet Associations** → Attach it to **Public-Subnet**.

### **2️⃣ Private Route Table (For Private EC2)**
1. **Go to VPC** → **Route Tables** → **Create Route Table**.
2. **Name it**: `Private-RT`.
3. Select `My-Bastion-VPC`.
4. Click **Create**.
5. **Attach it to `Private-Subnet`**.

---

## **🔐 Step 5: Create a Security Group**
### **1️⃣ Bastion Host Security Group**
1. Go to **EC2 Dashboard** → **Security Groups** → **Create Security Group**.
2. **Name it**: `Bastion-SG`.
3. **Rules:**
   - **Inbound Rule:**  
     - Type: `SSH`
     - Port: `22`
     - Source: **Your IP** (`X.X.X.X/32` for security)
   - **Outbound Rule:**  
     - Allow **All Traffic (`0.0.0.0/0`)**
4. Click **Create Security Group**.

### **2️⃣ Private Instance Security Group**
1. Create another **Security Group** called `Private-Instance-SG`.
2. **Rules:**
   - **Inbound Rule:**
     - Type: `SSH`
     - Port: `22`
     - **Source:** `Bastion-SG`
   - **Outbound Rule:** Allow **All Traffic (`0.0.0.0/0`)**.
3. Click **Create Security Group**.

---

## **💻 Step 6: Launch EC2 Instances**
### **1️⃣ Launch Bastion Host**
1. **Go to EC2** → Click **Launch Instance**.
2. **AMI**: Amazon Linux 2 / Ubuntu.
3. **Instance Type**: `t2.micro` (Free Tier).
4. **Subnet**: `Public-Subnet`.
5. **Security Group**: Select `Bastion-SG`.
6. **Key Pair**: Create or select an existing one.
7. Click **Launch**.

### **2️⃣ Launch Private EC2 Instance**
1. **Go to EC2** → Click **Launch Instance**.
2. **AMI**: Amazon Linux 2 / Ubuntu.
3. **Instance Type**: `t2.micro`.
4. **Subnet**: `Private-Subnet`.
5. **Security Group**: Select `Private-Instance-SG`.
6. **Key Pair**: Use the same key as Bastion.
7. Click **Launch**.

---

## **🔗 Step 7: Connect to the Private Instance via Bastion Host**
### **1️⃣ SSH into Bastion Host**
```bash
ssh -i your-key.pem ec2-user@<Bastion-Public-IP>
```
### **2️⃣ SSH into Private EC2 from Bastion**
```bash
ssh -i your-key.pem ec2-user@<Private-Instance-Private-IP>
```
🎉 **Now, you can securely access private EC2 instances via Bastion Host!** 🚀

---
