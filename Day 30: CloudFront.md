Amazon CloudFront is a Content Delivery Network (CDN) that caches and delivers content from AWS edge locations worldwide.

## How CloudFront Works
CloudFront caches static content (e.g., images, CSS, JavaScript) and delivers it from edge locations near users.

## When a user requests content:
1. CloudFront checks if it has a cached version in an edge location.
2. If the cached content exists (cache hit), it serves the response instantly.
3. If not (cache miss), CloudFront fetches the data from the origin server (e.g., Amazon S3, EC2, ALB), caches it, and then serves it.

## When to Use CloudFront?
1. To cache and accelerate static content delivery (e.g., images, videos, CSS, JavaScript) from S3 or EC2.
2. To improve API performance by caching certain responses.
3. To speed up content delivery globally and reduce backend load.

## CDN
A Content Delivery Network (CDN) is a network of geographically distributed servers that cache and deliver content—such as web pages, images, videos, or other static assets—closer to end users. The goal of a CDN is to reduce latency (the time it takes to load content) and improve performance by serving content from a location nearest to the user rather than always retrieving it from a centralized server.


