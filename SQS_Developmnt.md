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
