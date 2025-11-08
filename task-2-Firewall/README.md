# Task 2: Firewall for Slack Chatbot

This task extends Task 1 by adding firewall rules (Security Groups).

## Resources Created
- Public Security Group: allows 22, 80, 443 from the Internet
- Private Security Group: allows 22, 80, 443 only from Public SG

## Deployment Instructions
1. Go to AWS Academy Sandbox → CloudFormation
2. Create Stack → With new resources
3. Upload `main.yaml`
4. Click Next → Next → submit
5. Wait until status CREATE_COMPLETE

## Notes
- Public SG is used for resources exposed to the internet (e.g., API gateway/bastion)
- Private SG is for internal services (Lambda/database)
- Follows the least-privilege access model
- Parameters allow reuse later in the project
