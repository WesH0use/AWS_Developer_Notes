# Refactoring in AWS

## A data analytics company is processing real-time Internet-of-Things (IoT) data via Kinesis Producer Library (KPL) and sending the data to a Kinesis Data Streams driven application. The application has halted data processing because of a ProvisionedThroughputExceeded exception. Which of the following actions would help in addressing this issue? (Select two)

Amazon Kinesis Data Streams enables you to build custom applications that process or analyze streaming data for specialized needs. You can continuously add various types of data such as clickstreams, application logs, and social media to an Amazon Kinesis data stream from hundreds of thousands of sources.

How Kinesis Data Streams Work
![image](https://user-images.githubusercontent.com/44325167/131129164-88f63149-61d2-49b6-b309-3623c4aaeb56.png)

**The capacity limits of an Amazon Kinesis data stream are defined by the number of shards within the data stream**. The limits can be exceeded by either data throughput or the number of PUT records. **While the capacity limits are exceeded, the put data call will be rejected with a ProvisionedThroughputExceeded exception**.

If this is due to a temporary rise of the data stream’s input data rate, retry (with exponential backoff) by the data producer will eventually lead to the completion of the requests.

If this is due to a sustained rise of the data stream’s input data rate, you should increase the number of shards within your data stream to provide enough capacity for the put data calls to consistently succeed.


## EC2 Autoscaling 

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

## VPC 

### A CRM application is hosted on Amazon EC2 instances with the database tier using DynamoDB. The customers have raised privacy and security concerns regarding sending and receiving data across the public internet. As a developer associate, which of the following would you suggest as an optimal solution for providing communication between EC2 instances and DynamoDB without using the public internet?

**Configure VPC endpoints for DynamoDB that will provide required internal access without using public internet**

When you create a VPC endpoint for DynamoDB, any requests to a DynamoDB endpoint within the Region (for example, dynamodb.us-west-2.amazonaws.com) are routed to a private DynamoDB endpoint within the Amazon network. You don't need to modify your applications running on EC2 instances in your VPC. The endpoint name remains the same, but the route to DynamoDB stays entirely within the Amazon network, and does not access the public internet. You use endpoint policies to control access to DynamoDB. Traffic between your VPC and the AWS service does not leave the Amazon network.

Using Amazon VPC Endpoints to Access DynamoDB:

![image](https://user-images.githubusercontent.com/44325167/131130761-72f32c61-af3f-4bdf-b71c-12d6675f4a97.png)


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

