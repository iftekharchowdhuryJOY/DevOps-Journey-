## Amazon Machine Image (AMI)
An Amazon Machine Image (AMI) is a pre-configured virtual machine image that provides the necessary information to launch an instance in Amazon EC2 (Elastic Compute Cloud). It acts as a template that includes an operating system, application server, and applications.

## Key Components of an AMI
1. Root Volume: The operating system and application data (Amazon EBS or Instance Store-backed).
2. Launch Permissions: Define who can use the AMI to launch instances.
3. Block Device Mapping: Specifies the storage volumes attached to the instance when launched.

## Types of AMIs
1. Public AMI: Available to all AWS users.
2. Private AMI: Only available to your AWS account.
3. AWS Marketplace AMI: Provided by third-party vendors.
4. Custom AMI: Created from an existing EC2 instance.

## Benefits of Using AMIs
1. Fast Deployment: Pre-configured environments for quicker instance launches.
2. Scalability: Easily replicate instances across different regions.
3. Customization: Modify and save custom AMIs for future use.
4. Security: AMIs can be made private and shared only with specific AWS accounts.

## Example: Creating a Custom AMI
Scenario: You want an AMI with Apache Web Server preinstalled.

1. Launch an EC2 instance using the latest "Amazon Linux" AMI.
2. Connect to the instance and install Apache:
```
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
```
3. Create AMI via AWS Console: Right-click the instance → Image and templates → Create Image.
4. Launch New Instances: Use the new AMI to deploy preconfigured web servers in seconds.
