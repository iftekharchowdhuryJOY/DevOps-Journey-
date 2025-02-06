## What is AWS Global Accelerator?
Blue/green deployment is a technique for releasing applications by shifting traffic between two identical environments running different versions of the application: "Blue" is the currently running version and "green" the new version. This type of deployment allows you to test features in the green environment without impacting the currently running version of your application. When you’re satisfied that the green version is working properly, you can gradually reroute the traffic from the old blue environment to the new green environment. Blue/green deployments can mitigate common risks associated with deploying software, such as downtime and rollback capability.

## Use AWS Global Accelerator to distribute a portion of traffic to a particular deployment

AWS Global Accelerator is a network layer service that directs traffic to optimal endpoints over the AWS global network, this improves the availability and performance of your internet applications. It provides two static anycast IP addresses that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions, such as your Application Load Balancers, Network Load Balancers, Elastic IP addresses or Amazon EC2 instances, in a single or in multiple AWS regions.

AWS Global Accelerator uses endpoint weights to determine the proportion of traffic that is directed to endpoints in an endpoint group, and traffic dials to control the percentage of traffic that is directed to an endpoint group (an AWS region where your application is deployed).

While relying on the DNS service is a great option for blue/green deployments, it may not fit use-cases that require a fast and controlled transition of the traffic. Some client devices and internet resolvers cache DNS answers for long periods; this DNS feature improves the efficiency of the DNS service as it reduces the DNS traffic across the Internet, and serves as a resiliency technique by preventing authoritative name-server overloads. The downside of this in blue/green deployments is that you don’t know how long it will take before all of your users receive updated IP addresses when you update a record, change your routing preference or when there is an application failure.

With AWS Global Accelerator, you can shift traffic gradually or all at once between the blue and the green environment and vice-versa without being subject to DNS caching on client devices and internet resolvers, traffic dials and endpoint weights changes are effective within seconds.

## Global Puppy Adoption Live Streams 🐾
Imagine a nonprofit that hosts live streams of rescue puppies from shelters worldwide. Viewers can watch, interact, and adopt in real-time. The streams come from shelters in São Paulo, Mumbai, Berlin, and Sydney.
## The Problem
A viewer in Toronto tries to watch a Mumbai puppy cam, but the video buffers endlessly because it’s routed through the public internet.
→ High latency: Misses the moment a puppy does a backflip (heartbreaking). ❤️🩹

If the Mumbai server crashes during a fundraising event, the stream dies.
→ Lost donations: Fewer puppies get adopted.

## Solution: AWS Global Accelerator Saves Puppies
1. Hook Up Shelters to Global Accelerator
    * Connect live-stream servers in each shelter to Global Accelerator’s static IPs.
    * Use endpoints in Mumbai, Frankfurt, Virginia, and Tokyo.

## How It Works

A viewer in Toronto clicks “Watch Mumbai Pups”:
✅ Traffic hits the nearest AWS edge location (e.g., Virginia).
✅ From there, it races over AWS’s private network to Mumbai (no buffering!).

If Mumbai’s server gets overwhelmed by puppy hype:
✅ Traffic instantly shifts to Frankfurt or Tokyo’s backup streams. Viewers don’t even notice!

Failover = Happy Tails

Health checks spot a server outage in Mumbai.

Toronto viewers automatically see backup streams from Tokyo or Frankfurt.
→ No missed adoption opportunities!

