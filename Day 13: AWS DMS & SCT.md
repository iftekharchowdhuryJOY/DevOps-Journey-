> A company has a license-based, expensive, legacy commercial database solution deployed at its on-premises data center. 
The company wants to migrate this database to a more efficient, open-source, and cost-effective option on AWS Cloud. 
The CTO at the company wants a solution that can handle complex database configurations such as secondary indexes, foreign keys, and stored procedures. 
As a solutions architect, which of the following AWS services should be combined to handle this use-case? (Select two)

**Answer: 1. AWS DMS 2.AWS SCT**

## What is AWS DMS-Database Migration Service?

1. fully managed service for migrating databases to AWS or between on-prem to cloud environments.
2. **Minimal Downtime: Continuous data replication during migration.**

### Use cases

** Lift-and-shift database migrations to AWS.
** Database consolidation (merge multiple databases into one).
** Replicating data to a data warehouse (e.g., Redshift) or analytics platform.
** Continuous synchronization (CDC - Change Data Capture) for hybrid setups.

## Pricing
* Pay per DMS replication instance (hourly, based on instance size).
* Example: A dms.t3.medium instance costs ~$0.17/hour (us-east-1)

## AWS SCT - Scheme Conversion tool

A free desktop application that converts database schemas and code (stored procedures, views, etc.) between different database engines. Primarily used for heterogeneous migrations (e.g., Oracle → PostgreSQL).

## How DMS and SCT Work Together
Heterogeneous Migration Workflow:<br/>

* Step 1: Use AWS SCT to convert the source schema/code to the target engine (e.g., Oracle → Aurora PostgreSQL).

* Step 2: Use AWS DMS to migrate data from the source to the target database.

* Step 3: Use DMS’s CDC to keep source and target in sync until cutover.

Homogeneous Migration Workflow: Only AWS DMS is needed (no schema conversion required).
