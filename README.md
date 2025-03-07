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

