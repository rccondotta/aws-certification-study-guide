# **Section: Compute**

### **Resources**

* All compute products: https://aws.amazon.com/products/compute/
* EC2 instance types: https://aws.amazon.com/ec2/instance-types/
* EC2 instance purchasing options: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-purchasing-options.html
* EBS volume types: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html

### **Cheat Sheet**

#### *EC2*

* Primary compute service used to create virtual servers
* Different pricing options (on-demand, reserved, spot, etc.)
* Amazon Machine Images (AMIs) shorten launch time by creating repeatable base images
* Elastic Block Store (EBS) essential a hard drive thats network-attached; persists when an instance is shut down
* Instance Store: physically attached to the underlying hardware; faster, but data is lost when shutting down

#### *Elastic Beanstalk*

* Platform as a services that allows you to "just write code"; all underlying work "magically" happens for you

#### *Lambda*

* Serverless functions or scripts; You're responsible for security of your code, data, and IAM; AWS does everything else

#### *Containers*

* Light Weight compute that lets you package up everything needed to run an application (no dedicated operating system required); built on docker technology
* Services: Elastic Container Service (ECS) or Elastic Kubernetes Service (EKS)
* Fargate is a serverless solution for runing containers (creates EC2 instances for you)
- Container images stored in Elastic Container Registry

---

## **EC2 Overview**

A virtual server that you "rent" in AWS called an instance
* Easy to to scale
* Reliable
* Use with other services
* Only pay for what you use

Instance Types:
* Compute, Memory, Accelerated, Storage, HPC

| Instance Purchasing Options | Description |
| --------------------- | --------|
| On-Demand Instances | Default option and pay by the second (min 60 seconds)|
| Reserved Instances | 1-3 years and savings up to 70% |
| Spot Instances | Bid on unused EC2 capacity and savings up to 90% but can lose anytime |
| Dedicated Hosts | Book an entire physical server and bring licenses. Purchased on-demand or reserved |
| Dedicated Instances | Ensures no other AWS customer shares your hardware and pay by the hour |
|Capacity Reservations| Reserve capacity for instances in a specific availabity zon for any duration |

### *Connection*

Secure Shell (SSH) - Protocol used to securely log into other computers and run commands form the command line (Uses TCP protocol on Port 22)

### *Placement Groups*

By default, EC2 spreads out instances across underlying hardware to minimize failures

Placement groups let you influence where instances live (no charge)

Types of Strategies:
* Cluster - Instances are physically close together (same rack) in a single availability zone
> * Very low latency between instances
> * High network throughput
> * harware failure brings down everything
* Spread - Instance is placed on distinct hardware, across AZs
> * Isolate impact of hardware failure
> * For workloads with small number of critical, separated instances
> * Can only have up to 7 runnin ginstances per AZ per group
> * Starting and launching additional instanes will fail
* Partition - instances are grouped into partitions, which are each on separate racks
> * Up to 7 partitions per AZ
> * isolate impact of hardware failure
> * Large distributed workloads, such as HDFS, Hbase and Cassandra

## **Amazon Machine Images (AMI)**

A preconfigured virtual machine that contains:
* Operating system and preinstalled software

Why Use an AMI?
* Repeatable and shorten launchg time

Available from Amazon, marketplace, or create your own

## **Elastic Block Store Overview**

Storage for an EC2 instance
* Think as Virtual hard drive
> * Attached over the network (not physically)
* Root Volume created for an EC2 instance; can add additional volumes as needed
* A volume can only be attached to one instance at a time
* Must be in the same AZ as the instance

Default persistenc settings
* Persists when instance is shutdown
* Deletes when an instance is terminated

IOPS - measurement of I/O per second

Throughput - how much you can read from a single access to the disk

| IOPS | Throughput |
|------------- | ----- |
| Databases | Big Data / Warehousing |
| frequent retrievals | large data files that require large "bites" |

Can create a snapshot of a volume and then restore it
* Stored in S3
* Useful for backup/recovery or copying to another region

## **EC2 Instance Store**

Storage thats physically attached to your instances' underlying hardware
* Faster Performance

Storage is ephemeral
* data is lost when instance is stopped (or hardware fails)

Use Cases
* Workloads that need to store temporary content or need fast caching performance

## **AWS Lambda**

Serverless computing (Runs on a sever you don't have to buy or manage)

Code runs in response to some event, on a server you don't have to buy or manage

### *Quotas/Limits*
* Compute and Storage (can request increases)
> * Concurrent executions (1,000)
> * Storage for uploaded function (75 GB)
* Deployment and Execution (cannot be increased)
> * Function memory allocaiton (128 MB to 10240 MB)
> * Function timeout 900 seconds
> * Function environment variables (4kb)
> * Deployment package (50 MB zipped, 250 MB unzipped)

## **AWS BeanStalk**

Platform as a Service (Paas)
* Infrastructure is handled for you
> * EC2 instances, load balancers, auto-scaling groups, etc
* Uses CloudFormation templates to deploy the infrastructure

Health Monitoring avialable in the Console

## **Containers on AWS**

### *Elastic Container Service*

> Used to run, stop and manage Docker containers in AWS

> Integrated with many AWS services, including IAM, load balancers, auto scaling, VPC, etc.

> ECS Cluster - logical grouping of tasks or services that run on infrastructure registered to your cluster (EC2 instance == Container Service)
> * Task - running container (eg NGINX) whose settings are defined in a task definition
> * Service - long running tasks with the same task definition

### *Elastic Kubernetes Service*

> Kubernetes as a service on AWS

> Automates deploying, scaling, management, and scheduling of containers

> Large community and support

> AWS installs, operates, and maintains the Kubernetes cluster/nodes

* Options for running ECS/EKS
> * You provision and maintain the EC2 instances that the containers run on

### *Fargate*

> Serverless solution where AWS handles the underlying infrastructure

### *Elastic Container Registry*

> Private repository on AWS for docker images

> ECS, EKS pull images from here to build containers

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