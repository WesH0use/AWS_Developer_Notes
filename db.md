## A diagnostic lab stores its data on DynamoDB. The lab wants to backup a particular DynamoDB table data on Amazon S3, so it can download the S3 backup locally for some operational use.

### How can I back up a DynamoDB table on an S3?

DynamoDB offers two built-in backup methods:

**1) On-demand: Create backups when you choose. <br>
2) Point-in-time recovery: Turn on automatic and continuous backups.**

Both of these methods are suitable for backing up your tables for disaster recovery purposes. 

### However, with these methods, you can't use the data for use cases involving data analysis or extract, transform, and load (ETL) jobs. The DynamoDB Export to S3 feature is the easiest way to create backups that you can download locally or use with another AWS service. To customize the process of creating backups, you can use use Amazon EMR, AWS Glue, or AWS Data Pipeline.


Use AWS Data Pipeline to export your table to an S3 bucket in the account of your choice and download locally - This is the easiest method. This method is used when you want to make a one-time backup using the lowest amount of AWS resources possible. Data Pipeline uses Amazon EMR to create the backup, and the scripting is done for you. You don't have to learn Apache Hive or Apache Spark to accomplish this task.

Use Hive with Amazon EMR to export your data to an S3 bucket and download locally - Use Hive to export data to an S3 bucket. Or, use the open-source emr-dynamodb-connector to manage your own custom backup method in Spark or Hive. These methods are the best practice to use if you're an active Amazon EMR user and are comfortable with Hive or Spark. These methods offer more control than the Data Pipeline method.

Use AWS Glue to copy your table to Amazon S3 and download locally - Use AWS Glue to copy your table to Amazon S3. This is the best practice to use if you want automated, continuous backups that you can also use in another service, such as Amazon Athena.

## The technology team at an investment bank uses DynamoDB to facilitate high-frequency trading where multiple trades can try and update an item at the same time. Which of the following actions would make sure that only the last updated value of any item is used in the application?

**DynamoDB supports eventually consistent and strongly consistent reads.**

**Eventually Consistent Reads**

When you read data from a DynamoDB table, the response might not reflect the results of a recently completed write operation. The response might include some stale data. If you repeat your read request after a short time, the response should return the latest data.

**Strongly Consistent Reads**

When you request a strongly consistent read, DynamoDB returns a response with the most up-to-date data, reflecting the updates from all prior write operations that were successful.

DynamoDB uses **eventually consistent reads by default**. **Read operations (such as GetItem, Query, and Scan) provide a ConsistentRead parameter. If you set this parameter to true, DynamoDB uses strongly consistent reads during the operation**. **As per the given use-case, to make sure that only the last updated value of any item is used in the application, you should use strongly consistent reads by setting ConsistentRead = true for GetItem operation.**

## A startup has been experimenting with DynamoDB in its new test environment. The development team has discovered that some of the write operations have been overwriting existing items that have the specified primary key. This has messed up their data, leading to data discrepancies. Which DynamoDB write option should be selected to prevent this kind of overwriting?

**Conditional writes** - DynamoDB optionally supports conditional writes for write operations (PutItem, UpdateItem, DeleteItem). A conditional write succeeds **only if the item attributes meet one or more expected conditions**. **Otherwise, it returns an error**.

**For example, you might want a PutItem operation to succeed only if there is not already an item with the same primary key.** Or you could prevent an UpdateItem operation from modifying an item if one of its attributes has a certain value. Conditional writes are helpful in cases where multiple users attempt to modify the same item. This is the right choice for the current scenario.

## A development team is working on an AWS Lambda function that accesses DynamoDB. The Lambda function must do an upsert, that is, it must retrieve an item and update some of its attributes or create the item if it does not exist. Which of the following represents the solution with MINIMUM IAM permissions that can be used for the Lambda function to achieve this functionality?

*dynamodb:UpdateItem, dynamodb:GetItem*

With Amazon DynamoDB transactions, you can group multiple actions together and submit them as a single all-or-nothing TransactWriteItems or TransactGetItems operation.

You can use AWS Identity and Access Management (IAM) to restrict the actions that transactional operations can perform in Amazon DynamoDB. Permissions for Put, Update, Delete, and Get actions are governed by the permissions used for the underlying PutItem, UpdateItem, DeleteItem, and GetItem operations. For the ConditionCheck action, you can use the dynamodb:ConditionCheck permission in IAM policies.

UpdateItem action of DynamoDB APIs, edits an existing item's attributes or adds a new item to the table if it does not already exist. You can put, delete, or add attribute values. You can also perform a conditional update on an existing item (insert a new attribute name-value pair if it doesn't exist, or replace an existing name-value pair if it has certain expected attribute values).

