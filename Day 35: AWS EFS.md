## Amazon Elastic File System (EFS)
Amazon EFS is a fully managed, scalable network file system (NFS) designed for shared access across multiple EC2 instances or on-premises servers. It’s ideal for workloads requiring shared storage with low-latency access, such as web servers, content management systems (CMS), or big data analytics.
## Key Features:
1. Shared Storage: Multiple EC2 instances, containers (ECS/EKS), or servers (via AWS Direct Connect) can access the same file system simultaneously.
2. Elastic Scalability: Automatically scales to petabytes without pre-provisioning.
3. Regional Durability: Data is redundantly stored across multiple Availability Zones (AZs) by default.
4. Security: Integrates with IAM, VPC security groups, and supports encryption at rest/transit.
5. Lifecycle Management: Automatically moves files to cheaper storage classes based on access patterns.

## EFS storage classes

1. Standard - Multi-AZ- active workloads
2. Standard-Infrequent Access (Standard-IA) - Multi-AZ - Archived data with occasional access.
3. One Zone 
4. One Zone-IA

## When to Use EFS vs EBS
## Use EFS If:
1. Multiple instances need concurrent access (e.g., shared CMS files).
2. Your app uses a traditional file system (e.g., NFS).
3. You need automatic scaling and regional redundancy.

### Use EBS If:
1. You need high-speed, low-latency block storage (e.g., databases).
2. Data is only accessed by one EC2 instance.
3. Cost optimization for single-instance workloads.
