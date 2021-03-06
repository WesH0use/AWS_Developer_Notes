## SQS 

### The development team at an analytics company is using SQS queues for decoupling the various components of application architecture. As the consumers need additional time to process SQS messages, the development team wants to postpone the delivery of new messages to the queue for a few seconds. As a Developer Associate, which of the following solutions would you recommend to the development team?

**Use delay queues to postpone the delivery of new messages to the queue for a few seconds**

Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications. SQS offers two types of message queues. Standard queues offer maximum throughput, best-effort ordering, and at-least-once delivery. SQS FIFO queues are designed to guarantee that messages are processed exactly once, in the exact order that they are sent.

Delay queues let you postpone the delivery of new messages to a queue for several seconds, for example, when your consumer application needs additional time to process messages. If you create a delay queue, any messages that you send to the queue remain invisible to consumers for the duration of the delay period. The default (minimum) delay for a queue is 0 seconds. The maximum is 15 minutes.

## Delay Queues VS Visitbility Timeouts

Delay queues are similar to visibility timeouts because both features make messages unavailable to consumers for a specific period of time. The difference between the two is that, for delay queues, a message is hidden when it is first added to queue, whereas for visibility timeouts a message is hidden only after it is consumed from the queue. The following diagram illustrates the relationship between delay queues and visibility timeouts.

**"Visibility timeout is the length of time that a message will be hidden on the queue after a consumer has grabbed it. If the consumer doesn't come back and delete the message within that time it will become visible again and another consumer can pick it up and try processing it. This protects against failure of individual consumers. A delay setting on a queue or a message timer on an individual message applies when messages are first added to the queue; visibility timeouts apply whenever a consumer grabs the message for processing."**

