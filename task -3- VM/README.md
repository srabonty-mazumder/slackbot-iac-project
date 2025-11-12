# Task 3: VM Deployment

## Objective
Deploy a Linux VM using CloudFormation, SSH into it, and retrieve instance metadata.

## Steps

### 1. Pre-Req: Create SSH Key (only once, local machine)
Run on my laptop → open window PowerShell 
Write below command to create an SSH key:

ssh-keygen -t rsa -b 2048 -f slackbot-key-srabonty

Upload public key to AWS → EC2 → Key Pairs → Import

### 2. Deploy Stack
AWS → CloudFormation → Create Stack
Upload `main.yaml`
Stack Name: slackbot-task3-srabonty

Wait for WORK_IN_PROCESS to CREATE_COMPLETE.

### 3. Get Public IP
CloudFormation → Outputs → VMPublicIP 
Copy IP VP publicIP address show: 54.211.193.46

### 4. SSH into VM (from your PC)
ssh -i slackbot-key-srabonty ec2-user@54.211.193.46

### 5. Metadata Command on VM
curl http://169.254.169.254/latest/meta-data/

### 6. Screenshot
Include screenshot of metadata output here:



## Tags Used
- Course: CloudTraining
- Implementation: IaC
- Task: Task3
- Student: srabonty
- DeploymentType: sandbox
