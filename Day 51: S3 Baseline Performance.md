Amazon S3 (Simple Storage Service) has baseline performance rules based on object access patterns and request rates.
1. Baseline Throughput per Prefix
* 3,500 PUT/COPY/POST/DELETE requests per second per prefix
* 5,500 GET/HEAD requests per second per prefix
✅ No need to pre-partition your bucket like old days!

🧩 What is a Prefix?
A prefix is the part of the object key before the first /.
Example:

Bucket: my-app-bucket
Object Key: logs/2025/05/01/logfile1.txt
Prefix: logs/2025/05/01/
This means S3 performance scales per prefix, not just the entire bucket.

## Amazon S3 Transfer Acceleration
S3 Transfer Acceleration uses Amazon CloudFront’s edge locations to speed up file uploads and downloads to your S3 bucket from long-distance locations
⚡ How It Works (Real Life Style)
Let’s say you’re in Bangladesh and your S3 bucket is in US East (N. Virginia).

✅ Normal Upload:
Your file travels all the way to the US, which takes time.

✅ With Transfer Acceleration:
You upload to the nearest AWS edge location, e.g., in Mumbai or Singapore. From there, Amazon’s internal fast AWS network moves the file to the US.

📦 Result: Much faster uploads and downloads over long distances!
🧪 How to Enable It?
Go to your S3 bucket.

Go to Properties.

Scroll to Transfer Acceleration.

Click Edit → Enable.

Use the accelerated endpoint:
https://BUCKETNAME.s3-accelerate.amazonaws.com
