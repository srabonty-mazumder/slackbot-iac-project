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

1. Create test files:
   ```bash
   echo "Hello from Public Bucket" > public-test.txt
   echo "Hello from Protected Bucket" > private-test.txt
