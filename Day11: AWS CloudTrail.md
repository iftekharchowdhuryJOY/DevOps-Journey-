> Sample Question: A company has grown from a small startup to an enterprise employing over 1000 people. As the team size has grown, the company has recently observed some strange behavior, with Amazon S3 buckets settings being changed regularly.
How can you figure out what's happening without restricting the rights of the users?<br/>

Answer: **Use AWS CloudTrail to analyze API calls**

## AWS Cloudtrail<br/>
**FOCUSES ON WHO DID WHAT (API activity)**
1. It is a managed service.
2. In my whole AWS infra who is doing what, all sorts of actions taken by users, roles or services, API activity all are monitored by AWS cloudtrail.
3. logs are there

## Why Use AWS CloudTrail?
1. Auditing & Compliance.
2. Meet regulatory requirements (e.g., GDPR, HIPAA) by maintaining an audit trail.
3. Security Analysis - Detect unauthorized access or suspicious activity (e.g., API calls from unfamiliar IPs).
4. Operational Troubleshooting: Diagnose issues by reviewing API call histories (e.g., failed EC2 instance launches).
5. Automation



AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. With AWS CloudTrail, you can log, continuously monitor, and 
retain account activity related to actions across your AWS infrastructure. AWS CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management 
Console, AWS SDKs, command-line tools, and other AWS services. In general, to analyze any API calls made within an AWS account, AWS CloudTrail is used. You can record the actions that are taken by users, roles, 
or AWS services on Amazon S3 resources and maintain log records for auditing and compliance purposes. To do this, you can use server access logging, AWS CloudTrail logging, or a combination of both. AWS recommends that 
you use AWS CloudTrail for logging bucket and object-level actions for your Amazon S3 resources.

## Key Concepts

1. Trails - A configuration that defines which events to log.
2. Event types - Three events. 1) control plane 2) data plane 3) insights events
3. Log files - **JSON logs stored in an S3 bucket (immutable and encrypted by default)**
4. Integration: cloudwatch, eventbridge, athena

**Root account activity is always logged. To monitor root account logins, create a CloudWatch alarm for eventName=RootLogin**

## Important tips
1. Enable Multi-Factor Authentication (MFA) Delete on the S3 bucket storing logs.
2. Use SSE-KMS encryption for CloudTrail logs (control access via KMS keys).
3. To build a real-time security alert system → CloudTrail → EventBridge → Lambda.
4. Organization Trail: 1) Centralized logging for all accounts in AWS Organizations. 2) Created in the management account and auto-applies to all regions.
5. Mangement events - Logged by default (stored for 90 days in the CloudTrail Console).
6. To track unauthorized changes to an S3 bucket’s policy, use CloudTrail.

## COST



1. Free Tier
Management Events (Control Plane): AWS automatically logs management events (e.g., creating/deleting resources, modifying IAM roles) for free. These logs are stored in the CloudTrail Event History (retained for 90 days).
* One Trail: You can create one single-region trail (logging management events to an S3 bucket) for free.
2. Cost to watch for
  * $0.10 per 100,000 events (e.g., S3 GetObject, Lambda Invoke, DynamoDB PutItem).
  * Enable data events selectively (e.g., only for critical S3 buckets or Lambda functions).
  * $2.00 per trail per region (beyond the first free trail).
  * $0.35 per GB of log data analyzed
 
3. Monitor CloudTrail costs via AWS Cost Explorer or billing alerts.

## Free vs. Paid Summary
| Feature     | Free? |
| ----------- | ----------- |
| Management Events	Free       | (90-day history in Console)      |
| One Single-Region Trail	Free    | (management events only)        |
| Data Events    | Paid ($0.10/100k events)        |
| Additional Trails    | Paid ($2.00/trail/region)        |
| CloudTrail Insights    | Paid ($0.35/GB analyzed)        |
| S3 Storage	   | Paid (standard S3 rates apply)       |


