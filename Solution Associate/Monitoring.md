# **Section: Monitoring**

### *Resources*

* CLI documentation for setting alarm state on a CloudWatch Alarm: https://awscli.amazonaws.com/v2/documentation/api/latest/reference/cloudwatch/set-alarm-state.html#

### *Cheat Sheet*

#### *CloudWatch*
* Used for performance monitoring of applications and resources
  * e.g CPU, network, disk, GPU utilization
* Alarms are used to send notifications when metrics hit some thrshold
* the Unified CloudWatch Agent can send logs AND metrics from EC2 and on-premises servers
  * Required to get memory usage information

#### *CloudTrail*
* Captures user activity and API calls
  * e.g who created an EC2 instance, who terminated an EC2 instance, who logged into the Console
* CloudTrail logs can be sent to CloudWatch for monitoring and alerting

#### *AWS Config*
* Used to inventory resarouces and record the configuration/changes

----
## **CloudWatch**

Provides visibility into AWS resources and applications
* Near-real-time **metrics** such as CPU, disk, GPU utilization
* **CloudWatch Logs** allows you to collect logs from AWS and non-AWS sources, to search/extract metrics
* **Alarms** can trigger notifications for metrics
  * Example: Billing alarm to notify you when you've hit a certain amount
* **Dashboards** offer at-a-glance views

### *Metrics*

Time-Ordered set of data points published to CloudWatch  
Exist only in the **region** they were created

Namespaces
* A container for metrics
* Can create your own custom namespaces

Basic Monitoring
* Supported by most services, and enabled automatically
* Free of charge
* Metrics are pulbished at 5-minute intervals

Detailed Monitoring
* Supported by some services, and must be manually activated
* Incurs additional cost
* Metrics published at 1-minute intervals

Metric Resolution
* Standard resolution
  * Data at a granularity of 1 minute
  * e.g CPUUtilization taken at 15:00:16 would have a timestamp of 15:00
* High Resolution
  * Data ata a granularity of 1 second
  * e.g CPUUtilization taken at 15:00:16 would have a timestamp of 15:00:16
* Examples of combinations
  * Basic monitoring with High resolution
    * Data published every 5 minutes, and you can drill down to a specific second
  * Detailed monitoring with standard resolution
    * Data published every 1 minute, and you drill down to a specific minute

Can create Custom Metrics

### *Logs*
Collect logs from AWS and non-AWS sources; search and extract metrics

Log Streams
* A collection of log events from the same source (e.g. a lambda function)

Log Groups
* A collection of log streams
* a stream can only exist in one log group

Log retention can be set at 1 day to 10 years
* you DO pay for storage of the logs

Sources of Logs
* ECS, Lambda, Beanstalk, API Gateway, VVPC Flow logs, CloudTrail, Route53, CloudWatch Logs Agent, SDK

Filters and Insights can be used to query the data
* To save a filter, create a Metric Filter and it will be treated as any other metric
  * e.g. Search for "404" in logs, and show that on a dashboard

### *Alarms*
Notifications can be triggered for any CloudWatch metric

Alarm States
* INSUFFICIENT_DATA
* OK
* ALARM

Actions that can be taken on alarm
* EC2: Stop, terminate, reboot or recover an instance
* Auto-scaling action
* SNS notification

To test alarms
* aws cloudwatch set-alarm-state

### *Dashboards*
Easy way to get an at-a-glance view of important metrics and alarms 
Dahshboards are global
* They can include data from different AWS accounts and regions
  * Remember: Metrics are regional

Free, up to three dashboards

### *Agents*

"Unified" CloudWatch Agent
* Can send logs AND metrics
  * Metrics are more extensive and more granular than those produce natively by EC2
    * e.g memory or swap utilization
* CloudWatch "Log" Agent is the olde version, and can only send logs

----
## **CloudTrail**

Records user activity and API usage on your AWS acccount
* Examples: Create an IAM role, terminate an EC2 instance, log into the Console

Primarily used for auditing  
Automatically enabled  
Save a history of API calls made through:
* AWS Management Console
* CLI
* SDKs
* Higher-level AWS services (like CloudFormation)

Logs can be saved to CloudWatch or S3
* Needed for storage longer than 90 days

## **CloudWatch vs CloudTrail**

CloudWatch
* Performance monitoring of apllications and resources
* Metrics such as CPU, memory, disk, GPU Utilization

CloudTrail
* Captures user activity and API calls on an AWS account
* Activity such as creating new resources, terminating resources, logins, etc.

----
## **AWS Config**

Inventory, record and audit the configuration of your AWS resrouces

Example use cases:
* Inventory all your S3 buckets, and when one of them becomes publicly accessible, receive an alert
* Receive an alert when an unauthorized port opens on a security group
* During a compliance audit, show when configurations changed

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