## EBS Volumes
persistent hard drive or block storage provided by AWS. 
### Why we exactly need EBS?
When we deployed a instance, we need ebs vol to store the operating system and application data.
**The root EBS volume holds the OS (like a C: drive in Windows or /root in Linux).Without EBS, EC2 instances wouldn't have permanent storage**
When we create EC2 instance, by default there will be EBS vol.

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

