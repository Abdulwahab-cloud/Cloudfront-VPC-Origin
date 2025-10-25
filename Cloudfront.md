# CloudFront Distribution with VPC Origin

This guide walks through configuring **Amazon CloudFront** to serve content securely from a **VPC-based private origin** (an EC2 instance or internal load balancer).  
It ensures that your web content is **delivered globally** while keeping your origin **fully private and accessible only through CloudFront**.

# Step 1: Create the VPC Origin (Before CloudFront)

Your **origin** is where CloudFront retrieves your web content.  
In this setup, the origin will be :  
- An **Internal Load Balancer (recommended for scalability)**

  ### Go to the Cloudfront console and Select The VPC Origin 
    <img width="1920" height="960" alt="Screenshot (92)" src="https://github.com/user-attachments/assets/aa85fa63-95d9-4c2c-9afb-54aad45a3f3d" />

### Name your VPC Origin and Select the internal load balancer arn and protocol HTTP Only and create the VPC Origin
<img width="1920" height="964" alt="Screenshot (94)" src="https://github.com/user-attachments/assets/a29ae752-2620-4cd9-9fd0-6ff98e65e597" />

- VPC Origin will take a time to be provisoned and deployed wait for it

  ##  Open the CloudFront Console
  Go to **Amazon CloudFront > Create Distribution**.
  <img width="1920" height="957" alt="Screenshot (95)" src="https://github.com/user-attachments/assets/468e2d41-bf9f-4873-bd74-ad56b2536a98" />

  ### Select VPC Origin as Origin
  <img width="1920" height="593" alt="Screenshot (96)" src="https://github.com/user-attachments/assets/6cf44d5a-8035-4c08-b292-1cccab94ae34" />

 ### Select VPC Origin Created Before
 <img width="1920" height="926" alt="Screenshot (97)" src="https://github.com/user-attachments/assets/ba3a25eb-03ef-4fd8-a783-93aa8c9ed36f" />

 ### Customize Cache settings as below
 <img width="1920" height="964" alt="Screenshot (98)" src="https://github.com/user-attachments/assets/084c7137-0c92-4516-9fa1-6842b7f14c16" />

 ### then create the Distribution and access the domain name 
 <img width="1920" height="893" alt="Screenshot (106)" src="https://github.com/user-attachments/assets/af4fabd0-cda9-447f-a0dd-6a06bc0fbd5c" />


