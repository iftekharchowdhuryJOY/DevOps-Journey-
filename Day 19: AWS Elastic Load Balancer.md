## What is AWS Elastic Load Balancer
AWS Elastic Load Balancer (ELB) is a service that automatically distributes incoming application traffic across multiple targets, 
such as Amazon EC2 instances, containers, IP addresses, and Lambda functions. It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zones. ELB ensures that incoming traffic is distributed optimally so that no single server bears too much demand. By spreading the traffic, ELB helps increase the fault tolerance of your applications.

AWS offers several types of load balancers that fit different needs:

1. Application Load Balancer (ALB): Best suited for load balancing of HTTP and HTTPS traffic, ALB offers advanced request routing targeted at the delivery of modern application architectures, including microservices and containers.
2. Network Load Balancer (NLB): Optimized for low latency and high throughput, it works at the connection level (Layer 4). NLB is capable of handling millions of requests per second while maintaining ultra-low latencies, making it ideal for TCP traffic.
3. Classic Load Balancer (CLB): Provides basic load balancing across multiple EC2 instances and operates at both the request level and connection level. CLB is generally considered a legacy option and is best used for applications that were built within the EC2-Classic network.
4. Gateway Load Balancer (GLB): Makes it easy to deploy, scale, and manage virtual appliances, such as firewalls, intrusion detection and prevention systems, and deep packet inspection systems.

### What is Load Balancer? 
Imagine a restaurant chain has several branches and a centralized call center to handle reservations and customer inquiries. 
The call center receives hundreds of calls every hour, and there are several customer service agents available to take these calls.

## Without a Load Balancer:
Calls come in sequentially and are routed to the next available agent. If all agents are busy, new callers have to wait in line 
until someone becomes available. If one agent is much faster than the others, they might end up sitting idle because calls are not evenly distributed.

## With a Load Balancer:

As calls come into the call center, a "load balancer" (in this case, an automated call distributor) instantly routes each incoming call 
to the next available agent. The load balancer ensures that no single agent is overwhelmed with calls while others have nothing to do.
If an agent finishes a call, the load balancer immediately assigns them the next waiting caller, 
optimizing the use of agent time and reducing customer wait times.

## How It Relates to AWS ELB:
In a similar way, AWS Elastic Load Balancer acts as a "traffic director" for your web applications:

* Incoming internet traffic (like HTTP requests) to your website is like the calls coming into the call center.
* The servers (or other resources like containers or Lambda functions) that host your website are like the agents answering the calls.
* The ELB distributes incoming website traffic across multiple servers to ensure that no single server gets too much load and
potentially becomes a bottleneck or fails from being overloaded.
* It continuously checks the health of servers and only routes traffic to those that are operational,
similar to how only available agents would receive calls.
By balancing the load in this manner, ELB helps enhance the responsiveness and availability of applications to end-users. This is essential for maintaining performance during peak times or under varying load conditions, much like a busy call center during lunch hours or special events.
