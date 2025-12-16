AWS S3 — the architect’s mental model

One sentence truth:
S3 is infinitely scalable object storage, optimized for durability, not low latency.

Objects live in buckets

Buckets live in regions

Objects are immutable by default

Everything is API-driven

1. What is S3 (plain English)

Think of S3 as:

A global hard drive

That never runs out of space

Never loses data (11 nines durability)

But is not a filesystem

You don’t “mount” S3.
You PUT, GET, DELETE objects.

2. Real-life use cases (how companies actually use it)
Use case	Who uses it
Static website hosting	Startups, landing pages
App assets (images, videos)	Almost every SaaS
Data lake	Netflix, Airbnb
Backups	Everyone sane
Logs (ALB, CloudTrail)	Security teams
ML training data	AI companies
Cross-region DR	Enterprises

Rule of thumb:
👉 If data must survive disasters, it belongs in S3.

3. S3 in system design

S3 usually sits here:

User
 ↓
CloudFront
 ↓
S3  ←→  Lambda / Athena / Glue


Or:

App → S3 (uploads)
App → DynamoDB (metadata)


What S3 is NOT

Not a database

Not for millisecond reads (unless cached)

Not transactional

SECURITY (this is where people fail exams and production)
2. S3 security – Bucket Policy (console, hands-on concept)

Bucket policy = resource-based policy

It answers:

“Who can access THIS bucket?”

Simple example (public read – DON’T DO THIS IN PROD)
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Principal": "*",
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::my-bucket/*"
  }]
}

Reality check

IAM policy → attached to users/roles

Bucket policy → attached to bucket

Both must allow

3. Advanced bucket policies (exam gold)
Enforce HTTPS only
"Condition": {
  "Bool": { "aws:SecureTransport": "false" }
}

Restrict to VPC endpoint
"Condition": {
  "StringEquals": {
    "aws:sourceVpce": "vpce-123"
  }
}

Allow cross-account access
"Principal": {
  "AWS": "arn:aws:iam::ACCOUNT_ID:root"
}


Production truth:
Most breaches = bad bucket policies.

4. S3 Versioning

What it does

Keeps multiple versions of objects

Deletes become delete markers

Why it exists

Protection from:

Accidental deletes

Ransomware

Bad deployments

Costs

You pay for every version

Best practice

Enable versioning

Combine with lifecycle rules

5. Troubleshooting S3 (real-world)
Symptom	Cause
AccessDenied	IAM + bucket policy mismatch
403 via CloudFront	OAC / OAI misconfigured
High cost	Old versions + no lifecycle
Slow uploads	No multipart upload
Replication failing	IAM role missing permissions

Debug tools:

IAM Policy Simulator

S3 Access Logs

CloudTrail

6–7. S3 Replication (same & cross-account)

What it is

Async copy of objects

Requires versioning ON

Use cases

DR

Compliance

Data residency

Cross-account replication

You need:

Source bucket policy

Destination bucket policy

IAM role trusted by S3

Exam trap: replication ≠ backup
Deletes replicate too (unless filtered).

8. S3 Lifecycle Rules (hands-on logic)

Lifecycle rules automate storage tier movement.

Typical rule
Day 0   → S3 Standard
Day 30  → IA
Day 90  → Glacier
Day 365 → Delete


Cost reality

This saves thousands.

Not optional in real companies.

9. S3 Event Notifications

Trigger actions when objects change.

Targets:

Lambda

SQS

SNS

EventBridge

Example

Upload image → Lambda resizes → saves thumbnail

Limitation

No retries

Use SQS for durability

10. S3 Performance

Facts:

Unlimited throughput

Prefix-based scaling no longer needed (old myth)

Optimizations:

Multipart uploads

CloudFront in front

Byte-range GETs

11–12. S3 Batch Operations

What

Perform actions on millions of objects

Actions:

Copy

Delete

Restore from Glacier

Invoke Lambda

Use cases

Encrypt old data

Change ACLs

Bulk restore

Driven by S3 Inventory report

13. S3 Inventory

Daily/weekly CSV or Parquet report:

Object size

Storage class

Encryption

Replication status

Feeds:

Athena

Batch Operations

Cost analysis

14–15. Multipart Upload (deep dive)

Used when object > 100 MB (mandatory at 5 GB+).

Flow:

Initiate upload

Upload parts in parallel

Complete upload

Why it matters

Faster

Resumable

More reliable

16–17. MFA Delete

What

Requires MFA to:

Delete objects

Disable versioning

Truth

Rarely used

Root-only

Operationally painful

But exam loves it.

18 & 22. S3 Server Access Logs

Logs every request:

Who accessed

From where

What action

Stored in another bucket

Cost warning

Logs generate logs

Use lifecycle rules

19. Glacier Vault Lock vs Object Lock
Feature	Purpose
Object Lock	WORM for S3
Vault Lock	WORM for Glacier

Used for:

Finance

Healthcare

Legal compliance

Modes:

Governance

Compliance (even root can’t delete)

20. S3 VPC Endpoints

Why

Private access to S3

No internet

No NAT costs

Types:

Gateway endpoint (S3, DynamoDB)

Attached to route tables

Enterprise default

21. IAM Access Analyzer for S3

Answers:

“Is this bucket accessible publicly or cross-account?”

Finds:

Unintended access

Shadow sharing

25. S3 Encryption (very important)
At rest

SSE-S3 (default)

SSE-KMS (most common)

SSE-C (rare)

In transit

HTTPS (TLS)

Best practice

SSE-KMS + bucket policy enforcing encryption

Terraform mental skeleton (simplified)
resource "aws_s3_bucket" "this" {
  bucket = "my-prod-bucket"
}

resource "aws_s3_bucket_versioning" "v" {
  bucket = aws_s3_bucket.this.id
  versioning_configuration {
    status = "Enabled"
  }
}

Final truth (mentor moment)

S3 is:

Simple on the surface

Ruthless underneath

People lose money, data, and jobs by:

Ignoring lifecycle rules

Writing sloppy bucket policies

Forgetting replication deletes

Logging without cleanup
