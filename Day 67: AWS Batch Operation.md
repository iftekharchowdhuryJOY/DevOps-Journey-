S3 Batch Operations lets you run the same action across massive numbers of S3 objects—safely, audibly, and with receipts.
What actions can it perform?

Cold, powerful moves:

Copy objects (same bucket, another bucket, another account)

Invoke Lambda on every object

Apply tags

Change ACLs

Restore from Glacier / Deep Archive

Re-encrypt objects (SSE-S3 → SSE-KMS)

Replicate existing objects (backfill replication)

Every object is treated as a task.
Every task is tracked.

Real-life scenarios (how grown-ups use it)
🔐 Scenario 1: “Security screwed up”

A startup stored 50 million objects unencrypted.

New compliance rule.
Deadline: 7 days.

What they do:

Enable S3 Inventory

Create a Batch Job to re-encrypt all objects with SSE-KMS

Run job

Archive report

No downtime. No code changes. No panic.

Exam traps (AWS Developer Associate)

Watch for these:

❌ Batch Ops is NOT real-time

❌ It does NOT trigger on new objects

✅ It works on existing objects

✅ Inventory + Batch is the recommended pattern

✅ Best for backfills, mass changes, compliance
