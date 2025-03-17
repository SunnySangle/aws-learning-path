# **Step-by-Step Guide to Creating an IAM Role, Attaching It to a User, and Granting Full S3 Access**

In this guide, you will learn how to:

✅ **Create an IAM Role**

✅ **Attach the Role to a User**

✅ **Grant Full S3 Access to the User**

---

## **🔹 Step 1: Create an IAM Role**

An IAM Role allows AWS services or users to access specific AWS resources securely.

### **1️⃣ Navigate to IAM Roles**

1. Log in to the **AWS Management Console**.
2. Search for **IAM** and open the **Identity and Access Management (IAM) Dashboard**.
3. Click on **"Roles"** in the left sidebar.
4. Click **"Create Role"**.

### **2️⃣ Select a Trusted Entity**

1. Choose **AWS Service** if you want an AWS service (like EC2) to assume this role.
2. Choose **Another AWS account** if you want a user from another AWS account to assume the role.
3. Choose **Custom Trust Policy** if you want to define specific conditions.
4. Click **Next**.

### **3️⃣ Attach Policies to the Role**

1. In the **Permissions policies** step, select the **AmazonS3FullAccess** policy.
2. Click **Next**.

### **4️⃣ Name and Create the Role**

1. Enter a **Role Name** (e.g., `S3FullAccessRole`).
2. Add a description (optional).
3. Click **Create Role**.

---

## **🔹 Step 2: Attach the Role to a User**

Now, we will attach the IAM Role to a specific user.

### **1️⃣ Navigate to IAM Users**

1. In the **IAM Dashboard**, click **"Users"** on the left sidebar.
2. Select the user to whom you want to attach the role.

### **2️⃣ Assign the Role to the User**

1. Click on the **"Permissions"** tab.
2. Click **"Add Permissions"** → **"Attach policies directly"**.
3. Search for `AmazonS3FullAccess` and select it.
4. Click **"Attach Policy"**.

---

## **🔹 Step 3: Verify Role & User Access**

### **1️⃣ Check the User’s Permissions**

1. Go back to **IAM → Users**.
2. Select the user.
3. In the **Permissions** tab, verify that the `AmazonS3FullAccess` policy is attached.

### **2️⃣ Test the Access**

1. Log in as the IAM user.
2. Open the **S3 Console**.
3. Try to **Create, Delete, and Upload files** in an S3 bucket.
4. If everything works fine, the role and permissions are correctly applied.

---

## **🎯 Summary of Steps**

1. **Create an IAM Role** (`S3FullAccessRole`).
2. **Attach the `AmazonS3FullAccess` Policy** to the Role.
3. **Assign the Role to a User**.
4. **Verify and Test Access**.