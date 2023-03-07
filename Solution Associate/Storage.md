# **Section: Storage**

### *Resources*

* S3 storage classes comparison and FAQs: https://aws.amazon.com/s3/storage-classes/?nc=sn&loc=3

* Example S3 bucket policies: https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html

### *Cheat Sheet*

#### *S3*
* Inexpensive, unlimited, reliable object storeage (files, photos, logs, etc)
* Names must be globally unique; flat hierarchy where folders are emulated
* Works in an "eventually consisten" model
* Storage classes optimize cost by storing data according to frequency of of access
* Encryption options are server-side (SSE-S3, SSE-KMS, SSE-C) or client-side
* Versioning, MFA Delete and object lock help prevent accidental object deletion
> * Governance (Some) and Compliance Mode (Nodody) for object lock
* Access Control: IAM policies, bucket policies, and access control lists (ACL)
> * Possible to block all public access at the account level
* Presigned URLs grant temporary access toa  file
* Can be used to host a static website
> * If resources are stored on different domains, CORS needs to be enable
> * Must be granted FROM the cross-origin server

#### *S3 Storage Classes*
Most expensive to least expensive
| Standard | Standard IA | Intelligent | One Zone IA | Glacier Instant | Glacier Flexible | Glacier Deep Archive | 
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Frequently accessed | Long-Lived infrequently accessed | Long-lived data with changing or unknown acess patterns | Long-Lived, infrequently accessed, non-critical data (1 AZ) | Long-Lived, accessed quarterly; needs immediate access | Long-Lived; accessed 1-2 times per year; does not required immediate access | Long-term data acessed less than once per year |
| No min storage duration | 30-day min | No min storage | 30 day min | 90-day min | 90 day min | 180 day min |
| Retrieval milliseconds | milliseconds | milliseconds | milliseconds | milliseconds | 1 min to 12 hours | 12-48 hours | 

#### *Elastic File System*
* Storage that can be used by multiple services (EC2, lambda, on-premises servers, etc)
* Only pay for what you use (no up-front provisioning)
* Has different storage classes (similar to S3)

#### *Amazon FSx*
* Third-part file system
* FSx for Windows File Server - built on Windows Server
* FSx for Lustre - high performance file system

#### *Storage Gateway*
* Used in hybrid architecture, to store data in AWS from on-premises
* File Gateway uses NFS and SMB for files; Tape Gateway deals with tape backups
* Volume Gateways (ISCSI)
> * Stored mode (data stored on-prem; AWS for backup); CACHED mode (data stored in AWS; frequently-accessed cached on-prem)

#### *Snow Family of Products*
* Physical storage devices used to transfer massive amounts of dat (SnowCone, SnowBall, SnowMobile)

----
## **Simple Storage Service (S3) Overview**

Inexpensive object (think "file") storage in AWS  
"Unlimited" storage capacity  
Organize by "buckets"
* Can create up to 100 buckets per account (can also request a limit increase)

### *Benefits*
Easy to scale  
Highly Available (99.99%)
Inexpensive

### *Naming and Architecture*
Exists within a single region, but name must be globally unique  
Can Access through the browser or programmatically

### *Size Limits*
Limit for a single object: 5 TB  
Limit for a single PUT: 5 GB
* For larger objects (100MB+), "Multipart Upload" is recommended

----
## **Durability and Availability**

Durability - Data won't be lost  
Availability - Data will be avilable on request

Eventually Consistent Data
* Data is replicated across multiple locations (at least three AZs)
* This may cause a brief delay as changes propagate
* Design accordingly

----
## **Encryption**

At REST
* As a best practice, S3 data should always be encrypted at rest (unless intended for public consumption)
* Can be set at the bucket or file level
* Once applied to a bucket, all new files will be encrypted upon upload
* Two options for encryption at rest

> * Server-side:
>> * Amazon S3-Managed Keys (S3 creates, manages and uses the keys for you)
>> * AWS KMS-Managed Keys (manages the keys for you and provides audit trail and user management)
>> * Customer-Provided Keys (must be done programmatically)
> * Client-Side:
>> * Encrypted before its uploaded to S3
>> * More complex
>> * Must be done programmatically

