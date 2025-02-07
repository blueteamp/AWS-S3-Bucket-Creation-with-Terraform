## Deployment Steps

### 1. Install Prerequisites
Ensure you have the following installed:
- Terraform ([Download Here](https://developer.hashicorp.com/terraform/downloads))
- AWS CLI ([Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html))
- AWS Account with Access Keys

### 2. Configure AWS Credentials
Run the following command to configure AWS credentials:
```sh
aws configure
```
Enter your AWS access key, secret key, default region, and output format when prompted.

### 3. Initialize Terraform
Navigate to your Terraform project directory and run:
```sh
terraform init
```
This will initialize the working directory and download required providers.

### 4. Plan the Deployment
To preview the planned changes before applying them:
```sh
terraform plan
```

### 5. Apply the Configuration
To create the S3 bucket, run:
```sh
terraform apply
```
Type `yes` when prompted to confirm the changes.

### 6. Verify the S3 Bucket
Go to the AWS Management Console and navigate to **S3** to check if the bucket has been created successfully.

### 7. Upload an Object to S3
Modify `main.tf` to include an object upload, then reapply the configuration:
```sh
terraform apply
```
Confirm that the object appears in the bucket.

## Source Code

### main.tf
```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "my_bucket" {
  bucket = "my-terraform-bucket"

  tags = {
    Name        = "MyS3Bucket"
    Environment = "Dev"
  }
}

resource "aws_s3_bucket_public_access_block" "public_access" {
  bucket = aws_s3_bucket.my_bucket.id

  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}
```

## Customization
The S3 bucket is customized with tags:
- **Name**: Identifies the bucket
- **Environment**: Helps classify resources

## Challenges & Solutions
- **AWS Credentials Configuration**: Resolved using AWS CLI to set up access keys.
- **Terraform Initialization**: Used `terraform init` to configure the working directory.

## Next Steps
- Implement additional AWS services using Terraform.
- Automate S3 bucket lifecycle policies.

For detailed deployment steps, refer to `deployment_steps.md`.

