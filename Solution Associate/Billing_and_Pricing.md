# **Section: Billing and Pricing**

### **Resources**

* EC2 Pricing Models: https://aws.amazon.com/ec2/pricing/

* Savings Plans: https://docs.aws.amazon.com/savingsplans/latest/userguide/what-is-savings-plans.html

* AWS Pricing Calculator: https://calculator.aws/#/

### **Cheat Sheet**

#### *EC2 Pricing*
* On-Demand is the easiest but most expensive
* Spot instances alow you to bid on excess capacity (90& savings), but instances can be terminated at any time
* Resreved off 30-60% savings for reservations of 1-3 years for a specific instance type
* Savings plans combine on-demand and reserved; you receive savings on the commitment of spend for 1-3 year and then get on-demand pricing after that
  * EC3 Saving Plan: Applies only to EC3 Instance
  * Compute Savings Plan: Applies to EC3, Lambda and Fargate

#### *AWS Organiziations*
* Organizations are a collection of accounts
* Enable consolidate billing (costs for all account roll up into a single bill)
* Can share discounted pricing across accounts

#### *Cost Allocation Tags*
* Once Activated, can be used to group and filter charges

#### *Billing Dashboard*
* Provides a snaphshot of costs by service, forecasted costs, etc.

#### *Cost Explorer*
* Provides a way to drill into specific charges and group/filter by service, region, tags, etc.
* Can provide a forecast of charges base on existing usage

#### *AWS Pricing Calculator*
* Prior iterations were call Total Cost of Ownership (TCO) Calculator and the simple monthly calculator
* Publicly available at calculator.aws
* Provides an estimate of costs based on the services chose (useful for existing customers, as well as those who are evaluating AWS)

#### *AWS Budgets*
* Create and track budgets and send alerts
* Alerts can be based on actual AND forecasted spend
* Can filter alarms by region and service
* Budgets can be created for cost, usage, Savings Plans, and Reservations

#### *CloudWatch Billing Alerts/Alarms*
* Activated through Billing
* More limited than Budgets; only used to send alerts
* Alerts can only be based on actual spend (NOT forecasted)
* Filtering by region is not possible

----
## **EC2 Pricing Models**

|  | On-Demand | Spot | Reserved | Savings Plan |
| ---- | ----| ---- | ---- | ---- |
| What is it? | Pay as you go; No up-front commitment| Bid on AWS spare capacity | Commitment 1-3 years for a specific instance type | Commitment 1-3 years on spend; Savings on the commitment; on-demand pricing after that |
| Cost | Most expensive | Least expensive; 90% savings | 30-60% saving over on-demand | Up to 72% saving over on-demand |
| Best Used for | General; trying things out | Interruptible workloads | steady known workloads | steady, known workloads but with more flexibility |
| Important Point | Flexible and easy to work with | can be terminated at any time | Pay for capacity regardles of usage | Flexible and easy to work with |

----
## **Organizations and Consolidated Billing**

Receive a single bill for all accounts in the organization

Track combined costs, but can itemize by account

Can share discount pricing across accounts

----
## **AWS Cost Explorer**

Cost management tool offered by Amazon Web Services (AWS) that helps you analyze, visualize, and manage your AWS spending. With Cost Explorer, you can:

* View your AWS usage and costs over a specified time period.
* Analyze your costs by service, resource, tag, and other dimensions.
* Identify cost trends and anomalies to help you optimize your usage and reduce costs.
* Create custom cost reports and share them with other members of your organization.
* Set up cost alerts to notify you when your spending exceeds a certain threshold.

----
## **AWS Pricing Calculator**

Helps you estimate the cost of using AWS services for your specific use case. It allows you to select and configure the services you want to use, and then provides you with an estimate of the monthly costs based on your usage.

The pricing calculator offers a range of features, including:
* Selection of AWS services: You can choose from over 100 different AWS services and configure them based on your specific needs.
* Flexible input options: You can input your usage data manually, or import data from AWS CloudTrail logs or AWS Cost and Usage Reports.
* Customizable parameters: You can customize the parameters of each service to fit your specific needs, such as the amount of storage or compute capacity required.
* Cost breakdown: The pricing calculator provides a detailed breakdown of the estimated costs for each service, including data transfer, storage, and compute costs.
* Comparison with different regions: You can compare the costs of running your services in different AWS regions to find the most cost-effective option.

----
## **AWS Budgets and Billing Alerts/Alarms**

* Used to create and track budgets and send alerts
* Can receive alerts based on actual spend AND forecasted spend
* Can filter alarms by region and service
* Create budgtes for cost, usage, Savings plans and reservations
* Newer Service

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