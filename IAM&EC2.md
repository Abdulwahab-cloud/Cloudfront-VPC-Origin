# IAM Role & EC2 Configuration Guide

This document details how to create and configure the **IAM Role** and **EC2 instance** for the CloudFront + VPC Origin + SSM Endpoint project.

It ensures that your EC2 instance:
- Operates **without a public IP**
- Uses **SSM Session Manager** for management


##  1. IAM Role Creation

### Objective
Create an IAM role that grants your EC2 instance permission to:
- Use **AWS Systems Manager (SSM)** for session access

###  Step-by-Step (Console)

1. Go to the **IAM Console → Roles → Create Role**
2. Choose **Trusted entity type:**  
   → **AWS Service**
   
4. Choose **Use case:**  
   → **EC2**
5. Click **Next**
6. Attach the following managed policies:
   - ✅ `AmazonSSMManagedInstanceCore`
   
7. Click **Next**
8. Name your role:  
