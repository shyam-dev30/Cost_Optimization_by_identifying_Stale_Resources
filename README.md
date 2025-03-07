# 🚀 AWS Cost Optimization - Stale EC2 Snapshots Cleanup

## 📌 Overview  
This project automates AWS cost optimization by identifying stale EC2 snapshots that have not been used for a long time. It removes unnecessary snapshots to reduce storage costs.
![AWS Lambda Function](images/screenshot.png)

---

## 🛠️ Prerequisites  
- **AWS Account** with appropriate permissions  
- **IAM Role** with the following permissions:  
  - `AmazonEC2ReadOnlyAccess` (to read snapshots)  
  - `AmazonSNSFullAccess` (to send notifications)    
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
   ```  

### **4️⃣ Test the Lambda Function**  
1. Click **Test** → Create a new test event  
2. Give it a name (e.g., `TestEvent`)  
3. Click **Invoke**  
4. If you see an **execution timeout error**, go to **Configuration** → **General settings**  
5. Increase the timeout to **10 seconds**  
6. Run the test again  

### **5️⃣ Automate Execution with CloudWatch EventBridge**  
1. Go to **EventBridge** → **Create Rule**  
2. Name it **`stale-snapshots-rule`**  
3. Choose **Schedule Expression**  
4. Set a cron job (e.g., run monthly):  
   ```cron
   cron(0 0 1 * ? *)
   ```  
5. Choose **AWS Lambda** as the target  
6. Click **Create Rule**  

### **6️⃣ Enable Email Notifications via SNS**  
1. Go to **AWS SNS** → **Create Topic**  
2. Select **Standard** and give it a name (e.g., `StaleSnapshotsTopic`)  
3. Click **Create Topic**  
4. Click on the topic and **Create Subscription**  
5. Choose **Protocol: Email**, enter your **email address**, and click **Create**  
6. **Confirm the email** by clicking the verification link sent to your inbox  
7. Now, go back to **Lambda → Configuration → Destinations**  
8. Add **SNS Topic** as a destination for successful execution  

---

## 🎯 Conclusion  
Your AWS Lambda function is now configured to automatically identify stale EC2 snapshots, delete them, and notify developers via AWS SNS. This setup helps in cost optimization by removing unnecessary storage expenses.

🚀 **Happy Cloud Optimization!**

