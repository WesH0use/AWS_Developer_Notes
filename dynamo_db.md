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

