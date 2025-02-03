> A financial services company is looking to move its on-premises IT infrastructure to AWS Cloud. The company has multiple long-term server bound licenses across the application 
stack and the CTO wants to continue to utilize those licenses while moving to AWS.
As a solutions architect, which of the following would you recommend as the MOST cost-effective solution?

**Answer: Use Amazon EC2 dedicated hosts**

## Key Points from the Question
1. Server-Bound Licenses: These are licenses that are typically tied to a specific server’s physical resources (e.g., CPU sockets, cores, or hardware ID).
Vendors often require dedicated physical servers to ensure compliance.
3. Move to AWS: The company wants to shift entirely to the AWS Cloud, but still wants to reuse existing licenses instead of buying new ones (to save costs).
4. Cost-Effectiveness: You need a solution on AWS that maximizes license usage and minimizes additional spending.

## Why Amazon EC2 Dedicated Hosts?

1. Physical Server Allocation-With Amazon EC2 Dedicated Hosts, you rent a physical server fully dedicated to your use.
2. Licensing Compliance - Dedicated Hosts allow you to bring your own licenses (BYOL) legally, as you can map those licenses directly to the underlying physical resources, fulfilling the vendor’s server-based licensing terms.
3. Cost-Effective for Long-Term Usage -If you already own the licenses, you don’t have to pay extra for AWS-offered licenses (like license-included AMIs).

## what is a dedicated physical servers?
A dedicated physical server in the AWS context means a physical host (the actual machine hardware, not just a slice of it) that’s allocated for the exclusive use of one AWS account. You do not share that server’s resources with other AWS customers.
AWS offering: In AWS, a Dedicated Host is an option that gives you a full physical server, so you can see the number of physical cores, sockets, and other details for license or compliance reasons. This is different from the default “shared tenancy” model where multiple customers share the same underlying hardware.

