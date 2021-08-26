Amazon Kinesis Data Firehose is a fully managed service for delivering real-time streaming data to destinations such as Amazon Simple Storage Service (Amazon S3), Amazon Redshift, Amazon Elasticsearch Service (Amazon ES), and Splunk. With Kinesis Data Firehose, you don't need to write applications or manage resources. You configure your data producers to send data to Kinesis Data Firehose, and it automatically delivers the data to the destination that you specified.

**Amazon Elasticsearch Service (Amazon ES) with optionally backing up data to Amazon S3** - Amazon ES is a supported destination type for Kinesis Firehose. Streaming data is delivered to your Amazon ES cluster, and can optionally be backed up to your S3 bucket concurrently.

**Amazon Simple Storage Service (Amazon S3) as a direct Firehose destination** - For Amazon S3 destinations, streaming data is delivered to your S3 bucket. If data transformation is enabled, you can optionally back up source data to another Amazon S3 bucket.

**Amazon Redshift with Amazon S3** - For Amazon Redshift destinations, streaming data is delivered to your S3 bucket first. Kinesis Data Firehose then issues an Amazon Redshift COPY command to load data from your S3 bucket to your Amazon Redshift cluster. If data transformation is enabled, you can optionally back up source data to another Amazon S3 bucket.

