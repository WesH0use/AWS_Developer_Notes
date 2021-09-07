## How can I provide cross-account access to objects that are in Amazon S3 buckets?

Use one of the following methods to grant cross-account access to objects that are stored in S3 buckets:

### The development team at a HealthCare company has deployed EC2 instances in AWS Account A. These instances need to access patient data with Personally Identifiable Information (PII) on multiple S3 buckets in another AWS Account B. As a Developer Associate, which of the following solutions would you recommend for the given use-case?

Create an IAM role with S3 access in Account B and set Account A as a trusted entity. Create another role (instance profile) in Account A and attach it to the EC2 instances in Account A and add an inline policy to this role to assume the role from Account B

You can give EC2 instances in one account ("account A") permissions to assume a role from another account ("account B") to access resources such as S3 buckets. You need to create an IAM role in Account B and set Account A as a trusted entity. Then attach a policy to this IAM role such that it delegates access to Amazon S3. Then you can create another role (instance profile) in Account A and attach it to the EC2 instances in Account A and add an inline policy to this role to assume the role from Account B.

## You are an administrator for a video-on-demand web application where content creators upload videos directly into S3. Recent support requests from customers state that uploading video files near 500GB size causes the website to break. After doing some investigation you find the following error: 'Your proposed upload exceeds the maximum allowed size'.What must you do to solve this error?

Amazon recommends that you use multipart uploading for the following use-cases:

If you're uploading large objects over a stable high-bandwidth network, use multipart uploading to maximize the use of your available bandwidth by uploading object parts in parallel for multi-threaded performance.

If you're uploading over a spotty network, use multipart uploading to increase resiliency to network errors by avoiding upload restarts.

You need to use multi-part upload for large files: In general, when your object size reaches 100 MB, you should consider using multipart uploads instead of uploading the object in a single operation.

## As part of their on-boarding, the employees at an IT company need to upload their profile photos in a private S3 bucket. The company wants to build an in-house web application hosted on an EC2 instance that should display the profile photos in a secure way when the employees mark their attendance. As a Developer Associate, which of the following solutions would you suggest to address this use-case?

**"Save the S3 key for each user's profile photo in a DynamoDB table and use a lambda function to dynamically generate a pre-signed URL. Reference this URL for display via the web application"**

**On Amazon S3, all objects by default are private**. Only the object owner has permission to access these objects. **However, the object owner can optionally share objects with others by creating a pre-signed URL, using their own security credentials, to grant time-limited permission to download the objects.**

You can also use an IAM instance profile to create a pre-signed URL. When you create a pre-signed URL for your object, you must provide your security credentials, specify a bucket name, an object key, specify the HTTP method (GET to download the object), and expiration date and time. The pre-signed URLs are valid only for the specified duration. So for the given use-case, the object key can be retrieved from the DynamoDB table, and then the application can generate the pre-signed URL using the IAM instance profile.

### To meet compliance guidelines, a company needs to ensure replication of any data stored in its S3 buckets. Which of the following characteristics are correct while configuring an S3 bucket for replication? (Select two)

**Same-Region Replication (SRR) and Cross-Region Replication (CRR) can be configured at the S3 bucket level, a shared prefix level, or an object level using S3 object tags** - Amazon S3 Replication (CRR and SRR) is configured at the S3 bucket level, a shared prefix level, or an object level using S3 object tags. You add a replication configuration on your source bucket by specifying a destination bucket in the same or different AWS region for replication.

**S3 lifecycle actions are NOT replicated with S3 replication** - With S3 Replication (CRR and SRR), you can establish replication rules to make copies of your objects into another storage class, in the same or a different region. Lifecycle actions are not replicated, and if you want the same lifecycle configuration applied to both source and destination buckets, enable the same lifecycle configuration on both.


## A development team uses shared Amazon S3 buckets to upload files. Due to this shared access, objects in S3 buckets have different owners making it difficult to manage the objects. As a developer associate, which of the following would you suggest to automatically make the S3 bucket owner, also the owner of all objects in the bucket, irrespective of the AWS account used for uploading the objects?

**Use _S3 Object Ownership_ to default bucket owner to be the owner of all objects in the bucket**

S3 Object Ownership is an Amazon S3 bucket setting that you can use to control ownership of new objects that are uploaded to your buckets. By default, when other AWS accounts upload objects to your bucket, the objects remain owned by the uploading account. With S3 Object Ownership, any new objects that are written by other accounts with the bucket-owner-full-control canned access control list (ACL) automatically become owned by the bucket owner, who then has full control of the objects.

S3 Object Ownership has two settings: 

1. **Object writer** – The uploading account will own the object.<br>
2. **Bucket owner preferred** – The bucket owner will own the object if the object is uploaded with the bucket-owner-full-control canned ACL. Without this setting and canned ACL, the object is uploaded and remains owned by the uploading account.

### You are getting ready for an event to show off your Alexa skill written in JavaScript. As you are testing your voice activation commands you find that some intents are not invoking as they should and you are struggling to figure out what is happening. You included the following code console.log(JSON.stringify(this.event)) in hopes of getting more details about the request to your Alexa skill. You would like the logs stored in an Amazon Simple Storage Service (S3) bucket named MyAlexaLog. How do you achieve this?

**Use CloudWatch integration feature with S3**

You can export log data from your CloudWatch log groups to an Amazon S3 bucket and use this data in custom processing and analysis, or to load onto other systems.

## A developer is migrating an on-premises application to AWS Cloud. The application currently processes user uploads and uploads them to a local directory on the server. All such file uploads must be saved and then made available to all instances in an Auto Scaling group. As a Developer Associate, which of the following options would you recommend for this use-case?

**Use Amazon S3 and make code changes in the application so all uploads are put on S3**

Amazon S3 is an object storage built to store and retrieve any amount of data from anywhere on the Internet. It’s a simple storage service that offers an extremely durable, highly available, and infinitely scalable data storage infrastructure at very low costs.

Amazon S3 provides a simple web service interface that you can use to store and retrieve any amount of data, at any time, from anywhere on the web. Using this web service, you can easily build applications that make use of Internet storage.

You can use S3 PutObject API from the application to upload the objects in a single bucket, which is then accessible from all instances.
