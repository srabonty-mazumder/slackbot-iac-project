# Task 6: Custom VM Image
## 1. Launch Base VM
### 1. Pre-Req: Create SSH Key (only once, local machine)
Run on my laptop → open window PowerShell 
Write below command to create an SSH key:

ssh-keygen -t rsa -b 2048 -f slackbot-key-srabonty
Upload public key to AWS → EC2 → Key Pairs → Import

### 2. Deploy Stack
AWS → CloudFormation → Create Stack
Upload `main.yaml.`
Stack Name: slackbot-task3-srabonty

Wait for WORK_IN_PROCESS to CREATE_COMPLETE.

### 3. Get Public IP
CloudFormation → Outputs → VMPublicIP 
Copy IP VP publicIP address show: 54.144.111.105

### 4. SSH into VM (from your PC)
ssh -i .\slackbot-key-srabonty ec2-user@54.144.111.105

## 2. Install Apache HTTP Web Server
Inside the EC2 terminal:
sudo yum update -y
sudo yum install -y httpd
sudo systemctl enable httpd
sudo systemctl start httpd

### Create a test webpage:
echo "<h1>Hello from slackbot custom VM image</h1>" | sudo tee /var/www/html/index.html

## 4. Test HTTP Access
Open browser: http://54.144.111.105/
<img width="806" height="322" alt="Image" src="https://github.com/user-attachments/assets/15b919df-7664-4996-899c-e57e47687f11" />


### 5. Create a Custom AMI

EC2 → Instances
Select task6-base-vm
Actions → Image and Templates → Create Image
Image name: slackbot-custom-image-srabonty
Submit and wait
Go to EC2 → AMIs
Confirm status = Available
Screenshot of practice: 
<img width="956" height="167" alt="Image" src="https://github.com/user-attachments/assets/4d852cf7-58d6-4a14-9580-762b9a179e8f" />


## 6. Attempt to Launch a VM from Custom AMI (Sandbox Restriction)
<img width="952" height="382" alt="Image" src="https://github.com/user-attachments/assets/7bd510ae-d3e0-4bd1-990b-bd49ececf9a5" />
