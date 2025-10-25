CloudFront with VPC Origin & SSM Endpoint

A simple yet elegant demo project showcasing how to deliver a web application securely through **Amazon CloudFront** with a **VPC origin**, using **Internal load balancer, EC2, SSM, and private networking** on **Amazon Linux 2023**.

---

##  Architecture Overview

**Components Used:**
- **Amazon CloudFront** – Global CDN delivering content securely.
- **VPC Origin internal application load balancer (Private EC2)** – NGINX web server in a private subnet.
- **SSM Session Manager** – Secure access to EC2 instance without public IP.
- **VPC Endpoints** – For private connectivity to SSM.
- **IAM Roles & Security Groups** – For least privilege and network isolation.

  **Architecture Diagram**
  <img width="2469" height="1040" alt="Cloudfront-VPCOrigin" src="https://github.com/user-attachments/assets/4f5ed851-46b3-44e8-b795-d3bf80dc5302" />


  ## VPC Origin created
  <img width="1920" height="968" alt="Screenshot (107)" src="https://github.com/user-attachments/assets/6f9d1ddb-997c-4ac0-9ec3-7099ae6f9de3" />

  ## Cloudfront Distribution
  <img width="1920" height="893" alt="Screenshot (106)" src="https://github.com/user-attachments/assets/5846531c-1422-4f50-b800-1b8a6082d357" />

  ## Access the app inside private EC2 instance through Cloudfront using VPC Origin
  <img width="1920" height="1137" alt="Screenshot (108)" src="https://github.com/user-attachments/assets/8f7e9daa-a927-4a65-9d84-41a17dd12cf1" />

  
  
