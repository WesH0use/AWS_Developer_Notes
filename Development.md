# Development with AWS Services

## [EC2](https://github.com/WesH0use/AWS_Developer_Notes/blob/main/EC2_Development.md)

## [Load Balancers](https://github.com/WesH0use/AWS_Developer_Notes/blob/main/Load_Balancers_Development.md)

## [Elastic Beanstalk](https://github.com/WesH0use/AWS_Developer_Notes/blob/main/Elastic_Beanstalk_Development.md) 

## [Policies & Permissions](https://github.com/WesH0use/AWS_Developer_Notes/blob/main/Policies_Permissions_Development.md)

## [Data Volumes](https://github.com/WesH0use/AWS_Developer_Notes/blob/main/Data_Volumes_Development.md)

## [CNAME Records](https://github.com/WesH0use/AWS_Developer_Notes/blob/main/Resource_Record_Sets_Development.md)


## SQS 
 
### DeleteQueue API Call
Deletes the queue specified by the QueueUrl, regardless of the queue's contents. When you delete a queue, any messages in the queue are no longer available.

When you delete a queue, the deletion process takes up to 60 seconds. Requests you send involving that queue during the 60 seconds might succeed. For example, a SendMessage request might succeed, but after 60 seconds the queue and the message you sent no longer exist.

When you delete a queue, you must wait at least 60 seconds before creating a queue with the same name.
 
### PurgeQueue API Call
 
Deletes the messages in a queue specified by the QueueURL parameter. When you use the PurgeQueue action, you can't retrieve any messages deleted from a queue. The queue however remains.

 ### RemovePermission 
 
 Revokes any permissions in the queue policy that matches the specified Label parameter.

### CreateQueue API Call
**You can't change the queue type after you create it**- You can't change the queue type after you create it and you can't convert an existing standard queue into a FIFO queue. You must either create a new FIFO queue for your application or delete your existing standard queue and recreate it as a FIFO queue.

**The visibility timeout value for the queue is in seconds, which defaults to 30 seconds** - The visibility timeout for the queue is in seconds. Valid values are: An integer from 0 to 43,200 (12 hours), the Default value is 30.
 
 ## AWS Budget Alerts
  
  You can configure AWS Budgets to take actions on your behalf when your budget exceeds a certain cost or usage threshold. Budget alerts can be sent to up to 10 email addresses and one Amazon SNS topic per alert. You can set budgets to alert against either actual values or forecasted values.

Actual alerts are only sent out once per budget, per budget period, when a budget first reached the actual alert threshold.

Forecast-based budget alerts are sent out on a per-budget, per-budget period basis. They might alert more than once in a budgeted period if the forecasted values exceed, dip below, and then exceed the alert threshold again during the budgeted period.

AWS requires approximately 5 weeks of usage data to generate budget forecasts. If you set a budget to alert based on a forecasted amount, this budget alert isn't triggered until you have enough historical usage information.
  
  ## AWS API Gateway
  
Amazon API Gateway is an AWS service for creating, publishing, maintaining, monitoring, and securing REST, HTTP, and WebSocket APIs at any scale. API developers can create APIs that access AWS or other web services, as well as data stored in the AWS Cloud.
  
A usage plan specifies who can access one or more deployed API stages and methods—and also how much and how fast they can access them. The plan uses API keys to identify API clients and meters access to the associated API stages for each key.

You can configure usage plans and API keys to allow customers to access selected APIs at agreed-upon request rates and quotas that meet their business requirements and budget constraints.
  
  ![image](https://user-images.githubusercontent.com/44325167/129881859-4a5697e0-f0e7-41f0-9be2-24771572c44e.png)

 
 
## Policies 
 
You manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources. **A policy is an object in AWS that, when associated with an identity or resource, defines their permissions.** Resource-based policies are JSON policy documents that you attach to a resource such as an Amazon S3 bucket. These policies grant the specified principal permission to perform specific actions on that resource and define under what conditions this applies.
 
**Trust policy** - Trust policies define which principal entities (accounts, users, roles, and federated users) can assume the role. An IAM role is both an identity and a resource that supports resource-based policies. For this reason, you must attach both a trust policy and an identity-based policy to an IAM role. **The IAM service supports only one type of resource-based policy called a role trust policy, which is attached to an IAM role.**
 
**AWS Organizations Service Control Policies (SCP)** - If you enable all features of AWS organization, then you can apply service control policies (SCPs) to any or all of your accounts. SCPs are JSON policies that specify the maximum permissions for an organization or organizational unit (OU). The SCP limits permissions for entities in member accounts, including each AWS account root user. An explicit deny in any of these policies overrides the allow.

**Access control list (ACL)** - Access control lists (ACLs) are service policies that allow you to control which principals in another account can access a resource. ACLs cannot be used to control access for a principal within the same account. Amazon S3, AWS WAF, and Amazon VPC are examples of services that support ACLs.

**Permissions boundary** - AWS supports permissions boundaries for IAM entities (users or roles). **A permissions boundary is an advanced feature for using a managed policy to set the maximum permissions that an identity-based policy can grant to an IAM entity.** An entity's permissions boundary allows it to perform only the actions that are allowed by both its identity-based policies and its permissions boundaries.
