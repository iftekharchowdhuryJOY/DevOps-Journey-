## What is a Spread Placement Group in AWS?
A Spread Placement Group (SPG) in AWS is a placement strategy that distributes EC2 instances across different hardware racks within an Availability Zone (AZ).
It is designed to reduce the risk of simultaneous failures by ensuring that instances are placed on separate physical hardware.

## When Should You Use a Spread Placement Group?
A Spread Placement Group is useful for: ✅ High Availability applications (e.g., mission-critical workloads).
✅ Workloads requiring fault isolation between instances.
✅ Small applications needing low latency and distributed failure domains.
✅ Systems that cannot afford hardware-level failures affecting multiple instances.

## Key Features of a Spread Placement Group
1. Instances are placed on separate hardware
* Each instance in the group is on a different underlying server/rack.
* This reduces the risk of hardware failure affecting multiple instances.
2. Maximum of 7 instances per AZ
* AWS allows only up to 7 instances per AZ in a Spread Placement Group.
* vIf you need more than 7 instances, they must be distributed across multiple AZs.

3. Best for critical applications
* Used when high availability and fault tolerance are critical.
* Helps ensure minimal downtime if a hardware failure occurs.

4. Works across multiple AZs
* You can spread instances across different AZs in the same AWS Region.
* Ideal for use cases where failure isolation is important.
