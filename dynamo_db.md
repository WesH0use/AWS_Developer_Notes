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