In Transit
* Use amazons encrypted API endpoints to to encrypt data in transit
* HTTP endpoint also available, but HTTPS with TLS/SSL is required for encryption
* HTTPS also required for SSE-C

----
## **Versioning**

Enabled and suspended at the bucket level, and allows you to keep multiple variants of an object  
Once is enabled on a bucket, cannot be unversioned
* Can be suspended by the bucket owner

Versionin state applies to ALL objects in the bucket  
Enabling versioning will give new objects a unique version ID  
Existing objects will have a version ID of null and then get a unique version ID when modified in the future

Benefits
* Restore objects that are accidentally overwritten or deleted
* Prevent deletion of objects by enforcing "Object Lock" and/or "MFA delete"

Preventing Deletion with MFA Delete
* MFA Delete (applied on the bucket)

Preventing deletion with Object Lock
* Prevents object deletion/overwriting for a fixed amount of time or indefinitely
* Retention period: a fixed period of time that an object is locked
> * Governance mode: only users with special permissions can delete/overwrite objects or alter settings
> * Compliance mode: NOBODY (not even root) can delete/overwrite objects or alter settings
* Legal Hold: Object is locked until is it explicitly unlocked
* Only works in versioned buckets
* Stores objects using a write-once-read-many (WORM) model

Versioning can result in one or more objects of MILLIONS of versions  
S3 will throttle reuqest resulting in HTTP 503 responses  
Use the S3 inventory tool to identify these objects
Expiration policies can also help prevent this issue

----
## **Storage Classes and Lifecycle**

Store objects in the most cost-efficient way  
Actions: Transition and Expiration

Storage Classes (Very Important)
* Standard
* Standard-IA
* Intelligent-Tiering
* One Zone-IA
* Glacier Instant Retrieval
* Glacier Flexible Retrieval
* Glacier Deep Archive

Create a lifecycle rule to change storage class types  
Objects must be stored for a min of 30 days in Standar, Standar-IA, One Zone-IA before they can be transitioned

----
## **Accessing S3 Objects**

Access Policies:
* User - IAM Policies
* Resource - S3 Bucket Policies or Access Control Lists (ACLs)

----
## **Cross-Origin Resource Sharing (COORS)**

Defines how resources in one domain interact with resources in another domain  
* Protocol: http  
* Host: www.mywebsite.com  
* Port: 80

Enforced by the browser (this is NOT an AWS thing)  

----
## **Elastic File System (EFS)**

Storage for an EC2 instances, containers, Lambda functions, on-premises servers
* Can be used by MULTIPLE things at a time
* Can be used across MULTIPLE AZs

Only pay for the storage you use (no up-front provisioning)

Storage Classes
* Standard - Frequently accessed data (>= 3 AZ)
* Standard IA - Long-lived, infrequently accessed data (>= 3 AZ)
* One Zone - Frquently accessed, but non-critical data (1 AZ)
* One Zone IA - Long-lived, infrequently accessed, non-critical data (1 AZ)

----
## **Amazon FSx**

Fully managed third-party file systems
* Benefits of the cloud (replication, high availability, etc.), but also features specific to third-party (Active Directory integrations, NTFS, etc.)

Amazon FSx for Windows File Server
* Built on Windows Server

Amazon FSx for Lustre
* High Performance Server

----
## **Storage Gateway**

File Gateway
* A place to store and share files
* Uses Network File System (NFS) and Server Message Block (SMB)

Tape Gateway
* Deals with backups (think of the hpysical tapes used to back up servers)
* Stores the contents of the tapes in S3/Glacier

Volume Gateway
* STORED - Data stored/accessed on-prem; data going to AWS is for backup purposes
* CACHED - Data stored in S3; only frequently-used data is cached on-premises
* ISCSI

----
## **Snow Family of Products**

Migrating an on-premises data center  
Backing up or restoring massive amounts of data  
Edge computing and storage (Limited Storage)

| AWS SnowCone | SnowBall | SnowMobile |
| ---- | ---- | ---- |
| Smallest | Medium | Largest |
| |

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