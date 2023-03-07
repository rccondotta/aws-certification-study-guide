# **Section: Networking**

### *Resources*

* Helpful site for learning about CIDR: https://cidr.xyz/
* AWS Regions and Availability Zones: https://aws.amazon.com/about-aws/global-infrastructure/regions_az/
* Direct Connect locations: https://aws.amazon.com/directconnect/locations/

### *Cheat Sheet*

#### *Virtual Private Cloud (VPC)*
* Your own private cloud/network within the cloud that isolates your resources
* Splits into subnets
> * Public: has route to an Internet Gateway
> * Private: does NOT have a route to an Internet Gateway; if you need access to the internet, use a NAT Gateway
* VPCs are tied toa region and span multiple AZs
* IP Addressing
> * For CIDR blocks, the higher the network mask (the "slash number"), the fewer addresses available
> * RFC 1918 addressing is for private address
* Route Tables control the flow of traffic between different resources
* VPC Endpoints allow you to acess other AWS resources over the private AWS network (rather than the inernet)
> * "Gateway" type endpoits are for S3 and DynamoDB; "Interface" type endpoints are for all services
*VPC FLow Logs give visibility into all network traffice (VPC level, subnet level, security group level, etc.)

#### *Network Security*
* Network Access Control Lists (NACLs) control traffic at the subnet level; stateless
* Security groups control traffic at the EC2 instance level; stateful

#### *Elastic Network Interfaces (ENIs)*
* A virtual network card
* All EC2 instances (or their ENIs) have a private IP; can optionally have a public IP and Elastic (fix, public) IP

#### *Network Address Translation (NAT)*
* Translates a private address to a public address
* Can be performed by: Internet Gateway, NAT Gateway and NAT instance (no longer supported)
* Bastion Hosts can be used in a public subnet to allow SSH-ing into an instance in a private subnet ("jump host")

#### *Hybrid Networking*
* Site-to-Site VPN
> * Traffic is encrypted, but flows over the Internet
> * Inexpensive and easy to set up
* Direct Connect
> * A dedicated physical connection (i.e., bypassess the internet)
> * Data not encrypted by default
> * Faster performance, but takes longer to set up
-----

## *Virtual Private Cloud (VPC)*

> Your own private cloud/network within the cloud

### *IP Addresses*

| Example | Private | Public | Elastic |
| ---- | ---- | ---- | --- |
| Person | Nickname | Cell Phone Number | Social Security Number |
| | Used only by close friends and family (private network) | Anyone can use it to reach you but only temporary | Uniquely identifies you and never changes |
| AWS EC2 Instance | Private IP Address | Public IP Address | Elastic IP Address |
| | Used to identify resources on a private network (can't reach from internet) | Accessible to anyone over the internet but only temporary (changes when you stop/start an instance) | A static public IP (doesn't change); Can be attached to an instance |

### *Classless Inter-Domain Routing (CIDR) Notation*

> Notation for describing blocks of IP addresses

### *RFC 1918 (Private) Ranges*

