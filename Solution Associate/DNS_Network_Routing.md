# **Section: DNS and Network Routing**

### *Resources*

* Route 53 Routing Policies: https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html

* CloudFront Global Network: https://aws.amazon.com/cloudfront/features/?whats-new-cloudfront.sort-by=item.additionalFields.postDateTime&whats-new-cloudfront.sort-order=desc#Global_Edge_Network

* AWS Global Accelerator Speed Test: https://speedtest.globalaccelerator.aws/#/

### *Cheat Sheet*

#### *Route 53*
* Managed domain name service (DNS)
* Used to map IP address to domain names
* Can register domain names
* Used to route traffic ACROSS regions using various routing policies
  * Can be used in combination with elastic load balancer (which route traffic only in a single region)
* DNS record types
  * A Record: Points a host name to a specific Ip address
  * CNAME: Points a host name to another name or A Record
  * Alias: Specific to AWS; Points a host name to an AWS resource

#### *CloudFront*
* Content Delivery Network (CDN) thats geographically distributed to deliver content faster by caching
* Commonly used to deliver media files (videos, images)
* Can be used in conjunction with Route 53

#### *Global Accelerator*
* Uses global network of edge locations to improve speeds for a variety of applications
* Does not use caching; improvement comes from network routing of traffic (moving off the public internet)

----
## **Domain Name System (DNS)**
Maps IP addresss (142.251.215.238) to domain names (google.com)

Anatomy of a domain name (aws.amazon.com)
* com - Top-level domain (TLD)
* amazon - Second-level domain (SLD)
* aws - Subdomain
* aws.amazon.com - Fully qualified domain name (FQDN)

DNS Record Types - Used for mapping host names and IP records in DNS

| Type | Function | Example |
| ---- | ---- | ---- |
| A Record | Points a host name to a specific (IPv4) IP address | aws.amazon.com -> 205.251.242.103 |
| CNAME Record | Points a host name to another name or A Record (Only works on non-root domains) | amznwebsvcs.mywebsite.com -> aws.amazon.com |
| ALIAS | Specific to AWS, used in conjunction with above; Points a host name to AWS resource | app.mywebsite.com -> website.s3.region.amazonaws.com |

----
## **Amazon Route 53**

Managed DNS Service
* DNS server requests are addressed to TCP/UDP port 53

Primary Functions
* Domain name registration (mywebsite.com)
* DNS Routing
* Health Checking

Public and Private Hosted Zones
* A container that holds records* defining how to route traffic
* Public hosted zone
  * Defines how traffic is routed on the internet (public domain names)
  * Created when you register a domain name through Route 53, or transfer an existing domain to Route 53
* Private hosted zone
  * Defines how traffic is routed in a VPC (private domain names)

Route 53 Routing Policies
* Simple
  * Routes all requests to the IP domain name you assign
  * Default routing policy
* Failover
  * Routes to the primary resource that you specify, so long as its healthy; if unhealthy routes to the secondary
* Geolocation
  * Routes based on the location of **users** (using IP addres, country, etc) and decides which resource to send
* Geoproximity
  * Routes based on the locaiton of **resources** and uses a bias
* Latency
  * Route traffic to the region that provides the best latency for the user
* Weighted
  * Traffic is routed to multiple resources based on a ratio you set

Routing with:
* ELastic Load Balancer (Region Based)
  * Balances traffic between EC2 instances in a SINGLE region
  * New instances can be added and routed automatically
  * Unhealthy instances can be removed immediately
  * Able to "see" which servers are busier and than route accordingly
* Route53
  * Balances traffic to resources ACROSS regions
  * New resrouces must be manually added/replaced
  * DNS is cached so unhealthy targets may be routed to for some time period
  * Note able to "see" which servers are busier than other 

----
## **CloudFront**

* Use AWS's global network and edge locations to improve speed (Geographically distributed)
* Content Delivery Network (CDN)  (e.g. media files)
* Serves cached content from edge locations

----
## **AWS Global Accelerator**

* Uses AWS's global network and edge locations to improve speed
* Works for a wide variety of applications (HTTP, TCP, UDP)
* No caching; improvement comes from network routing of traffic (moving off the public internet)

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

