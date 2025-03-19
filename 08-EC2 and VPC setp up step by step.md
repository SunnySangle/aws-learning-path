## **🚀 AWS EC2 & VPC Setup Step-by-Step Guide**  

This guide explains how to **set up a Virtual Private Cloud (VPC) and launch an EC2 instance** inside it.  

---

## **✅ Step 1: Create a VPC**  
1️⃣ **Login to AWS Console** → Open **VPC Service**  
2️⃣ Click **Create VPC**  
3️⃣ Enter VPC Name (e.g., `MyVPC`)  
4️⃣ **IPv4 CIDR Block**: `10.0.0.0/16`  
5️⃣ **Enable DNS Resolution**: ✅ Yes  
6️⃣ Click **Create VPC**  

---

## **✅ Step 2: Create Subnets**  
📌 **(Public and Private Subnet for better security)**  

### **🔹 Create a Public Subnet**  
1️⃣ Go to **VPC Dashboard** → Click **Subnets**  
2️⃣ Click **Create Subnet**  
3️⃣ Choose **VPC: MyVPC**  
4️⃣ Name it **PublicSubnet**  
5️⃣ Set **CIDR Block**: `10.0.1.0/24`  
6️⃣ Select an **Availability Zone**  
7️⃣ Click **Create Subnet**  

### **🔹 Create a Private Subnet**  
1️⃣ Click **Create Subnet** again  
2️⃣ Choose **VPC: MyVPC**  
3️⃣ Name it **PrivateSubnet**  
4️⃣ Set **CIDR Block**: `10.0.2.0/24`  
5️⃣ Select a different **Availability Zone**  
6️⃣ Click **Create Subnet**  

---

## **✅ Step 3: Set Up an Internet Gateway (IGW) for Public Access**  
1️⃣ Go to **VPC Dashboard** → Click **Internet Gateway**  
2️⃣ Click **Create Internet Gateway**  
3️⃣ Enter Name **MyIGW**  
4️⃣ Click **Create**  
5️⃣ Select **MyIGW** → Click **Attach to VPC**  
6️⃣ Choose **MyVPC** → Click **Attach**  

---

## **✅ Step 4: Configure Route Tables**  
### **🔹 Public Route Table (Allows Internet Access)**  
1️⃣ Go to **Route Tables** → Click **Create Route Table**  
2️⃣ Name it **PublicRouteTable**  
3️⃣ Choose **VPC: MyVPC**  
4️⃣ Click **Create Route Table**  
5️⃣ Select **PublicRouteTable** → Click **Edit Routes**  
6️⃣ Add Route:  
   - **Destination:** `0.0.0.0/0`  
   - **Target:** `Internet Gateway (MyIGW)`  
7️⃣ Click **Save**  
8️⃣ Click **Subnet Associations** → Select **PublicSubnet** → Click **Save**  

### **🔹 Private Route Table (For Private Instances - Optional)**  
1️⃣ Go to **Route Tables** → Click **Create Route Table**  
2️⃣ Name it **PrivateRouteTable**  
3️⃣ Choose **VPC: MyVPC**  
4️⃣ Click **Create Route Table**  
5️⃣ Click **Subnet Associations** → Select **PrivateSubnet** → Click **Save**  

---

## **✅ Step 5: Set Up Security Group for EC2**  
1️⃣ Go to **EC2 Dashboard** → Click **Security Groups**  
2️⃣ Click **Create Security Group**  
3️⃣ Name it **MyEC2SecurityGroup**  
4️⃣ Choose **VPC: MyVPC**  
5️⃣ **Inbound Rules** → Click **Edit Inbound Rules**  
   - Add **HTTP (80)** → **Anywhere (0.0.0.0/0)**  
   - Add **HTTPS (443)** → **Anywhere (0.0.0.0/0)**  
   - Add **SSH (22)** → **Your IP Only** (for security)  
6️⃣ Click **Create Security Group**  

---

## **✅ Step 6: Launch an EC2 Instance in VPC**  
1️⃣ Go to **EC2 Dashboard** → Click **Launch Instance**  
2️⃣ Enter Name: **MyWebServer**  
3️⃣ Select **Amazon Linux 2 AMI (Free Tier Eligible)**  
4️⃣ Choose **Instance Type**: `t2.micro`  
5️⃣ Click **Next: Configure Instance Details**  
6️⃣ **Network**: Select **MyVPC**  
7️⃣ **Subnet**: Select **PublicSubnet**  
8️⃣ **Auto-assign Public IP**: ✅ Enable  
9️⃣ Click **Next: Add Storage** → Keep default **8GB**  
🔟 Click **Next: Add Tags** → Add **Key: Name, Value: MyEC2**  
1️⃣1️⃣ Click **Next: Configure Security Group**  
   - Select **MyEC2SecurityGroup**  
1️⃣2️⃣ Click **Review and Launch**  
1️⃣3️⃣ Click **Launch** → **Create New Key Pair**  
   - Name it **MyKeyPair** → Download it  
1️⃣4️⃣ Click **Launch Instance**  

---

## **✅ Step 7: Connect to EC2 Instance**  
1️⃣ Go to **EC2 Dashboard** → **Instances**  
2️⃣ Select **MyWebServer** → Click **Connect**  
3️⃣ Choose **SSH Client**  
4️⃣ Open a terminal and run:  
   ```sh
   ssh -i MyKeyPair.pem ec2-user@<Public-IP>
   ```  
5️⃣ **You are now connected!** 🎉  

---

## **✅ Step 8: (Optional) Set Up a Private EC2 Instance**  
🔹 **If you need a backend EC2 instance (database, private app)**  
1️⃣ Repeat Step 6 but:  
   - Choose **PrivateSubnet**  
   - **No Public IP**  
   - Use a **different security group**  

📌 **Private EC2 needs a Bastion Host or NAT Gateway to connect to the internet.**  

---

## **🎯 Conclusion**  
✅ You created a **VPC with public & private subnets**.  
✅ Launched an **EC2 instance** inside the VPC.  
✅ Connected the EC2 instance **via SSH**.  

🚀 **Now you can deploy apps or host a website!** Let me know if you need help. 😊