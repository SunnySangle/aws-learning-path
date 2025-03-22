### **How to Create and Launch an EC2 Launch Template with User Data Script to Install Apache2**  

A **Launch Template** helps you automate EC2 instance provisioning, including **Apache2 installation** using a **User Data Script**. Follow the steps below:

---

## **Step 1: Sign in to AWS Console**  
1. Log in to your **AWS Management Console**.  
2. Navigate to **EC2 Dashboard**.  
3. Click **Launch Templates** in the left panel.  

---

## **Step 2: Create a Launch Template**  
1. Click **Create launch template**.  
2. Enter a **Template name** (e.g., `Apache-Web-Template`).  
3. (Optional) Enter a **Description** (e.g., "Launch template to install Apache2").  
4. Select **Amazon Machine Image (AMI)**:  
   - **Amazon Linux 2** (Recommended).  
   - **Ubuntu** (Modify the script accordingly).  
5. Select an **Instance Type**:  
   - `t2.micro` (Free Tier eligible).  
6. Select an **Existing Key Pair** or **Create a New Key Pair**.  

---

## **Step 3: Configure User Data Script**  
1. Scroll down to **Advanced details**.  
2. Find the **User Data** section and enter the following script:  

### **For Amazon Linux 2 / RHEL**  
```bash
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
echo "<h1>Welcome to My Apache Web Server - $(hostname)</h1>" > /var/www/html/index.html
```

### **For Ubuntu / Debian**  
```bash
#!/bin/bash
apt update -y
apt install apache2 -y
systemctl start apache2
systemctl enable apache2
echo "<h1>Welcome to My Apache Web Server - $(hostname)</h1>" > /var/www/html/index.html
```

---

## **Step 4: Configure Security Group (Allow HTTP & SSH)**  
1. Scroll to **Network settings**.  
2. Select an existing **Security Group** or create a new one:  
   - **Allow SSH (Port 22)** → Your IP only (`0.0.0.0/0` is not secure).  
   - **Allow HTTP (Port 80)** → Open to the world (`0.0.0.0/0`).  
3. Click **Create launch template**.  

---

## **Step 5: Launch an EC2 Instance Using the Template**  
1. Navigate to **EC2 Dashboard** → **Launch Templates**.  
2. Select the **Apache-Web-Template**.  
3. Click **Actions** → **Launch instance from template**.  
4. Configure:
   - Number of instances (e.g., `1`).
   - Select a VPC and subnet.
5. Click **Launch instance**.

---

## **Step 6: Verify Apache Installation**  
### **Option 1: Check via Browser**  
1. Open a browser and enter:  
   ```
   http://<Public-IP>
   ```
2. You should see:  
   ```
   Welcome to My Apache Web Server - <Instance-Hostname>
   ```

### **Option 2: Check via SSH**  
1. Connect to the instance using SSH:  
   ```
   ssh -i your-key.pem ec2-user@<Public-IP>   # Amazon Linux  
   ssh -i your-key.pem ubuntu@<Public-IP>     # Ubuntu  
   ```
2. Check Apache status:  
   ```
   systemctl status httpd    # Amazon Linux  
   systemctl status apache2  # Ubuntu  
   ```

---

✅ **Done!** You have successfully created a **Launch Template** to automatically deploy EC2 instances with **Apache2 installed**.