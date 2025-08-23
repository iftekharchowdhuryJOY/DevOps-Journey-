# Understanding Terraform and AWS Basics
The provider keyword tells Terraform which service provider to use. A provider is a plugin that Terraform uses to interact with a specific cloud service or platform.
```
provider "aws" {
  region = "ca-central-1"
}
```
- What it does: This configures Terraform to use AWS as the provider.
- Why it's needed: **Without it, Terraform wouldn't know how to communicate with AWS services.**

# Why we need region
Purpose: The region parameter specifies which AWS geographic region your resources will be created in.
# What happens if omitted:
If you don't specify a region, Terraform will look for it in: AWS_REGION environment variable. ~/.aws/config file If not found in either place, Terraform will fail with an error. Different regions have different availability of services, pricing, and latency to your users.  

# resource keyword
The resource keyword defines an infrastructure object that Terraform will manage. 
```
resource "aws_iam_user" "test_user" {
  name = "terraform-test-user"
}
```
# What it does: Tells Terraform to create, update, or delete a specific type of resource.
Format: resource "TYPE" "NAME" { ... }
## aws_iam_user
- What it is: This is a resource type specific to AWS, representing an IAM (Identity and Access Management) user.
- What it does: Creates a user account in AWS IAM, which could be used to access AWS services with specific permissions.
- Format: Always starts with the provider name (aws_) followed by the specific resource (iam_user).

## test_user
- What it is: This is a local name you assign to the resource within your Terraform configuration.
- Purpose: It's used to reference this specific resource elsewhere in your Terraform code.
- Not visible in AWS: This name (test_user) only exists in your Terraform code, not in AWS.
- Actual AWS name: The name of the IAM user in AWS is determined by the name parameter inside the resource block (in this case, "terraform-test-user").

## Complete Flow Example
- Terraform reads the provider "aws" block to know it needs to talk to AWS.
- It uses the region parameter to determine which AWS region to connect to.
- It reads the resource "aws_iam_user" "test_user" block to understand you want an IAM user.
- It creates an IAM user named "terraform-test-user" (from the name parameter).
In your Terraform code, you can reference this user as aws_iam_user.test_user.

