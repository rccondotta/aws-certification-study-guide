# **Section: Databases**

### *Resources*

* MySQL Workbench: https://dev.mysql.com/downloads/workbench

### *Cheat Sheet*

#### *RDS*
* Supports six engines (aurora, mysql, postgresql, etc)
* Managed database service
  * AWS does all the underlying administrative work
  * You are reponsible for network access and managing database users and permissions
* Read replicas used for read-heavy applications, where read-only traffic is directed to the replica, alleviating traffic from the primary database
  * Works cross-region
* Multi-AZ deployment provide high availability by synchronously (and automatically) replicating the primary database to a standby replica

#### *Redshift*
* Used for data warehousing and analytics
  * central repository of data that pulls from many other sources (e.g. S3, databases, etc)

#### *DynamoDB*
* Non-relation or NoSQL database
  * Data stored as key/value pairs
  * Massively scalable and highly performant
* Two options for scaling: 1: Auto Scaling (provisioned) 2: On-demand (more expensive)
* DynamoDB Accelerator is in-memory caching, delivering 10x performance with microsecond READ latency
  * no re-coding necessary

#### *ElastiCache*
* In-memory database used for caching and session management
* Used for read-intensive web applications, such as gaming or media streaming

#### *Neptune*
* Graph Database
* Used for social media, fraud detection, and recommendation engines

----

## **Databases Overview**

| Database Type | Use Case | AWS Service |
| ---- | ---- | ---- |
| Relational | Traditional apps, CRM, eCommerce | Amazon RDS, Aurora, Redshit |
| Non-Relational or NoSQL (key-value) | High-Traffic Web Apps, eCommerce, Gaming | Amazon DynamoDB | 
| In-Memory | Caching, session management | Amazon ElastiCache |
| Graph | Fraud Detection, Social Networking, Recommendation Engines | Amazon Neptune |
| |

Managed Database Service
* A database where Amazon does all the underlying administrative work (backups, patching, recovery, etc)
* vs
* You installing the database diretgly on a server and managing it

----
## *Amazon Relational Database Service*

Web service that makes it easier to set up, operate, and scale a relational database in the cloud

Six Engines supported
* Aurora
* MySQL
* MariaDB
* PostgreSQL
* Oracle
* Microsoft SQL Server

### Import Study Point
Read Replicas
* asynchoronous replication between master and read replicas
* All read replicas are avilable and can be scaled
* Automated backups taken by default; you must configure
* Can be 1 AZ, cross-AZ or cross region
* Failover happens by manually promoting replica to a standalone instance

Multi-AZ Deployments for High Availability
* Synchronous replication beween primary and standby
* Only primary database instance is active
* Automated backups taken from standby database
* Always spans 2 AZs in 1 region
* Failover happens automatically to the standby

### Other Notes for High Availability
Snapshots can be made of EBS volumes on the database instances
* Used for backup and recovery
* Stored in S3, like all other EBS snapshots

Automated snapshots are also possible
* can impact peformance, so choose a time when the database is less busy

Auto Scaling for RDS
* Scales up storage capacity on the database instance when usage is reaching limits of its provisioned size
* Does not cause downtime or disrupt in-flight operations/transactions

----
## *Amazon Redshift*

Data warehousing service
* Can handle massive amount of data (exabytes), structured and unstructured

OLAP-style (Online Analytical Processing) columnar databased based on PostgreSQL
* Can use SQL queries

Use Cases
* Real-time analytics
* Log Analysis
* Combining multiple data sources

----
## *Amazon DynamoDB*

Key-Value Database 

Benefits and Uses Cases
* High performance, very fast for read and write operations  
* Massively scalable and serverless  
* Highly available across three AZs

Scaling
* Autoscaling ("provisioned"): You set target, min and max capacity, and AWS will try to meet it
* On-demand: Scaling happens automatically based on demand (Similar to serverless/ lambda)
  * More expensive than auto scaling / provisioned

DynamoDB Accelerator (DAX)
* Fully Managed, in-memory cache
* Delivers up to 10 tinmer performance (microsecond READ latency), even millions of request per second
* No re-coding necessary; provision a DAX cluster and shift existing calls to it
  * Similar performance results as ElastiCache, but with less effort

----
## *Amazon ElastiCache*

Managed Caching Service
* Removes the complexity of deploying and managing a distributed cache environment
* Compaitble with Redis or Memcached engines
* Integration with other AWS services

Use Cases
* Distributed session management
  * vs. "sticky sessions* with a load balancer
* Read-intensive web applications
* Real-time apps that require fast data access

----
## *Amazon Neptune*

Fully-managed graph database service provided by Amazon Web Services (AWS). It is designed to store and query highly connected data such as social media networks, recommendation engines, and knowledge graphs.

Neptune supports popular graph query languages like Gremlin and SPARQL, and allows users to easily run queries that traverse millions or billions of relationships. It also provides features like automatic data replication, backups, and point-in-time recovery to ensure data durability and availability.

Neptune is compatible with AWS services like Lambda, EC2, and S3, making it easy to integrate with existing AWS infrastructure. It can also be accessed through a web-based console, APIs, and SDKs for popular programming languages like Java, Python, and .NET.

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