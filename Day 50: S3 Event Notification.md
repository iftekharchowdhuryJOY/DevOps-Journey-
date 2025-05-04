## S3 Event Notification
Before diving into S3 event notification whenever you see S3 event notification: **Remember when something happens in your S3 bucket, do something automatically**
So, basically i upload a pdf or a image to my S3 bucket. My S3 event notifies to AWS lambda function and i write a rule in lambda that resize or compress the pdf and save it back.
Hey, when someone **uploads, deletes, or changes a file**, please inform this service (Lambda/SNS/SQS) right away.

S3 event notification can send notification to these services:
1. Lambda
2. SNS
3. SQS
4. EventBridge

 Why S3 Event Talks with SNS, SQS, Lambda?
 Because S3 can’t run logic or store messages—it just stores files.So it needs to "talk" to other services to do something when a file is uploaded or deleted.
 