> Private IP addresses can only be in certain ranges (so they don't conflict with public IPs)

----

## **Subnets**

> Public - has direct route to the internet and are typically used for resources that need to be accessible from the internet  
> Private do not have direct internet access and are used for resources that need to be isolated from the internet.  
> AWS reserves 5 ip addresses

----

## **Internet Gateways and Routes Tables**

Internet Gateway (IGW) is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. An IGW is used to enable communication between your VPC and other networks, including the internet.

Route Table is a set of rules, called routes, that are used to determine where network traffic is directed. Each subnet in a VPC must be associated with a route table, and the route table controls the traffic routing for the subnet. You can add, remove, or modify routes in a route table to control the flow of traffic to and from your VPC.

### *Default Route to Enable Internet Access*

| Destination | Target | What This Means |
| ---- | ----| ----|
| 10.0.0.0/16 | Local | If you see a request to an IP Address inside of our VPC's CIDR block, route it locally within the VPC |
| 0.0.0.0/0 | Internet Gateway | If its any other IP (other than the ones listed above), route it to the Internet Gateway |

----

## **Elastic Network Interfaces (ENI)**

Used by an EC2 instance to communicate with other network resources (AWS, on-premises, Internet, etc.)  
* Think of it as a virtual networking card  

Every instance has a primary ENI  
* Connected to only one subnet, and cannot be removed
* Can attach additional ENIs  

Can be created independently of an instance and attached at a later point  
Can be moved to another instance to support failover

----

## **Security Groups**

Firewall that sits around our EC2 Instance  
Specific to a region and VPC
* If you don't see a security group, it might be in a different region

Source and Destination can be a CIDR or another security group  
Stateful
* When traffic is allowed in one driection, the security group allows reply traffic in the opposite direction

Default security group
* automatically created for each VPC
* cannot delete it, but you can modify it to meet your needs

----
## **Network Access Control Lists (NACLs)**

Type of security control used to control traffic flow at the subnet level in a Virtual Private Cloud (VPC). NACLs act as a firewall that can allow or deny traffic based on the rules that you configure.  

Each subnet in a VPC can have its own NACL attached to it, and NACLs evaluate traffic as it enters or exits a subnet. NACLs operate at the protocol and port level, and rules are evaluated in order, from lowest to highest. The can be associated with many subnets.

### *Other Notes*  
Common Use case: block traffic from a specific IP address (not possible with a security group)  
Stateless
* When traffic is allowed in on direction, the return direction is NOT automatically allowed (unlike with stateFUL security groups)
* must explicitly permit reutn traffic

New NACLs will automatically deny everything
* vs. the Default NACL, which allows everything

----
## **NACL vs Security Groups**

NACL
* Firewall that controls traffic in/out of a subnet
* Rule for Allow and Deny
* Rule include IP Addresses / CIDRs (only)
* Stateless (return traffic must be explicitly allowed)

Security Groups
* Firewall that controls traffic in/out of an EC2 instance
* Rules for Allow (only)
* Rules include Ip address / CIDRs and other security groups
* Stateful (return traffic automatically allowed)

----
## **Network Address Translation (NAT) Devices**

In addition to network address translation in the Internet Gateway, two other resources can perform this function
* 1: NAT Gateways and 2: NAT Instances
* NAT devices allow instances WITHOUT PUBLIC IPs to get out to the internet, but prevents traffic in; Internet Gateway handles translation for instances WITH PUBLIC IPs
* Common use case: doing patching, updates, or uploading data

NAT Gateway
* Recommended approach
* Managed by AWS and scales automatically to accommodate bandwidth requirements
* Must live in a public subnet
* Does not have an ENI, so security groups do no apply (use NACLs on the subnet)
* Requires and Internet Gateway; Routes required from private subnet to NAT Gateway to Internet Gateway
* Is tied to a single AZ; for redundancy, create additional NAT Gateways in other AZs

NAT Instance
* Older technology, support discontinued at end of 2020
* preconfigured linux-based AMI
* Has an ENI; must assign public ip address; must use a security group with it
* does not automatically scale
* must disable source/destination check so it can receive traffic addresssed to an IP other than its own

----
## **Bastion Host**

Specially secured server that acts as a gateway between a private network and the public internet. The primary purpose of a bastion host is to provide secure access to the private network from remote locations.

Used where virtual machines or other resources in a private network are not directly accessible from the internet. Instead, administrators must first connect to the bastion host, and then use that connection to access other resources in the private network.

----

## **VPC Peering**

Allows you to connect two or more Virtual Private Clouds (VPCs) in the same or different regions within the same AWS account or across different accounts. VPC peering enables you to route traffic between the peered VPCs as if they were on the same network.

Can extend your network across multiple regions or accounts and share resources such as EC2 instances, RDS databases, or other services. This can simplify your network architecture and reduce data transfer costs, as traffic between the peered VPCs does not need to traverse the public internet.

----
## **VPC Endpoints**

Allow you to privately connect your Amazon VPC to supported AWS services and VPC endpoint services without requiring an internet gateway, NAT device, VPN connection, or a direct connection. This provides more secure and scalable access to these services from within your VPC.

Gateway Endpoints
* Used to connect to: S3 DynamoDB

Interface
* Used to connect to all other AWS Services

----
## **VPC Flow Logs**

Allow you to capture information about the IP traffic going to and from network interfaces in your Virtual Private Cloud (VPC). VPC flow logs provide visibility into your network traffic, which can be useful for troubleshooting connectivity issues, monitoring network activity, and analyzing security threats.

----
## **VPC Reachability Analyzer**

Analyzes the configuration between two endpoints in a VPC
* Doesn't send/receive traffic

Returns a "reachable" or "not reachable"
* "Not reachable" will identify the blocking component

Costs 10 cents (U.S) each time it runs

----
## **Site-to-Site VPN**

Hybrid Networking
* Encrypted
* Uses public internet
* Fast to set up

On-Premis Side - Customer Gateway (CGW)  
VPC Side - Virtual Private Gateway (VGW)  
VPN Cloudhub for multiple on-premis data centers

----
## **Direct Connect**

Hybrid Networking
* Dedicated Physical Network
* Bypasses public internet; uses dedicated private network (not encrypted by default)
* Faster and more expensive
* Takes longer to set up

Process
* VPC - Virtual Private Gateway
* Direct Connect Location
* Corporate Data Center

More Secure option

----
## **Transit Gateway**

Fully-managed network transit hub that enables you to connect your Amazon Virtual Private Cloud (VPC) and on-premises networks to a single gateway. It acts as a hub for routing traffic between connected networks, simplifying network architecture and reducing operational costs.

Can include VPC, Direct Connect, site-to-site VPN 

### *Other Notes*

Sits at the region level  
Supports cross-region, and can peer Transit Gateways together  
To limit VPC access, update the route tables  
Supports IP multicast
* Multicast: delivers a single stream of data to multiple receiving computers simultaneously
* Supports routing multicast traffic between subnets
* Serves as a multicast router for instances
* Only AWS service to support multicast

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
