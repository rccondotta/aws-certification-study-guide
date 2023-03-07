# **Section: Well-Architected Framework**

### **Resources**

* The Well-Architected Framework: https://aws.amazon.com/architecture/well-architected

----
## **Reliability Pillar**

* Ability to avoid failure, and if it occurs, to recover quickly
* Measure in termas of availability (the percentage of time an applicaiton performs as expected)

Design Principles
* Automatically recover from failure
  * Monitor for performance and act (e.g CloudWatch Alarms, Load Balancers and Auto Scaling Groups)
* Test Recovery
  * Check backup/recovery of S3, EBS, EFS
* Scale Horizontally
  * Distribute load across multiple small resources rather than one large resource
* Stop guessing capacity
  * Monitor performance and scale resource out/in, and/or go serverless
* Manage change in automation
  * Changes should be track and reviewed (e.g CloudFormation)

----
## **Performance Efficiency Pillar**

* Use computing resources efficiently to meet system requirements
* Maintain efficiency as demand changes and technologies evolve

Design Principles
* Democratize advanced technologies
  * Outsource complex tasks to AWS
* Go globail in minutes
  * Deploy across multiple regions to provide lower latency and a better user experience
* User serverless architectures
  * Let AWS manage the underlying infrastructure (e.g Lambda, Fargate)
* Experiment more often
  * Test different types/configurations of compute and storage to find the optimal solution
* Consider mechanical sympathy
  * Choose a solution that aligns to workloads goals (e.g EC2 instance types)

----
## **Security Pillar**

* Improve security through cloud technologies to protect data, systems and assets

Design Principles
* Implement a strong identity foundation
  * Principle of least privilege; separation of duties
* Enable tracability
  * Monitor, alert, and audit
* Apply security at all layers
  * NACLs, security groups, applications, etc.
* Automate security best practices
* Protect data in transit and at rest
* Keep people away from data
* Prepare for security events

----
## **Cost Optimization Pillar**

* Run systems to deliver business values at the lowest price point

Design Principles
* Implement cloud financial management
  * Invest time across the organization to understand/manage finances
* Adopt a consumption model
  * Get in the mindset of paying for what you use; shut things down when you don't need them
* Measure overall efficiency
  * What gets measured gets done
* Stop spending money on undifferentiated heavy lifting
  * Let AWS do things like data center operations so you can focus on your business
* Analyze and attribute expenditure
  * Dig into the details of resource costs

----
## **Operational Excellence Pillar**

* Support development and run workloads effectively; gain insight into their operations
* Continuously improve support to deliver business value

Design Principles
* Perform operations as code
  * CloudFormation
* Make frequent, small, reversible changes
  * Small changes are easier to reveres if needed
* Refine operations proceures frequently
  * Set up regular time to review and validate procedures
* Anticipate failure
 * Identify and mitigate potential failures early and often
* Learn from operational failures
  * Identify lessons learned, and share them

----
## **Sustainability Pillar**

* Focuses on environmental impacts, especially energy consumption and efficiency

Design Principles
* Understand your impact
  * Measure the impact of your workloads
* Establish sustainability goals
* Maximize utilization
  * Right-size workloads
* Anticipate and adopt new, more efficient offerings
* Use managed services
* Reduce downstream impact of your workloads

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