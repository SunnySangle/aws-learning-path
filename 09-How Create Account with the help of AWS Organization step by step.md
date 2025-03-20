### **How to Create an AWS Account Using AWS Organizations**  

AWS Organizations allow you to **centrally manage** multiple AWS accounts. Follow these step-by-step instructions to create an AWS account using **AWS Organizations**.

---

## **Step 1: Sign in to AWS Organizations**  
1. Log in to your **AWS Management Console** as an **Administrator**.
2. Navigate to **AWS Organizations**:  
   - In the **search bar**, type **"Organizations"** and select **AWS Organizations**.

---

## **Step 2: Enable AWS Organizations (If Not Already Enabled)**  
1. If you haven't set up AWS Organizations, click **Create Organization**.  
2. Choose between:
   - **All Features** (Recommended) – Full control over accounts.
   - **Consolidated Billing Only** – Only manage billing.  
3. Click **Enable AWS Organizations**.

---

## **Step 3: Create a New AWS Account**  
1. In the left panel, click **Accounts**.
2. Click **Add an AWS Account** → **Create an AWS Account**.
3. Enter the following details:
   - **Account Name** (e.g., `Dev-Account`).
   - **Email Address** (must be unique and not used for any other AWS account).
   - **IAM Role Name** (default: `OrganizationAccountAccessRole`, used for cross-account access).
4. Click **Create AWS Account**.

---

## **Step 4: Verify the New Account**  
1. AWS will **send an email** to the provided email address.
2. Open the email and **verify the account** by following the instructions.
3. Log in to the new AWS account using the credentials provided.

---

## **Step 5: Manage the New AWS Account**  
Once created, you can:
- **View the new account** in **AWS Organizations** under the **Accounts** tab.
- **Manage permissions** using **Service Control Policies (SCPs)**.
- **Access the new account** via **AWS Single Sign-On (SSO)** or by logging in separately.

---

✅ **Done!** You have successfully created an AWS account using AWS Organizations.