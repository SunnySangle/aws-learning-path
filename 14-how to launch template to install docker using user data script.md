### **How to Create an EC2 Launch Template to Install Docker Using User Data Script**

To install **Docker** automatically when launching an EC2 instance, you can use a **Launch Template** with a **User Data script**.

---

## **Step 1: Create a Launch Template**
1. **Go to EC2 Dashboard** → Click on **Launch Templates**.
2. Click **Create launch template**.
3. **Enter a name** (e.g., `Docker-Instance-Template`).
4. Select an **Amazon Machine Image (AMI)**:
   - **Amazon Linux 2** (Recommended)
   - **Ubuntu** (Modify the script accordingly)
5. Choose an **Instance Type** (`t2.micro` for free tier).
6. **Key Pair**: Choose an existing one or create a new key pair.

---

## **Step 2: Add User Data Script**
Scroll down to **Advanced details** → **User data** → Paste the following script:

### **For Amazon Linux 2 / RHEL**
```bash
#!/bin/bash
sudo yum update -y
sudo amazon-linux-extras enable docker
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user
```

### **For Ubuntu**
```bash
#!/bin/bash
sudo apt update -y
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu
```

---

## **Step 3: Configure Security Group**
1. **Allow SSH (Port 22)** → Your IP only (`0.0.0.0/0` is not secure).
2. **Allow HTTP (Port 80)** if needed.
3. **Allow Custom TCP (Port 2376)** if you plan to manage Docker remotely.

---

## **Step 4: Create and Launch the Instance**
1. Click **Create launch template**.
2. Go to **EC2 Dashboard** → **Launch Templates**.
3. Select **Docker-Instance-Template** → **Actions** → **Launch instance from template**.
4. Choose a **VPC and subnet**.
5. Click **Launch instance**.

---

## **Step 5: Verify Docker Installation**
Once the instance is running:  
1. **Connect via SSH**:  
   ```bash
   ssh -i your-key.pem ec2-user@<Public-IP>  # Amazon Linux
   ssh -i your-key.pem ubuntu@<Public-IP>    # Ubuntu
   ```
2. **Check Docker Version**:  
   ```bash
   docker --version
   ```
3. **Run a Test Container**:  
   ```bash
   docker run hello-world
   ```

---

✅ **Success!** Your EC2 instance now installs Docker automatically at launch using the User Data script.