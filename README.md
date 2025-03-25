# AWS Cloud Cost Optimization - Identifying Stale EBS Snapshots

## 📌Project Overview
This project focuses on optimizing AWS cloud costs by identifying and deleting stale EBS snapshots using a Lambda function. The function automates the cleanup process by detecting snapshots that are no longer associated with active EC2 instances and removing them to reduce unnecessary storage costs.

## 🚀Features
- Automated Snapshot Cleanup: Identifies and deletes unassociated EBS snapshots.
- Lambda Function Execution: Runs on AWS Lambda with Python and Boto3.
- AWS IAM Role & Permissions: Configures necessary policies for snapshot management.
- Cost Optimization: Reduces AWS storage costs by deleting unused snapshots.
- Customizable Execution Time: Adjustable timeout to optimize function execution.

## 🛠️Setup Instructions

### Step 1: Launch an EC2 Instance
1. Create EC2 Instance:
   - Name: Any of your choice
   - OS: Ubuntu
   - Instance Type: t2.micro (modifiable)
   - Key Pair: .pem format (RSA encryption)
   - Default settings remain unchanged
   - Ensure a volume is connected (1 default, add more if needed)
2. Launch Instance and wait until the status changes to "Running".

### Step 2: Create EBS Snapshot
1. Identify your volume:
   - Check the last three characters of your volume ID (e.g., 98u, 456, jf4).
2. Create a snapshot:
   - Select "Volumes" in EC2 Dashboard.
   - Find the volume using the last three digits.
   - Add a description (e.g., "test").
   - Click "Create Snapshot".

### Step 3: Create an AWS Lambda Function
1. Go to AWS Lambda and create a new function:
   - Name: Any of your choice
   - Runtime: Python 3.10
   - Architecture: x86_64
   - Permissions: Default permissions (Modify later)
2. Copy the script from your GitHub repository and paste it into the Lambda function.
3. Save (Ctrl+S / Cmd+S) and Deploy.

### Step 4: Configure Lambda Test Event
1. Click "Test" → Create a new event.
2. Enter a name (e.g., "test").
3. Save and run the test (It will fail initially due to timeout and permission issues).

### Step 5: Modify Execution Timeout
1. Go to "Configuration" → "General Settings".
2. Edit the timeout and increase it to 10 seconds.
3. Save the settings.

### Step 6: Modify IAM Role & Permissions
1. Go to "Configuration" → "Permissions".
2. Click the linked IAM role to modify permissions.
3. Add permissions for managing EBS snapshots:
   - Click "Add Permissions" → "Attach Policies" → "Create Policy".
   - Choose "Service": EC2.
   - In "Actions Allowed", add:
     - DescribeSnapshots
     - DeleteSnapshot
   - Set "Resources" to "All".
   - Click "Next" → "Name Policy" → "Create Policy".
4. Attach the newly created policy to the Lambda role.

### Step 7: Execute Lambda Function
- Run the test again, and it will successfully identify and delete stale snapshots.
- If a snapshot is attached to an instance, it won't be deleted.
- Experiment with different scenarios by creating and deleting volumes & snapshots.

### Step 8: Cleanup
- Delete EC2 Instance: Shuts down associated volumes.
- Delete Lambda Function: To avoid unnecessary charges.
- Delete IAM Policies (if no longer needed).

## 📌Technologies Used
- AWS Lambda - Serverless function execution
- Amazon EC2 - Virtual machine management
- Amazon EBS - Elastic Block Store snapshots
- IAM Roles & Policies - Secure resource access
- Python (Boto3) - AWS SDK for automation

## 📜Problem Statement
### Challenge:
AWS users often accumulate unnecessary EBS snapshots, leading to increased storage costs. Manually identifying and deleting stale snapshots is inefficient and prone to errors.

### Solution:
This project automates the process of detecting and removing stale EBS snapshots using an AWS Lambda function. By leveraging Boto3, it scans all snapshots, checks if their associated volumes are in use, and deletes the stale ones to optimize storage costs.

## References
- AWS Boto3 Documentation: https://boto3.amazonaws.com/v1/documentation/api/latest/index.html
- AWS Lambda Guide: https://docs.aws.amazon.com/lambda/latest/dg/welcome.html

## ⚠️Important Notes
- AWS charges for running instances and Lambda execution time. Delete unused resources.
- Ensure proper IAM permissions to avoid security risks.
- Modify execution time carefully to balance cost and performance.

## 🏆Future Enhancements
- Implement a logging mechanism for snapshot tracking.
- Add SNS notifications when snapshots are deleted.
- Enhance with CloudWatch metrics for monitoring.

## 📜License
This project is licensed under the MIT License.

## 💬Contact
For any questions, feel free to reach out via GitHub Issues.
