Here’s a step-by-step guide to setting up AWS Web Application Firewall (WAF) with a VPC, EC2 instances, an Application Load Balancer (ALB), and a Target Group.

---

## **Step 1: Create a VPC**
1. Open the **AWS Management Console** → Go to **VPC**.
2. Click on **Create VPC**.
   - Name: `MyVPC`
   - IPv4 CIDR block: `10.0.0.0/16`
   - Click **Create VPC**.

---

## **Step 2: Create Subnets**
1. Go to **Subnets** → Click **Create Subnet**.
2. Choose `MyVPC` and create **two subnets** in different Availability Zones:
   - **Public Subnet**: `10.0.1.0/24`
   - **Private Subnet**: `10.0.2.0/24`
3. Click **Create Subnet**.

---

## **Step 3: Create an Internet Gateway (IGW)**
1. Go to **Internet Gateways** → Click **Create IGW**.
2. Attach it to `MyVPC`.
3. Modify the route table:
   - Go to **Route Tables** → Select the default route table for `MyVPC`.
   - Add a route: `0.0.0.0/0` → Internet Gateway.

---

## **Step 4: Create a Security Group for EC2**
1. Go to **Security Groups** → Click **Create Security Group**.
2. Name it `WebSecurityGroup`, select `MyVPC`.
3. Add inbound rules:
   - **HTTP (80)** from `0.0.0.0/0`.
   - **HTTPS (443)** from `0.0.0.0/0`.
   - **SSH (22)** from your IP.

---

## **Step 5: Launch EC2 Instances**
1. Go to **EC2** → Click **Launch Instances**.
2. Choose Amazon Linux or Ubuntu.
3. Place one instance in the **Private Subnet**.
4. Select `WebSecurityGroup`.
5. Install a web server:
   ```sh
   sudo yum update -y
   sudo yum install httpd -y
   sudo systemctl start httpd
   sudo systemctl enable httpd
   echo "Welcome to my website" | sudo tee /var/www/html/index.html
   ```

---

## **Step 6: Create a Target Group**
1. Go to **EC2** → **Target Groups** → **Create Target Group**.
2. Choose:
   - Type: **Instance**
   - VPC: `MyVPC`
   - Health check path: `/`
3. Register your EC2 instances.

---

## **Step 7: Create an Application Load Balancer**
1. Go to **Load Balancers** → Click **Create Load Balancer**.
2. Choose **Application Load Balancer (ALB)**.
3. Set up:
   - Name: `MyALB`
   - Scheme: **Internet-facing**
   - VPC: `MyVPC`
   - Subnets: **Public Subnets**
4. Create a **Listener**:
   - Protocol: **HTTP (80)**
   - Forward traffic to **Target Group**.
5. Click **Create Load Balancer**.

---

## **Step 8: Set Up AWS WAF**
1. Go to **AWS WAF & Shield** → Click **Web ACLs**.
2. Click **Create Web ACL**.
   - Name: `MyWebACL`
   - Resource: **Application Load Balancer**
3. Add rules (Optional):
   - **Block SQL Injection**.
   - **Block XSS Attacks**.
   - **Limit IP Requests**.
4. Associate it with **MyALB**.
5. Click **Create Web ACL**.

---

## **Step 9: Test the Setup**
1. Copy the **ALB DNS Name** from **EC2 > Load Balancers**.
2. Open it in a browser, and it should show `Welcome to my website`.
3. Test WAF by simulating SQL injection:
   ```sh
   curl "http://ALB-DNS-Name/?id=' OR 1=1--"
   ```
   - If WAF is working, it should block the request.

---

✅ **AWS WAF is now protecting your EC2 instances behind an ALB!** 