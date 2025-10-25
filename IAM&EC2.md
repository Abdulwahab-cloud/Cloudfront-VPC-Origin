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
   <img width="1920" height="956" alt="Screenshot (80)" src="https://github.com/user-attachments/assets/23b6a90c-8c25-4b09-803e-eabcd0976a23" />

4. Choose **Use case:**  
   → **EC2**
5. Click **Next**
6. Attach the following managed policies:
   - ✅ `AmazonSSMManagedInstanceCore`
     <img width="1920" height="940" alt="Screenshot (81)" src="https://github.com/user-attachments/assets/05066669-7784-413b-9040-5a5cdd5a9a25" />

7. Click **Next**
8. Name your role:
   <img width="1920" height="936" alt="Screenshot (82)" src="https://github.com/user-attachments/assets/b01c53bc-8e6d-4b25-8269-f0ce52539745" />


## 2. EC2 Creation

- Go to EC2 → Instances → Launch Instance

- Choose:

- Name your EC2

- AMI: Amazon Linux 2023

- Instance Type: t2.micro (free-tier eligible)

- Key Pair: (not needed for SSM access)

- Under Network Settings:

- VPC: Select your project VPC

- Subnet: Choose Private Subnet

- Auto-assign Public IP: Disabled

- Security Group: Select The security group created before 'Server-sg'
<img width="1920" height="945" alt="Screenshot (83)" src="https://github.com/user-attachments/assets/6afb7f7e-836c-41dc-96d7-c77e4de53207" />

- Under IAM Instance Profile:
Select: EC2 Role Created before
<img width="1920" height="960" alt="Screenshot (84)" src="https://github.com/user-attachments/assets/c6204da8-28b6-4062-90f7-03b8ccf67f1a" />


## 3. Internal Application load balancer creation
 ### Objective

- Deploy an **Internal ALB** within a private subnet  
- Route traffic to **EC2 instances (VPC origin)**  
- Restrict access so only **CloudFront** and **VPC resources** can communicate with it  
- Ensure full **network isolation** (no public exposure)

  ###  Load Balancer Design Overview

| Component | Description |
|------------|-------------|
| **Type** | Application Load Balancer (ALB) |
| **Scheme** | Internal (accessible only inside VPC) |
| **Network** | Private Subnets |
| **Target Type** | Instance (private EC2 servers) |
| **Protocol** | HTTP (port 80) |
| **Listener** | Listens on port 80 and routes to target group |
| **Target Group** | EC2 instances running NGINX |

### Create Target Group

#### **Step 1:** Open **EC2 → Target Groups → Create Target Group**

- **Target Type:** `Instance`
- **Protocol:** `HTTP`
- **Port:** `80`
- **VPC:** Select your project VPC  
- **Health Check Path:** `/`
- **Health Check Protocol:** `HTTP`
<img width="1920" height="960" alt="Screenshot (85)" src="https://github.com/user-attachments/assets/03aca558-fdd5-4796-aee7-3fd905b08c8b" />

<img width="1920" height="947" alt="Screenshot (86)" src="https://github.com/user-attachments/assets/662af35e-c0c3-4014-8517-f4c5f01e8b48" />

#### Create Internal Load Balancer
- Step 1: Go to EC2 → Load Balancers → Create Load Balancer

- Select Application Load Balancer
<img width="1920" height="951" alt="Screenshot (87)" src="https://github.com/user-attachments/assets/fa5234d0-bf80-4d11-9d88-2dd81ea1fbf3" />

- Name it

- Scheme: Internal
  <img width="1920" height="956" alt="Screenshot (88)" src="https://github.com/user-attachments/assets/4319c6c5-6e5d-435a-a305-e1db678b92a1" />

IP address type: IPv4

Network Mapping:

Select your VPC

- Choose at least two private subnets (for HA)
<img width="1920" height="953" alt="Screenshot (89)" src="https://github.com/user-attachments/assets/48c54245-9372-487e-80a2-dee8a4d4c957" />

Security Group:

- Attach Security group (created before)
<img width="1920" height="953" alt="Screenshot (90)" src="https://github.com/user-attachments/assets/bb82176a-e5cc-434e-a118-10ca253be720" />

Listener:
Protocol: HTTP
Port: 80

- Forward to: (target group)
<img width="1920" height="951" alt="Screenshot (91)" src="https://github.com/user-attachments/assets/6a0381fd-bed5-4e72-94aa-6287f8e3aebe" />
- Create Load Balancer
  
    
