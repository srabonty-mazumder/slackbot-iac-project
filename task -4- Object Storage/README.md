# Task 4: Object Storage (S3)

## Goal
Create two S3 buckets:
- Public bucket (readable by everyone)
- Protected bucket (private access)

## Deployment Steps

1. Go to AWS → CloudFormation → Create Stack.
2. Upload `main.yaml`.
3. Stack name: `slackbot-task4-srabonty`
4. Click Next → Next → Create Stack.
5. Wait until CREATE_COMPLETE.

## Verify Buckets
Go to AWS → S3 → Buckets.

You should see two new buckets:
- slackbot-public-srabonty-<accountID>
- slackbot-protected-srabonty-<accountID>

## Upload Test Files via CLI

### Inside your EC2 instance: 
1. Go to my laptop's PowerShell from my computer and command using the IP address to enter my EC2:

ssh -i .\slackbot-key-srabonty ec2-user@<54.234.184.169>
2. Create test files by writing a command:
   echo "Hello from Public Bucket" > public-test.txt
   echo "Hello from Protected Bucket" > private-test.txt
### Create the test files in CloudShell
1. Go to AWS Console, then click the CloudShell icon (top-right corner).
Write below command to create tast file: 
    $ echo "Hello from Public Bucket" > public-test.txt
    $ echo "Hello from Protected Bucket" > private-test.txt
### Now Upload to the PUBLIC bucket 
~ $ aws s3 cp public-test.txt s3://slackbot-public-srabonty-471112751828/
upload: ./public-test.txt to s3://slackbot-public-srabonty-471112751828/public-test.txt
### Upload to the PROTECTED bucket
~ $ aws s3 cp private-test.txt s3://slackbot-protected-srabonty-471112751828/
upload: ./private-test.txt to s3://slackbot-protected-srabonty-471112751828/private-test.txt
### Verify files
~ $ aws s3 ls s3://slackbot-public-srabonty-471112751828/
2025-11-19 16:54:33         25 public-test.txt
~ $ aws s3 ls s3://slackbot-protected-srabonty-471112751828/
2025-11-19 16:54:45         28 private-test.txt

