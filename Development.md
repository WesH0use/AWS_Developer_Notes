# Development with AWS Services

## [EC2](https://github.com/WesH0use/AWS_Developer_Notes/blob/main/EC2_Development.md)


## Load Balancers

<u>A load balancer accepts incoming traffic from clients and routes requests to its registered targets (such as EC2 instances) in one or more Availability Zones</u>. The load balancer also monitors the health of its registered targets and ensures that it routes traffic only to healthy targets. **When the load balancer detects an unhealthy target, it stops routing traffic to that target**. It then resumes routing traffic to that target when it detects that the target is healthy again.

Elastic Load Balancing supports three types of load balancers:
1) Application Load Balancers
2) Network Load Balancers
3) Classic Load Balancers

**Load balancers separate public traffic from private traffic** - The nodes of an internet-facing load balancer have public IP addresses. Load balancers route requests to your targets using private IP addresses. Therefore, your targets do not need public IP addresses to receive requests from users over the internet.

**Load balancers build a highly available system**- Elastic Load Balancing provides fault tolerance for your applications by automatically balancing traffic across targets – Amazon EC2 instances, containers, IP addresses, and Lambda functions – in multiple Availability Zones while ensuring only healthy targets receive traffic.

A load balancer accepts incoming traffic from clients and routes requests to its registered targets (such as EC2 instances) in one or more Availability Zones.

The nodes for a load balancer distribute requests from clients to registered targets. When cross-zone load balancing is enabled, each load balancer node distributes traffic across the registered targets in all enabled Availability Zones. When cross-zone load balancing is disabled, each load balancer node distributes traffic only across the registered targets in its Availability Zone. With Application Load Balancers, cross-zone load balancing is always enabled.

## X-Ray

AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture. With X-Ray, you can understand how your application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors. X-Ray provides an end-to-end view of requests as they travel through your application, and shows a map of your application’s underlying components.

You can use X-Ray to collect data across AWS Accounts. The X-Ray agent can assume a role to publish data into an account different from the one in which it is running. This enables you to publish data from various components of your application into a central account.

## AWS Cloud Development Kit (CDK)

The AWS Cloud Development Kit (AWS CDK) is an open-source software development framework to define your cloud application resources using familiar programming languages.

Provisioning cloud applications can be a challenging process that requires you to perform manual actions, write custom scripts, maintain templates, or learn domain-specific languages. AWS CDK uses the familiarity and expressive power of programming languages such as JavaScript/TypeScript, Python, Java, and .NET for modeling your applications. It provides you with high-level components called constructs that preconfigure cloud resources with proven defaults, so you can build cloud applications without needing to be an expert. **AWS CDK provisions your resources in a safe, repeatable manner through AWS CloudFormation.** It also enables you to compose and share your own custom constructs that incorporate your organization's requirements, helping you start new projects faster.

# Billing and Cost Management 

You need to activate IAM user access to the Billing and Cost Management console for all the users who need access - **By default, IAM users do not have access to the AWS Billing and Cost Management console. You or your account administrator must grant users access**. You can do this by activating IAM user access to the Billing and Cost Management console and attaching an IAM policy to your users. Then, you need to activate IAM user access for IAM policies to take effect. You only need to activate IAM user access once.

# Elastic Beanstalk 

When processing a batch, Elastic Beanstalk detaches all instances in the batch from the load balancer, deploys the new application version, and then reattaches the instances. If you enable connection draining, Elastic Beanstalk drains existing connections from the Amazon EC2 instances in each batch before beginning the deployment.

**If a deployment fails after one or more batches completed successfully, the completed batches run the new version of your application while any pending batches continue to run the old version.** You can identify the version running on the instances in your environment on the health page in the console. This page displays the deployment ID of the most recent deployment that was executed on each instance in your environment. **If you terminate instances from the failed deployment, Elastic Beanstalk replaces them with instances running the application version from the most recent successful deployment.**

When creating configuration files for AWS Elastic Beanstalk which naming convention should you follow?

**.ebextensions/<my_settings>.config**

.ebextensions/<mysettings>.config : You can add AWS Elastic Beanstalk configuration files (.ebextensions) to your web application's source code to configure your environment and customize the AWS resources that it contains. Configuration files are YAML or JSON formatted documents with a .config file extension that you place in a folder named .ebextensions and deploy in your application source bundle.


## Policy Types 

**AWS Organizations Service Control Policy (SCP)**– Use an AWS Organizations Service Control Policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU). SCPs limit permissions that identity-based policies or resource-based policies grant to entities (users or roles) within the account, but do not grant permissions.

