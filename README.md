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

## 📂 Project Structure  
