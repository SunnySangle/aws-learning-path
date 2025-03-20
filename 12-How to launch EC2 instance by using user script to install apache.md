### **How to Launch an EC2 Instance with a User Data Script to Install Apache**  

You can launch an EC2 instance and automatically install **Apache (HTTPD)** using a **User Data Script**. Follow the steps below:

---

## **Step 1: Sign in to AWS Console**
1. Log in to **AWS Management Console**.
2. Navigate to **EC2 Dashboard**.

---

## **Step 2: Launch an EC2 Instance**
1. Click **Launch Instance**.
2. Enter an **Instance Name** (e.g., `Apache-Server`).
3. Choose an **Amazon Machine Image (AMI)**:
   - **Amazon Linux 2** (Recommended).
   - **Ubuntu** (Modify script accordingly).
4. Select an **Instance Type**:
   - `t2.micro` (Free Tier eligible).
5. Click **Key Pair** → Select an existing key or create a new one.
6. Configure **Network Settings**:
   - Allow **HTTP (Port 80)** and **SSH (Port 22)**.

---

## **Step 3: Add User Data Script to Install Apache**
Scroll down to **Advanced details** and find the **User Data** section. Copy and paste the following script:

### **For Amazon Linux 2 & RHEL:**
```bash
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
echo "<h1>Welcome to My Apache Web Server - $(hostname)</h1>" > /var/www/html/index.html
```

### **For Ubuntu & Debian:**
```bash
#!/bin/bash
apt update -y
apt install apache2 -y
systemctl start apache2
systemctl enable apache2
echo "<h1>Welcome to My Apache Web Server - $(hostname)</h1>" > /var/www/html/index.html
```

---

## **Step 4: Launch the Instance**
1. Click **Launch Instance**.
2. Wait for the instance to **initialize**.
3. Click on the instance → Note the **Public IPv4 Address**.

---

## **Step 5: Verify Apache Installation**
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
1. Connect to the instance:
   ```
   ssh -i your-key.pem ec2-user@<Public-IP>  # Amazon Linux
   ssh -i your-key.pem ubuntu@<Public-IP>    # Ubuntu
   ```
2. Check Apache status:
   ```
   systemctl status httpd   # Amazon Linux
   systemctl status apache2 # Ubuntu
   ```
   
---

✅ **Done!** You have successfully launched an EC2 instance with Apache installed using a **User Data Script**. 🚀