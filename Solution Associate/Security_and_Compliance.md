# **Section: Security and Compliance**

### *Resources*

* AWS Security Products: https://aws.amazon.com/products/security
* AWS Shared Responsibility Model: https://aws.amazon.com/compliance/shared-responsibility-model

### *Cheat Sheet*

#### *AWS Shared Responsibility Model*
* Customer responsible for Security "IN" the Cloud
* Amazon Responsible for Security "OF" the cloud

| Service | Primary Function | Points to Remember |
| ---- | ---- | ---- |
| AWS Shield | Infrastructure | Protects against DDoS attacks |
| AWS Web Application Firewall (WAF) | Infrastructure | Protects against commmon web exploits like SQL injections |
| AWS Key Management System (KMS) | Data Protection | Primary service for encryption; AWS manages the encryption hardware, software and keys for you |
| AWS CloudHSM | Data Protection | AWS provisions the hardware and you do everything else |
| AWS Certification Manager (ACM) | Data Protection | Provision, manage, and deploy SSL/TLS certificates |
| AWS Secrets Manager | Data Protection | Securely store and rotate secrets, such as a database name/password | 
| Amazon Macie | Data Protection | Scans S3 for personally identifiable information (PII) |
| Amazon Inspector | Detection | Monitors EC2 instances and ECR repositories for software vulnerabilities and network exposure | 
| Amazon GuardDuty | Detection | Monitors AWS accounts, network, and S3 for malicious activity |
| AWS Config | Detection | Inventory of resources and recording of configuration/changes |
| AWS Security Hub | Detection | Consolidated view of all things security; works for multiple accounts | 
| Amazon Detective | Incident Response | Used to quickly get to the root cause of security issues | 
| AWS Artifact | Compliance | View AWS's internal compliance reports and agreements | 

----
## **AWS Shared Responsibility Model**

Customer
* Responsible for Security "IN" the Cloud

Amazon
* Responsible for Security "OF" the cloud

Responsibility can change depending on the service (i.e managed vs non-managed)

----
## **Infrastructure Protection**

### *AWS Shield*

Protecting against DDos Attacks

* Standard
  * Automatically protects all AWS customers
  * Free
  * Protects from the most common types of DDoS attacks
* Advanced
  * A paid service that protects against more sophisticated attacks
  * Integrates with other services like CloudFront, Route 53, and Elastic Load Balancing
  * AWS Web Application Firewall (WAF) included at no extra cost

### *AWS Web Application Firewall (WAF)*
Protects from common web exploits (SQL injection, XSS, etc.)

Configure Rules
* Allow, block, monitor/count
* IP addressses, country of origin, presence of a script, URL strings, etc.

Examples:
* Block IP addresses and values in the request that are used by known attackers
* A specific IP address cn only send 100 requests to your application in 5 minutes
* Check HTTP headers, body, and query strings for common attacks like cross-site scripting and SQL injection

Where to Deploy WAF
* API Gateway
* Application Load Balancer (Layer 7)
  * Not on Network Load Balancer (Layer 4)
* CloudFront Distribution
* Cognito User Pools
* AppSync GraphQL API

----
## **Data Protection**

Two Types of Encryption
* At REST
  * Data thats stored or archived ona a device
  * Examples: S3 bucket, Hard disk, database
* In Transit
  * Data being transferred from one location to another
  * Examples
    * Moving data from an EC2 instance to an S3 bucket
    * Moving data from an on-premises data center to AWS

Types of Keys
* AWS Managed
  * AWS created and manges
  * Used by AWS services
    * aws/lambda; aws/cloud9; aws/s3
* Customer Managed
  * You (customer) creates and manages
  * Can create policies to rotate keys
  * Specify who can use and manage the keys
  * Supports "bring your own key"
* Custom Key Stores
  * Created with CloudHSM
  * You own and manage

### *AWS Key Management System (KMS)*

Primary service for encryption in AWS  
AWS manages the encryption hardware, software and keys for you  
Integrated with many AWS services, including EBS, S3, Redshift and CloudTrail
* Example: I want to encrypt a document stored in an S3 bucket

FIPS 140-2 Compliance: Level 2 overall (3 in some areas)

### *AWS CloudHSM*
Hardware Security Module (HSM)  
AWS provisions the hardware and you do everything else
* AWS cannot access your keys
* AWS cannot recover your keys

Integreated with a limited number of other AWS services  
FIPS 140-2 Compliance: Level 3 (considered more secure)

### *AWS Certificate Manager (ACM)*

Provision, manage and deploy public and private SSL/TLS certificates
* Public = for resrouces on the public internet (these certificates are free)
* Private = for resources on private networks

Loads Certificates on:
* API Gateway
* Elastic Load Balancers
* CloudFront Distributions

### *AWS Secrets Manager*

The recommended way to protect secrets (e.g user names and passwords) needed by your applications and services  

SSM Parameter Store
* Can store encrypted AND unecrypted data (uses KNS for encryption)
* Uses IAM to control access to secrets
* Integrates with CloudFormation
* No additional cost, up to 10,000 parameters
* Does not support secrets rotation

Secrets Manager
* Can ONLY store encrypted data (uses KMS for encryption)
* Uses IAM to control access to secrets
* Integrates with CloudFormation
* 0.40 per stored secrete and 0.05 for 10,000 API Calls
* Can automatically rotate secrets
* Can generate random secrets

### *Amazon Macie*

Automatically inventories S3 Buckets  
Identifies and analyzes PII data using machine learning and pattern learning  
Uses findings to automate workflows and remediation

----
## **Detection**

### *AWS Inspector*
Limited to applications

* Automatically detects and scans for software vulnerabilities and network exposure  
* Make sense of findings and assigns a risk score  
* Uses findings to automate workflows and ticketing  


### *AWS GuardDuty*
Entire Account

* Continuously analyzes network, accoutn, and data access  
* Using machine learning, identifies and prioritizes potential threats
* Uses findings to automate workflows and remediations 

### *AWS Config*
Inventory, record and audit the configuration of your AWS resources

### *AWS Security Hub*
Pulls everything together into a consolidated place where you can view and take actions on security issues
* Requires AWS Config
* Cross-Account
* Aggregates data from GuardDuty, Inspector, Macie, IAM Access ANalyzer, Systems Manager, and Firewall Manager

----
## **Incident Response**

### *Amazon Detective*
Finding root cause quickly and in conjunction with GuardDuty

* Automatically distils and organizes data into a graph model
* Builds a linked set of data using machine learning, statistical analysis and graph theory
* Provides visualizations, context and dteailed findings to help get to the root cause

----
## **Compliance**

### *AWS Artifact*
Self-service portal to access AWS's internal compliance reports and agreements and Free

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