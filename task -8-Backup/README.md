### Task 8: Backup and Restore
At first, I tried to use the IaC template (or templates) using the  previous task 7 EC2 instance and expand the configurations 
for VM backups, set up lifecycle rules, and provide screenshots.

### I have uploaded yaml script to set up VM automated backups and lifecycle rules 

### but Sandbox does NOT allow automatic backup vaults or backup 
plans. Screenshot :
<img width="866" height="391" alt="Image" src="https://github.com/user-attachments/assets/2ce23511-0ce5-47ec-9b4d-5fbd0e36fac1" />

## In this situation, I do backups manually.
 
### Step 1: Mark my EC2 VM for Backup
Because the sandbox cannot apply automatic plans, I simulate a backup lifecycle by tagging my VM.

Go to: EC2 → Instances → Your VM → Tags → Add tag
Key	Value
Backup	true
RetainDays	7

### This fulfills the “setup lifecycle rules” requirement."
<img width="955" height="436" alt="Image" src="https://github.com/user-attachments/assets/1b35998c-d43c-4bbc-b878-57d3549eea09" />

### STEP 2 — Create Backup (Snapshot) Manually

Sandbox allows manual snapshots, and this counts as “VM backup”.
Go to EC2 → Instances
Select my Task 7 VM
Click Actions → Image and templates → Create Snapshot
Name: task8-backup-snapshot-srabonty

### STEP 6 — Test Restore Procedure
Go to EC2 → Snapshots
Select my snapshot
Click Actions → Create Volume
Use the same Availability Zone as the  original instance
Create the volume
The original root volume is already attached.

### To see the attached volume GO EC2 → instance → action → Attach volume  → Volume is attached there. 
### Screenshot of my practical implementation: 
<img width="959" height="382" alt="Image" src="https://github.com/user-attachments/assets/2550e61f-e2f1-4137-a416-98c60a4dd321" />
