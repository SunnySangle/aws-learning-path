To create a **User**, add it to a **Group**, and attach **Policies** in AWS IAM, follow these step-by-step instructions:

---

## **Step 1: Sign in to AWS Management Console**
1. Go to **AWS Console**: [https://aws.amazon.com/console/](https://aws.amazon.com/console/)
2. Search for **IAM (Identity & Access Management)** and open it.

---

## **Step 2: Create a New IAM User**
1. In the **IAM Dashboard**, click **Users** (left panel).
2. Click **Add users** (top right).
3. Enter a **User name** (e.g., `JohnDoe`).
4. **Select AWS Access Type**:
   - **Programmatic access**: If the user needs access via CLI, SDK, or API.
   - **AWS Management Console access**: If the user needs to log in to the AWS Console.
   - If selecting **Console access**, set a password (either auto-generated or custom).
   - Choose whether to require password reset on first login.
5. Click **Next**.

---

## **Step 3: Add the User to a Group**
1. If a group already exists, **select it**.
2. If you need to create a new group:
   - Click **Create group**.
   - Enter a **Group name** (e.g., `Developers`).
   - Attach **permissions (policies)**, such as:
     - `AdministratorAccess` (Full access to AWS)
     - `AmazonS3FullAccess` (Full access to S3)
     - `AmazonEC2ReadOnlyAccess` (Read-only access to EC2)
   - Click **Create group**.
3. Ensure the user is **assigned to the correct group**.
4. Click **Next**.

---

## **Step 4: Attach Policies Directly (Optional)**
- If the user needs additional permissions beyond the group, attach policies manually:
  1. Click **Attach policies directly**.
  2. Search and select policies (e.g., `AmazonRDSFullAccess`, `AmazonS3ReadOnlyAccess`).
  3. Click **Next**.

---

## **Step 5: Review and Create User**
1. Review user details, group, and attached policies.
2. Click **Create user**.
3. AWS will display:
   - **Access Key ID** and **Secret Access Key** (if **Programmatic access** was selected).
   - A **sign-in link** for AWS Console access.
4. Click **Download .csv** to save credentials securely.

---

## **Step 6: Verify User and Permissions**
1. Go back to the **IAM Dashboard**.
2. Click **Users** and select the new user.
3. Under the **Permissions tab**, confirm:
   - The user is part of the correct **group**.
   - The correct **policies** are attached.

---

✅ **Done!** The IAM user is now created, added to a group, and has the necessary policies attached. 🚀