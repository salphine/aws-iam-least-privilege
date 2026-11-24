# AWS Cloud Security: IAM Least Privilege & S3 Baseline

## 📌 Project Overview
This project demonstrates the foundational cloud security concept of **Least Privilege** in AWS. The objective was to configure an Amazon S3 environment and create a programmatic IAM user that is strictly limited to read-only access for a specific bucket, ensuring they cannot delete, modify, or access any other resources in the AWS account.

## 🏗️ Architecture & Configuration
The project was implemented in an AWS Sandbox environment and consists of the following components:

**1. Amazon S3 (Storage):**
* Created a bucket named `security-test-bucket-salphinechemos`.
* Enforced secure defaults by keeping "Block all public access" enabled.
* Created a test directory/object (`test.txt/`) to test access controls.

**2. AWS IAM (Identity & Access Management):**
* **Custom Policy (`S3ReadOnlySpecificBucket`):** Authored a custom JSON policy that explicitly allows `s3:ListBucket` and `s3:GetObject`, scoped strictly to the specific bucket ARN and its contents.
* **IAM User (`s3-readonly-user`):** Created a programmatic user and attached the custom policy directly.

## 💻 The IAM Policy (JSON)
Below is the exact policy used to enforce the least privilege principle:

```json
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
}<img width="1352" height="593" alt="Screenshot 2026-11-23 175714" src="https://github.com/user-attachments/assets/ba10fed7-c3ff-4d61-8a77-bd935aaaafaa" />
<img width="1348" height="604" alt="Screenshot 2026-11-23 175858" src="https://github.com/user-attachments/assets/cba89fcb-edd7-45ce-b7b1-e54020e699fe" />
<img width="1356" height="610" alt="Screenshot 2026-11-24 100221" src="https://github.com/user-attachments/assets/06293059-67bc-4bed-addc-895658abd428" />
<img width="1358" height="603" alt="Screenshot 2026-11-24 100518" src="https://github.com/user-attachments/assets/91a1d839-227e-4ea4-82e0-02c786b162ac" />
