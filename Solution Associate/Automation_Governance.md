# **Section: Automation and Governance**

### *Cheat Sheet*

#### *CloudFormation*
* "Infrastructure as code" defined by JSON or YAML template
* Repeatable way to deploy, update and delete resources
* Can be used cross-account and cross-region

#### *AWS Service Catalog*
* An approved "catalog" of products that developers can use
* Organized into protfolios (e.g. web development, data analysis)

#### *AWS Systems Manager (SSM)*
* Manage a fleet of servers at scale
* Commonly used for patching and maintenance
* Parameter Store is used to store configuration information and secrets (encrypted and unencrypted)
  * if you needc to rotate secretes, you should use Secrets Manager instead

----
## **CloudFormation**
Infrastructure as Code

Benefits
* Huge time savings over manual work
* Repeatable
* Changes are also made as code
* Can delete all resources at once
* Estimate costs based on a template
* Can be used cross-account and cross-region

----
## **AWS Service Catalog**
IT-approved resources that teams can provision  
Engineering teams that can provision things from the catalog

----
## **AWS Systems Manager and Parameter Store**
Manage fleet of servers at scale
* EC2 instances and on-premises servers
* Supports Linux and Windows

Common Use cases
* Patching and maintenance
* "Run Command" to install applications, capture log files, perform configuration changes
* Parameter Store to manage global configuration settings

SSM Parameter Store
* Can store encrypted AND unencrypted data (uses KMS for encryption)
* Uses IAM to control access to secrets
* Integrates with CloudFormation
* No additional cost, up to 10,000 parameters
* Does not support secrets rotation

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
