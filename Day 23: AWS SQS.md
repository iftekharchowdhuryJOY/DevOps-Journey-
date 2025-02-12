## AWS SQS (Simple Queue Service) 
AWS SQS (Simple Queue Service) is a fully managed message queuing service that enables decoupled communication between distributed components 
of a cloud application. It allows systems to send, store, and receive messages between software components asynchronously, ensuring reliability, 
scalability, and fault tolerance. Messages are stored in queues, and components (producers/consumers) interact with the queue without needing 
to be active simultaneously. SQS supports two types of queues:

Standard Queues: High throughput, "at-least-once" delivery, and best-effort ordering.

FIFO Queues: Exactly-once processing, strict first-in-first-out order.

Real-Life Scenario: E-Commerce Order Fulfillment
Problem: In an e-commerce system, placing an order triggers multiple steps: payment processing, inventory update, and shipping. If these steps are handled synchronously, failures (e.g., payment service downtime) can block the entire process.

SQS Solution:

Order Placement: When a customer places an order, the frontend sends a message to an SQS queue (e.g., orders-queue) with order details.

Payment Service: A payment processor reads the message, charges the customer, and sends a success/failure message to a payments-queue.

Inventory Service: On successful payment, the inventory system deducts stock from the database and sends a message to a shipping-queue.

Shipping Service: The shipping system schedules delivery and notifies the customer.

Benefits:

Decoupling: Each service (payment, inventory, shipping) scales independently.

Fault Tolerance: If the inventory service fails, messages remain in the queue until it recovers.

Scalability: Handle Black Friday traffic spikes by adding more consumers.

* FIFO queues must have a name that ends with .fifo.
* This distinguishes them from Standard queues.
* AWS enforces this naming convention for FIFO queues.
* Create a new FIFO queue.
* Modify applications to send messages to the FIFO queue instead of the Standard queue.
* Delete the old Standard queue (optional, but recommended).
