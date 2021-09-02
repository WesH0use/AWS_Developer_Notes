# Refactoring in AWS

# Websocket APIs

### A banking application needs to send real-time alerts and notifications based on any updates from the backend services. The company wants to avoid implementing complex polling mechanisms for these notifications. Which of the following types of APIs supported by the Amazon API Gateway is the right fit?

In a **WebSocket API**, the client and the server can both send messages to each other at any time. Backend servers can easily push data to connected users and devices, _avoiding the need to implement complex polling mechanisms_.

For example, you could build a serverless application using an API Gateway WebSocket API and AWS Lambda to send and receive messages to and from individual users or groups of users in a chat room. Or you could invoke backend services such as AWS Lambda, Amazon Kinesis, or an HTTP endpoint based on message content.

**You can use API Gateway WebSocket APIs to build secure, real-time communication applications without having to provision or manage any servers to manage connections or large-scale data exchanges**. Targeted use cases include real-time applications such as the following:<br>

Chat applications<br>
Real-time dashboards such as stock tickers<br>
Real-time alerts and notifications<br>

**API Gateway provides WebSocket API management functionality such as the following**:<br>

Monitoring and throttling of connections and messages<br>
Using AWS X-Ray to trace messages as they travel through the APIs to backend services<br>
Easy integration with HTTP/HTTPS endpoints<br>

## A data analytics company is processing real-time Internet-of-Things (IoT) data via Kinesis Producer Library (KPL) and sending the data to a Kinesis Data Streams driven application. The application has halted data processing because of a ProvisionedThroughputExceeded exception. Which of the following actions would help in addressing this issue? (Select two)

Amazon Kinesis Data Streams enables you to build custom applications that process or analyze streaming data for specialized needs. You can continuously add various types of data such as clickstreams, application logs, and social media to an Amazon Kinesis data stream from hundreds of thousands of sources.

