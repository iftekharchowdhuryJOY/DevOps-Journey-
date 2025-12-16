Step 0: The mindset (this matters more than syntax)

A production bucket policy answers four questions:

Who can access this bucket?

What can they do?

From where can they do it?

Under what conditions is it allowed?

If you can’t answer all four clearly, your policy is not production-ready.

Step 1: Define the intent (engineers do this first)

Before writing JSON, good teams write intent in plain English.

Example intent (typical SaaS private bucket)

• Only my application can read/write
• No public access, ever
• Only encrypted uploads
• Only HTTPS
• Only from my VPC
• Nobody deletes objects directly

This is security design, not configuration.
Step 2: Start with DENY (this is how pros do it)

Core production DENY patterns (you’ll see these everywhere)
1️⃣ Deny unencrypted uploads

Intent:

“If someone uploads without encryption, block it.”

Why:

Prevents accidental plaintext data

Protects against bad SDK usage

This DENY applies to:

PutObject

All principals

All objects



2️⃣ Deny wrong encryption (force SSE-KMS)
3️⃣ Deny non-TLS access
4️⃣ Deny access outside VPC

Allow only what is explicitly needed. Bucket policy is NOT sequential
AWS evaluates all statements. Explicit DENY anywhere → request fails ALLOW only works if no DENY matches
So your mental evaluation should be: “Is there any statement that denies this request?” If yes → done.

Common production patterns (very important)
Pattern 1: Private app bucket (most common)

Used for:

User uploads

Internal documents

App assets

Characteristics:

No public access

SSE-KMS enforced

VPC endpoint only

App role only

This is the default for modern SaaS.


Pattern 2: Public content via CloudFront (safe way)

Used for:

Images

Videos

Static assets

Key idea:

Bucket itself is private

Only CloudFront can read

Users never talk to S3 directly

This avoids public buckets entirely.

Pattern 3: Central logging bucket

Used for:

ALB logs

CloudTrail logs

VPC flow logs

Characteristics:

Many accounts write

Nobody deletes

Encryption enforced

Prefix isolation per account

Auditors love this pattern.

Step 6: How policies are managed in real companies

This is the part tutorials never tell you.

What actually happens in prod

Bucket policies live in Git

Reviewed by security

Deployed via IaC

Rarely changed

Protected by SCPs

Monitored by Access Analyzer

Nobody edits policies manually at 2am
(At least, nobody competent.)

Step 7: How to READ a bucket policy like a senior

When you see a bucket policy, ask:

Where are the DENY statements?

What conditions do they enforce?

Who is allowed?

From where?

What happens if a new role appears?

If you can answer those, you own the policy









