## Step 1 completed earlier (from Task 6):

Launched a VM using Amazon Linux 2
SSH'ed into the VM
### Installed Apache manually:

sudo yum update -y
sudo yum install -y httpd
sudo systemctl enable httpd
sudo systemctl start httpd
echo "<h1>Hello from Task 7 Manual Install</h1>" | sudo tee /var/www/html/index.html

### Verified in browser: http://54.198.226.201/

### Screenshot: <img width="604" height="314" alt="Image" src="https://github.com/user-attachments/assets/53bfc5e9-80a5-4c72-b11d-2875780fe52f" />

### Step 2: The goal is to ensure the VM configures itself automatically without manual SSH installation.
Updated EC2Instance block in main.yaml 
EC2Instance:
  Type: AWS::EC2::Instance
  Properties:
    ImageId: ami-0c2b8ca1dad447f8a
    InstanceType: t2.micro
    KeyName: !Ref KeyPairName
    SubnetId: !Ref PublicSubnetAZ1
    SecurityGroupIds:
      - !Ref PublicSG
    UserData:
      Fn::Base64: |
        #!/bin/bash
        yum update -y
        yum install -y httpd
        systemctl enable httpd
        systemctl start httpd
        echo "<h1>Hello from automated Apache install (Task 7)</h1>" > /var/www/html/index.html
## This script automatically:
Installs Apache
Enables and starts the service
Creates /var/www/html/index.html
Confirms automation worked

## Deploy Updated CloudFormation Template
Go to AWS → CloudFormation → Create Stack
Upload main.yaml from the Task 7 folder
Stack name: slackbot-task7-srabonty
Wait for CREATE_COMPLETE
Open Outputs → VMPublicIP  → 52.87.157.212


## est Automated Apache Setup

Open your browser: 

http://52.87.157.212

## Screenshot: 
<img width="643" height="272" alt="Image" src="https://github.com/user-attachments/assets/edd011b6-f89d-45e4-a8be-bc4fcfdb60a0" />

