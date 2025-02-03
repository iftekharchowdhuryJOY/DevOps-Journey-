## What is AWS Lambda?
AWS Lambda is a **serverless computing service** that lets you run code without provisioning or managing servers.<br/>
AWS Lambda is best used in situations where you need short-lived, event-driven, scalable compute power without maintaining servers. 

## What is a Serverless Compute Service?
A serverless compute service is a cloud computing model where the cloud provider automatically manages the infrastructure (servers, scaling, patching, etc.), allowing developers to focus solely on writing code. You deploy your code in small, event-triggered functions, and you pay only for the compute time consumed (no charges when idle).

## Why "Serverless"?

* No visible servers: Developers don’t provision, patch, or manage servers.
* Focus on code: Write business logic, not infrastructure.
* Cost efficiency: No idle costs (e.g., unlike EC2 instances running 24/7).


## Pros & Cons of AWS Lambda
### ✅ Pros
* No server management → AWS handles infrastructure
* Auto-scaling → Scales automatically with demand
* Pay-per-use pricing → No idle costs, you pay only when your function runs
* Quick deployment → Upload your code and run instantly
* Built-in security & integration → Seamless with AWS services (S3, DynamoDB, API Gateway, etc.)
* Supports multiple programming languages → Python, Node.js, Java, Go, C#, Ruby
### ❌ Cons
* Execution time limit → Max 15 minutes per function execution
* Cold starts → Initial execution latency if the function has not run recently (can be mitigated with provisioned concurrency)
* Limited storage → Max 512MB of temp storage (/tmp) per execution
* Not ideal for long-running processes → If you need processes running for hours, use EC2 or Fargate instead
* Complex debugging → Debugging serverless applications can be harder compared to traditional applications

## Real-Life Example of AWS Lambda
### Scenario: Auto-Resizing Images on S3
* A photo-sharing app needs to automatically resize images when a user uploads a photo.
* A user uploads an image to an S3 bucket
* The S3 upload event triggers an AWS Lambda function
* The function processes the image (resizes it, applies filters, etc.)
* The processed image is saved back to S3
* The app fetches and displays the optimized image
✅ Benefits:
* No need for dedicated servers to process images
* Only pays when an image is uploaded
* Scales automatically when traffic increases

## Cost of AWS LambdaAWS Lambda pricing is pay-per-use, based on:

* Number of requests

1. First 1M requests per month → FREE , After that, $0.20 per 1M requests
2. Compute time (GB-seconds): You are billed based on memory used and execution time. Example: 1GB RAM function running for 1 second = 1 GB-second
3. Other costs: If your Lambda interacts with S3, DynamoDB, API Gateway, etc., those services may have additional costs
Provisioned Concurrency (to avoid cold starts) has extra pricing
📝 Example Calculation

If a function runs 2 million times in a month and uses 512MB of memory, running for 200ms each time:
* 2M requests = (2M - 1M free) * $0.20 per 1M = $0.20
* Compute usage = 2M × 512MB × 200ms = ~200K GB-seconds
* Pricing = 200K GB-sec * $0.00001667 = $3.33
Total Monthly Cost = $3.53 🎉

## Real-world Example

A company like Uber uses Lambda to send ride confirmation SMS. When a ride is booked, an API Gateway endpoint triggers a Lambda function, which queues the SMS task in SQS. 
Thousands of Lambda instances process the queue in parallel, ensuring messages are sent within seconds.
