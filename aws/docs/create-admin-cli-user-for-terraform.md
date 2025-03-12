# Creating an Admin IAM User for AWS CLI v2 and Terraform Learning

This guide focuses specifically on creating and configuring an IAM user with administrative access for learning Terraform with AWS. This setup is **NOT** recommended for production environments.

## ⚠️ Important Limitations and Considerations

- This guide is for **learning purposes only**
- The IAM user created will have full administrative access
- This setup is **not suitable for production environments**
- This guide assumes you're using AWS CLI v2
- This setup is specifically for individual learning, not team environments

## Prerequisites

- An AWS account
- AWS CLI v2 installed on your machine
- Root account access (for initial IAM user creation only)

## Step-by-Step Setup

### 1. Create Admin IAM User

1. Sign in to AWS Console with root credentials
2. Go to IAM (Identity and Access Management)
3. Select "Users" → "Create user"
4. Username: Choose a descriptive name (e.g., "terraform-admin-cli")
5. **Important**: Uncheck "Provide user access to the AWS Management Console"
   - We only need programmatic access for Terraform and AWS CLI
   - Console access is not required for this learning setup

### 2. Assign Administrative Permissions

1. On the permissions page, select "Attach policies directly"
2. Search for and attach "AdministratorAccess"
   - ⚠️ This grants full access to all AWS services
   - This is acceptable for learning but never use in production

### 3. Create Access Keys

1. After user creation, select "Create access key"
2. Choose "Command Line Interface (CLI)"
3. ⚠️ Critical Security Notes:
   - Save both Access Key ID and Secret Access Key immediately
   - The Secret Access Key will never be shown again
   - Never share or commit these credentials
   - Store them securely on your local machine only

### 4. Configure AWS CLI v2

Run:

```bash
aws configure
```

Enter:

- AWS Access Key ID: (from step 3)
- AWS Secret Access Key: (from step 3)
- Default region: (e.g., us-east-1)
- Output format: json

### 5. Verify Setup

Verify your configuration:

```bash
aws configure list
```

Test API access:

```bash
aws sts get-caller-identity
```

If successful, you'll see your user ARN and account details.

## Configuration Files Location

AWS CLI v2 stores your configuration in:

- `~/.aws/credentials`: Contains access keys
- `~/.aws/config`: Contains region and output format

⚠️ Never commit the `.aws` directory to version control!

## Next Steps

With this admin user configured, you can now:

1. Follow the [official Terraform AWS tutorial](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-build)
2. Create and manage AWS resources via Terraform
3. Use AWS CLI v2 commands for verification and testing

## Security Warnings

1. This setup uses administrative access for learning purposes
2. Never use this configuration in production environments
3. Keep your access keys secure and private
4. Regularly rotate your access keys
5. Delete this admin user when you're done learning

## Troubleshooting

If `aws sts get-caller-identity` fails:

1. Check if credentials are correctly saved in ~/.aws/credentials
2. Verify AWS CLI v2 is installed: `aws --version`
3. Ensure no environment variables are overriding your configuration
