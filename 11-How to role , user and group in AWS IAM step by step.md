### **How to Create a Role, User, and Group in AWS IAM (Step by Step)**  

In **AWS Identity and Access Management (IAM)**, you can create **Users, Groups, and Roles** to manage permissions efficiently. Below is a step-by-step guide to setting up all three.

---

## **Step 1: Create an IAM User**
IAM Users represent individuals or applications that need access to AWS services.

### **1.1 Sign in to AWS IAM Console**  
1. Log in to your **AWS Management Console**.
2. Navigate to **IAM (Identity and Access Management)**.

### **1.2 Create a User**
1. In the left panel, click **Users**.
2. Click **Add users**.
3. Enter a **User name** (e.g., `JohnDoe`).
4. Select **Access Type**:
   - **Programmatic access** (for CLI, SDK, API).
   - **AWS Management Console access** (for web access).
5. If enabling **console access**, set a password (either auto-generated or custom).
6. Click **Next**.

### **1.3 Assign the User to a Group (Optional)**
1. If a group exists, select it.
2. If not, click **Create group**:
   - Enter a **Group name** (e.g., `Developers`).
   - Attach policies (e.g., `AdministratorAccess`, `AmazonS3FullAccess`).
   - Click **Create group**.
3. Ensure the user is added to the group.
4. Click **Next**.

### **1.4 Attach Additional Policies (Optional)**
- If the user needs extra permissions, attach policies directly.

### **1.5 Review and Create User**
1. Review the settings.
2. Click **Create user**.
3. **Download .csv** to save login credentials.

---

## **Step 2: Create an IAM Group**
IAM Groups allow you to assign permissions to multiple users at once.

### **2.1 Create a Group**
1. In IAM, click **User Groups** in the left panel.
2. Click **Create group**.
3. Enter a **Group name** (e.g., `Developers`).
4. Attach permissions:
   - `AdministratorAccess` (Full control).
   - `AmazonS3FullAccess` (Full S3 access).
   - `AmazonEC2ReadOnlyAccess` (Read-only EC2 access).
5. Click **Create group**.

### **2.2 Add Users to the Group**
1. Click on the group name.
2. Select **Add users**.
3. Choose users to add.
4. Click **Add users**.

---

## **Step 3: Create an IAM Role**
IAM Roles are used to grant permissions to AWS services or external users.

### **3.1 Create a New Role**
1. In IAM, click **Roles** in the left panel.
2. Click **Create role**.
3. Choose a **Trusted Entity**:
   - **AWS Service** (e.g., EC2, Lambda).
   - **Another AWS Account** (for cross-account access).
   - **Web Identity** (e.g., Cognito, Google, Facebook).
4. Click **Next**.

### **3.2 Attach Policies**
1. Choose the permissions the role needs (e.g., `AmazonS3FullAccess`).
2. Click **Next**.

### **3.3 Configure Role Name and Description**
1. Enter a **Role name** (e.g., `EC2-S3-Access`).
2. Click **Create role**.

---

## **Step 4: Verify & Assign the Role**
1. Click **Roles** → Select the newly created role.
2. If the role is for an AWS service (e.g., EC2):
   - Go to **EC2 Instance** → **Modify IAM Role** → Attach the role.
3. If it's for cross-account access, share the **ARN** with the trusted account.

---

✅ **Done!** You have successfully created a **User, Group, and Role in AWS IAM**.