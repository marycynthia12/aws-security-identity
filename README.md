AWS Security & Identity Management Project

Objective

In this project, I implemented core AWS Identity and Access Management (IAM) concepts by:

Creating an IAM user with restricted permissions,
Testing access for the IAM user,
Enabling Multi-Factor Authentication (MFA),
Creating and attaching a custom IAM policy to a role.

This project demonstrates how to secure AWS resources using best practices.

Step 1: Create an IAM User with Restricted Permissions

I logged into the AWS Management Console and navigated to the IAM dashboard.
1. Clicked on Users → Add Users

2. Entered a username; Restricted-user

3. Selected Uer access to AWS Management Console

4. Set a custom password for console access

5. Selected Attach policies directly

6. Attached a limited policy such as:

   AmazonS3ReadOnlyAccess (for read-only S3 access)

7. Clicked Next → Create User

Outcome:

I successfully created a user with restricted permissions.

Step 2: Test IAM User Access

To verify the restrictions:

Steps I followed:

1. Logged out of the root/admin account
2. Logged in using the IAM user credentials
3. Navigated to AWS services (S3)

Observations:

I user could view S3 buckets
I could NOT create or delete buckets

The restricted policy worked as expected.

Step 3: Set Up Multi-Factor Authentication (MFA)

To improve security, I enabled MFA for the IAM user.

Steps I followed:

1. Went to IAM → Users

2. Selected the created IAM user

3. Clicked on the Security credentials tab

4. Selected Assign MFA device

5. Chose Authenticator app

6. Scanned the QR code using:

   Google Authenticator 

7. Entered two consecutive codes from the app

8. Clicked Assign MFA

MFA was successfully enabled, adding an extra layer of security.

Step 4: Create a Custom IAM Policy

I created a custom policy to define specific permissions.

Steps I followed:

1. Navigated to IAM → Policies
2. Clicked Create Policy
3. Selected the JSON tab
4. Entered the following policy:

json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances"
      ],
      "Resource": "*"
    }
  ]
}


5. Clicked Next
6. Named the policy: EC2-ReadOnly-Custom
7. Created the policy

I successfully created a custom IAM policy.

Step 5: Create an IAM Role and Attach Policy

1. Navigated to IAM → Roles

2. Clicked Create Role

3. Selected:

   AWS Service
   Use case: EC2

4. Attached the custom policy:

   EC2-ReadOnly-Custom

5. Named the role: EC2ReadOnlyRole

6. Created the role

The IAM role was created and configured with the custom policy.

Step 6: Test Role Permissions

1. Launched an EC2 instance
2. Attached the IAM role (EC2ReadOnlyRole) to the instance
3. Connected to the instance via SSH
4. Ran AWS CLI command:
aws ec2 describe-instances

The command executed successfully
The instance could retrieve EC2 information

Conclusion:

The custom policy worked correctly when attached to the role.

What i learnt

IAM users should always follow the principle of least privilege,
MFA significantly improves account security,
Custom policies provide fine-grained control over AWS resources,
IAM roles are safer than embedding credentials in applications
<img width="1321" height="656" alt="SCREENSHOT OF TESTING ACCESS" src="https://github.com/user-attachments/assets/ed4ceaa5-076d-4cc0-b932-e3bc0526b675" />
