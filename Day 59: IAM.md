## IAM Policies 
Policy- JSON documents that define permissions 
Attached to: Users, groups, or roles
Types:
- AWS managed policies
- Customer managed policies
- Inline policies

## AWS evaluates permissions by combining all policies:

1. Default = Deny (if no policy → no access).

2. Explicit Deny > Allow (deny always wins).

3. Explicit Allow → access is granted unless denied elsewhere.

4. Permissions are cumulative (group + user + role).


# IAM Policy Structure

```code
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket", "s3:GetObject"],
      "Resource": [
        "arn:aws:s3:::mybucket",
        "arn:aws:s3:::mybucket/*"
      ]
    }
  ]
}
```
* Version → always "2012-10-17".
* Statement → list of rules.
* Effect → Allow or Deny.
* Action → API calls (e.g., ec2:StartInstances).
* Resource → ARN of resource (e.g., arn:aws:s3:::bucket/*).
* Condition → optional constraints (IP, MFA, time, tags).

## IAM Password Policy
You can enforce rules for IAM user passwords.

Examples:

Minimum length

Require numbers, uppercase, lowercase, special chars

Password expiration

Prevent password reuse

👉 Managed at the account level (not per user).


## Multi-Factor Authentication (MFA)
Adds a second layer of security. Even if password/keys are stolen → can’t login.

Options:

Virtual MFA App (Google Authenticator, Authy, AWS MFA app).

U2F Security Key (YubiKey, FIDO2 keys).

Hardware MFA Device (Gemalto tokens).

SMS MFA (for AWS GovCloud only, mostly deprecated).

👉 Exam tip: Virtual MFA is the most common.

## IAM Roles for AWS Services

Roles are used when AWS services need permissions:

* EC2 Role → instance profile, lets EC2 access S3/DynamoDB.

* Lambda Execution Role → allows Lambda to access DynamoDB/SQS.

* ECS Task Role → gives container-specific permissions.

* CloudFormation Service Role → allows CFN to create/manage resources.

👉 No long-term credentials, only temporary STS tokens delivered by AWS.


## IAM Security Tools

AWS provides built-in tools:

- IAM Credentials Report → lists all users, keys, MFA, last usage.

- IAM Access Advisor → shows last-used services for a user/role.

- Access Analyzer → detects resources (S3, KMS, IAM) shared with external accounts.

- Policy Simulator → test what a policy actually allows/denies.

# IAM Best Practices

 - Don’t use root account (enable MFA, lock it away).
 - Use IAM roles instead of embedding keys in apps.   
 - Grant least privilege (start restrictive → open up if needed).   
 - Rotate credentials regularly.   
 - Enable MFA for all IAM users.   
 - Use groups for permissions, not direct user policies.   
 - Audit IAM using Credentials Report & CloudTrail.   
 - Use IAM Access Analyzer to spot overly permissive access.

# IAM Integration Scenarios

 ## IAM + S3 (Accessing Buckets)

### Real-life example

-   You have an **EC2 app** that needs to **read/write S3 objects**.
    
-   Instead of embedding keys → use an **IAM Role** attached to the EC2 instance.

Policy Example

    {
      "Version": "2012-10-17",
      "Statement": [{
        "Effect": "Allow",
        "Action": ["s3:GetObject", "s3:PutObject"],
        "Resource": "arn:aws:s3:::mybucket/*"
      }]
    }

 Attach this to the **EC2 Role**.  
Now EC2 can fetch S3 creds from **Instance Metadata Service (IMDS)** automatically.

**Exam Tip:** If app can’t access S3 → check:

-   Role attached?
    
-   Policy correct resource ARN (bucket vs bucket/*)?

# IAM + CloudWatch (Logs/Monitoring)
### Real-life example

-   Lambda → needs permission to write logs to CloudWatch.
    
Policy:

    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "*"
    }



## What’s usually _extra_ on the exam (don’t skip):

-   **Temporary credentials (STS)** → `AssumeRole`, session duration, intersection of session policy & role policy.
    
-   **Cross-account roles** → trust policy + permission policy needed (they love this scenario).
    
-   **SigV4 signing** → for API Gateway & S3 presigned URLs (highly testable).
    
-   **Resource vs identity policies** → e.g., S3 bucket policy vs IAM user policy.
    
-   **Condition keys** → especially MFA (`aws:MultiFactorAuthPresent`), source IP (`aws:SourceIp`), request tags.
    
-   **Permissions boundaries vs SCPs** (know the difference conceptually).
