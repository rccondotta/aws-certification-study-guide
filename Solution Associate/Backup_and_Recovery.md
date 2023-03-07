# **Section: Backup and Recovery**

### **Resources**

* Disaster Recovery Strategies: https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/rel_planning_for_recovery_disaster_recovery.html

### **Cheat Sheet**

#### *Disaster Recovery*
* Recovery Point Objective (RPO): Has to do with loss; when was data last backup up BEFORE a disaster
* Recovery Time Objective (RTO): Related to the downtime AFTER a disaster
* Pilot Light: Tens of minutes: start and scale resources after an event (core services)
* Warm Standby: Minute: scale resrouces after an event (busines critical services)
* Multi-site/Active-Active: Zero downtime (mission critical services)

#### *Data Lifecycle Manager*
* Used for backup and recovery of EBS volumes (only)

#### *AWS Backup*
* Used to do backups for multiple services (EBS, EFS, RDS, etc.) all from a single interface

#### *Backup and Restore with RDS
* Automated backups; RDS does a full daily snapshot (single region)
* Snapshots; user-initiated (cross-region)
* Read replicas (cross-region)
* Restoration: To a point in time; From a snapshot; Promoting a red replica

#### *Backup and Restore with Aurora*
* Generally going to be faster and require less effort
* Mult-Master: All db instances have read/write capability (single region); if writer becomes unavailable, another takes over
* Global Database: Spans up to 5 regions; during failover, a secondary region promoted to primary

----
## **Disaster Recovery Terminology and Strategies**

RPO (Recovery Point Objective)
* Acceptable data loss
* Expressed in hours
* Example:
  * With an RPO of 1 hour, you could lose up to 1 hour of data

RTO (Recovery Time Objective)
* Acceptable downtime
* Expressed in hours
* Example:
  * With an RTO of 1 hour, systems should be up and running within 1 hour of disruption

Disaster Recovery Strategies
* Backup and Restore
  * RPO/RTO - Hours
  * Cost - $
  * Lower priority use cases
  * Restore data after event
  * Deploy resources after event
* Pilot Light
  * RPO/RTO - Tens of minuts
  * Cost - $$
  * Less stringent RPO/RTO
  * Core Services
  * Start and scale resrouces after event
* Warm Standby
  * RPO/RTO - Minutes
  * Cost - $$$
  * More stringent RPO/RTO
  * Business critical services
  * Scale resources after event
* Multi-Site Active/Active
  * RPO/RTO - Real-Time
  * Cost - $$$$
  * Zero Downtime
  * Near zero loss
  * Mission critical services

----
## **Backup features in AWS**

| | Backup Features |
| ---- | ---- |
| Elastic Block Storage | Snapshots of EBS Volumes; Stored in S3 |
| Relational Database Service (RDS) | Automated backup; RDS does a full daily snapshot; Snapshots user-initiated (Cross-region); Read Replicas|
| DynamoDB | On-Demand table backups |
| Storage Gateway | Back up on-premises files, applications, databases, and volumes to AWS |

### *Data Lifecycle Manager (EBS Only)*
Enables you to automate the creation, retention, and deletion of snapshots taken of Amazon Elastic Block Store (EBS) volumes.

### *AWS Backup (for mulitple services)*
Fully managed backup service that enables you to centralize and automate the backup of your AWS resources across multiple AWS services, such as Amazon EBS volumes, Amazon Relational Database Service (RDS) databases, and Amazon DynamoDB tables.

----
## **Amazon Aurora Multi-Master and Global Databases**

Multi-Master
* All DB instances have read/write capability
* Applies to a single region
* Failover: if a writer DB instance becomes unavilable, another writer takes over automatically

Global Database
* A single Aurora database spans multiple regions (up to 5)
* Writes ares issued to primary region, then replicating to other regions (with no impact to performance)
* Failover: a secondary region is promoted to primary region

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