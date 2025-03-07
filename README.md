# 🚀 AWS Cost Optimization - Identifying & Removing Stale EC2 Snapshots  

## 📖 Overview  
This project automates **AWS cost optimization** by identifying **stale EC2 snapshots** that have not been used for a long time.  
It removes **unnecessary snapshots** to **reduce AWS storage costs** and prevent resource wastage.  

## 🎯 Features  
✅ Scans AWS **EC2 snapshots** and identifies stale resources  
✅ **Automatically deletes** snapshots older than a set threshold  
✅ Sends **notifications to developers** via AWS **SNS**  
✅ Uses **AWS Lambda** for automation  
✅ Supports **scheduled execution** using **CloudWatch EventBridge**  

---

## 🛠️ AWS Services Used  
- **AWS Lambda** → Runs the script to check and delete stale snapshots  
- **AWS EC2** → Retrieves snapshot details  
- **AWS SNS** → Sends notifications to developers after deletion  
- **AWS CloudWatch EventBridge** → Automates scheduled execution  

---


---

## 🛠️ Prerequisites  
- **AWS Account** with appropriate permissions  
- **IAM Role** with the following permissions:  
  - `AmazonEC2ReadOnlyAccess` (to read snapshots)  
  - `AmazonEC2FullAccess` (to delete snapshots)  
  - `AmazonSNSFullAccess` (to send notifications)  
- **AWS CLI installed & configured** (for local testing)  
- **Python 3.x** (if running the script locally)  

---

## 🚀 Setup & Deployment  

### **1️⃣ Deploy AWS Lambda Function**  
1. Go to **AWS Lambda** → Click **Create function**  
2. Choose **"Author from scratch"**  
3. Set **Function Name** (e.g., `DeleteStaleSnapshots`)  
4. Select **Runtime:** `Python 3.x`  
5. Click **Create Function**  

### **2️⃣ Upload the Python Script**  
1. Click on your newly created Lambda function  
2. Go to the **Code** section  
3. Remove the existing content inside `lambda_handler(event, context):`  
4. Upload **`lambda_function.py`** (found in `/src/` folder)  
5. Click **Deploy**  

### **3️⃣ Configure Permissions (IAM Role)**  
1. Go to **Configuration** → **Permissions**  
2. Click **Create inline policy**  
3. Add the following permissions (**JSON format**) and save:  
   ```json
   {
       "Effect": "Allow",
       "Action": [
           "ec2:DescribeSnapshots",
           "ec2:DeleteSnapshot",
           "ec2:DescribeVolumes",
           "sns:Publish"
       ],
       "Resource": "*"
   }

   Test the Lambda Function

Click Test → Create a new test event

Give it a name (e.g., TestEvent)

Click Invoke

If you see an execution timeout error, go to Configuration → General settings

Increase the timeout to 10 seconds

Run the test again

5️⃣ Automate Execution with CloudWatch EventBridge

Go to EventBridge → Create Rule

Name it stale-snapshots-rule

Choose Schedule Expression

Set a cron job (e.g., run monthly):

cron(0 0 1 * ? *)

Choose AWS Lambda as the target

Click Create Rule

6️⃣ Enable Email Notifications via SNS

Go to AWS SNS → Create Topic

Select Standard and give it a name (e.g., StaleSnapshotsTopic)

Click Create Topic

Click on the topic and Create Subscription

Choose Protocol: Email, enter your email address, and click Create

Confirm the email by clicking the verification link sent to your inbox

Now, go back to Lambda → Configuration → Destinations

Add SNS Topic as a destination for successful execution



