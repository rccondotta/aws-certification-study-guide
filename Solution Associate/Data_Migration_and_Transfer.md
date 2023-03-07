# **Section: Data Migration and Transfer**

### *Cheat Sheet*

#### *DMS*
* Used to migrate databases from on-premises to AWS, AWS to AWS, or AWS to on-premises
* Supports homogeneous (same database engines) or heterogeneous (different database engine)
  * For heterogeneous, use Schema Conversion Tool

#### *DataSync*
* Used to transfer large amounts of data from on-premises to AWS, AWS to AWS, or other cloud providers to AWS
  * DataSynce agent installed at the source
  * On a schedule, data is transferred to DataSynce in AWS, and then copied to the AWS destination service (S3, EFS, FSx)

#### *Application Migration Service*
* Use for lift-and-shift migrations from on-premises to AWS
* Replaces the Server Migration Service (SMS)

#### *AWS Transfer Family*
* Used to transfer files over FTP to either S3 or EFS

#### *AWS Snow Family*
* Physical devices used to transfer data from on-premises to AWS
* SnowCone, SnowBall, SnowMobile

----
## **AWS Database Migration Service**

Fully managed service that helps you migrate your databases to AWS quickly and securely

Schema Conversion Tool
* Used to translate your database schema when your source and target databases are using different engines (e.g, PostgreSQl to Oracle)
* You can also pre-create the schema on the target

----
## **AWS DataSync**

Fully managed data transfer service that makes it easy to move large amounts of data between on-premises storage systems and AWS cloud storage services such as Amazon S3, Amazon EFS, and Amazon FSx for Windows File Server

Used to move large amounts of data
* from on-premisess to AWS
* From AWS to AWS
* From other clouds to AWS

----
## **AWS Application Migration Service**

Lift-and-Shift Migrations (As it sounds)  
Replaces AWS Server Migration Service (AWS SMS), which will likely be deprecated in the future  

How it works
* Map the on-premises environment
* Install replication agents on on-premises servers
* Replicate servers to AWS
* Perform Tests
* Cut over to AWS

----
## **AWS Transfer Family**

Fully managed service  
Support three protocols
* File Transfer Protocol (FTP)
* File Transfer Protocol Over SSL (FTPS)
* Secure File Transfer Protocol (SFTP)  

Credential can be stored within AWS Transfer Family, or you can integrate with other authentication system (e.g Okta, Active Directory, etc.) 

----
## **AWS Snow Family**

Increase in size of data
* SnowCone
* SnowBall
* SnowMobile 

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