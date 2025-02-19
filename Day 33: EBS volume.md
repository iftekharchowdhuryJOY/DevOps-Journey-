## EBS Volumes
persistent hard drive or block storage provided by AWS. 
### Why do we exactly need EBS?
When we deploy an instance, we need EBS vol to store the operating system and application data.
**The root EBS volume holds the OS (like a C: drive in Windows or /root in Linux). Without EBS, EC2 instances wouldn't have permanent storage**

When we create an EC2 instance, by default there will be EBS vol.

## How EBS Volumes Work?

1. Attach to EC2 Instance
* EBS volumes must be attached to an EC2 instance to be used.
* An instance can have multiple EBS volumes attached.

2. Format & Mount (Linux/Windows)
* Once attached, the volume needs to be formatted (if new) and mounted for use.

3. Read/Write Operations
* The volume can store files, databases, or application data just like a regular hard drive.

4. Snapshot & Backup
* You can take snapshots of an EBS volume for backup or migration.

## What Exactly Does EBS Do with EC2?
When you launch an EC2 instance, it needs a storage device to save files, OS data, logs, or databases. EBS acts as that storage and remains available even if you stop or restart your EC2 instance.
Unlike a physical hard drive, an EBS volume can be detached from one EC2 instance and attached to another. This makes it easy to move data between EC2 instances.
If your application needs more storage, you can increase the size of an EBS volume without stopping the EC2 instance. SSD-based EBS volumes (gp3, io1, io2) are used for fast and frequent access like databases, boot volumes, and applications.

## Availability Zones (AZ) and Amazon EBS
In AWS, Availability Zones (AZs) and Amazon Elastic Block Store (EBS) are closely related because EBS volumes are designed to operate within a single Availability Zone. AZs are independent but connected with low-latency networking. Each AWS Region (like us-east-1) has multiple AZs (e.g., us-east-1a, us-east-1b, us-east-1c).

## How Availability Zones (AZs) Affect EBS?
When you create an EBS volume, it is stored in one specific AZ. This means the volume can only be attached to an EC2 instance in the same AZ. Example: If you create an EBS volume in us-east-1a, it cannot be attached to an EC2 instance in us-east-1b.
EBS replicates data across multiple physical servers within the same AZ to prevent data loss from hardware failures. However, it does NOT replicate across multiple AZs or Regions automatically.

## What is an EBS Snapshot?
Backup service of EBS volume. 

## Key Features of EBS Snapshots
The first snapshot captures the entire EBS volume. Subsequent snapshots only store changes since the last snapshot (to optimize storage and reduce costs). EBS snapshots are automatically stored in Amazon S3, but you cannot directly access them like normal S3 files.
They are managed within AWS Backup or the EC2 console. You can copy a snapshot from one AWS Region to another.
You can create a new EBS volume from a snapshot in a different AZ (useful for migrating workloads).
Normally, when restoring from a snapshot, reading data for the first time is slower. FSR enables near-instant access to restored volumes.
You can automate EBS snapshots using AWS Backup, setting backup policies and retention rules.

## Key points
1. EBS Snapshots are essential for backup, disaster recovery, and migration.
2. They store incremental backups efficiently, reducing costs.
3. You can restore snapshots into new EBS volumes, even in different AZs or Regions.

## Key Notes
* EBS volumes are AZ-specific and provide high availability within an AZ.
* To make an EBS-backed system fault-tolerant, use EBS snapshots, Multi-AZ EC2 deployments, or Amazon EFS for shared storage.
* For mission-critical applications, consider Amazon RDS Multi-AZ or Amazon FSx for Windows File Server for redundancy.


