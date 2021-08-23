# Refactoring in AWS

## Lambda 

### A development team wants to deploy an AWS Lambda function that requires significant CPU utilization. As a Developer Associate, which of the following would you suggest for reducing the average runtime of the function?

You deploy the function with its memory allocation set to the maximum amount - **Lambda allocates CPU power in proportion to the amount of memory configured.** Memory is the amount of memory available to your Lambda function at runtime. You can increase or decrease the memory and CPU power allocated to your function using the Memory (MB) setting. To configure the memory for your function, set a value between 128 MB and 10,240 MB in 1-MB increments. At 1,769 MB, a function has the equivalent of one vCPU (one vCPU-second of credits per second).

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