There is no need to inlcude the dynamodb:PutItem action for the given use-case.

So, the IAM policy must include permissions to get and update the item in the DynamoDB table.

## A development team is building a game where players can buy items with virtual coins. For every virtual coin bought by a user, both the players table as well as the items table in DynamodDB need to be updated simultaneously using an all-or-nothing operation. As a developer associate, how will you implement this functionality?

Use _TransactWriteItems API_ of DynamoDB Transactions

**With Amazon DynamoDB transactions, you can group multiple actions together and submit them as a single all-or-nothing TransactWriteItems or TransactGetItems operation.**

TransactWriteItems is a synchronous and idempotent write operation that groups up to 25 write actions in a single all-or-nothing operation. These actions can target up to 25 distinct items in one or more DynamoDB tables within the same AWS account and in the same Region. The aggregate size of the items in the transaction cannot exceed 4 MB. The actions are completed atomically so that either all of them succeed or none of them succeeds.

You can optionally include a client token when you make a TransactWriteItems call to ensure that the request is idempotent. Making your transactions idempotent helps prevent application errors if the same operation is submitted multiple times due to a connection time-out or other connectivity issue.


## A social gaming application supports the transfer of gift vouchers between users. When a user hits a certain milestone on the leaderboard, they earn a gift voucher that can be redeemed or transferred to another user. The development team wants to ensure that this transfer is captured in the database such that the records for both users are either written successfully with the new gift vouchers or the status quo is maintained. Which of the following solutions represent the best-fit options to meet the requirements for the given use-case? 

**Use the DynamoDB transactional read and write APIs on the table items as a single, all-or-nothing operation**

You can use DynamoDB transactions to make coordinated all-or-nothing changes to multiple items both within and across tables. Transactions provide atomicity, consistency, isolation, and durability (ACID) in DynamoDB, helping you to maintain data correctness in your applications.

**Complete both operations on RDS MySQL in a single transaction block**

Amazon Relational Database Service (Amazon RDS) makes it easy to set up, operate, and scale a relational database with support for transactions in the cloud. A relational database is a collection of data items with pre-defined relationships between them. RDS supports the most demanding database applications. You can choose between two SSD-backed storage options: one optimized for high-performance Online Transaction Processing (OLTP) applications, and the other for cost-effective general-purpose use.

## Your web application reads and writes data to your DynamoDB table. The table is provisioned with 400 Write Capacity Units (WCU’s) shared across 4 partitions. One of the partitions receives 250 WCU/second while others receive much less. You receive the error 'ProvisionedThroughputExceededException'. What is the likely cause of this error?

**_You have a hot partition_**

It's not always possible to distribute read and write activity evenly. When data access is imbalanced, a "hot" partition can receive a higher volume of read and write traffic compared to other partitions. To better accommodate uneven access patterns, DynamoDB adaptive capacity enables your application to continue reading and writing to hot partitions without being throttled, provided that traffic does not exceed your table’s total provisioned capacity or the partition maximum capacity.

_ProvisionedThroughputExceededException_ explained: When you create a new provisioned table in Amazon DynamoDB, you must specify its provisioned throughput capacity. This is the amount of read and write activity that the table can support. DynamoDB uses this information to reserve sufficient system resources to meet your throughput requirements.

## A company uses Amazon RDS as its database. For improved user experience, it has been decided that a highly reliable fully-managed caching layer has to be configured in front of RDS. Which of the following is the right choice, keeping in mind that cache content regeneration is a costly activity?

**Implement Amazon ElastiCache Redis in Cluster-Mode** - One can leverage ElastiCache for Redis with cluster mode enabled to enhance reliability and availability with little change to your existing workload. Cluster mode comes with the primary benefit of horizontal scaling of your Redis cluster, with almost zero impact on the performance of the cluster.

When building production workloads, you should consider using a configuration with replication, unless you can easily recreate your data. Enabling Cluster-Mode provides a number of additional benefits in scaling your cluster. In short, it allows you to scale in or out the number of shards (horizontal scaling) versus scaling up or down the node type (vertical scaling). This means that Cluster-Mode can scale to very large amounts of storage (potentially 100s of terabytes) across up to 90 shards, whereas a single node can only store as much data in memory as the instance type has capacity for.

## Your company has a three-year contract with a healthcare provider. The contract states that monthly database backups must be retained for the duration of the contract for compliance purposes. Currently, the limit on backup retention for automated backups, on Amazon Relational Database Service (RDS), does not meet your requirements.Which of the following solutions can help you meet your requirements?

