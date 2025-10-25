## 1. VPC Design Overview

**Goal:**  
To deploy a web server (EC2) in a **private subnet** accessible only via:
- **CloudFront (Origin Access)**
- **SSM Session Manager (for administration)**

###  Key Design Principles
- No public IP assigned to the EC2 instance
- All traffic stays inside the AWS private network
- Access for management only via SSM
- CloudFront handles all external web requests

### 2 Private Subnets 

## 2. Security Groups Configuration

### a. Internal Application load balancer Security Group (`InternalLB-sg`)
**Purpose:** Allow HTTP traffic from the Cloudfront managed prefix list.
<img width="1920" height="935" alt="Screenshot (79)" src="https://github.com/user-attachments/assets/160b21a8-1e39-47b8-bbaa-f4ced658a29a" />

### b. EC2 Security Group (`Server-sg`)
**Purpose:** Allow HTTP traffic from the internal load balancer only.
<img width="1920" height="406" alt="Screenshot (109)" src="https://github.com/user-attachments/assets/e8e09c28-ff8d-4c90-99b7-4e17b249bb92" />

### c. SSM Endpoint Security Group (`SSM-endpoint-sg`)
**Purpose:** Allow HTTPS traffic from the the VPC CIDR.
<img width="1920" height="770" alt="Screenshot (99)" src="https://github.com/user-attachments/assets/709f42fe-e7bb-4572-bfec-251ac99db8d0" />


## 3. SSM Creation
- Steps (Console)

- Go to VPC Console → Endpoints → Create Endpoint

- Choose the service name (e.g., com.amazonaws.<region>.ssm)
<img width="1920" height="720" alt="Screenshot (100)" src="https://github.com/user-attachments/assets/1b57dcbf-f419-4d14-97d7-233e105187a0" />

<img width="1920" height="953" alt="Screenshot (101)" src="https://github.com/user-attachments/assets/2c9477d5-da76-4bfd-8747-58dbc6e76637" />


- Select your VPC and private subnet(s)
<img width="1920" height="471" alt="Screenshot (102)" src="https://github.com/user-attachments/assets/5b5ea736-ed2c-4d8b-914c-924338834971" />

- Attach the SG-SSM-Endpoint security group
<img width="1920" height="678" alt="Screenshot (103)" src="https://github.com/user-attachments/assets/1fe97d0b-e9d5-40f6-aa33-96b21a5165ee" />

- Enable Private DNS Name

Repeat for the other services listed below
| Service                                  | Type      | Endpoint Name   | Purpose                                         |
| ---------------------------------------- | --------- | --------------- | ----------------------------------------------- |
| com.amazonaws.<region>.ssm               | Interface | SSM             | Enables Session Manager commands                |
| com.amazonaws.<region>.ssmmessages       | Interface | SSM Messages    | Data channel for sessions                       |
| com.amazonaws.<region>.ec2messages       | Interface | EC2 Messages    | Communication between SSM agent and AWS backend |

### Endpoints created
<img width="1920" height="487" alt="Screenshot (110)" src="https://github.com/user-attachments/assets/ec7b5b98-e69d-4a24-a46b-629523d37ff5" />














