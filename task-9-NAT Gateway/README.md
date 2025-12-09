# Task 9 – NAT Gateway (Step-by-Step Instructions)

This README explains exactly how to reproduce my setup:

- VPC with **public + private** subnets  
- **NAT Gateway** in the public subnet  
- **Bastion host** in public subnet  
- **Private EC2** in private subnet (no public IP)  
- App (Apache + test page) installed via
- **user data** and verified from inside the private EC2

### 1. Prerequisites

AWS account with permission to use EC2, VPC, IAM, and CloudFormation.
AWS region selected (e.g., us-east-1).
OpenSSH client is installed on my computer.
PowerShell or a terminal on my local machine.

### 2. Create SSH Key Pair (for EC2)
Though I am working on the AWS sandbox, so I have to repeat key pair creation and install the VM (task 3)  
In AWS Console, go to: EC2 → Key pairs → Create key pair.
Set: Name: slackbot-key-srabonty    Type: RSA  Private key format: PEM
Click Create key pair and download the file
Save it as: C:\AWSKeys\slackbot-key-srabonty.pem
Fix permissions on Windows (PowerShell):
icacls "C:\AWSKeys\slackbot-key-srabonty.pem" /inheritance:r
icacls "C:\AWSKeys\slackbot-key-srabonty.pem" /grant:r "$($env:USERNAME):R"

### 3. Deploy the CloudFormation Template
In AWS Console, go to CloudFormation → Stacks → Create stack → With new resources (standard).
Choose Upload a template file and select slackbot-task3-9.yaml from this folder.
Click Next. Stack name: slackbot-task-9
Parameters: KeyPairName → select slackbot-key-srabonty
All others → leave as default
Click Next → Next → Create stack.
Wait until the status is CREATE_COMPLETE.

### The stack will create:
VPC with public and private subnets
Internet Gateway and NAT Gateway
I tried to connect to the EC2 Instance private, but AWS sandbox limitations, I cannot create an  IAM allows EC2 instance, that why I  use the Bastion EC2 instance 
Bastion EC2 instance (public subnet) 
Private EC2 instance (private subnet)
Routing and security groups

<img width="852" height="504" alt="Image" src="https://github.com/user-attachments/assets/43e41417-aeda-4da9-995a-e7fe107c571f" />

### Connect to bastion (Task 3 VM)
From my PC:
ssh -i "C:\AWSKeys\slackbot-key-srabonty.pem" ec2-user@18.234.39.61
Use the BastionPublicIP from CloudFormation Outputs or EC2 console.
get permission :
icacls "C:\AWSKeys\slackbot-key-srabonty.pem" /inheritance:r
icacls "C:\AWSKeys\slackbot-key-srabonty.pem" /remove:g "BUILTIN\Users"
icacls "C:\AWSKeys\slackbot-key-srabonty.pem" /grant:r "$($env:USERNAME):R"

Now I have inside EC2 instance inside using Bastion : 

On the bastion, I  can run:
curl http://169.254.169.254/latest/meta-data/

Get an IMDSv2 token:
TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" \
  -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`

Use the token to request metadata:
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
  http://169.254.169.254/latest/meta-data/
  
#### Screenshot of my practice:
<img width="947" height="489" alt="Image" src="https://github.com/user-attachments/assets/dbf4a53a-6b1f-43e9-9f45-21aed17b0651" />

### 5. Connect bastion → private EC2 (Task 9 VM)
On my PC, copy the key to bastion:
scp -i "C:\AWSKeys\slackbot-key-srabonty.pem" C:\AWSKeys\slackbot-key-srabonty.pem ec2-user@18.234.39.61:/home/ec2-user/
On bastion: chmod 400 slackbot-key-srabonty.pem
ls -l
Get the private instance’s private IP from the EC2 console (instance name: slackbot-privatevm-srabonty).
From bastion: ssh -i slackbot-key-srabonty.pem ec2-user@10.0.2.174

Once inside the private instance → run the verification commands
<img width="956" height="449" alt="Image" src="https://github.com/user-attachments/assets/9999c393-fb32-44cf-b5df-bdd0040ed9fd" />

#### 1. Check NAT (internet access): curl https://google.com
#### 2. Check Apache sudo systemctl status httpd
#### 3. Verify the local web app

#### Screenshot of my practice:
<img width="852" height="504" alt="Image" src="https://github.com/user-attachments/assets/bda54a16-ee40-4b70-be26-8d7368be2eed" />




