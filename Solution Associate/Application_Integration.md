# **Section: Application Integration**

### **Resources**

* Simple Queue Service (SQS) Features: https://aws.amazon.com/sqs/features

### **Cheat Sheet**

#### *Simple Queue Service (SQS)*
* Key way to decouple components
* Producer sends to the queue; consumer polls from the queue
* If order of processing matters; use a FIFO Queue
* If duplicates cannot be tolerated, use a FIFO queue
* Visibility Timeout is the length of time that a message is "invisible" when its being processed; may need to lengthen this time if messages are being processed more than once
* Auto scaling is possible by setting up a CloudWatch alarm (using a custom metric to calculate length of queue) that scales EC2 instances in an auto scaling group
* Long polling will wait 20 seconds to poll an empty queue (savings costs and extraneous polls)
* Dead letter queues can be used to collect messages that failed to process

#### *Simple Notification Service*
* Send notifications by email, text, HTTP, Lambda
* "Pub-sub" model where a publisher publishes to a SNS topic, and subscribers subscribe to receive notifications

#### *EventBridge*
* Some features were formerly called CloudWatch Events
* Used to build event-driven architectures (also a "pub-sub" model)
  * Subscribers set rules about what to receive
  * Schemas defined up front
  * Publishers can be third-parties
  * Events can be scheduled

#### *Step Functions*
* Provides a visual designer to orchestrate Lambda funtions and other serverless services

---
## **Amazon API Gateway**

* Supports REST and WebSocket APIs
* Supports monitoring, authentication, security, throttling and more

----
## **Amazon Simple Queue Service**

* Supports multiple producers and multiple containers
* Messages deleted after they are read by the consumer
  * Must happen within 14 days (Max storage time)

Queue Types
* Standard
  * Nearly unlimited number of transactions per second
  * At-least-once deliver; occasionally more than one copy is deliver
  * Best-effort ordering; may be delivered in an order different from which they were sent
* FIFO (First in First Out)
  * Up to 30 messages per second or 3000 messages if batched into 10
  * Exactly-once processing; duplicates are not introduced into the queue
  * First-in-first-out delivery; preserves the order in which they were received

When to Use
* Standard
  * Decouple user requests from background work/processing (e.g video encoding)
  * Distribute tasks to multiple nodes
  * Batch requests for future processing
* FIFO
  * When order of operations is critical (e.g. validate credit card before allowing a purchase)
  * When duplicates cannot be tolerated (e.g. two debits from a bank account)

Visibility Timeout
* need more time to process message from queue

Auto Scaling
* Add a CloudWatch alarm that uses a metirc to spin up more instances

Other Notes
* Unlimited queues and messages
  * to prioritize queues, create multiple
* Messaes payloads of 256KB in any text format, retained for 14 days
* Batching (1 batch = 10 messages)
  * Send, receive or delete in batches
  * batch costs the same as a single message so helps with cost savings
* Long Polling
  * When the queue is empty, wait 20 seconds to poll again
  * Reduces extraneous polling and minimizes cost
* Dead Letter Queues
  * Messages that failed to process in the "regular" queue can be moved to a Dead Letter Queue to be handled separately

----
## **Simple Notification Service (SNS)**

Messaging service that enables developers to send notifications and messages to multiple recipients or subscribers. (Pub/Sub)

It is a highly scalable, flexible, and cost-effective service that allows applications, services, and devices to send or receive messages over various protocols such as email, SMS, mobile push notifications, and more.

----
## **Amazon EventBridge**

Build decoupled, event-driven architectures

Differences from SQS and SNS
* Subscribers set rules about what to receive
* Schema Registry to defin up-front what the event will look like
* Publisher can be a third-party (e.g shopify)
* Schedule events (e.g every hour, call a lambda function to write to a log)

----
## **Amazon Step Functions**
Provides a visual designer to orchestrate lambda functions

Use Cases:
* Data processing workflows
* eCommerce/order processing
* Serverless web applicaitons

Can be used in conjunction with EventBridge

----
<style>
table {
  border-collapse: collapse;
  width: 100%;
}

th, td {
  text-align: left;
  padding: 8px;
}

th {
  background-color: #4CAF50;
}

</style>
