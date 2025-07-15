# AWS S3 Pre-Signed URLs – Key Points
## What is a Pre-Signed URL?
A pre-signed URL is a time-limited URL that grants temporary access to a specific S3 object (for download or upload) without requiring AWS credentials.

## Key Features:
✅ Temporary Access – Expires after a set time (default: up to 7 days with SDK, but can be extended to 1 year via AWS CLI).
✅ No AWS Credentials Needed – Anyone with the URL can access the object.
✅ Supports GET (download), PUT (upload), and DELETE operations.
✅ Uses IAM Credentials – The URL is signed using an IAM user/role’s credentials.

## Common Use Cases:
1. Share private files securely (e.g., reports, invoices).
2. Allow users to upload files directly to S3 (e.g., user-generated content).
3. Provide time-limited access (e.g., one-time download links).

# How to Generate?
```aws s3 presign s3://bucket-name/object-key --expires-in 3600  # 1 hour```
1. Generate a Pre-Signed URL for Download (GET)
Allow temporary access to download a private file (e.g., a report).
