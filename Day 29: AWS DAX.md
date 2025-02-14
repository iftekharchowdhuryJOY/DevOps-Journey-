## Amazon DynamoDB Accelerator (DAX)
Amazon DynamoDB Accelerator (DAX) is an in-memory cache designed to improve the read performance of Amazon DynamoDB.
## How DAX Works
DAX acts as a caching layer between your application and DynamoDB.

When an application queries DynamoDB:
1. DAX first checks if the requested data is in the cache.
2. If the data is found in DAX (cache hit), it is returned instantly (microseconds).
3. If the data is not in the cache (cache miss), DAX retrieves it from DynamoDB, stores it in memory, and then serves the response.
4. DAX maintains eventual consistency with DynamoDB.

## When to Use DAX?
1. When you have a read-heavy workload with frequently accessed data.
2. When low-latency responses are critical (e.g., e-commerce, gaming, recommendation engines).
3. When DynamoDB read costs are high due to repeated queries for common data.
