# Task 1: Networking for Slack Chatbot

This folder contains the CloudFormation template (`main.yaml`) for creating the networking layer of the Slack Chatbot project.

## Project Details
- Project Name: slackbot
- Student Name: srabonty

## Resources Created
- 1 VPC (10.0.0.0/16)
- 2 Public Subnets (10.0.1.0/24, 10.0.2.0/24)
- 2 Private Subnets (10.0.3.0/24, 10.0.4.0/24)

## Naming Convention
Format: `<project>-<task>-<resource>-<student>`  
Example: `slackbot-t1-public-az1-srabonty`

## Tags Applied
- Course = CloudTraining  
- Implementation = IaC  
- Task = Task1  
- Student = srabonty  
- DeploymentType = Sandbox

## Deployment Instructions
1. Go to **AWS Academy Sandbox → CloudFormation**.  
2. Click **Create Stack → With new resources (standard)**.  
3. Upload `main.yaml`.  
4. Click **Next → Next → Create Stack**.  
5. Wait until stack status = `CREATE_COMPLETE`.

## Notes
- Public subnets are for Slack API endpoints.  
- Private subnets are for backend services (Lambda, databases).  
- AZ1 and AZ2 ensure high availability.

