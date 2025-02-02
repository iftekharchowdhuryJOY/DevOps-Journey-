> A pharma company is working on developing a vaccine for the COVID-19 virus. The researchers at the company want to process the reference healthcare data in a highly available as well as HIPAA compliant in-memory database 
that supports caching results of SQL queries. As a solutions architect, which of the following AWS services would you recommend for this task?

Answer: **Amazon ElastiCache for Redis/Memcached**

## What is an In-Memory Database?
An in-memory database (IMDB) stores data primarily in RAM (instead of disk) for ultra-fast read/write operations. It’s ideal for latency-sensitive workloads like real-time analytics, caching, and session management. Key features:
** Speed: Microsecond response times (no disk I/O).

** Volatility: Data is lost if the system crashes (unless persisted to disk).

** Use Cases: Caching, gaming leaderboards, financial trading systems.

Examples: Redis, Memcached, Apache Ignite, Amazon ElastiCache.

## HIPAA-Compliant In-Memory Databases for Caching SQL Queries
To meet HIPAA compliance, a database must safeguard Protected Health Information (PHI) with encryption, access controls, and audit logging.<br/>

* In-Memory Cache (HIPAA-eligible): Amazon ElastiCache for Redis or Amazon MemoryDB for Redis.
* Caching SQL Results: After executing a SQL query (e.g., SELECT * FROM patients WHERE id=123), store the result in Redis with a key like patient:123.
* 


> For AWS SAA questions about HIPAA-compliant caching, focus on ElastiCache/MemoryDB + RDS/Aurora with encryption and access controls. The key is combining a compliant SQL database with an in-memory cache.

<p>Amazon ElastiCache for Redis is a blazing fast in-memory data store that provides sub-millisecond latency to power internet-scale real-time applications. 
Amazon ElastiCache for Redis is a great choice for real-time transactional and analytical processing use cases such as caching, chat/messaging, gaming leaderboards, 
geospatial, machine learning, media streaming, queues, real-time analytics, and session store. ElastiCache for Redis supports replication, high availability, and cluster sharding right out of the box.</p>

<p>Amazon ElastiCache for Memcached is a Memcached-compatible in-memory key-value store service that can be used as a cache or a data store. Amazon ElastiCache for Memcached is a great choice for implementing an in-memory cache to decrease access latency, 
increase throughput, and ease the load off your relational or NoSQL database. Session stores are easy to create with Amazon ElastiCache for Memcached.</p>

