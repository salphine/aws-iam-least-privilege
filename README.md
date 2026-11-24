**AWS Cloud Security: IAM Least Privilege & S3 Baseline
**** Project Overview**
This project demonstrates the foundational cloud security concept of Least Privilege in AWS. The objective was to configure an Amazon S3 environment and create a programmatic IAM user that is strictly limited to read-only access for a specific bucket, ensuring they cannot delete, modify, or access any other resources in the AWS account.

** Architecture & Configuration**
The project was implemented in an AWS Sandbox environment and consists of the following components:

**Amazon S3 (Storage):**

Created a bucket named security-test-bucket-salphinechemos.

Enforced secure defaults by keeping "Block all public access" enabled.

Created a test directory/object (test.txt/) to test access controls.

**AWS IAM (Identity & Access Management):**

Custom Policy (S3ReadOnlySpecificBucket): Authored a custom JSON policy that explicitly allows s3:ListBucket and s3:GetObject, scoped strictly to the specific bucket ARN and its contents.

IAM User (s3-readonly-user): Created a programmatic user and attached the custom policy directly.

**The IAM Policy (JSON)**
Below is the exact policy used to enforce the least privilege principle:

json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
               "s3:ListBucket"
               ],
            "Resource": "arn:aws:s3:::security-test-bucket-salphinechemos"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::security-test-bucket-salphinechemos/*"
        }
    ]
}
     **Verification & Testing**
Note: Due to AWS Sandbox environment restrictions (new account verification limits), AWS CloudShell was temporarily unavailable for CLI testing. The verification logic below represents the expected behavior of the policy.

If tested via the AWS CLI with the s3-readonly-user credentials:

1. Allowed Operation (Read):

bash
# This command should succeed and list the bucket contents
aws s3 ls s3://security-test-bucket-salphinechemos/
2. Denied Operation (Delete):

bash
# This command should FAIL with an AccessDenied error
aws s3 rm s3://security-test-bucket-salphinechemos/test.txt/<img width="1352" height="593" alt="Screenshot 2026-11-23 175714" src="https://github.com/user-attachments/assets/aca53ce8-0e76-4f3a-a808-89ecab24b6b8" />
<img width="1348" height="604" alt="Screenshot 2026-11-23 175858" src="https://github.com/user-attachments/assets/03761740-b525-4aec-b03a-e1711d890158" />
<img width="1356" height="610" alt="Screenshot 2026-11-24 100221" src="https://github.com/user-attachments/assets/81bf51bb-5c23-4b8b-8606-6f1309d468a5" />
<img width="1358" height="603" alt="Screenshot 2026-11-24 100518" src="https://github.com/user-attachments/assets/4194b967-f825-4e44-939e-8c0cff9f8d21" />


