# **Section: Elastic Load Balancing and Auto Scaling**

### **Cheat Sheet**

#### *Load Balancing*
* Load balancing helps achieve high avialability by distributing load acrossmultiple instances, across multiple AZs
* Sticky sessions (session affinity) allow you to route requests to the same instance for a period of time set by a cookie (e.g. save session state)
* Connection draining and deregistration delay are used to control the length of time in-flight request have to finish before the connection is cut of (e.g. when an instance is taken off line)
* SSL/TLS certificates can be used with a Load Balancer; the listener specifies a default certificate

#### *Auto Scaling*
* Automatically scales out/in instances based on the load
* Can replace unhealthy instances automatically, and helps optimize costs by only running what you need
* Scaling Policies:
> * Dynamic: based on CloudWatch metrics or alarms
>> * Target tracking: keeps you at a target metrics you define
>> * Step/simple scaling: based on high/low thresholds of CloudWatch Alarms
> * Predictive: Based on historical use (Machine Learning)
> * Scheduled: Based on a schedule thats known ahead of time
* Warmup/cooldown periods
> * Warmup: instances shouldn't report their metrics until theyre fully booted up
> * Cooldown: asg shoudn't take additional actions until the results of previous actions are visible
* Auto scaling is also availabe for non-EC2 services
> * ECS - scales the capaciity of container tasks and instances; triggered by CloudWatch metrics
> * Relation Database Service (RDS) - Scales up storage capacity on db instance when usage is reaching the limits of its provisioned size; does not cause downtime or disruptions to operations/transactions
> * DynamoDB
>> * auto scaling: you set tarhget, min and max capacity, and AWS will try to meet it
>> * on-demand: scaling hapen automatically based on demand (similar to serverless/lambda)

----

## **Elastic Load Balancing**

> Balances the load across multiple servers

Benefits:
* Managed Service
> * AWS guarantees uptime
> * AWS handles maintenance, upgrades, etc.
* Distributes the load across multiple instances, and across availability zones
* Can handle instance failures by doing regular health checks
* Only exposes a single endpoint (DNS) to your application

### *Types of Load Balancers*
| Types | Description |
| ----- | --- |
| Application Load Balancer | Handles HTTP/HTTPS Traffic; Layer 7 |
| Network Load Balancer | Handles TCP, UDP, TLS; Ultra-high performance, ultra low latencies; Layer 4 |
| Gateway Load Balancer | Used to deploy ana manage third-party virtual applicanes such as firewalls |
| Classic Load Balancer | Previous generation load balancer for use with the EC2-Classic Network |


### *Sticky Sessions*

A sticky session in AWS refers to the practice of directing a user's requests to the same EC2 instance in a load-balanced environment.

When a user sends a request to an application running on a load-balanced environment, the request is typically routed to one of several EC2 instances. However, in some cases, it is important to ensure that subsequent requests from the same user are sent to the same instance that handled the initial request. This is particularly important for applications that rely on user sessions or require a consistent connection to a particular instance.

### *Connection Draining and Deregistration Delay*

Connection draining allows an Elastic Load Balancer to complete all in-flight requests that are currently being handled by an EC2 instance before the instance is terminated or removed from the ELB's target group.
* Use by the Classic Load Balancer

Deregistration delay allows a time buffer before an EC2 instance is removed from an ELB's target group, during which time the instance continues to handle new requests but is not included in the target group for new load balancing requests.

Together, connection draining and deregistration delay provide a way to gracefully handle scaling operations and ensure that client requests are not interrupted or dropped


### *Load Balancing with TSL/SSL Certificates*

1. Identifiees the server as reputable
2. Ensures communication between us is encrypted

Server Name Indication (SNI)
* Newer Protocol
> * Only supported by the Application Load balancer, Network Load Balancer and CloudFront
> * Not support by all clients
> * Test: most likely answer if multiple certificates on load balancer

---

## *Auto Scaling Groups (ASG)*

* Automatically scale out/in instances based on the load
> * Specify instance number: desired capacity, min, and max
> * Specify certain metric triggers
> * Registers new instances with load balancers
* Replace unhealthy instances automatically
* Run at optimal capacity, meaning cost savings

### *Auto Scaling Policies*

Types:
* Dynamic - Based on CloudWatch metrics or alarms
> * Target Tracking - Used to keep you at a target metric you define
>> * Can scale on metrics: CPU Utilizatoin, Network in/out (Not memory usage)
> * Step Scaling - Based on high and low thresholds for CloudWatch alarms
> * Simple Scaling - Similar to step but not able to respond to additional alarms afer a scaling activity starts
* Predictive - Based on historical use (Machine Learning)
* Scheduled - Based on a schedule known ahead of time

| Warmup | Cooldown |
| ---- | -----|
| Instances don't start reporting usage data until fully warmed up | Prevents ASG from launching or terminating instances until effects from previous activities are visible |
| Example: new instanc emight have a spike in compute resources as its booting up; this shouldn't be included in the metrics | Example ASG launches 2 new instances; it should wait for a time to see the rsults of those 2 launches before it takes addition action |
| Recommended to set this value | Default is 300 second (5 minutes) |

### *Auto Scaling with ECS*

* Scaling the ECS service/tasks
> * Uses applicaiton auto scaling
> * automatically increase/decrease tasks based on: avg CPU utilizaiton, memory util, reuquest count per target
* Scaling the EC2 instances
> * Uses Auto Scaling Group
* Fargate launch type (serverless)

### *Auto Scaling for Databases*

* Relational Database Service (RDS)
> * Scales up storage capacity on the database instance when usage is reaching the limits of its provisioned size
> * Does not cause downtime or disrupt in-flight operations/transactions
* DynamoDB
> * Auto Scaling: you set target, min and max capacity, and AWS will try to meet it
> * On-demand: Scaling happens automatically based on deman (similar to serverless/Lambda)

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
  background-color: #008080;
  color: white;
}

td {
  border: 1px solid #ddd;
}
</style>