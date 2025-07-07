# AWS-EC2-Instance-Setup-and-Vertical-Scaling-Guide
Setting up EC2 Instances and Vertical Scaling


## Overview

This guide provides step-by-step instructions to:
- Launch a virtual server (EC2 instance) on AWS
- Configure essential settings like key pair, security group, and AMI
- Perform **vertical scaling** (changing the instance type) for performance improvement

## Step 1: Launch an EC2 Instance
![instance types](https://github.com/user-attachments/assets/85b58be4-4b3e-449c-bc15-33612d34cd58)

### Using AWS Console

1. Sign in to AWS Console.
2. Navigate to **EC2** under "Compute".
3. Click **Launch Instance**.
4. Enter a name for your instance.
5. Select an Amazon Machine Image (AMI) like **Amazon Linux 2023**.
6. Choose an instance type t2.micro`.
7. Create or select an existing **Key Pair** (for SSH access).
![download pem file](https://github.com/user-attachments/assets/36adc8a6-6a6f-46dd-bbbe-1da200300ccc)
8. Configure networking: use custom VPC and subnet.
![vpc creation](https://github.com/user-attachments/assets/173e5d29-0b25-4009-b97e-2be3c03d7ae0)
9.Add inbound rules to allow HTTP(port 80) traffic from anywhere(0.0.0.0/0)
![inbound rules](https://github.com/user-attachments/assets/3200460e-5d1e-43d1-b3e5-99bd64868657)
10. Add storage (default: 8 GB gp3).
11. Click **Launch Instance**.

## Step 2: Connect to the Instance:

ssh -i aws-key-pair.pem ec2-user@13.217.110.182 --> SSH access
or
EC2 instance Connect -you can connect to your EC2 instance using EC2 Instance Connect — no need for a .pem file or SSH client.

1. Go to the **EC2 Dashboard**.
2. Click on **Instances** in the left sidebar.
3. Select the instance you want to connect to.
4. Click the **Connect** button at the top.
5. Choose the **EC2 Instance Connect** tab.
6. Leave the default username (e.g., `ec2-user` for Amazon Linux).
7. Click **Connect**.
![connecting to t3 micro](https://github.com/user-attachments/assets/1187bc7f-9c9b-4495-b0d8-8064dd87d171)
8. Access logs from AWS CLI
![accessing aws logs from instance](https://github.com/user-attachments/assets/c5a26cd3-40b2-422e-b34c-d88a0af3bbb4)


## Step 3: Perform Vertical Scaling (Change Instance Type)

To increase CPU, memory, or network capacity for an existing instance.

Example: Scale from t2.micro to m4.large
1.AWS Console: Right-click instance → Instance State → Stop

CLI:
bash

aws ec2 stop-instances --instance-ids i-0a7ad06e557a797ee

2.Modify the Instance Type
AWS Console:

Select the instance → Actions → Instance Settings → Change Instance Type

Choose a new instance type m4.lage

Save changes

![m4large](https://github.com/user-attachments/assets/e2ebab4c-0af7-45bb-a3dd-0ef62d58befe)
![change instance type](https://github.com/user-attachments/assets/92efb97c-30b2-4592-8343-6029f7e56161)


## can restrict terminating or stopping accidentally

![enabled termination protection](https://github.com/user-attachments/assets/44516432-cc5b-4673-a1ec-965e89daf038)
![shutdown behaviour](https://github.com/user-attachments/assets/c99f36ac-2825-4ad0-91fd-4df006731a2e)
![autorecovery](https://github.com/user-attachments/assets/55426a18-857b-4163-8243-070ef53e5d1b)







