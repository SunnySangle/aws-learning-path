## **Step-by-Step Guide to Setting Up VPC Peering in AWS**  
VPC Peering allows private communication between two VPCs using private IPs. Follow these steps to set up VPC Peering between two VPCs (`VPC A` and `VPC B`).

---

## **Step 1: Create Two VPCs**  
1. **Go to AWS Console → VPC → Create VPC**.  
2. Create **VPC A**:
   - **VPC Name**: `VPC-A`
   - **IPv4 CIDR**: `10.0.0.0/16`  
   - Click **Create VPC**.  

3. Create **VPC B**:  
   - **VPC Name**: `VPC-B`
   - **IPv4 CIDR**: `192.168.0.0/16`  
   - Click **Create VPC**.

⚠️ **Ensure the CIDR blocks do not overlap**.  

---

## **Step 2: Create Subnets in Each VPC**  
1. **Go to AWS Console → VPC → Subnets → Create Subnet**.  
2. Select `VPC-A`, create a subnet:
   - **Subnet Name**: `Subnet-A`
   - **CIDR**: `10.0.1.0/24`
   - **Availability Zone**: Choose any.  

3. Select `VPC-B`, create a subnet:
   - **Subnet Name**: `Subnet-B`
   - **CIDR**: `192.168.1.0/24`
   - **Availability Zone**: Choose any.  

---

## **Step 3: Create a VPC Peering Connection**  
1. **Go to AWS Console → VPC → Peering Connections → Create Peering Connection**.  
2. Enter details:  
   - **Peering connection name**: `VPC-A-to-VPC-B`  
   - **Requester VPC**: `VPC-A`  
   - **Accepter VPC**: `VPC-B`  
   - Click **Create Peering Connection**.  
3. The request will now be pending.

---

## **Step 4: Accept the Peering Request**  
1. Go to **VPC → Peering Connections**.  
2. Find `VPC-A-to-VPC-B`.  
3. Click **Actions → Accept Request**.  
4. Status should now be **Active**.  

---

## **Step 5: Update Route Tables**  
Now, both VPCs need routes to communicate.

1. **Go to AWS Console → VPC → Route Tables**.  
2. Find the route table for `VPC-A`:  
   - Click **Routes → Edit Routes → Add Route**.  
   - **Destination**: `192.168.0.0/16` (VPC-B CIDR).  
   - **Target**: `VPC Peering Connection` (`VPC-A-to-VPC-B`).  
   - Click **Save Routes**.  

3. Find the route table for `VPC-B`:  
   - Click **Routes → Edit Routes → Add Route**.  
   - **Destination**: `10.0.0.0/16` (VPC-A CIDR).  
   - **Target**: `VPC Peering Connection` (`VPC-A-to-VPC-B`).  
   - Click **Save Routes**.  

---

## **Step 6: Update Security Groups**  
1. **Go to EC2 → Security Groups**.  
2. Edit **VPC-A Security Group**:
   - Allow **Inbound Rule**:  
     - **Protocol**: All TCP  
     - **Source**: `192.168.0.0/16` (VPC-B)  
3. Edit **VPC-B Security Group**:
   - Allow **Inbound Rule**:  
     - **Protocol**: All TCP  
     - **Source**: `10.0.0.0/16` (VPC-A)  

---

## **Step 7: Test the Peering Connection**  
1. **Launch EC2 Instances**:
   - One in `VPC-A` (`10.0.1.10`).
   - One in `VPC-B` (`192.168.1.10`).

2. **SSH into EC2 in VPC-A**:
   ```sh
   ssh ec2-user@10.0.1.10
   ```
3. **Ping EC2 in VPC-B**:
   ```sh
   ping 192.168.1.10
   ```
   ✅ If peering is working, you should receive responses.

---

## **VPC Peering is Now Set Up! 🎉**  
Now, resources in `VPC A` and `VPC B` can communicate securely.