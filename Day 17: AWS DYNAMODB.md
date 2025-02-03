## What is AWS DynamoDB?
1. fully managed NoSQL database service
2. fast and scalable key-value storage.
3. serverless, meaning AWS handles the infrastructure, scaling, and management, so you don’t have to worry about provisioning or maintaining servers.

## Key Features of DynamoDB:
✅ Key-Value & Document Store – Stores data as key-value pairs or JSON documents
✅ Highly Scalable – Automatically scales to handle millions of requests per second
✅ Low Latency – Delivers single-digit millisecond response times
✅ Serverless – No need to manage infrastructure
✅ Multi-Region Replication – Ensures high availability and disaster recovery
✅ Integrated Security – Supports IAM roles, encryption, and access controls
✅ Event-Driven – Integrates with AWS Lambda for real-time triggers

## 🚀 When to Use DynamoDB:
1. High-Traffic Web Apps → Handle millions of reads/writes per second
2. Real-Time Data Processing → Chat apps, leaderboards, or analytics
3. E-Commerce & Retail → Shopping carts, order tracking, inventory
4. IoT Applications → Storing sensor data from connected devices
5. Serverless Applications → Works well with AWS Lambda for event-driven workloads
6. Gaming Leaderboards → Stores rankings, player stats, and real-time updates
7. Streaming & Social Media → Likes, shares, comments, and user activity logs
8. Machine Learning Data Storage → Storing model metadata and feature engineering datasets

## ❌ When NOT to Use DynamoDB:
1. If you need complex joins & transactions → Use Amazon RDS (SQL-based databases)
2. If you have small, predictable workloads → DynamoDB can be costly; RDS or S3 might be better
3. If you need full-text search → Use Elasticsearch/OpenSearch instead

## Real-Life Example of AWS DynamoDB
### Example: Building a Scalable E-Commerce Application
Imagine you're running an e-commerce website and need a highly scalable database for:

User Profiles & Orders – Fast lookups for user data and order history
Product Catalog – Storing millions of products with attributes (name, price, category)
Shopping Cart – Handling real-time user sessions
Order Tracking – Storing and updating order statuses
How DynamoDB Helps: ✅ Key-Value Lookup → Quickly retrieve products or orders using Primary Keys
✅ Auto-Scaling → Easily handles Black Friday spikes with on-demand scaling
✅ Event-Driven → Works with AWS Lambda to trigger updates, notifications, or analytics
✅ Global Tables → Synchronize order data across multiple regions for faster performance

## DynamoDB Pricing (Cost Model)
DynamoDB pricing is based on Read & Write Capacity and Storage.

🛒 Two Pricing Modes:
On-Demand Mode (Best for unpredictable workloads)
1. Pay only for the actual read/write requests made
2. Reads: $1.25 per million requests
3. Writes: $1.25 per million requests
4. Provisioned Mode (Best for stable workloads)<br/>

You manually set read/write capacity
1. Reads: $0.00013 per RCUs (Read Capacity Units)
2. Writes: $0.00065 per WCUs (Write Capacity Units)

## Other Costs
1. Data Storage: $0.25 per GB per month
2. Global Tables (Multi-Region Replication): Additional write costs apply
3. DynamoDB Streams (Event-Driven Triggers): Free for the first 2.5M reads per month

## 📝 Example Cost Estimation:
A small app with 10M reads and 1M writes per month (On-Demand Mode):
* 10M Reads = $12.50
* 1M Writes = $1.25
* Total = ~$13.75 per month

