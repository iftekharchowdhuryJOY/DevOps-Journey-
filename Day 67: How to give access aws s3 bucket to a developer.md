# How can you give access your developer S3 data or bucket or sth??

First principle (burn this in)
**You never give a developer access to a bucket.**
**You give a developer access to a role — and the role has access to the bucket.**

First principle (burn this in)

You never give a developer access to a bucket.
You give a developer access to a role — and the role has access to the bucket.

Step 1 — Understand the developer’s need (critical)

Ask exactly:

Read only or read/write?

Entire bucket or one folder?

Just one CSV or many?

Console access or programmatic?

Example answer:

“Read and update CSV files under data/ prefix only.”

Step 2 — Create an IAM policy (least privilege)

You create a policy like:

s3:ListBucket (scoped to prefix)

s3:GetObject

s3:PutObject (if needed)

Scope it to:

One bucket

One prefix

No wildcards unless justified

This is non-negotiable in good orgs.

Step 2 — Create an IAM policy (least privilege)

You create a policy like:

s3:ListBucket (scoped to prefix)

s3:GetObject

s3:PutObject (if needed)

Scope it to:

One bucket

One prefix

No wildcards unless justified

This is non-negotiable in good orgs.

Step 3 — Attach policy to an IAM role

Create a role, for example:

role: s3-data-analyst


Attach:

Your custom S3 policy

(If encrypted) the KMS permissions too

The goal (what you wanted)

You were acting as an AWS sysadmin.

A developer needed:

Console access

Read-only

To one S3 bucket

Only one folder (data/)

Only CSV files

Bucket encrypted with SSE-S3

Bucket must remain private

This is a real enterprise scenario, not a toy problem.

The correct design we aimed for

We followed best practice, not shortcuts:

❌ No public bucket

❌ No ACLs

❌ No broad AmazonS3ReadOnlyAccess

❌ No access keys sharing

Instead:

✅ IAM user for login

✅ IAM role with least privilege

✅ User assumes role

✅ Role has scoped S3 permissions

That architecture was correct from the start.

What went wrong (the real problems)
1️⃣ First failure: objects not visible inside the bucket

You gave:

s3:GetObject → correct

s3:ListBucket with prefix conditions → correct

But the S3 console:

First lists the bucket root

Then uses prefix + delimiter to show folders

Without allowing:

prefix = ""

delimiter = "/"

👉 The console showed nothing, even though the file existed.

Fix: allow root-level ListBucket only for UI discovery, still locked down.

2️⃣ Second (bigger) failure: no buckets visible at all

This was the real blocker.

The S3 console always starts with:

s3:ListAllMyBuckets


You did not grant that.

Result:

No error

No warning

Console silently dropped you on “Get started”

Looked like everything was broken

IAM, bucket policy, encryption — all irrelevant until this was fixed.

Fix: add account-level permission:

{
  "Action": "s3:ListAllMyBuckets",
  "Effect": "Allow",
  "Resource": "*"
}


This does not grant data access — only visibility of bucket names.

Why this was confusing (important insight)

s3:ListAllMyBuckets is account-level

s3:ListBucket is bucket-level

s3:GetObject is object-level

The S3 console needs all three, in that order.

The CLI and SDK do not.

AWS does not document this clearly.
AWS does not show helpful errors.
This is why even experienced engineers get stuck here.

The final working permission model

The role ended up with exactly:

Account-level

s3:ListAllMyBuckets

Bucket-level

s3:ListBucket (root, with delimiter)

s3:ListBucket (only data/ prefix)

Object-level

s3:GetObject on bucket/data/*

No write.
No other buckets.
No other folders.
No public access.
No KMS complexity.

This is true least privilege and console-compatible.

How we proved the fix

After adding account-level permission and re-assuming the role:

Buckets appeared

Only the intended bucket was visible

Only data/ folder appeared

Only data.csv was accessible

Download worked

Upload was denied

That confirmed:

Role was assumed correctly

Policy was attached correctly

No hidden denies remained

The big takeaway (this is the lesson)

S3 console access is not the same as S3 API access.
The console requires extra permissions just to render the UI.

Because of this:

Many teams avoid console S3 access entirely

Or use CLI / Athena / Access Points instead

But now you understand it end-to-end.