**Permissions boundary** - Permissions boundary is a managed policy that is used for an IAM entity (user or role). The policy defines the maximum permissions that the identity-based policies can grant to an entity, but does not grant permissions.

## Instance & Host Types

**Dedicated Instances** - Dedicated Instances are Amazon EC2 instances that run in a virtual private cloud (VPC) on hardware that's dedicated to a single customer. Dedicated Instances that belong to different AWS accounts are physically isolated at a hardware level, even if those accounts are linked to a single-payer account. However, Dedicated Instances may share hardware with other instances from the same AWS account that are not Dedicated Instances. A Dedicated Host is also a physical server that's dedicated for your use. With a Dedicated Host, you have visibility and control over how instances are placed on the server.

**Spot Instances** - A Spot Instance is an unused EC2 instance that is available for less than the On-Demand price. Your Spot Instance runs whenever capacity is available and the maximum price per hour for your request exceeds the Spot price. Any instance present with unused capacity will be allocated. Even though this is cost-effective, it does not fulfill the single-tenant hardware requirement of the client and hence is not the correct option.

**Dedicated Hosts** - An Amazon EC2 Dedicated Host is a physical server with EC2 instance capacity fully dedicated to your use. Dedicated Hosts allow you to use your existing software licenses on EC2 instances. With a Dedicated Host, you have visibility and control over how instances are placed on the server. This option is costlier than the Dedicated Instance.

**On-Demand Instances** - With On-Demand Instances, you pay for compute capacity by the second with no long-term commitments. You have full control over its lifecycle—you decide when to launch, stop, hibernate, start, reboot, or terminate it. Hardware isolation is not possible and on-demand has one of the costliest instance charges.

# Security Groups 

Security Groups are **stateful**, **so allowing inbound traffic to the necessary ports enables the connection**. 
Network ACLs are **stateless, so you must allow both inbound and outbound traffic 
**
To enable the connection to a service running on an instance, the associated network ACL must allow both inbound traffic on the port that the service is listening on as well as allow outbound traffic from ephemeral ports. When a client connects to a server, a random port from the ephemeral port range (1024-65535) becomes the client's source port.

The designated ephemeral port then becomes the destination port for return traffic from the service, so outbound traffic from the ephemeral port must be allowed in the network ACL.

By default, network ACLs allow all inbound and outbound traffic. If your network ACL is more restrictive, then you need to explicitly allow traffic from the ephemeral port range.

If you accept traffic from the internet, then you also must establish a route through an internet gateway. If you accept traffic over VPN or AWS Direct Connect, then you must establish a route through a virtual private gateway.

# Kinesis Data Streams

Amazon Kinesis Data Streams is useful for rapidly moving data off data producers and then continuously processing the data, be it to transform the data before emitting to a data store, run real-time metrics and analytics, or derive more complex data streams for further processing. Kinesis data streams can continuously capture gigabytes of data per second from hundreds of thousands of sources such as website clickstreams, database event streams, financial transactions, social media feeds, IT logs, and location-tracking events.

## EFS Volume 

EFS volumes provide a simple, scalable, and persistent file storage for use with your Amazon ECS tasks. With Amazon EFS, storage capacity is elastic, growing and shrinking automatically as you add and remove files. Your applications can have the storage they need, when they need it. Amazon EFS volumes are supported for tasks hosted on Fargate or Amazon EC2 instances.

You can use Amazon EFS file systems with Amazon ECS to export file system data across your fleet of container instances. That way, your tasks have access to the same persistent storage, no matter the instance on which they land. However, you must configure your container instance AMI to mount the Amazon EFS file system before the Docker daemon starts. Also, your task definitions must reference volume mounts on the container instance to use the file system.

## CNAME Records

A CNAME record maps DNS queries for the name of the current record, such as acme.example.com, to another domain (example.com or example.net) or subdomain (acme.example.com or zenith.example.org).

CNAME records can be used to map one domain name to another. Although you should keep in mind that the DNS protocol does not allow you to create a CNAME record for the top node of a DNS namespace, also known as the zone apex. For example, if you register the DNS name example.com, the zone apex is example.com. You cannot create a CNAME record for example.com, but you can create CNAME records for www.example.com, newproduct.example.com, and so on.

## Alias Records

Create an Alias Record - Alias records let you route traffic to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets. They also let you route traffic from one record in a hosted zone to another record. 3rd party websites do not qualify for these as we have no control over those. 'Alias record' cannot be used to map one domain name to another.

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
