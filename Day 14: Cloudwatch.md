> A medium-sized business has a taxi dispatch application deployed on an Amazon EC2 instance. Because of an unknown bug, the application causes the instance to freeze regularly. 
Then, the instance has to be manually restarted via the AWS management console.

Which of the following is the MOST cost-optimal and resource-efficient way to implement an automated solution until a permanent fix is delivered by the development team?

**Answer: Setup an Amazon CloudWatch alarm to monitor the health status of the instance. In case of an Instance Health Check failure, an EC2 Reboot CloudWatch Alarm Action can be used to reboot the instance**

## What is AWS CloudWatch?
1. two words remember: monitoring and observability tool
2. monitor all aws services & resources.

## What it does?
> collects and tracks metrics, monitors logs, sets alarms, and automates responses to system changes.

## Why Do You Need CloudWatch?
1. Real-Time Monitoring
2. proactive alerts
3. troublshooting
4. automation
5. cost and performance optimization
6. unified view

## Overlooking the Cost of Custom Metrics

What people mix up: They assume all metrics are free in CloudWatch. Actually, the default metrics (e.g., CPU, memory, disk utilization for EC2) are free up to certain limits, but custom metrics (like application-specific counters) can incur additional cost.
How to avoid it: Keep an eye on how many custom metrics you are publishing and consider whether you can aggregate multiple data points into a single custom metric.


> Setup an Amazon CloudWatch alarm to monitor the health status of the instance. In case of an Instance Health Check failure, 
an EC2 Reboot CloudWatch Alarm Action can be used to reboot the instance

* StatusCheckFailed_Instance is the CloudWatch metric that reports whether the instance-level health check has passed (0) or failed (1).
* When this metric is greater than 0, it means the instance has failed its instance health check.

## What is the “instance-level health check”?

AWS runs two types of status checks on your EC2 instances:
1. System Status Check (checks the underlying AWS infrastructure/hardware)
2. Instance Status Check (checks issues within the OS or software on the instance)
The instance-level health check is the second one. If it fails, it often indicates a problem like a crashed process, kernel panic, or OS issue on the EC2 instance itself.

## How does the CloudWatch alarm help?
CloudWatch tracks a metric called StatusCheckFailed_Instance.<br/>

If StatusCheckFailed_Instance = 0, the instance is healthy.
If StatusCheckFailed_Instance = 1, the instance has failed the instance status check.
You can create a CloudWatch alarm that watches this metric. The alarm triggers when StatusCheckFailed_Instance is above 0.

As part of setting up that alarm, you can specify an alarm action. This alarm action can be:

1. Sending an email (via SNS),
2. Executing a Lambda function,
3. rebooting the EC2 instance.

**This is a basic form of self-healing or auto-recovery without manual intervention.**

