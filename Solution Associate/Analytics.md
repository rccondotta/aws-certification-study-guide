# **Section: Analytics**

### *Cheat Sheet*

#### *Athena*
* Used to query data in S3 using SQL queries

#### *Kinesis*
* Used for stream or real-time processing of data (such as stock prices or video streaming)

#### *QuickSight*
* Use for business intelligence/analytics to visualize your data using reports and dashboards

#### *EMR (Elastic MapReduce)
* A hosted Hadoop framework that also supports Spark, Hive and Presto

----
## **Amazon Athena**

Serverless
* Underlying instances are handled
* Fast querying due to parallel execution

Use Cases
* Querying AWS logs (CloudWatch, VPC Flow Logs, CloudTrail, etc)
* Business Intelligence/Analytics
* Querying S3 using SQL statements

----
## **Amazon Kinesis Family**

Big Data Stream (Real-Time) Processing
* Video Streams
  * Ingests, processes/streams and stores streaming video and audio data
* Data Streams
  * Ingests, processes, and stores streaming data, breaking it into "shards"
  * Data has to be processed (e.g Lambda, Data Analytics) before storing (which is optional)
* Data Firehouse
  * Ingests, processes and stores streaming data, without "shards"
  * Can stream directly to storage (processing is optional)
* Data Analytics
  * Analyzes streaming data
  * Enables SQL querying and custom Java applications

----
## **Amazon QuickSight**

Serverless  
* Underlying instances are handled by AWS

Integrates with a variety of AWS services (Athena, Redshift, RDS, S3, etc.)

Use Cases
* Business intelligence/analytics
* Data visualization and dashboards

----
## **Amazon Elastic MapReduce (EMR)**

Hosted Haddop Framework
* Hadoop is an open-source framework to store and process huge amounts of data in scalable clusters (i.e, collection of computers)
* Also supports Apache Spark, Hive, Presto, and other workloads

Use Cases
* Big Data processing
* Machine Learning

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
