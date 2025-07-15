S3 Access Points simplify managing shared datasets by providing unique hostnames with custom permissions for different applications or users.
# What is an S3 Access Point?
A named network endpoint attached to an S3 bucket.

Each access point has its own:
1. DNS hostname (e.g., {access-point-name}-{account-id}.s3-accesspoint.{region}.amazonaws.com).
2. IAM policies (controls who can access it).
3. Block Public Access settings (independent of the bucket).

# Use Cases:
1. Share subsets of data securely (e.g., separate access for analytics vs. apps).
2. Enforce different permissions per application.
3. Simplify multi-account access (via VPC or AWS Organizations).

