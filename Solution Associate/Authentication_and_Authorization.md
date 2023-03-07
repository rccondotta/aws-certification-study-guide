# **Section: Identity and Access Management (IAM)**

### **Cheat Sheet**

#### *Identity and Access Management (IAM)*

> * Root account has permission to do everything, including access to billing info
> * IAM users have no permissions by default
> * Multi-Factor Authentication can and should be enforced for the root account and individual user
> * Access keys are required for programmatic access (CLI, SDK)
> * Roles should be used to give permision to other AWS services
> * Permisions are controlled by policies; give least privileges
> * If permission isn't given, then by default, it is denied
> * If two policies are in place, the most restrictive "wins"


#### *Authentication and Integration Tools*
* Security and token Service
> * Used to grant temporary credential to AWS (eg AssumeRole)
* Cognito
> * Recommended way to manage users for mobile and web-based applications
* Managed Microsoft AD
> * Controls how microsoft technologies in a VPC interact with AWS resources
* AD Connector
> * A proxy to on-premises Active Directory; all users managed on-premises
* AWS Single Sign On
> * Allows users to log in only once, and credentials are used across account and other applications
* Organizations
> * A collection of accounts; required to use SSO
> * Service Control Policies (SCP) let you define allow/deny for an entire account

---

## **IAM Overview**

> Service used to securely control access to your AWS Resources

> Controls authentication (who) and authorization (what they do)

## **Users**

>Best practice is to always work in your IAM account, not in the root account

> Set up IAM users with the least number of permission needed.

### *Root User*

* One per account
* Unrestrictd Access
* Difficult to restrict or revoke access
* Can perform the following tasks:
> * Close an AWS Account
> * Change an AWS support Plan
> * Change AWS account settings

### *IAM User*

* Multiple per account
* Users can be deleted or disabled
* Easy to restrict access

## **Groups**

A collection of users

## **Roles**

Permission of one service to another

* Similar to a user (an identity with permissions)
* Does not have credentials (password or keys)
* Assumable, temporarily, by anyone who needs it

Example:
* Read from S3, write to CloudWatch, read from DynamoDB
* Read from S3
* Write to CloudWatch

## **Policies**

Who can dow what to which resources and when. Written in JSON

Example:
* Allow IAM users to rotate their own credentials programmatically and in the console
* Alllow user to start and stop EC2 instances
* Allow a lambda function to access a DynamoDB table

## **Security Token Service (STS)**

> Enables you to request temporary, limited-privilege credentials for IAM or federated (external) users

> Example EC2 instance in Production:
* Call STS:AssumeRole
* Return temporary credential
* Delete EC2 instance using temporary credentials
* Credential automatically expire 15-60 minutes

## **Identity Federation**

Managing user identities outside of AWS and getting those identities permission to use

Identity Providers:
* Amazon Cognito
> * Recommended for Mobile and Web-based Applications
> * Does most of the behind-the-scenes work for you
> * Supports anonymous sign-ins
* Web identity Federation
> * No longer recommended, but works with Amazon, Facebook, Google, or any provider compatible with OpenID Connect (OIDC)
* SAML 2.0
> * Older way of doing things
> * Examples: Active Directory, Active Directory Federated Services (ADFS)
* Custom Identity Broker
> * User when identity provider is not compatible with SAML 2.0

### *Active Directory*

Microsofts proprietary directory service
* Runs on Windows Server
* Used to manage permissions and control access to network resources
* Data is stored as objects (Users, Groups, Apps, Devices)

### *Directory Service Types*

| AWS Managed Microsoft AD | AD Connector |
| -----------------------| ------------ |
| Mangaed Active Directory in the cloud | A proxy to redirect request to on-premises Active Directory |
| Can connect to/trust an Active Directory on-premises | Users are managed on premises |
| User authenticating to AWS can be looked up on-prem and vice-versa |  |
| Controls how SharePoint, .NET and SQL Server workloads in a VPC connect to AWS |  |

## **AWS single Sign-On**

> Simplifies the process of managing user access to multiple AWS accounts and business applications.

> With AWS SSO, users can sign in once using their existing corporate credentials and access multiple AWS accounts and third-party applications. AWS SSO provides a centralized place to manage access to all accounts and applications, as well as the ability to easily grant or revoke access for individual users or groups.

> AWS SSO integrates with several identity providers, including Microsoft Active Directory, Azure Active Directory, and Okta, allowing users to continue using their existing identity provider for authentication.

> Needs AWS Organizations

### *AWS Organization*

> Enables you to centrally manage and govern multiple AWS accounts. It allows you to create groups of AWS accounts, known as "organizational units" (OUs), and apply policies across those OUs.

> Service Control Policy
* Used with AWS Organization, SCPs let you define AWS services and actions that are allowed/disallowed
* Additional layer beyond IAM

### *AWS Control Tower*

> Simplifies the process of setting up and managing a multi-account AWS environment. It provides a centralized hub for configuring and managing multiple AWS accounts, and it includes pre-built templates for configuring accounts with security, compliance, and governance policies.

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