How Kinesis Data Streams Work
![image](https://user-images.githubusercontent.com/44325167/131129164-88f63149-61d2-49b6-b309-3623c4aaeb56.png)

**The capacity limits of an Amazon Kinesis data stream are defined by the number of shards within the data stream**. The limits can be exceeded by either data throughput or the number of PUT records. **While the capacity limits are exceeded, the put data call will be rejected with a ProvisionedThroughputExceeded exception**.

If this is due to a temporary rise of the data stream’s input data rate, retry (with exponential backoff) by the data producer will eventually lead to the completion of the requests.

If this is due to a sustained rise of the data stream’s input data rate, you should increase the number of shards within your data stream to provide enough capacity for the put data calls to consistently succeed.


# RDS 

## A mobile gaming company is experiencing heavy read traffic to its Amazon Relational Database Service (RDS) database that retrieves player’s scores and stats. The company is using RDS database instance type db.m5.12xlarge, which is not cost-effective for their budget. They would like to implement a strategy to deal with the high volume of read traffic, reduce latency, and also downsize the instance size to cut costs. As a Developer, which of the following solutions do you recommend?

**Setup ElastiCache in front of RDS**

Amazon ElastiCache is an ideal front-end for data stores such as Amazon RDS, providing a high-performance middle tier for applications with extremely high request rates and/or low latency requirements. The best part of caching is that it’s minimally invasive to implement and by doing so, your application performance regarding both scale and speed is dramatically improved.


# EC2 

## As a developer, you are looking at creating a custom configuration for Amazon EC2 instances running in an Auto Scaling group. The solution should allow the group to auto-scale based on the metric of 'average RAM usage' for your Amazon EC2 instances. Which option provides the best solution?

**Create a custom metric in CloudWatch and make your instances send data to it using PutMetricData**. Then, create an alarm based on this metric - You can create a custom CloudWatch metric for your EC2 Linux instance statistics by creating a script through the AWS Command Line Interface (AWS CLI). Then, you can monitor that metric by pushing it to CloudWatch.

You can publish your own metrics to CloudWatch using the AWS CLI or an API. Metrics produced by AWS services are standard resolution by default. When you publish a custom metric, you can define it as either standard resolution or high resolution. When you publish a high-resolution metric, CloudWatch stores it with a resolution of 1 second, and you can read and retrieve it with a period of 1 second, 5 seconds, 10 seconds, 30 seconds, or any multiple of 60 seconds.

High-resolution metrics can give you more immediate insight into your application's sub-minute activity. But, every PutMetricData call for a custom metric is charged, so calling PutMetricData more often on a high-resolution metric can lead to higher charges.

With **target tracking scaling policies**, you select a scaling metric and set a target value. Amazon EC2 Auto Scaling creates and manages the CloudWatch alarms that trigger the scaling policy and calculates the scaling adjustment based on the metric and the target value.

It is important to note that a target tracking scaling policy assumes that it should scale out your Auto Scaling group when the specified metric is above the target value. You cannot use a target tracking scaling policy to scale out your Auto Scaling group when the specified metric is below the target value.

For example, you can use target tracking scaling to:

**Configure a target tracking scaling policy to keep the average aggregate CPU utilization of your Auto Scaling group at 40 percent.**

**Configure a target tracking scaling policy to keep the request count per target of your Application Load Balancer target group at 1000 for your Auto Scaling group.**

The following predefined metrics are available:

_ASGAverageCPUUtilization_ — Average CPU utilization of the Auto Scaling group.

_ASGAverageNetworkIn_ —Average number of bytes received on all network interfaces by the Auto Scaling group.

_ASGAverageNetworkOut_ —Average number of bytes sent out on all network interfaces by the Auto Scaling group.

_ALBRequestCountPerTarget_ —Number of requests completed per target in an Application Load Balancer target group.

## EC2 Instances 

**A new recruit is trying to configure what an Amazon EC2 should do when it interrupts a Spot Instance. What options are there for  interruption behavior?**

A Spot Instance is an unused EC2 instance that is available for less than the On-Demand price. Your Spot Instance runs whenever capacity is available and the maximum price per hour for your request exceeds the Spot price. Any instance present with unused capacity will be allocated.

You can specify that Amazon EC2 should do one of the following when it interrupts a Spot Instance:

**Stop** the Spot Instance

**Hibernate** the Spot Instance

**Terminate** the Spot Instance

**The default is to terminate Spot Instances when they are interrupted**.

## You are running a cloud file storage website with an Internet-facing Application Load Balancer, which routes requests from users over the internet to 10 registered Amazon EC2 instances. Users are complaining that your website always asks them to re-authenticate when they switch pages. You are puzzled because this behavior is not seen in your local machine or dev environment. What could be the reason?

**The Load Balancer does not have stickiness enabled** - Sticky sessions are a mechanism to route requests to the same target in a target group. This is useful for servers that maintain state information to provide a continuous experience to clients. To use sticky sessions, the clients must support cookies.

When a load balancer first receives a request from a client, it routes the request to a target, generates a cookie named AWSALB that encodes information about the selected target, encrypts the cookie, and includes the cookie in the response to the client. The client should include the cookie that it receives in subsequent requests to the load balancer. When the load balancer receives a request from a client that contains the cookie, if sticky sessions are enabled for the target group and the request goes to the same target group, the load balancer detects the cookie and routes the request to the same target.

## As a Senior Developer, you manage 10 Amazon EC2 instances that make read-heavy database requests to the Amazon RDS for PostgreSQL. You need to make this architecture resilient for disaster recovery. Which of the following features will help you prepare for database disaster recovery? 

**Use cross-Region Read Replicas**

In addition to using Read Replicas to reduce the load on your source DB instance, you can also use Read Replicas to implement a DR solution for your production DB environment. If the source DB instance fails, you can promote your Read Replica to a standalone source server. Read Replicas can also be created in a different Region than the source database. Using a cross-Region Read Replica can help ensure that you get back up and running if you experience a regional availability issue.

**Enable the automated backup feature of Amazon RDS in a multi-AZ deployment that creates backups in a single AWS Region**

Amazon RDS provides high availability and failover support for DB instances using Multi-AZ deployments. Amazon RDS uses several different technologies to provide failover support. _Multi-AZ deployments for MariaDB, MySQL, Oracle, and PostgreSQL DB instances use Amazon's failover technology_.

The automated backup feature of Amazon RDS enables point-in-time recovery for your database instance. Amazon RDS will backup your database and transaction logs and store both for a user-specified retention period. If it’s a Multi-AZ configuration, backups occur on the standby to reduce I/O impact on the primary. Automated backups are limited to a single AWS Region while manual snapshots and Read Replicas are supported across multiple Regions.


## You have deployed a traditional 3-tier web application architecture with a Classic Load Balancer, an Auto Scaling group, and an Amazon Relational Database Service (RDS) database. Users are reporting that they have to re-authenticate into the website often. Which of the following represents a scalable solution to make the application tier stateless and outsource the session information?

**Add an ElastiCache Cluster** - To provide a shared data storage for sessions that can be accessed from any individual web server, you can abstract the HTTP sessions from the web servers themselves. A common solution for this is to leverage an ElastiCache service offering which is an In-Memory Key/Value store such as Redis and Memcached.

## VPC 

### A CRM application is hosted on Amazon EC2 instances with the database tier using DynamoDB. The customers have raised privacy and security concerns regarding sending and receiving data across the public internet. As a developer associate, which of the following would you suggest as an optimal solution for providing communication between EC2 instances and DynamoDB without using the public internet?

**Configure VPC endpoints for DynamoDB that will provide required internal access without using public internet**

When you create a VPC endpoint for DynamoDB, any requests to a DynamoDB endpoint within the Region (for example, dynamodb.us-west-2.amazonaws.com) are routed to a private DynamoDB endpoint within the Amazon network. You don't need to modify your applications running on EC2 instances in your VPC. The endpoint name remains the same, but the route to DynamoDB stays entirely within the Amazon network, and does not access the public internet. You use endpoint policies to control access to DynamoDB. Traffic between your VPC and the AWS service does not leave the Amazon network.

Using Amazon VPC Endpoints to Access DynamoDB:

![image](https://user-images.githubusercontent.com/44325167/131130761-72f32c61-af3f-4bdf-b71c-12d6675f4a97.png)

# Elastic Beanstalk 

## You company runs business logic on smaller software components that perform various functions. Some functions process information in a few seconds while others seem to take a long time to complete. Your manager asked you to decouple components that take a long time to ensure software applications stay responsive under load. You decide to configure Amazon Simple Queue Service (SQS) to work with your Elastic Beanstalk configuration. Which of the following Elastic Beanstalk environment should you choose to meet this requirement?

With Elastic Beanstalk, you can quickly deploy and manage applications in the AWS Cloud without having to learn about the infrastructure that runs those applications. Elastic Beanstalk reduces management complexity without restricting choice or control. You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring.

**Dedicated worker environment** - If your AWS Elastic Beanstalk application performs operations or workflows that take a long time to complete, you can offload those tasks to a dedicated worker environment. Decoupling your web application front end from a process that performs blocking operations is a common way to ensure that your application stays responsive under load.

A long-running task is anything that substantially increases the time it takes to complete a request, such as processing images or videos, sending emails, or generating a ZIP archive. These operations can take only a second or two to complete, but a delay of a few seconds is a lot for a web request that would otherwise complete in less than 500 ms.

# S3

## Your team lead has requested code review of your code for Lambda functions. Your code is written in Python and makes use of the Amazon Simple Storage Service (S3) to upload logs to an S3 bucket. After the review, your team lead has recommended reuse of execution context to improve the Lambda performance. Which of the following actions will help you implement the recommendation?

**Move the Amazon S3 client initialization, out of your function handler** - AWS best practices for Lambda suggest taking advantage of execution context reuse to improve the performance of your functions. Initialize SDK clients and database connections outside of the function handler, and cache static assets locally in the /tmp directory. Subsequent invocations processed by the same instance of your function can reuse these resources. This saves execution time and cost. To avoid potential data leaks across invocations, don’t use the execution context to store user data, events, or other information with security implications.

## A company has hosted its website on an Amazon S3 bucket and have used another Amazon S3 bucket for storing the rest of the assets like images, fonts, etc. Which technique/mechanism will help the hosted website access its assets without access/permission issues?

S3 Cross-Origin Resource Sharing (CORS) - Cross-origin resource sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain. With CORS support, you can build rich client-side web applications with Amazon S3 and selectively allow cross-origin access to your Amazon S3 resources.

To configure your bucket to allow cross-origin requests, you create a CORS configuration. The CORS configuration is a document with rules that identify the origins that you will allow to access your bucket, the operations (HTTP methods) that will support each origin, and other operation-specific information. You can add up to 100 rules to the configuration. You can add the CORS configuration as the cors subresource to the bucket.

If you are configuring CORS in the S3 console, you must use JSON to create a CORS configuration. The new S3 console only supports JSON CORS configurations.

## Your company hosts a static website on Amazon Simple Storage Service (S3) written in HTML5. The website targets aviation enthusiasts and it has grown a worldwide audience with hundreds of thousands of visitors accessing the website now on a monthly basis. While users in the United States have a great user experience, users from other parts of the world are experiencing slow responses and lag. Which service can mitigate this issue?

**Use Amazon CloudFront**

Storing your static content with S3 provides a lot of advantages. But to help optimize your application’s performance and security while effectively managing cost, AWS recommends that you also set up Amazon CloudFront to work with your S3 bucket to serve and protect the content. **CloudFront is a content delivery network (CDN) service that delivers static and dynamic web content, video streams, and APIs around the world, securely and at scale. By design, delivering data out of CloudFront can be more cost-effective than delivering it from S3 directly to your users**.

_By caching your content in Edge Locations, CloudFront reduces the load on your S3 bucket and helps ensure a faster response for your users when they request content_. In addition, data transfer out for content by using CloudFront is often more cost-effective than serving files directly from S3, and there is no data transfer fee from S3 to CloudFront.

A security feature of CloudFront is Origin Access Identity (OAI), which restricts access to an S3 bucket and its content to only CloudFront and operations it performs.

## Lambda 

### A development team wants to deploy an AWS Lambda function that requires significant CPU utilization. As a Developer Associate, which of the following would you suggest for reducing the average runtime of the function?

You deploy the function with its memory allocation set to the maximum amount - **Lambda allocates CPU power in proportion to the amount of memory configured.** Memory is the amount of memory available to your Lambda function at runtime. You can increase or decrease the memory and CPU power allocated to your function using the Memory (MB) setting. To configure the memory for your function, set a value between 128 MB and 10,240 MB in 1-MB increments. At 1,769 MB, a function has the equivalent of one vCPU (one vCPU-second of credits per second).

### The development team at a retail company is gearing up for the upcoming Thanksgiving sale and wants to make sure that the application's serverless backend running via Lambda functions does not hit latency bottlenecks as a result of the traffic spike. As a Developer Associate, which of the following solutions would you recommend to address this use-case?

Configure Application Auto Scaling to manage Lambda provisioned concurrency on a schedule

Concurrency is the number of requests that a Lambda function is serving at any given time. If a Lambda function is invoked again while a request is still being processed, another instance is allocated, which increases the function's concurrency.

Due to a spike in traffic, when Lambda functions scale, this causes the portion of requests that are served by new instances to have higher latency than the rest. To enable your function to scale without fluctuations in latency, use provisioned concurrency. By allocating provisioned concurrency before an increase in invocations, you can ensure that all requests are served by initialized instances with very low latency.

You can configure Application Auto Scaling to manage provisioned concurrency on a schedule or based on utilization. Use scheduled scaling to increase provisioned concurrency in anticipation of peak traffic. To increase provisioned concurrency automatically as needed, use the Application Auto Scaling API to register a target and create a scaling policy.

## Kinesis Data Stream 

**Amazon Kinesis Data Streams is useful for rapidly moving data off data producers and then continuously processing the data, be it to transform the data before emitting to a data store, run real-time metrics and analytics, or derive more complex data streams for further processing.** Kinesis data streams can continuously capture gigabytes of data per second from hundreds of thousands of sources such as website clickstreams, database event streams, financial transactions, social media feeds, IT logs, and location-tracking events.

Kinesis Data Streams Overview:
![image](https://user-images.githubusercontent.com/44325167/130438804-46c39c47-78c6-46c6-b622-fddd3f2c2ecc.png)

##  AWS Serverless Application Repository (SAM)

The AWS Serverless Application Repository is **a managed repository for serverless applications**. It enables teams, organizations, and individual developers to **store** and s**hare reusable applications, and easily assemble and deploy serverless architectures** in powerful new ways. Using the Serverless Application Repository, **you don't need to clone, build, package, or publish source code to AWS before deploying it**. Instead, **you can use pre-built applications from the Serverless Application Repository in your serverless architectures, helping you and your teams reduce duplicated work, ensure organizational best practices, and get to market faster**. **Integration with AWS Identity and Access Management (IAM) provides resource-level control of each application**, enabling you to publicly share applications with everyone or privately share them with specific AWS accounts.

Each application is packaged with an AWS Serverless Application Model (SAM) template that defines the AWS resources used. Publicly shared applications also include a link to the application’s source code. There is no additional charge to use the Serverless Application Repository - you only pay for the AWS resources used in the applications you deploy.

## API Gateway

In API Gateway, an API's method request can take a payload in a different format from the corresponding integration request payload, as required in the backend. Similarly, vice versa is also possible. **API Gateway lets you use mapping templates to map the payload from a method request to the corresponding integration request and from an integration response to the corresponding method response**.

Suppose we have an API for managing fruit and vegetable inventory in the produce department of a supermarket. When a manager queries the backend for the current inventory, the server sends back the following response payload:

![Screen Shot 2021-08-23 at 2 15 22 PM](https://user-images.githubusercontent.com/44325167/130445296-3ac16240-9d23-4d39-a435-14a2696f22b2.png)

When the backend returns the query results shown above, the manager of the produce department might be interested in reading them, as follows:

![Screen Shot 2021-08-23 at 2 19 06 PM](https://user-images.githubusercontent.com/44325167/130445771-a670ec93-0bc0-4301-bcfd-3c0282fe079c.png)

**To enable this, we need to provide API Gateway with a mapping template** to translate the data from the backend format like so:

![Screen Shot 2021-08-23 at 2 19 40 PM](https://user-images.githubusercontent.com/44325167/130445834-9917ea46-4cdb-4676-a5cb-b8e78a187a7d.png)

## A developer is configuring an Amazon API Gateway as a front door to expose backend business logic. To keep the solution cost-effective, the developer has opted for HTTP APIs. Which of the following services are not available as an HTTP API via Amazon API Gateway?

AWS Identity and Access Management (IAM)<br>
AWS Lambda<br>
AWS Application Firewall (AWS WAF)<br>
AWS Cognito<br>

**AWS Web Application Firewall (AWS WAF)**

Amazon API Gateway is an AWS service for creating, publishing, maintaining, monitoring, and securing REST, HTTP, and WebSocket APIs at any scale.

API Gateway REST APIs: A collection of HTTP resources and methods that are integrated with backend HTTP endpoints, Lambda functions, or other AWS services. You can deploy this collection in one or more stages. Typically, API resources are organized in a resource tree according to the application logic. Each API resource can expose one or more API methods that have unique HTTP verbs supported by API Gateway.

API Gateway HTTP API: A collection of routes and methods that are integrated with backend HTTP endpoints or Lambda functions. You can deploy this collection in one or more stages. Each route can expose one or more API methods that have unique HTTP verbs supported by API Gateway.

AWS Lambda, AWS Identity and Access Management (IAM) and Amazon Cognito services are all available as HTTP APIs. AWS Web Application Firewall (AWS WAF) however, is only available in REST APIs.


## Dead letter queue (SQS)

**An application running on EC2 instances processes messages from an SQS queue. However, sometimes the messages are not processed and they end up in errors. These messages need to be isolated for further processing and troubleshooting. Which of the following options will help achieve this?**

**Implement a Dead-Letter Queue** - Amazon SQS supports dead-letter queues, which other queues (source queues) can target for messages that can't be processed (consumed) successfully. Dead-letter queues are useful for debugging your application or messaging system because they let you isolate problematic messages to determine why their processing doesn't succeed. Amazon SQS does not create the dead-letter queue automatically. You must first create the queue before using it as a dead-letter queue.

### When should I use a dead-letter queue?

**DO** use dead-letter queues with standard queues. You should always take advantage of dead-letter queues when your applications don’t depend on ordering. Dead-letter queues can help you troubleshoot incorrect message transmission operations.

**DO** use dead-letter queues to decrease the number of messages and to reduce the possibility of exposing your system to poison-pill messages (messages that can be received but can’t be processed).

**DON’T** use a dead-letter queue with standard queues when you want to be able to keep retrying the transmission of a message indefinitely. For example, don’t use a dead-letter queue if your program must wait for a dependent process to become active or available.

**DON'T** use a dead-letter queue with a FIFO queue if you don’t want to break the exact order of messages or operations. For example, don’t use a dead-letter queue with instructions in an Edit Decision List (EDL) for a video editing suite, where changing the order of edits changes the context of subsequent edits.


## Pre-signed URLS 

**After a code review, a developer has been asked to make his publicly accessible S3 buckets private, and enable access to objects with a time-bound constraint. Which of the following options will address the given use-case?**

**Share pre-signed URLs with resources that need access** - All objects by default are private, with the object owner having permission to access the objects. However, the object owner can optionally share objects with others by creating a pre-signed URL, using their own security credentials, to grant time-limited permission to download the objects. When you create a pre-signed URL for your object, you must provide your security credentials, specify a bucket name, an object key, specify the HTTP method (GET to download the object), and expiration date and time. The pre-signed URLs are valid only for the specified duration.

## COGNITO USER POOLS

**The app development team at a social gaming mobile app wants to simplify the user sign up process for the app. The team is looking for a fully managed scalable solution for user management in anticipation of the rapid growth that the app foresees. As a Developer Associate, which of the following solutions would you suggest so that it requires the LEAST amount of development effort?**

**Use Cognito User pools to facilitate sign up and user management for the mobile app**

Amazon Cognito provides authentication, authorization, and user management for your web and mobile apps. Your users can sign in directly with a user name and password, or through a third party such as Facebook, Amazon, Google or Apple.

A user pool is a user directory in Amazon Cognito. With a user pool, your users can sign in to your web or mobile app through Amazon Cognito, or federate through a third-party identity provider (IdP). Whether your users sign-in directly or through a third party, all members of the user pool have a directory profile that you can access through an SDK.

Cognito is fully managed by AWS and works out of the box so it meets the requirements for the given use-case.


### You have created a continuous delivery service model with automated steps using AWS CodePipeline. Your pipeline uses your code, maintained in a CodeCommit repository, AWS CodeBuild, and AWS Elastic Beanstalk to automatically deploy your code every time there is a code change. However, the deployment part to Elastic Beanstalk is taking a very long time due to resolving dependencies on all of your 100 target EC2 instances. Which of the following actions should you take to improve performance with limited code changes?

**"Bundle the dependencies in the source code during the last stage of CodeBuild"**

AWS CodeBuild is a fully managed build service. There are no servers to provision and scale, or software to install, configure, and operate.

A typical application build process includes phases like preparing the environment, updating the configuration, downloading dependencies, running unit tests, and finally, packaging the built artifact.

Downloading dependencies is a critical phase in the build process. These dependent files can range in size from a few KBs to multiple MBs. **Because most of the dependent files do not change frequently between builds, you can noticeably reduce your build time by caching dependencies.**

This will allow the code bundle to be deployed to Elastic Beanstalk to have both the dependencies and the code, hence speeding up the deployment time to Elastic Beanstalk.