**Create a cron event in CloudWatch, which triggers an AWS Lambda function that triggers the database snapshot** - There are multiple ways to run periodic jobs in AWS. CloudWatch Events with Lambda is the simplest of all solutions. To do this, create a CloudWatch Rule and select “Schedule” as the Event Source. You can either use a cron expression or provide a fixed rate (such as every 5 minutes). Next, select “Lambda Function” as the Target. Your Lambda will have the necessary code for snapshot functionality. **You can enable automatic backups but as of 2020, the retention period is 0 to 35 days**.

## Your company uses an Application Load Balancer to route incoming end-user traffic to applications hosted on Amazon EC2 instances. The applications capture incoming request information and store it in the Amazon Relational Database Service (RDS) running on Microsoft SQL Server DB engines.As part of new compliance rules, you need to capture the client's IP address. How will you achieve this?

**Use the header X-Forwarded-For** - The X-Forwarded-For request header helps you identify the IP address of a client when you use an HTTP or HTTPS load balancer. Because load balancers intercept traffic between clients and servers, your server access logs contain only the IP address of the load balancer. To see the IP address of the client, use the X-Forwarded-For request header. Elastic Load Balancing stores the IP address of the client in the X-Forwarded-For request header and passes the header to your server.

## You have migrated an on-premise SQL Server database to an Amazon Relational Database Service (RDS) database attached to a VPC inside a private subnet. Also, the related Java application, hosted on-premise, has been moved to an Amazon Lambda function. Which of the following should you implement to connect AWS Lambda function to its RDS instance?

**Configure Lambda to connect to VPC with private subnet and Security Group needed to access RDS** - You can configure a Lambda function to connect to private subnets in a virtual private cloud (VPC) in your account. Use Amazon Virtual Private Cloud (Amazon VPC) to create a private network for resources such as databases, cache instances, or internal services. Connect your lambda function to the VPC to access private resources during execution. When you connect a function to a VPC, Lambda creates an elastic network interface for each combination of the security group and subnet in your function's VPC configuration. **This is the right way of giving RDS access to Lambda**.

## You are a developer working with the AWS CLI to create Lambda functions that contain environment variables. Your functions will require over 50 environment variables consisting of sensitive information of database table names What is the total set size/number of environment variables you can create for AWS Lambda?

**The total size of all _environment variables shouldn't exceed 4 KB_. There is no limit on the number of variables.** An environment variable is a pair of strings that are stored in a function's version-specific configuration. The Lambda runtime makes environment variables available to your code and sets additional environment variables that contain information about the function and invocation request. The total size of all environment variables doesn't exceed 4 KB. There is no limit defined on the number of variables that can be used.

## A cybersecurity company is running a serverless backend with several compute-heavy workflows running on Lambda functions. The development team has noticed a performance lag after analyzing the performance metrics for the Lambda functions. As a Developer Associate, which of the following options would you suggest as the BEST solution to address the compute-heavy workloads?

**Increase the amount of memory available to the Lambda functions**

AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume.

_In the AWS Lambda resource model, you choose the amount of memory you want for your function which allocates proportional CPU power and other resources_. This means you will have access to more compute power when you choose one of the new larger settings. You can set your memory in 64MB increments from 128MB to 3008MB. You access these settings when you create a function or update its configuration. The settings are available using the AWS Management Console, AWS CLI, or SDKs.

## The development team at a company wants to encrypt a 111 GB object using AWS KMS. Which of the following represents the best solution?

**Make a _GenerateDataKey_ API call that returns a plaintext key and an encrypted copy of a data key.** Use a plaintext key to encrypt the data - **GenerateDataKey API, generates a unique symmetric data key for client-side encryption**. This operation returns a plaintext copy of the data key and a copy that is encrypted under a customer master key (CMK) that you specify. You can use the plaintext key to encrypt your data outside of AWS KMS and store the encrypted data key with the encrypted data.

GenerateDataKey returns a unique data key for each request. The bytes in the plaintext key are not related to the caller or the CMK.

To encrypt data outside of AWS KMS:

Use the GenerateDataKey operation to get a data key.

Use the plaintext data key (in the Plaintext field of the response) to encrypt your data outside of AWS KMS. Then erase the plaintext data key from memory.

Store the encrypted data key (in the CiphertextBlob field of the response) with the encrypted data.

To decrypt data outside of AWS KMS:

Use the Decrypt operation to decrypt the encrypted data key. The operation returns a plaintext copy of the data key.

Use the plaintext data key to decrypt data outside of AWS KMS, then erase the plaintext data key from memory.
