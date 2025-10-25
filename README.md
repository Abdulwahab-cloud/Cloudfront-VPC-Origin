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
  
  