![image](https://user-images.githubusercontent.com/44325167/130941435-59e0d8fc-8d8e-48eb-aad6-89258d80bb39.png)


## API Calls

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

## Practice Questions 

# Amazon Simple Queue Service (SQS) has a set of APIs for various actions supported by the service. As a developer associate, which of the following would you identify as correct regarding the CreateQueue API? (Select two)

Explanation
Correct options:

**You can't change the queue type after you create it** - You can't change the queue type after you create it and you can't convert an existing standard queue into a FIFO queue. You must either create a new FIFO queue for your application or delete your existing standard queue and recreate it as a FIFO queue.

**The visibility timeout value for the queue is in seconds, which defaults to 30 seconds** - The visibility timeout for the queue is in seconds. Valid values are: An integer from 0 to 43,200 (12 hours), the Default value is 30.

Incorrect options:

The dead-letter queue of a FIFO queue must also be a FIFO queue. Whereas, the dead-letter queue of a standard queue can be a standard queue or a FIFO queue - The dead-letter queue of a FIFO queue must also be a FIFO queue. Similarly, the dead-letter queue of a standard queue must also be a standard queue.

The length of time, in seconds, for which the delivery of all messages in the queue is delayed is configured using MessageRetentionPeriod attribute - The length of time, in seconds, for which the delivery of all messages in the queue is delayed is configured using DelaySeconds attribute. MessageRetentionPeriod attribute controls the length of time, in seconds, for which Amazon SQS retains a message.

Queue tags are case insensitive. A new tag with a key identical to that of an existing tag overwrites the existing tag - Queue tags are case-sensitive. A new tag with a key identical to that of an existing tag overwrites the existing tag. To be able to tag a queue on creation, you must have the sqs:CreateQueue and sqs:TagQueue permissions.

## A new member of your team is working on creating Dead Letter Queue (DLQ) for AWS Lambda functions. As a Developer Associate, can you help him identify the use cases, wherein AWS Lambda will add a message into a DLQ after being processed?

**The Lambda function invocation is asynchronous** - When an asynchronous invocation event exceeds the maximum age or fails all retry attempts, Lambda discards it. Or sends it to dead-letter queue if you have configured one.

**The event fails all processing attempt** - A dead-letter queue acts the same as an on-failure destination in that it is used when an event fails all processing attempts or expires without being processed.

## A media company uses Amazon Simple Queue Service (SQS) queue to manage their transactions. With changing business needs, the payload size of the messages is increasing. The Team Lead of the project is worried about the 256 KB message size limit that SQS has. What can be done to make the queue accept messages of a larger size?

**Use the SQS Extended Client** - **To manage large Amazon Simple Queue Service (Amazon SQS) messages, you can use Amazon Simple Storage Service (Amazon S3) and the Amazon _SQS Extended Client Library for Java_.** This is especially useful for storing and consuming messages up to 2 GB. Unless your application requires repeatedly creating queues and leaving them inactive or storing large amounts of data in your queues, consider using Amazon S3 for storing your data.

## A company???s e-commerce website is expecting hundreds of thousands of visitors on Black Friday. The marketing department is concerned that high volumes of orders might stress SQS leading to message failures. The company has approached you for the steps to be taken as a precautionary measure against the high volumes. What step will you suggest as a Developer Associate?

**Amazon SQS is highly scalable and does not need any intervention to handle the expected high volumes**

Amazon SQS leverages the AWS cloud to dynamically scale, based on demand. SQS scales elastically with your application so you don't have to worry about capacity planning and pre-provisioning. For most standard queues (depending on queue traffic and message backlog), there can be a maximum of approximately 120,000 inflight messages (received from a queue by a consumer, but not yet deleted from the queue).

### Your company has been hired to build a resilient mobile voting app for an upcoming music award show that expects to have 5 to 20 million viewers. The mobile voting app will be marketed heavily months in advance so you are expected to handle millions of messages in the system. You are configuring Amazon Simple Queue Service (SQS) queues for your architecture that should receive messages from 20 KB to 200 KB. Is it possible to send these messages to SQS?

**Yes, the max message size is 256KB**

The minimum message size is 1 byte (1 character). The maximum is 262,144 bytes (256 KB).

### DevOps engineers are developing an order processing system where notifications are sent to a department whenever an order is placed for a product. The system also pushes identical notifications of the new order to a processing module that would allow EC2 instances to handle the fulfillment of the order. In the case of processing errors, the messages should be allowed to be re-processed at a later stage. The order processing system should be able to scale transparently without the need for any manual or programmatic provisioning of resources. Which of the following solutions can be used to address this use-case?

**SNS + SQS**

Amazon SNS enables message filtering and fanout to a large number of subscribers, including serverless functions, queues, and distributed systems. Additionally, Amazon SNS fans out notifications to end users via mobile push messages, SMS, and email.

Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications. SQS offers two types of message queues. Standard queues offer maximum throughput, best-effort ordering, and at-least-once delivery. **SQS _FIFO queues are designed to guarantee that messages are processed exactly once, in the exact order that they are sent_**.

Because each buffered request can be processed independently, Amazon _SQS can scale transparently to handle the load without any provisioning instructions from you_.

SNS and SQS can be used to create a fanout messaging scenario in which messages are "pushed" to multiple subscribers, which eliminates the need to periodically check or poll for updates and enables parallel asynchronous processing of the message by the subscribers. SQS can allow for later re-processing and dead letter queues. This is called the fan-out pattern.

## AWS SDK for Java

### A developer is creating access credentials for an Amazon EC2 instance that hosts the web application using AWS SDK for Java. If the default credentials provider chain is used on the instance, which parameter will be checked first for the required credentials?

**Parameters _aws.accessKeyId_ and _aws.secretKey_ will be checked in the Java system properties**

If your application creates an AWS client using the default constructor, then the client will search for credentials using the default credentials provider chain, in the following order:

In the Java system properties: aws.accessKeyId and aws.secretKey.

In system environment variables: AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY.

In the default credentials file (the location of this file varies by platform).

Credentials delivered through the Amazon EC2 container service if the AWS_CONTAINER_CREDENTIALS_RELATIVE_URI environment variable is set and security manager has permission to access the variable.

In the instance profile credentials, which exist within the instance metadata associated with the IAM role for the EC2 instance.

Web Identity Token credentials from the environment or container.

The instance profile credentials step in the default provider chain is available only when running your application on an Amazon EC2 instance, but provides the greatest ease of use and best security when working with Amazon EC2 instances. You can also pass an InstanceProfileCredentialsProvider instance directly to the client constructor to get instance profile credentials without proceeding through the entire default provider chain.

### You work as a developer doing contract work for the government on AWS gov cloud. Your applications use Amazon Simple Queue Service (SQS) for its message queue service. Due to recent hacking attempts, security measures have become stricter and require you to store data in encrypted queues. Which of the following steps can you take to meet your requirements without making changes to the existing code?

**Enable SQS KMS encryption**

Server-side encryption (SSE) lets you transmit sensitive data in encrypted queues. SSE protects the contents of messages in queues using keys managed in AWS Key Management Service (AWS KMS).

AWS KMS combines secure, highly available hardware and software to provide a key management system scaled for the cloud. When you use Amazon SQS with AWS KMS, the data keys that encrypt your message data are also encrypted and stored with the data they protect.

You can choose to have SQS encrypt messages stored in both Standard and FIFO queues using an encryption key provided by AWS Key Management Service (KMS).

### A senior cloud engineer designs and deploys online fraud detection solutions for credit card companies processing millions of transactions daily. The Elastic Beanstalk application sends files to Amazon S3 and then sends a message to an Amazon SQS queue containing the path of the uploaded file in S3. The engineer wants to postpone the delivery of any new messages to the queue for at least 10 seconds. Which SQS feature should the engineer leverage?

**Use DelaySeconds parameter**

Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications. SQS offers two types of message queues. Standard queues offer maximum throughput, best-effort ordering, and at-least-once delivery. SQS FIFO queues are designed to guarantee that messages are processed exactly once, in the exact order that they are sent.

**Delay queues** _let you postpone the delivery of new messages to a queue for several seconds, for example, when your consumer application needs additional time to process messages._ **If you create a delay queue, any messages that you send to the queue remain invisible to consumers for the duration of the delay period. The default (minimum) delay for a queue is 0 seconds. The maximum is 15 minutes**.

### What is long polling in SQS?

LongPolling - Long polling makes it inexpensive to retrieve messages from your Amazon SQS queue as soon as the messages are available. Long polling helps reduce the cost of using Amazon SQS by eliminating the number of empty responses (when there are no messages available for a ReceiveMessage request) and false empty responses (when messages are available but aren't included in a response). When the wait time for the ReceiveMessage API action is greater than 0, long polling is in effect. The maximum long polling wait time is 20 seconds. You cannot use LongPolling to postpone the delivery of new messages to the queue for a few seconds.
