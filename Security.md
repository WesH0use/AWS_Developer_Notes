# Security with AWS

# Lambda

### An e-commerce company has an order processing workflow with several tasks to be done in parallel as well as decision steps to be evaluated for successful processing of the order. All the tasks are implemented via Lambda functions. Which of the following is the BEST solution to meet these business requirements?

**AWS Step Functions** is a web service that enables you to coordinate the components of distributed applications and microservices using visual workflows. You build applications from individual components that each perform a discrete function, or task, allowing you to scale and change applications quickly.

How Step Functions Work:

![image](https://user-images.githubusercontent.com/44325167/131663903-5a870df4-87ea-444d-ab98-e7f80033f0fe.png)


The following are key features of AWS Step Functions:

Step Functions are based on the concepts of tasks and state machines. You define state machines using the JSON-based Amazon States Language. A state machine is defined by the states it contains and the relationships between them. States are elements in your state machine. Individual states can make decisions based on their input, perform actions, and pass output to other states. In this way, a state machine can orchestrate workflows.

Please see this note for a simple example of a State Machine:

![image](https://user-images.githubusercontent.com/44325167/131664116-8ba5bdbe-b86f-47c6-9ed4-09f1524acab2.png)

# SQS 

### A high-frequency stock trading firm is migrating their messaging queues from self-managed message-oriented middleware systems to Amazon SQS. The development team at the company wants to minimize the costs of using SQS. As a Developer Associate, which of the following options would you recommend to address the given use-case?

**Use SQS long polling to retrieve messages from your Amazon SQS queues**

Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.

_Amazon SQS provides short polling and long polling to receive messages from a queue_. **By default, queues use short polling**. **With short polling, Amazon SQS sends the response right away, even if the query found no messages. With long polling, Amazon SQS sends a response after it collects at least one available message, up to the maximum number of messages specified in the request. Amazon SQS sends an empty response only if the polling wait time expires.**

_Long polling makes it inexpensive to retrieve messages from your Amazon SQS queue as soon as the messages are available_. Long polling helps reduce the cost of using Amazon SQS by eliminating the number of empty responses (when there are no messages available for a ReceiveMessage request) and false empty responses (when messages are available but aren't included in a response). When the wait time for the ReceiveMessage API action is greater than 0, long polling is in effect. The maximum long polling wait time is 20 seconds.

### An Amazon Simple Queue Service (SQS) has to be configured between two AWS accounts for shared access to the queue. AWS account A has the SQS queue in its account and AWS account B has to be given access to this queue. Which of the following options need to be combined to allow this cross-account access? (Select three)

**The account A administrator creates an IAM role and attaches a permissions policy**

**The account A administrator attaches a trust policy to the role that identifies account B as the principal who can assume the role**

**The account B administrator delegates the permission to assume the role to any users in account B**

To grant cross-account permissions, you need to attach an identity-based permissions policy to an IAM role. For example, the AWS account A administrator can create a role to grant cross-account permissions to AWS account B as follows:

The account A administrator creates an IAM role and attaches a permissions policy—that grants permissions on resources in account A—to the role.

The account A administrator attaches a trust policy to the role that identifies account B as the principal who can assume the role.

The account B administrator delegates the permission to assume the role to any users in account B. This allows users in account B to create or access queues in account A.


# Users
### A HealthCare mobile app uses proprietary Machine Learning algorithms to provide early diagnosis using patient health metrics. To protect this sensitive data, the development team wants to transition to a scalable user management system with log-in/sign-up functionality that also supports Multi-Factor Authentication (MFA) Which of the following options can be used to implement a solution with the LEAST amount of development effort? (Select two)

**Use Amazon Cognito for user-management and facilitating the log-in/sign-up process**

**Use Amazon Cognito to enable Multi-Factor Authentication (MFA) when users log-in**

Amazon Cognito lets you add user sign-up, sign-in, and access control to your web and mobile apps quickly and easily. Amazon Cognito scales to millions of users and supports sign-in with social identity providers, such as Facebook, Google, and Amazon, and enterprise identity providers via SAML 2.0.

A Cognito user pool is a user directory in Amazon Cognito. With a user pool, your users can sign in to your web or mobile app through Amazon Cognito, or federate through a third-party identity provider (IdP). Whether your users sign-in directly or through a third party, all members of the user pool have a directory profile that you can access through an SDK.

Cognito user pools provide support for sign-up and sign-in services as well as security features such as multi-factor authentication (MFA).


# S3

### A telecom service provider stores its critical customer data on Amazon Simple Storage Service (Amazon S3). Which of the following options can be used to control access to data stored on Amazon S3?

**Bucket policies, Identity and Access Management (IAM) policies**

**Query String Authentication, Access Control Lists (ACLs)**

### A company developed an app-based service for citizens to book transportation rides in the local community. The platform is running on AWS EC2 instances and uses Amazon Relational Database Service (RDS) for storing transportation data. A new feature has been requested where receipts would be emailed to customers with PDF attachments retrieved from Amazon Simple Storage Service (S3). Which of the following options will provide EC2 instances with the right permissions to upload files to Amazon S3 and generate S3 Signed URL?

**Create an IAM Role for EC2**

IAM roles have been incorporated so that your applications can securely make API requests from your instances, without requiring you to manage the security credentials that the applications use. Instead of creating and distributing your AWS credentials, you can delegate permission to make API requests using IAM roles.

Amazon EC2 uses an instance profile as a container for an IAM role. When you create an IAM role using the IAM console, the console creates an instance profile automatically and gives it the same name as the role to which it corresponds.

Customers may use four mechanisms for controlling access to Amazon S3 resources: <br>_Identity and Access Management (IAM) policies <br> Bucket policies <br> Access Control Lists (ACLs) <br> Query String Authentication._

IAM enables organizations with multiple employees to create and manage multiple users under a single AWS account. With IAM policies, customers can grant IAM users fine-grained control to their Amazon S3 bucket or objects while also retaining full control over everything the users do.

With bucket policies, customers can define rules which apply broadly across all requests to their Amazon S3 resources, such as granting write privileges to a subset of Amazon S3 resources. Customers can also restrict access based on an aspect of the request, such as HTTP referrer and IP address.

With ACLs, customers can grant specific permissions (i.e. READ, WRITE, FULL_CONTROL) to specific users for an individual bucket or object.

With Query String Authentication, customers can create a URL to an Amazon S3 object which is only valid for a limited time. Using query parameters to authenticate requests is useful when you want to express a request entirely in a URL. This method is also referred as presigning a URL.

### You are storing your video files in a separate S3 bucket than your main static website in an S3 bucket. When accessing the video URLs directly the users can view the videos on the browser, but they can't play the videos while visiting the main website. What is the root cause of this problem?

**Enable CORS**

Cross-origin resource sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain. With CORS support, you can build rich client-side web applications with Amazon S3 and selectively allow cross-origin access to your Amazon S3 resources.

To configure your bucket to allow cross-origin requests, you create a CORS configuration, which is an XML document with rules that identify the origins that you will allow to access your bucket, the operations (HTTP methods) that will support for each origin, and other operation-specific information.

For the given use-case, you would create a <CORSRule> in <CORSConfiguration> for bucket B to allow access from the S3 website origin hosted on bucket A.

## A digital marketing company has its website hosted on an Amazon S3 bucket A. The development team notices that the static JavaScript files, that are hosted on another S3 bucket B, are not loading correctly on the website. Which of the following solutions can be used to address this issue?

**Configure CORS on the bucket B that is hosting the JavaScript files to allow Bucket A origin to make the requests**

Cross-origin resource sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain.

To configure your bucket to allow cross-origin requests, you create a CORS configuration, which is an XML document with rules that identify the origins that you will allow to access your bucket, the operations (HTTP methods) that will support for each origin, and other operation-specific information.

For the given use-case, you would create a <CORSRule> in <CORSConfiguration> for bucket B to allow access from the S3 website origin hosted on bucket A.
 
**A financial services company wants to ensure that the customer data is always kept encrypted on Amazon S3 but wants a fully managed solution to create, rotate and remove the encryption keys. As a Developer Associate, which of the following would you recommend to address the given use-case?**

**Server-Side Encryption with Customer Master Keys (CMKs) Stored in AWS Key Management Service (SSE-KMS)**

You have the following options for protecting data at rest in Amazon S3:

Server-Side Encryption – Request Amazon S3 to encrypt your object before saving it on disks in its data centers and then decrypt it when you download the objects.

Client-Side Encryption – Encrypt data client-side and upload the encrypted data to Amazon S3. In this case, you manage the encryption process, the encryption keys, and related tools.

When you use server-side encryption with AWS KMS (SSE-KMS), you can use the default AWS managed CMK, or you can specify a customer-managed CMK that you have already created.

Creating your own customer-managed CMK gives you more flexibility and control over the CMK. For example, you can create, rotate, and disable customer-managed CMKs. You can also define access controls and audit the customer-managed CMKs that you use to protect your data.
 
 
## A recruit has created an Amazon Simple Storage Service (S3) bucket. He needs assistance in getting the security principles right for this bucket. Which of the following is NOT a security practice for access control to S3 buckets?
 
 Use of Access Control List (ACL)
 Security Groups
 Bucket Policies
 IAM Roles
 
 
Correct option:

**Use of Security Groups** - A security group acts as a virtual firewall for your instances to control incoming and outgoing traffic. S3 is a managed object storage service. _Security Groups are not meant for S3_.

Incorrect options:

**Use of IAM Roles** - For applications on Amazon EC2 or other AWS services to access Amazon S3 resources, they must include valid AWS credentials in their AWS API requests. IAM role is the perfect option in such scenarios. When you use a role, you don't have to distribute long-term credentials (such as a user name and password or access keys) to an Amazon EC2 instance or AWS service such as AWS Lambda. The role supplies temporary permissions that applications can use when they make calls to other AWS resources.
 
**Use of Access Control Lists (ACLs)** - Amazon S3 access control lists (ACLs) enable you to manage access to buckets and objects. Each bucket and object has an ACL attached to it as a subresource. It defines which AWS accounts or groups are granted access and the type of access. When a request is received against a resource, Amazon S3 checks the corresponding ACL to verify that the requester has the necessary access permissions.

**Use of Bucket Policies** - A bucket policy is a resource-based AWS Identity and Access Management (IAM) policy. You add a bucket policy to a bucket to grant other AWS accounts or IAM users access permissions for the bucket and the objects in it. Object permissions apply only to the objects that the bucket owner creates.
 
### You have a web application hosted on EC2 that makes GET and PUT requests for objects stored in Amazon Simple Storage Service (S3) using the SDK for PHP. As the security team completed the final review of your application for vulnerabilities, they noticed that your application uses hardcoded IAM access key and secret access key to gain access to AWS services. They recommend you leverage a more secure setup, which should use temporary credentials if possible. Which of the following options can be used to address the given use-case?
 
**Use an IAM Instance Role**

An instance profile is a container for an IAM role that you can use to pass role information to an EC2 instance when the instance starts. The AWS SDK will use the EC2 metadata service to obtain temporary credentials thanks to the IAM instance role. This is the most secure and common setup when deploying any kind of applications onto an EC2 instance.
 
 
### A cybersecurity company is publishing critical log data to a log group in Amazon CloudWatch Logs, which was created 3 months ago. The company must encrypt the log data using an AWS KMS customer master key (CMK), so any future data can be encrypted to meet the company’s security guidelines. How can the company address this use-case?
 
 **Use the AWS CLI associate-kms-key command and specify the KMS key ARN**

Log group data is always encrypted in CloudWatch Logs. You can optionally use AWS AWS Key Management Service for this encryption. If you do, the encryption is done using an AWS KMS (AWS KMS) customer master key (CMK). Encryption using AWS KMS is enabled at the log group level, by associating a CMK with a log group, either when you create the log group or after it exists.

After you associate a CMK with a log group, all newly ingested data for the log group is encrypted using the CMK. This data is stored in an encrypted format throughout its retention period. CloudWatch Logs decrypts this data whenever it is requested. CloudWatch Logs must have permissions for the CMK whenever encrypted data is requested.

To associate the CMK with an existing log group, you can use the _associate-kms-key_ command.
 
### A development team is storing sensitive customer data in S3 that will require encryption at rest. The encryption keys must be rotated at least annually. What is the easiest way to implement a solution for this requirement?
 
Use AWS KMS with automatic key rotation - Server-side encryption is the encryption of data at its destination by the application or service that receives it. Amazon S3 encrypts your data at the object level as it writes it to disks in its data centers and decrypts it for you when you access it. You have three mutually exclusive options, depending on how you choose to manage the encryption keys: Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3), Server-Side Encryption with Customer Master Keys (CMKs) Stored in AWS Key Management Service (SSE-KMS), Server-Side Encryption with Customer-Provided Keys (SSE-C).

When you use server-side encryption with AWS KMS (SSE-KMS), you can use the default AWS managed CMK, or you can specify a customer managed CMK that you have already created. If you don't specify a customer managed CMK, Amazon S3 automatically creates an AWS managed CMK in your AWS account the first time that you add an object encrypted with SSE-KMS to a bucket. By default, Amazon S3 uses this CMK for SSE-KMS.

You can choose to have AWS KMS automatically rotate CMKs every year, provided that those keys were generated within AWS KMS HSMs.

 ### An organization recently began using AWS CodeCommit for its source control service. A compliance security team visiting the organization was auditing the software development process and noticed developers making many git push commands within their development machines. The compliance team requires that encryption be used for this activity. How can the organization ensure source code is encrypted in transit and at rest?
 
** Repositories are automatically encrypted at rest**

Data in AWS CodeCommit repositories is encrypted in transit and at rest. When data is pushed into an AWS CodeCommit repository (for example, by calling git push), AWS CodeCommit encrypts the received data as it is stored in the repository.


# SHH Keys 

**A key pair, consisting of a public key and a private key, is a set of security credentials that you use to prove your identity when connecting to an Amazon EC2 instance.** Amazon EC2 stores the public key on your instance, and you store the private key. For Linux instances, the private key allows you to securely SSH into your instance. Anyone who possesses your private key can connect to your instances, so it's important that you store your private key in a secure place.

Because Amazon EC2 doesn't keep a copy of your private key, there is no way to recover a private key if you lose it. However, there can still be a way to connect to instances for which you've lost the private key. For more information, see Connect to your Linux instance if you lose your private key.

### A company runs its flagship application on a fleet of Amazon EC2 instances. After misplacing a couple of private keys from the SSH key pairs, they have decided to re-use their SSH key pairs for the different instances across AWS Regions. As a Developer Associate, which of the following would you recommend to address this use-case?

**Generate a public SSH key from a private SSH key. Then, import the key into each of your AWS Regions**

Here is the correct way of reusing SSH keys in your AWS Regions:

1) Generate a public SSH key (.pub) file from the private SSH key (.pem) file.

2) Set the AWS Region you wish to import to.

3) Import the public SSH key into the new Region.

# SSM Parameter Store

### Your application is deployed automatically using AWS Elastic Beanstalk. Your YAML configuration files are stored in the folder .ebextensions and new files are added or updated often. The DevOps team does not want to re-deploy the application every time there are configuration changes, instead, they would rather manage configuration externally, securely, and have it load dynamically into the application at runtime. What option allows you to do this?

Use SSM Parameter Store

_AWS Systems Manager Parameter Store provides secure, hierarchical storage for configuration data management and secrets management_. You can store data such as passwords, database strings, and license codes as parameter values. For the given use-case, as the DevOps team does not want to re-deploy the application every time there are configuration changes, so _they can use the SSM Parameter Store to store the configuration externally_.

# Geolocation

Geolocation routing lets you choose the resources that serve your traffic based on the geographic location of your users, meaning the location that DNS queries originate from. For example, you might want all queries from Europe to be routed to an ELB load balancer in the Frankfurt region. You can also use geolocation routing to restrict distribution of content to only the locations in which you have distribution rights

You can create a default record that handles both queries from IP addresses that aren't mapped to any location and queries that come from locations that you haven't created geolocation records for. If you don't create a default record, Route 53 returns a "no answer" response for queries from those locations.

## Multi-factor Authentication

**Hardware MFA device** - This hardware device generates a six-digit numeric code. The user must type this code from the device on a second webpage during sign-in. Each MFA device assigned to a user must be unique. A user cannot type a code from another user's device to be authenticated. Can be used for root user authentication.

**U2F security key** - A device that you plug into a USB port on your computer. U2F is an open authentication standard hosted by the FIDO Alliance. When you enable a U2F security key, you sign in by entering your credentials and then tapping the device instead of manually entering a code.

**Virtual MFA devices** - A software app that runs on a phone or other device and emulates a physical device. The device generates a six-digit numeric code. The user must type a valid code from the device on a second webpage during sign-in. Each virtual MFA device assigned to a user must be unique. A user cannot type a code from another user's virtual MFA device to authenticate.

## Using Tokens with User Pools

"Cognito User Pools"

After successful authentication, Amazon Cognito returns user pool tokens to your app. You can use the tokens to grant your users access to your own server-side resources, or to the Amazon API Gateway.

Amazon Cognito user pools implement ID, access, and refresh tokens as defined by the OpenID Connect (OIDC) open standard.

**The ID token is a JSON Web Token** (JWT) that contains claims about the identity of the authenticated user such as name, email, and phone_number. You can use this identity information inside your application. The ID token can also be used to authenticate users against your resource servers or server applications.

## Cognito Sync

**Amazon Cognito Sync is an AWS service and client library that enables cross-device syncing of application-related user data**. You can use it to synchronize user profile data across mobile devices and the web without requiring your own backend. The client libraries cache data locally so your app can read and write data regardless of device connectivity status. When the device is online, you can synchronize data, and if you set up push sync, notify other devices immediately that an update is available.


## IAM Access Analyzer

 AWS IAM Access Analyzer **helps you identify the resources in your organization and accounts, such as Amazon S3 buckets or IAM roles, that are shared with an external entity.** **This lets you identify unintended access to your resources and data, which is a security risk.**

You can set the scope for the analyzer to an organization or an AWS account. This is your zone of trust. The analyzer scans all of the supported resources within your zone of trust. When Access Analyzer finds a policy that allows access to a resource from outside of your zone of trust, it generates an active finding.

## Access Advisor feature on IAM console

To help identify the unused roles, IAM reports the last-used timestamp that represents when a role was last used to make an AWS request. Your security team can use this information to identify, analyze, and then confidently remove unused roles. This helps improve the security posture of your AWS environments. Additionally, by removing unused roles, you can simplify your monitoring and auditing efforts by focusing only on roles that are in use.

## Secrets Manager

AWS Secrets Manager enables you to easily rotate, manage, and retrieve database credentials, API keys, and other secrets throughout their lifecycle. Users and applications retrieve secrets with a call to Secrets Manager APIs, eliminating the need to hardcode sensitive information in plain text. Secrets Manager offers secret rotation with built-in integration for Amazon RDS, Amazon Redshift, and Amazon DocumentDB.

## Key Pairs

Key pairs consist of a public key and a private key. You use the private key to create a digital signature, and then AWS uses the corresponding public key to validate the signature. **Key pairs are used only for Amazon EC2 and Amazon 
t**. AWS does not provide key pairs for your account; you must create them. You can create Amazon EC2 key pairs from the Amazon EC2 console, CLI, or API. Key pairs make a robust combination for accessing an instance securely, a better option than using passwords.


## KMS Encryption: 

**KMS stores the CMK, and receives data from the clients, which it encrypts and sends back**

A customer master key (CMK) is a logical representation of a master key. The CMK includes metadata, such as the key ID, creation date, description, and key state. The CMK also contains the key material used to encrypt and decrypt data. You can generate CMKs in KMS, in an AWS CloudHSM cluster, or import them from your key management infrastructure.

AWS KMS supports symmetric and asymmetric CMKs. A symmetric CMK represents a 256-bit key that is used for encryption and decryption. An asymmetric CMK represents an RSA key pair that is used for encryption and decryption or signing and verification (but not both), or an elliptic curve (ECC) key pair that is used for signing and verification.

AWS KMS supports three types of CMKs: customer-managed CMKs, AWS managed CMKs, and AWS owned CMKs.


## SSL/TLS server certificates

**Which AWS entities can be used to deploy SSL/TLS server certificates?** 

**AWS Certificate Manager** - AWS Certificate Manager (ACM) is the preferred tool to provision, manage, and deploy server certificates. With ACM you can request a certificate or deploy an existing ACM or external certificate to AWS resources. Certificates provided by ACM are free and automatically renew. In a supported Region, you can use ACM to manage server certificates from the console or programmatically.

**IAM** - IAM is used as a certificate manager only when you must support HTTPS connections in a Region that is not supported by ACM. IAM securely encrypts your private keys and stores the encrypted version in IAM SSL certificate storage. IAM supports deploying server certificates in all Regions, but you must obtain your certificate from an external provider for use with AWS. You cannot upload an ACM certificate to IAM. Additionally, you cannot manage your certificates from the IAM Console.

## Security Credentials

Which security credential can only be created by the AWS Account root user?

**CloudFront Key Pairs** - IAM users can't create CloudFront key pairs. You must log in using root credentials to create key pairs.

To create signed URLs or signed cookies, you need a signer. A signer is either a trusted key group that you create in CloudFront, or an AWS account that contains a CloudFront key pair. AWS recommends that you use trusted key groups with signed URLs and signed cookies instead of using CloudFront key pairs.


## AWS Billing and Cost Management

**You need to activate IAM user access to the Billing and Cost Management console for all the users who need access - By default, IAM users do not have access to the AWS Billing and Cost Management console.** You or your account administrator must grant users access. You can do this by activating IAM user access to the Billing and Cost Management console and attaching an IAM policy to your users. Then, you need to activate IAM user access for IAM policies to take effect. You only need to activate IAM user access once.
 
 # EC2 
 
 ### An application runs on an EC2 instance and processes orders on a nightly basis. This EC2 instance needs to access the orders that are stored in S3. How would you recommend the EC2 instance access the orders securely?
 
**Use an IAM role**

IAM roles have been incorporated so that your applications can securely make API requests from your instances, without requiring you to manage the security credentials that the applications use. Instead of creating and distributing your AWS credentials, you can delegate permission to make API requests using IAM roles.

Amazon EC2 uses an instance profile as a container for an IAM role. When you create an IAM role using the IAM console, the console creates an instance profile automatically and gives it the same name as the role to which it corresponds.

This is the most secure option as the role assigned to EC2 can be used to access S3 without storing any credentials onto the EC2 instance.

## Permissions & Policy Types 

**Permissions boundary** - Permissions boundary is a managed policy that is used for an IAM entity (user or role). The policy defines the maximum permissions that the identity-based policies can grant to an entity, but does not grant permissions.

**AWS Organizations Service Control Policy (SCP)** – Use an AWS Organizations Service Control Policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU). SCPs limit permissions that identity-based policies or resource-based policies grant to entities (users or roles) within the account, but do not grant permissions.

**Access control list (ACL)** - Use ACLs to control which principals in other accounts can access the resource to which the ACL is attached. ACLs are similar to resource-based policies, although they are the only policy type that does not use the JSON policy document structure. ACLs are cross-account permissions policies that grant permissions to the specified principal.

**Resource-based policy** - Resource-based policies grant permissions to the principal that is specified in the policy. Principals can be in the same account as the resource or in other accounts. The most common examples of resource-based policies are Amazon S3 bucket policies and IAM role trust policies.

**Identity-based policy** - Help attach managed and inline policies to IAM identities (users, groups to which users belong, or roles). Identity-based policies grant permissions to an identity.

## Cloudfront

**A developer is defining the signers that can create signed URLs for their Amazon CloudFront distributions. Which of the following statements should the developer consider while defining the signers?**

**When you create a signer, the public key is with CloudFront and private key is used to sign a portion of URL** - Each signer that you use to create CloudFront signed URLs or signed cookies must have a public–private key pair. The signer uses its private key to sign the URL or cookies, and CloudFront uses the public key to verify the signature.

When you create signed URLs or signed cookies, you use the private key from the signer’s key pair to sign a portion of the URL or the cookie. When someone requests a restricted file, CloudFront compares the signature in the URL or cookie with the unsigned URL or cookie, to verify that it hasn’t been tampered with. CloudFront also verifies that the URL or cookie is valid, meaning, for example, that the expiration date and time haven’t passed.

**When you use the root user to manage CloudFront key pairs, you can only have up to two active CloudFront key pairs per AWS account** - When you use the root user to manage CloudFront key pairs, you can only have up to two active CloudFront key pairs per AWS account.

Whereas, with CloudFront key groups, you can associate a higher number of public keys with your CloudFront distribution, giving you more flexibility in how you use and manage the public keys. By default, you can associate up to four key groups with a single distribution, and you can have up to five public keys in a key group.


**A pharmaceutical company uses Amazon EC2 instances for application hosting and Amazon CloudFront for content delivery. A new research paper with critical findings has to be shared with a research team that is spread across the world. Which of the following represents the most optimal solution to address this requirement without compromising the security of the content?**

**Use CloudFront signed URL feature to control access to the file**

A signed URL includes additional information, for example, expiration date and time, that gives you more control over access to your content.

Here's an overview of how you configure CloudFront for signed URLs and how CloudFront responds when a user uses a signed URL to request a file:

In your CloudFront distribution, specify one or more trusted key groups, which contain the public keys that CloudFront can use to verify the URL signature. You use the corresponding private keys to sign the URLs.

Develop your application to determine whether a user should have access to your content and to create signed URLs for the files or parts of your application that you want to restrict access to.

A user requests a file for which you want to require signed URLs. Your application verifies that the user is entitled to access the file: they've signed in, they've paid for access to the content, or they've met some other requirement for access.

Your application creates and returns a signed URL to the user. The signed URL allows the user to download or stream the content.

This step is automatic; the user usually doesn't have to do anything additional to access the content. For example, if a user is accessing your content in a web browser, your application returns the signed URL to the browser. The browser immediately uses the signed URL to access the file in the CloudFront edge cache without any intervention from the user.

CloudFront uses the public key to validate the signature and confirm that the URL hasn't been tampered with. If the signature is invalid, the request is rejected. If the request meets the requirements in the policy statement, CloudFront does the standard operations: determines whether the file is already in the edge cache, forwards the request to the origin if necessary, and returns the file to the user.

## Security Groups / ACL 

**Security Groups are stateful, so allowing inbound traffic to the necessary ports enables the connection. Network ACLs are stateless, so you must allow both inbound and outbound traffic - Security groups are stateful, so allowing inbound traffic to the necessary ports enables the connection. Network ACLs are stateless, so you must allow both inbound and outbound traffic.**

To enable the connection to a service running on an instance, the associated network ACL must allow both inbound traffic on the port that the service is listening on as well as allow outbound traffic from ephemeral ports. When a client connects to a server, a random port from the ephemeral port range (1024-65535) becomes the client's source port.

The designated ephemeral port then becomes the destination port for return traffic from the service, so outbound traffic from the ephemeral port must be allowed in the network ACL.

By default, network ACLs allow all inbound and outbound traffic. If your network ACL is more restrictive, then you need to explicitly allow traffic from the ephemeral port range.

If you accept traffic from the internet, then you also must establish a route through an internet gateway. If you accept traffic over VPN or AWS Direct Connect, then you must establish a route through a virtual private gateway.

## IAM policy variables

Instead of creating individual policies for each user, you can use policy variables and create a single policy that applies to multiple users (a group policy). Policy variables act as placeholders. When you make a request to AWS, the placeholder is replaced by a value from the request when the policy is evaluated.

As an example, the following policy gives each of the users in the group full programmatic access to a user-specific object (their own "home directory") in Amazon S3.

## Lambda 

**You have launched several AWS Lambda functions written in Java. A new requirement was given that over 1MB of data should be passed to the functions and should be encrypted and decrypted at runtime. Which of the following methods is suitable to address the given use-case?**

**Use Envelope Encryption and reference the data as file within the code**

While AWS KMS does support sending data up to 4 KB to be encrypted directly, envelope encryption can offer significant performance benefits. When you encrypt data directly with AWS KMS it must be transferred over the network. Envelope encryption reduces the network load since only the request and delivery of the much smaller data key go over the network. The data key is used locally in your application or encrypting AWS service, avoiding the need to send the entire block of data to AWS KMS and suffer network latency.

AWS Lambda environment variables can have a maximum size of 4 KB. Additionally, the direct 'Encrypt' API of KMS also has an upper limit of 4 KB for the data payload. To encrypt 1 MB, you need to use the Encryption SDK and pack the encrypted file with the lambda function.

**"Lambda Authorizer"**

An Amazon API Gateway Lambda authorizer (formerly known as a custom authorizer) **is a Lambda function that you provide to control access to your API.** A Lambda authorizer uses bearer token authentication strategies, such as OAuth or SAML. Before creating an API Gateway Lambda authorizer, **you must first create the AWS Lambda function that implements the logic to authorize and, if necessary, to authenticate the caller.**

![image](https://user-images.githubusercontent.com/44325167/130077075-f41e472c-7e7a-4b94-8066-51b015c6922a.png)


You can use versions to manage the deployment of your AWS Lambda functions. For example, you can publish a new version of a function for beta testing without affecting users of the stable production version. You can change the function code and settings only on the unpublished version of a function. When you publish a version, the code and most of the settings are locked to ensure a consistent experience for users of that version.

You can create one or more aliases for your AWS Lambda function. A Lambda alias is like a pointer to a specific Lambda function version. You can use routing configuration on an alias to send a portion of traffic to a Lambda function version. For example, you can reduce the risk of deploying a new version by configuring the alias to send most of the traffic to the existing version, and only a small percentage of traffic to the new version.

For examples: 

You can set up the application to use an alias that points to the current version. Deploy the new version of the code and configure the alias to send 10% of the users to this new version. If the deployment goes wrong, reset the alias to point all traffic to the current version

![image](https://user-images.githubusercontent.com/44325167/130074585-94e94977-ef47-4383-b21e-3f40dde18bd7.png)



Differences between Dedicated Hosts and Dedicated Instances (Dedicated host is more costly than dedicated instances):
![image](https://user-images.githubusercontent.com/44325167/130073418-edd31903-b822-433d-add7-2d97b4b53b79.png)

## API security 

**Signing AWS API requests helps AWS identify an authentic user from a potential threat. As a developer associate, which of the following would you identify as the use-case where you need to sign the API requests?**

**When you send HTTP requests to an AWS service** - When you send HTTP requests to AWS, you sign the requests so that AWS can identify who sent them. You sign requests with your AWS access key, which consists of an access key ID and secret access key.

When you write custom code to send HTTP requests to AWS, you need to include code to sign the requests. You might do this for the following reasons:

You are working with a programming language for which there is no AWS SDK.

You want complete control over how a request is sent to AWS.


## API Gateway

**A developer is looking at establishing access control for an API that connects to a Lambda function downstream. Which of the following represent mechanisms that can be used for authenticating with the API Gateway?**

**Standard AWS IAM roles and policies** - Standard AWS IAM roles and policies offer flexible and robust access controls that can be applied to an entire API or individual methods. IAM roles and policies can be used for controlling who can create and manage your APIs, as well as who can invoke them.

**Lambda Authorizer** - Lambda authorizers are Lambda functions that control access to REST API methods using bearer token authentication—as well as information described by headers, paths, query strings, stage variables, or context variables request parameters. Lambda authorizers are used to control who can invoke REST API methods.

**Cognito User Pools** - Amazon Cognito user pools let you create customizable authentication and authorization solutions for your REST APIs. Amazon Cognito user pools are used to control who can invoke REST API methods.
 
**You team maintains a public API Gateway that is accessed by clients from another domain. Usage has been consistent for the last few months but recently it has more than doubled. As a result, your costs have gone up and would like to prevent other unauthorized domains from accessing your API. Which of the following actions should you take?**
 
**Restrict access by using CORS** - Cross-origin resource sharing (CORS) _defines a way for client web applications that are loaded in one domain to interact with resources in a different domain_. When your API's resources receive requests from a domain other than the API's own domain and you want to restrict servicing these requests, you must disable cross-origin resource sharing (CORS) for selected methods on the resource.
 
 # EBS
 
### A company has a workload that requires 14,000 consistent IOPS for data that must be durable and secure. The compliance standards of the company state that the data should be secure at every stage of its lifecycle on all of the EBS volumes they use. Which of the following statements are true regarding data security on EBS?
 
Amazon EBS works with AWS KMS to encrypt and decrypt your EBS volume. You can encrypt both the boot and data volumes of an EC2 instance. When you create an encrypted EBS volume and attach it to a supported instance type, the following types of data are encrypted:

Data at rest inside the volume

All data moving between the volume and the instance

All snapshots created from the volume

All volumes created from those snapshots

**EBS volumes support both in-flight encryption and encryption at rest using KMS** - This is a correct statement. Encryption operations occur on the servers that host EC2 instances, ensuring the security of both data-at-rest and data-in-transit between an instance and its attached EBS storage.
 
 
# Codecommit
 
### A company would like to migrate the existing application code from a GitHub repository to AWS CodeCommit. As an AWS Certified Developer Associate, which of the following would you recommend for migrating the cloned repository to CodeCommit over HTTPS?

**Use Git credentials generated from IAM** - CodeCommit repositories are Git-based and support the basic functionalities of Git such as Git credentials. AWS recommends that you use an IAM user when working with CodeCommit. You can access CodeCommit with other identity types, but the other identity types are subject to limitations.

The simplest way to set up connections to AWS CodeCommit repositories is to configure Git credentials for CodeCommit in the IAM console, and then use those credentials for HTTPS connections. You can also use these same credentials with any third-party tool or individual development environment (IDE) that supports HTTPS authentication using a static user name and password.

An IAM user is an identity within your Amazon Web Services account that has specific custom permissions. For example, an IAM user can have permissions to create and manage Git credentials for accessing CodeCommit repositories. This is the recommended user type for working with CodeCommit. You can use an IAM user name and password to sign in to secure AWS webpages like the AWS Management Console, AWS Discussion Forums, or the AWS Support Center.


### An IT company has a web application running on Amazon EC2 instances that needs read-only access to an Amazon DynamoDB table. As a Developer Associate, what is the best-practice solution you would recommend to accomplish this task?
 
**Create an IAM role with an AmazonDynamoDBReadOnlyAccess policy and apply it to the EC2 instance profile**

As an AWS security best practice, you should not create an IAM user and pass the user's credentials to the application or embed the credentials in the application. Instead, create an IAM role that you attach to the EC2 instance to give temporary security credentials to applications running on the instance. When an application uses these credentials in AWS, it can perform all of the operations that are allowed by the policies attached to the role.

So for the given use-case, you should create an IAM role with an AmazonDynamoDBReadOnlyAccess policy and apply it to the EC2 instance profile.
 
### You have a popular web application that accesses data stored in an Amazon Simple Storage Service (S3) bucket. Developers use the SDK to maintain the application and add new features. Security compliance requests that all new objects uploaded to S3 be encrypted using SSE-S3 at the time of upload. Which of the following headers must the developers add to their request?

'_x-amz-server-side-encryption': 'AES256'_

Server-side encryption protects data at rest. Amazon S3 encrypts each object with a unique key. As an additional safeguard, it encrypts the key itself with a master key that it rotates regularly. Amazon S3 server-side encryption uses one of the strongest block ciphers available to encrypt your data, 256-bit Advanced Encryption Standard (AES-256).
 
### Your development team uses the AWS SDK for Java on a web application that uploads files to several Amazon Simple Storage Service (S3) buckets using the SSE-KMS encryption mechanism. Developers are reporting that they are receiving permission errors when trying to push their objects over HTTP. Which of the following headers should they include in their request?

'x-amz-server-side-encryption': 'aws:kms'

Server-side encryption is the encryption of data at its destination by the application or service that receives it. AWS Key Management Service (AWS KMS) is a service that combines secure, highly available hardware and software to provide a key management system scaled for the cloud. Amazon S3 uses AWS KMS customer master keys (CMKs) to encrypt your Amazon S3 objects. AWS KMS encrypts only the object data. Any object metadata is not encrypted.

If the request does not include the x-amz-server-side-encryption header, then the request is denied.

### A development team had enabled and configured CloudTrail for all the Amazon S3 buckets used in a project. The project manager owns all the S3 buckets used in the project. However, the manager noticed that he did not receive any object-level API access logs when the data was read by another AWS account. What could be the reason for this behavior/error?
 
**The bucket owner also needs to be object owner to get the object access logs**

If the bucket owner is also the object owner, the bucket owner gets the object access logs. Otherwise, the bucket owner must get permissions, through the object ACL, for the same object API to get the same object-access API logs.
 
### As part of internal regulations, you must ensure that all communications to Amazon S3 are encrypted. For which of the following encryption mechanisms will a request get rejected if the connection is not using HTTPS?
 
**SSE-C**

Server-side encryption is about protecting data at rest. Server-side encryption encrypts only the object data, not object metadata. Using server-side encryption with customer-provided encryption keys (SSE-C) allows you to set your encryption keys.

When you upload an object, Amazon S3 uses the encryption key you provide to apply AES-256 encryption to your data and removes the encryption key from memory. When you retrieve an object, you must provide the same encryption key as part of your request. Amazon S3 first verifies that the encryption key you provided matches and then decrypts the object before returning the object data to you.

Amazon S3 will reject any requests made over HTTP when using SSE-C. For security considerations, AWS recommends that you consider any key you send erroneously using HTTP to be compromised.

### You are a manager for a tech company that has just hired a team of developers to work on the company's AWS infrastructure. All the developers are reporting to you that when using the AWS CLI to execute commands it fails with the following exception: You are not authorized to perform this operation. Encoded authorization failure message: 6h34GtpmGjJJUm946eDVBfzWQJk6z5GePbbGDs9Z2T8xZj9EZtEduSnTbmrR7pMqpJrVYJCew2m8YBZQf4HRWEtrpncANrZMsnzk. Which of the following actions will help developers decode the message?
 
**AWS STS decode-authorization-message**

Use decode-authorization-message to decode additional information about the authorization status of a request from an encoded message returned in response to an AWS request. If a user is not authorized to perform an action that was requested, the request returns a Client.UnauthorizedOperation response (an HTTP 403 response). The message is encoded because the details of the authorization status can constitute privileged information that the user who requested the operation should not see. To decode an authorization status message, a user must be granted permissions via an IAM policy to request the DecodeAuthorizationMessage (sts:DecodeAuthorizationMessage) action.

### Your company stores confidential data on an Amazon Simple Storage Service (S3) bucket. New security compliance guidelines require that files be stored with server-side encryption. The encryption used must be Advanced Encryption Standard (AES-256) and the company does not want to manage S3 encryption keys. Which of the following options should you use?
 
**SSE-S3**

Using Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3), each object is encrypted with a unique key employing strong multi-factor encryption. As an additional safeguard, it encrypts the key itself with a master key that it regularly rotates. Amazon S3 server-side encryption uses one of the strongest block ciphers available, 256-bit Advanced Encryption Standard (AES-256), to encrypt your data.
 

### You are planning to build a fleet of EBS-optimized EC2 instances to handle the load of your new application. Due to security compliance, your organization wants any secret strings used in the application to be encrypted to prevent exposing values as clear text. The solution requires that decryption events be audited and API calls to be simple. How can this be achieved? (select two)
 
**Store the secret as SecureString in SSM Parameter Store**

With AWS Systems Manager Parameter Store, you can create SecureString parameters, which are parameters that have a plaintext parameter name and an encrypted parameter value. Parameter Store uses AWS KMS to encrypt and decrypt the parameter values of Secure String parameters. Also, if you are using customer-managed CMKs, you can use IAM policies and key policies to manage to encrypt and decrypt permissions. To retrieve the decrypted value you only need to do one API call.
 
**Audit using CloudTrail**

AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. CloudTrail provides an event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command-line tools, and other AWS services.

CloudTrail will allow you to see all API calls made to SSM and KMS.
 
 
### A media company is building an application that needs to store video files in Amazon S3. Management requires that the files be encrypted before they are sent to Amazon S3 for storage. The encryption keys need to be managed by an in-house security team but the key itself is stored on AWS. Which solution should the company use to meet these requirements?
 
 **Use client-side encryption with an AWS KMS managed customer master key (CMK)**

You have the following options for protecting data at rest in Amazon S3:

Server-Side Encryption – Request Amazon S3 to encrypt your object before saving it on disks in its data centers and then decrypt it when you download the objects.

Client-Side Encryption – Encrypt data client-side and upload the encrypted data to Amazon S3. In this case, you manage the encryption process, the encryption keys, and related tools.

As the company wants to make sure that the files are encrypted before they are sent to Amazon S3, therefore you should use client-side encryption.

To enable client-side encryption, you have the following options:

Use a customer master key (CMK) stored in AWS Key Management Service (AWS KMS).

Use a master key you store within your application.

As the use-case mentions that the encryption keys need to be managed by an in-house security team but the key itself should be stored on AWS, therefore you must use the customer master key (CMK) stored in AWS Key Management Service (AWS KMS).
 
### Your company leverages Amazon CloudFront to provide content via the internet to customers with low latency. Aside from latency, security is another concern and you are looking for help in enforcing end-to-end connections using HTTPS so that content is protected. Which of the following options is available for HTTPS in AWS CloudFront?
 
**Between clients and CloudFront as well as between CloudFront and backend**

For web distributions, you can configure CloudFront to require that viewers use HTTPS to request your objects, so connections are encrypted when CloudFront communicates with viewers.
____
 
### To improve their information security management system (ISMS), a company recently released a new policy which requires all database credentials to be encrypted and be automatically rotated to avoid unauthorized access. Which of the following is the MOST appropriate solution to secure the credentials?
 
**AWS Secrets Manager** is an AWS service that makes it easier for you to manage secrets. Secrets can be database credentials, passwords, third-party API keys, and even arbitrary text. You can store and control access to these secrets centrally by using the Secrets Manager console, the Secrets Manager command line interface (CLI), or the Secrets Manager API and SDKs.

In the past, when you created a custom application that retrieves information from a database, you typically had to embed the credentials (the secret) for accessing the database directly in the application. When it came time to rotate the credentials, you had to do much more than just create new credentials. You had to invest time to update the application to use the new credentials. Then you had to distribute the updated application. If you had multiple applications that shared credentials and you missed updating one of them, the application would break. Because of this risk, many customers have chosen not to regularly rotate their credentials, which effectively substitutes one risk for another.
 
Secrets Manager enables you to replace hardcoded credentials in your code (including passwords), with an API call to Secrets Manager to retrieve the secret programmatically. This helps ensure that the secret can't be compromised by someone examining your code, because the secret simply isn't there. Also, you can configure Secrets Manager to automatically rotate the secret for you according to a schedule that you specify. This enables you to replace long-term secrets with short-term ones, which helps to significantly reduce the risk of compromise.
 
### You are building a distributed system using KMS where you need to encrypt data at a later time. An API must be called that returns only the encrypted copy of the data key which you will use for encryption. After an hour, you will decrypt the data key by calling the Decrypt API then using the returned plaintext data key to finally encrypt the data. Which is the MOST suitable KMS API that the system should use to securely implement the requirements described above?
 
The **GenerateDataKeyWithoutPlaintext** API generates a unique data key. This operation returns a data key that is encrypted under a customer master key (CMK) that you specify. GenerateDataKeyWithoutPlaintext is identical to GenerateDataKey except that it returns only the encrypted copy of the data key.

Like GenerateDataKey, GenerateDataKeyWithoutPlaintext returns a unique data key for each request. The bytes in the key are not related to the caller or CMK that is used to encrypt the data key.

 This operation is useful for systems that need to encrypt data at some point, but not immediately. When you need to encrypt the data, you call the Decrypt operation on the encrypted copy of the key.

It's also useful in distributed systems with different levels of trust. For example, you might store encrypted data in containers. One component of your system creates new containers and stores an encrypted data key with each container. Then, a different component puts the data into the containers. That component first decrypts the data key, uses the plaintext data key to encrypt data, puts the encrypted data into the container, and then destroys the plaintext data key. In this system, the component that creates the containers never sees the plaintext data key.

Hence, the correct answer in this scenario is to use the GenerateDataKeyWithoutPlaintext API.

GenerateDataKey is incorrect because this operation also returns a plaintext copy of the data key along with the copy of the encrypted data key under a customer master key (CMK) that you specified. Take note that the scenario explicitly mentioned that the API must return only the encrypted copy of the data key which will be used later for encryption. Although this API can be used in this scenario, it is not recommended since the actual encryption process of the data happens at a later time and not in real-time.
 
 
### A Software Engineer is developing an application which will be hosted on an EC2 instance and will read messages from a standard SQS queue. The average time that it takes for the producers to send a new message to the queue is 40 seconds. Which of the following is the MOST efficient way for the application to query the new messages from the queue?
 
**Amazon SQS long polling** is a way to retrieve messages from your Amazon SQS queues. While the regular short polling returns immediately, even if the message queue being polled is empty, long polling doesn’t return a response until a message arrives in the message queue, or the long poll times out.

Long polling helps reduce the cost of using Amazon SQS by eliminating the number of empty responses (when there are no messages available for a ReceiveMessage request) and false empty responses (when messages are available but aren't included in a response). This type of polling is suitable if the new messages that are being added to the SQS queue arrive less frequently.
 
You can configure long polling to your SQS queue by simply setting the "Receive Message Wait Time" field to a value greater than 0. Hence, the correct answer for this scenario is to configure the SQS queue to use Long Polling.

The option that says: "Configure each message in the SQS queue to have a custom visibility timeout of 40 seconds" is incorrect because a visibility timeout is primarily used to prevent other consumers from processing the message again for a period of time. This is normally used if your application takes a long time to process and delete a message from the SQS queue.

The option that says: "Configure the SQS queue to use Short Polling" is incorrect because it is inefficient to poll the queue every second if the average time that it takes for the producers to send a new message to the queue is 40 seconds. It is better to do Long Polling, which will query the queue every 15 or 20 seconds considering that new messages are not being added every second.

The option that says: "Configure an SQS Delay Queue with a value of 40 seconds" is incorrect because this is primarily configured if you want to postpone the delivery of new messages to the SQS queue for a number of seconds. Having this SQS configuration which sets the new messages to remain invisible to the consumers for a duration of the delay period is not helpful in the given scenario. It is still better to use Long Polling instead of setting up a delay queue.
 
 
### You have several API Gateway APIs with Lambda Integration for each release life cycle of your application. There is a requirement to consolidate multiple releases into a single API Gateway for the ALPHA, BETA, RC (Release Candidate), and PROD releases. For example, their clients can connect to their ALPHA release by using the alpha.tutorialsdojo.com endpoint and beta release through the beta.tutorialsdojo.com endpoint. As the AWS developer, how can you satisfy this requirement?
 
**Stage variables** are name-value pairs that you can define as configuration attributes associated with a deployment stage of a REST API. They act like environment variables and can be used in your API setup and mapping templates.
 
For example, you can define a stage variable in a stage configuration, and then set its value as the URL string of an HTTP integration for a method in your REST API. Later, you can reference the URL string using the associated stage variable name from the API setup. This way, you can use the same API setup with a different endpoint at each stage by resetting the stage variable value to the corresponding URLs. You can also access stage variables in the mapping templates, or pass configuration parameters to your AWS Lambda or HTTP backend.

### A web application is running in an ECS Cluster and updates data in DynamoDB several times a day. The clients retrieve data directly from the DynamoDB through APIs exposed by Amazon API Gateway. Although API caching is enabled, there are specific clients that want to retrieve the latest data from DynamoDB for every API request sent. What should be done to only allow authorized clients to invalidate an API Gateway cache entry when submitting API requests? (Select TWO.)
 
A client of your API can invalidate an existing cache entry and reload it from the integration endpoint for individual requests. The client must send a request that contains the **Cache-Control: max-age=0 header**. The client receives the response directly from the integration endpoint instead of the cache, provided that the client is authorized to do so. This replaces the existing cache entry with the new response, which is fetched from the integration endpoint.

Ticking the **Require authorization** checkbox ensures that not every client can invalidate the API cache. If most or all of the clients invalidate the API cache, this could significantly increase the latency of your API.

Hence, to only allow authorized clients to invalidate an API Gateway cache entry when submitting API requests, you can just tick the Require Authorization checkbox in the Cache Settings of your API via the console and instruct the client to send a request which contains the Cache-Control: max-age=0 header. 

### A technical manager needs permission to create new repositories and delete them in CodeCommit. This will enable her to manage all of the code repositories of each development teams and remove duplicate or unused ones. Which of the following permissions should be given in order to comply with the standard security advice of granting least privilege?
 
Access to AWS CodeCommit requires credentials. Those credentials must have permissions to access AWS resources, such as CodeCommit repositories, and your IAM user, which you use to manage your Git credentials or the SSH public key that you use for making Git connections.

In CodeCommit, the primary resource is a repository. Each resource has a unique Amazon Resource Names (ARN) associated with it. In a policy, you use an Amazon Resource Name (ARN) to identify the resource that the policy applies to. To manage access to AWS resources, you attach permissions policies to IAM identities. You use identity-based policies to control access to repositories.

The codecommit:CreateRepository and codecommit:DeleteRepository permissions enable you to create and delete a CodeCommit repository respectively. Hence, these two permissions are the correct permissions that should be given to the technical manager. 
 
### Your customers require access to the REST APIs of your web application which is hosted on EC2 instances behind a load balancer in your VPC. To accommodate this request, your web services should be integrated with API Gateway that has a custom data mapping. You need to specify how the incoming request data is mapped to the integration request and how the resulting integration response data is mapped to the method response. Which of the following integration types is the MOST suitable one to use in API Gateway to meet this requirement?
 
 You can integrate an API method in your API Gateway with a custom HTTP endpoint of your application in two ways:

 - HTTP proxy integration

 - HTTP custom integration

In your API Gateway console, you can define the type of HTTP integration of your resource by toggling the "Configure as proxy resource" checkbox.
 
With proxy integration, the setup is simple. You only need to set the HTTP method and the HTTP endpoint URI, according to the backend requirements, if you are not concerned with content encoding or caching.

With custom integration, setup is more involved. In addition to the proxy integration setup steps, you need to specify how the incoming request data is mapped to the integration request and how the resulting integration response data is mapped to the method response. API Gateway supports the following endpoint ports: 80, 443 and 1024-65535.

Programmatically, you choose an integration type by setting the type property on the Integration resource. For the Lambda proxy integration, the value is AWS_PROXY. For the Lambda custom integration and all other AWS integrations, it is AWS. For the HTTP proxy integration and HTTP integration, the value is HTTP_PROXY and HTTP, respectively. For the mock integration, the type value is MOCK.

Since the integration type that is being described in the scenario fits the definition of an HTTP custom integration, the correct answer in this scenario is to use the HTTP integration type.
 
### A developer is building an e-commerce application which will be hosted in an ECS Cluster. To minimize the number of instances in use, she must select a strategy which will place tasks based on the least available amount of CPU or memory. Which of the following task placement strategy should the developer implement?
 
 **A task placement strategy** is an algorithm for selecting instances for task placement or tasks for termination. Task placement strategies can be specified when either running a task or creating a new service.

Amazon ECS supports the following task placement strategies:

**binpack** - Place tasks based on the least available amount of CPU or memory. This minimizes the number of instances in use.

**random** - Place tasks randomly.

**spread** - Place tasks evenly based on the specified value. Accepted values are attribute key-value pairs, instanceId, or host. 

The scenario states that the developer must select a task placement strategy which will place tasks based on the least available amount of CPU or memory. **By using bin pack strategy with CPU as the field parameter, ECS is able to place tasks onto an instance with the least available amount of CPU first, before moving on to the other instances**. Hence, the correct answer is to use the binpack task placement strategy.

random is incorrect because this will place the tasks randomly, rather than placing the tasks to the instances based on the least available amount of CPU or memory.

spread is incorrect because this will place tasks evenly to the instances based on a specified value.

distinctInstance is incorrect because this is not a valid task placement strategy, but a task placement constraint. This is primarily used as a constraint to place each task on a different container instance. It can be specified when either running a task or creating a new service. 

### A developer configured an Amazon API Gateway proxy integration named MyAPI to work with a Lambda function. However, when the API is being called, the developer receives a 502 Bad Gateway error. She tried invoking the underlying function but it properly returns the result in XML format. What is the MOST likely root cause of this issue?
 
Amazon API Gateway Lambda proxy integration is a simple, powerful, and nimble mechanism to build an API with a setup of a single API method. The Lambda proxy integration allows the client to call a single Lambda function in the backend. The function accesses many resources or features of other AWS services, including calling other Lambda functions.

In Lambda proxy integration, when a client submits an API request, API Gateway passes the raw request as-is to the integrated Lambda function, except that the order of the request parameters is not preserved. This request data includes the request headers, query string parameters, URL path variables, payload, and API configuration data. The configuration data can include current deployment stage name, stage variables, user identity, or authorization context (if any). The backend Lambda function parses the incoming request data to determine the response that it returns.

For API Gateway to pass the Lambda output as the API response to the client, the Lambda function must return the result in the following JSON format:
 
 ![Screen Shot 2021-09-16 at 12 58 59 PM](https://user-images.githubusercontent.com/44325167/133600518-adc10d1a-ffbd-45b2-9eaf-591d22cf2b30.png)
 
 Since the Lambda function returns the result in XML format, it will cause the 502 errors in the API Gateway. Hence, the correct answer is that **there is an incompatible output returned from a Lambda proxy integration backend**.
 
### A website hosted in AWS has a custom CloudWatch metric to track all HTTP server errors in the site every minute, which occurs intermittently. An existing CloudWatch Alarm has already been configured for this metric but you would like to re-configure this to properly monitor the application. The alarm should only be triggered when all three data points in the most recent three consecutive periods are above the threshold. Which of the following options is the MOST appropriate way to monitor the website based on the given threshold?

When you create an alarm, you specify three settings to enable CloudWatch to evaluate when to change the alarm state:

- Period is the length of time to evaluate the metric or expression to create each individual data point for an alarm. It is expressed in seconds. If you choose one minute as the period, there is one datapoint every minute.

- Evaluation Period is the number of the most recent periods, or data points, to evaluate when determining alarm state.

- Datapoints to Alarm is the number of data points within the evaluation period that must be breaching to cause the alarm to go to the ALARM state. The breaching data points do not have to be consecutive, they just must all be within the last number of data points equal to Evaluation Period.

In the following figure, the alarm threshold is set to three units. The alarm is configured to go to the ALARM state and both Evaluation Period and Datapoints to Alarm are 3. That is, when all three datapoints in the most recent three consecutive periods are above the threshold, the alarm goes to the ALARM state. In the figure, this happens in the third through fifth time periods. At period six, the value dips below the threshold, so one of the periods being evaluated is not breaching, and the alarm state changes to OK. During the ninth time period, the threshold is breached again, but for only one period. Consequently, the alarm state remains OK. Hence, the option that says: "Set both the Evaluation Period and Datapoints to Alarm to 3" is the correct answer.
 
 ![image](https://user-images.githubusercontent.com/44325167/133602142-5c933d91-7eb0-4685-ac93-3dedc317778d.png)

### A new IT policy requires you to trace all calls that your Node.js application sends to external HTTP web APIs as well as SQL database queries. You have to instrument your application, which is hosted in Elastic Beanstalk, in order to properly trace the calls via the X-Ray console. What should you do to comply with the given requirement?
 
 You can use the AWS Elastic Beanstalk console or a configuration file to run the AWS X-Ray daemon on the instances in your environment. X-Ray is an AWS service that gathers data about the requests that your application serves, and uses it to construct a service map that you can use to identify issues with your application and opportunities for optimization.

![image](https://user-images.githubusercontent.com/44325167/133602709-dae5fc40-2e00-43d9-965d-10278bb2d26e.png)
 
 To relay trace data from your application to AWS X-Ray, you can run the X-Ray daemon on your Elastic Beanstalk environment's Amazon EC2 instances. Elastic Beanstalk platforms provide a configuration option that you can set to run the daemon automatically. You can enable the daemon in a configuration file in your source code or by choosing an option in the Elastic Beanstalk console. When you enable the configuration option, the daemon is installed on the instance and runs as a service.

Hence, the correct answer is to: enable the X-Ray daemon by including the xray-daemon.config configuration file in the .ebextensions directory of your source code, just as shown above.
 
### A developer is building a web application which requires a multithreaded event-based key/value cache store that will cache result sets from database calls. You need to run large nodes with multiple cores for your cache layer and it should scale up or down as the demand on your system increases and decreases. Which of the following is the MOST suitable service that you should use?
 
 
 **Redis and Memcached are popular, open-source, in-memory data stores**. Although they are both easy to use and offer high performance, there are important differences to consider when choosing an engine. 
 
 **Memcached is designed for simplicity while Redis offers a rich set of features that make it effective for a wide range of use cases**.

In this scenario, Redis can provide a much more durable and powerful cache layer to the prototype distributed system, however, **you should take note of one keyword in the requirement: multithreaded**. In terms of commands execution, Redis is mostly a single-threaded server. It is not designed to benefit from multiple CPU cores unlike Memcached, however, you can launch several Redis instances to scale out on several cores if needed.

Memcached is a more suitable choice since the scenario specifies that the system will run large nodes with multiple cores or threads which Memcached can adequately provide. 

You can choose Memcached over Redis if you have the following requirements:

- You need the simplest model possible.

- You need to run large nodes with multiple cores or threads.

- You need the ability to scale out and in, adding and removing nodes as demand on your system increases and decreases.

- You need to cache objects, such as a database.
 
**This is why the most suitable answer to this scenario is Amazon ElastiCache for Memcached**.

Amazon ElastiCache for Redis is incorrect because it does not totally support a multithreaded architecture, unlike Memcached. Although Redis has more features compared with Memcached, the scenario requires that the cache layer is multithreaded. This is why Memcached is a more suitable cache engine to choose from instead of Redis.
Memcached is a more suitable choice since the scenario specifies that the system will run large nodes with multiple cores or threads which Memcached can adequately provide. 
 
 ### A Lambda function is sending data to an Aurora MySQL DB Instance in your VPC. However,  you are getting a MySQL: ERROR 1040: Too many connections error whenever there is a surge in incoming traffic. Upon investigation, you found that your function is always creating a new database connection whenever it is invoked. Which of the following is the MOST suitable and scalable solution to overcome this problem?

 When AWS Lambda executes your Lambda function, it provisions and manages the resources needed to run your Lambda function. When you create a Lambda function, you specify configuration information, such as the amount of memory and maximum execution time that you want to allow for your Lambda function. When a Lambda function is invoked, AWS Lambda launches an execution context based on the configuration settings you provide. The execution context is a temporary runtime environment that initializes any external dependencies of your Lambda function code, such as database connections or HTTP endpoints. This affords subsequent invocations better performance because there is no need to "cold-start" or initialize those external dependencies, as explained below.

It takes time to set up an execution context and do the necessary "bootstrapping", which adds some latency each time the Lambda function is invoked. You typically see this latency when a Lambda function is invoked for the first time or after it has been updated because AWS Lambda tries to reuse the execution context for subsequent invocations of the Lambda function.

After a Lambda function is executed, AWS Lambda maintains the execution context for some time in anticipation of another Lambda function invocation. In effect, the service freezes the execution context after a Lambda function completes, and thaws the context for reuse, if AWS Lambda chooses to reuse the context when the Lambda function is invoked again. This execution context reuse approach has the following implications:

-Any declarations in your Lambda function code (outside the handler code, see Programming Model) remains initialized, providing additional optimization when the function is invoked again. For example, if your Lambda function establishes a database connection, instead of reestablishing the connection, the original connection is used in subsequent invocations. It is recommended to add logic in your code to check if a connection exists before creating one.

### A developer is working on an application which stores data to an Amazon DynamoDB table with the DynamoDB Streams feature enabled. He set up an event source mapping with DynamoDB Streams and AWS Lambda function to monitor any table changes then store the original data of the overwritten item in S3. When an item is updated, it should only send a copy of the item's previous value to an S3 bucket and maintain the new value in the DynamoDB table. Which StreamViewType is the MOST suitable one to use in the DynamoDB configuration to fulfill this scenario?
 
**DynamoDB Streams provides a time-ordered sequence of item level changes in any DynamoDB table**. The changes are de-duplicated and stored for 24 hours. Applications can access this log and view the data items as they appeared before and after they were modified, in near real time.
 
Amazon DynamoDB is also integrated with AWS Lambda so that you can create triggers—pieces of code that automatically respond to events in DynamoDB Streams. With triggers, you can build applications that react to data modifications in DynamoDB tables.

When an item in the table is modified, StreamViewType determines what information are written to the stream for this table. Valid values for StreamViewType are KEYS_ONLY, NEW_IMAGE, OLD_IMAGE, and NEW_AND_OLD_IMAGES.

For the OLD_IMAGE type, the entire item which has the previous value as it appeared before it was modified is written to the stream. Hence, this is the correct answer in this scenario.
 
KEYS_ONLY is incorrect because it will only write the key attributes of the modified item to the stream. This choice is wrong since the question states that values should be copied as well.

NEW_IMAGE is incorrect because it will configure the stream to write the entire item with its new value as it appears after it was modified. This choice is wrong since the stream should capture the item's pre-modified values.

NEW_AND_OLD_IMAGES is incorrect because although it writes the new values of the item in the stream, it also includes the old one as well. Since this type will send both the new and the old item images of the item to the stream, this option is wrong. Remember that it should only send a copy of the item's previous value to the S3 bucket, and not the new value in the DynamoDB table. The most suitable one to use here is the OLD_IMAGE type.

### A developer is instructed to configure a worker daemon to queue messages based on a specific schedule using a worker environment hosted in Elastic Beanstalk. Periodic tasks should be defined to automatically add jobs to your worker environment's queue at a regular interval. Which configuration file should the developer add in the source bundle to meet the above requirement?
 
AWS resources created for a worker environment tier include an Auto Scaling group, one or more Amazon EC2 instances, and an IAM role. For the worker environment tier, Elastic Beanstalk also creates and provisions an Amazon SQS queue if you don’t already have one. When you launch a worker environment tier, Elastic Beanstalk installs the necessary support files for your programming language of choice and a daemon on each EC2 instance in the Auto Scaling group.

The daemon is responsible for pulling requests from an Amazon SQS queue and then sending the data to the web application running in the worker environment tier that will process those messages. If you have multiple instances in your worker environment tier, each instance has its own daemon, but they all read from the same Amazon SQS queue.
 
You can define periodic tasks in a file named cron.yaml in your source bundle to add jobs to your worker environment's queue automatically at a regular interval. For example, you can configure and upload a cron.yaml file which creates two periodic tasks: one that runs every 12 hours and a second that runs at 11pm UTC every day.

Hence, using the cron.yaml is the correct configuration file to be used in this scenario.
 
### There has been reports that your application, which has a MySQL RDS database, becomes unresponsive from time to time. You were instructed to collect all SQL statements that took longer to execute for troubleshooting. What should you do to properly troubleshoot this issue with the LEAST amount of effort?
 
You can monitor the MySQL error log, slow query log, and the general log. The MySQL error log is generated by default; you can generate the slow query and general logs by setting parameters in your DB parameter group. Amazon RDS rotates all of the MySQL log files; the intervals for each type are given following.

You can monitor the MySQL logs directly through the Amazon RDS console, Amazon RDS API, AWS CLI, or AWS SDKs. You can also access MySQL logs by directing the logs to a database table in the main database and querying that table. You can use the mysqlbinlog utility to download a binary log.

Hence, enabling the slow query log in RDS is the correct answer.

Instrumenting your application using the X-Ray SDK is incorrect because although this can help you troubleshoot your application, this entails a lot of effort to implement. Remember that the question specifically asks for the solution with the least amount of effort.

Enabling active tracing using AWS X-Ray is incorrect because this feature is only available in Lambda, but not in RDS.

### A company that sells smart security cameras uses an S3 bucket behind a CloudFront web distribution to store its static content, which they share to their customers around the world. They recently released a new firmware update that is intended to be used only by its premium customers. Any unauthorized access should be denied and the user authentication process must have a minimal latency. How can a developer refactor the current set up to achieve this requirement with the MOST efficient solution?
 
Lambda@Edge is a feature of Amazon CloudFront that lets you run code closer to users of your application, which improves performance and reduces latency. With Lambda@Edge, you don't have to provision or manage infrastructure in multiple locations around the world. You pay only for the compute time you consume - there is no charge when your code is not running.

With Lambda@Edge, you can enrich your web applications by making them globally distributed and improving their performance — all with zero server administration. Lambda@Edge runs your code in response to events generated by the Amazon CloudFront content delivery network (CDN). Just upload your code to AWS Lambda, which takes care of everything required to run and scale your code with high availability at an AWS location closest to your end user.
 
You can use Lambda@Edge to help authenticate and authorize users for the premium pay-wall content on your website, filtering out unauthorized requests before they reach your origin infrastructure. For example, you can trigger a Lambda function to authorize each viewer request by calling authentication and user management service such as Amazon Cognito.
 
(Using Signed URLs and Signed Cookies in CloudFront to distribute the firmware update file is incorrect because although this solution provides a way to authenticate the premium users for the private content, the process of authentication has a significant latency in comparison to the Lambda@Edge solution. In this option, you have to refactor your application (which is deployed to a specific AWS region) to either create and distribute signed URLs to authenticated users or to send Set-Cookie headers that set signed cookies on the viewers for authenticated users. This will cause the latency, which could have been improved if the authentication logic resides on CloudFront edge locations using Lambda@Edge.)
 
### A developer is working on a Lambda function which has an event source mapping to process requests from API Gateway. The function will consistently have 10 requests per second and it will take a maximum of 50 seconds to complete each request. What should the developer do to prevent the function from throttling?
 
If you create a Lambda function to process events from event sources that aren't poll-based (for example, Lambda can process every event from other sources, like Amazon S3 or API Gateway), each published event is a unit of work, in parallel, up to your account limits. Therefore, the number of invocations these event sources make influences the concurrency.

You can use this formula to estimate the capacity used by your function:
 
_concurrent executions = (invocations per second) x (average execution duration in seconds)_
 
 For example, consider a Lambda function that processes Amazon S3 events. Suppose that the Lambda function takes on average three seconds and Amazon S3 publishes 10 events per second. Then, you will have 30 concurrent executions of your Lambda function. See the calculation shown below to visualize the process: 

AWS Lambda dynamically scales function execution in response to increased traffic, up to your concurrency limit. Under sustained load, your function's concurrency bursts to an initial level between 500 and 3000 concurrent executions that varies per region. After the initial burst, the function's capacity increases by an additional 500 concurrent executions each minute until either the load is accommodated, or the total concurrency of all functions in the region hits the limit.

By default, AWS Lambda limits the total concurrent executions across all functions within a given region to 1000. This limit can be raised by requesting for AWS to increase the limit of the concurrent executions of your account. 

Since the expected concurrent executions of the Lambda function is well within the default concurrency limit, the best thing to do here is to do nothing since Lambda will automatically scale to handle the load.
 
### A developer is working on a photo-sharing application that can automatically add filters to the images uploaded by its users. For every new image that the user uploads, it will be handled by an image processing application hosted in a Lambda function. The processed image would then be stored in an S3 bucket. If the upload was successful, the application will return a prompt telling the user that the upload is successful. However, the entire processing typically takes an average of 5 minutes to complete, which causes the application to become unresponsive. Which of the following is the MOST suitable and cost-effective option which will prevent your application from being unresponsive?
 
 AWS Lambda supports synchronous and asynchronous invocation of a Lambda function. You can control the invocation type only when you invoke a Lambda function (referred to as on-demand invocation). The following examples illustrate on-demand invocations:

- Your custom application invokes a Lambda function.

- You manually invoke a Lambda function (for example, using the AWS CLI) for testing purposes.

In both cases, you invoke your Lambda function using the Invoke operation, and you can specify the invocation type as synchronous or asynchronous.

When you use AWS services as a trigger, the invocation type is predetermined for each service. You have no control over the invocation type that these event sources use when they invoke your Lambda function.

In the Invoke API, you have 3 options to choose from for the InvocationType:

RequestResponse (default) - Invoke the function synchronously. Keep the connection open until the function returns a response or times out. The API response includes the function response and additional data.

Event - Invoke the function asynchronously. Send events that fail multiple times to the function's dead-letter queue (if it's configured). The API response only includes a status code.

DryRun - Validate parameter values and verify that the user or role has permission to invoke the function.

In the scenario, we can modify the application to invoke the image processing Lambda function whenever it receives an image from a user. You can invoke Lambda functions asynchronously by changing its invocation type to Event. Below is a sample diagram of how we can do this.

![image](https://user-images.githubusercontent.com/44325167/133987127-d53cf9a9-80c2-4c41-af3c-4267539154de.png)
 
 If a user uploads a photo, the application will convert it to base64 and send that as a payload when invoking the Lambda function. Since the Lambda function is invoked asynchronously, AWS Lambda will temporarily place the event in its internal event queue. Once the event is queued successfully, a 202 status code will be sent as a response to the client indicating that his request has been accepted for processing. The user won't have to wait for any payload from the Lambda function.

Hence, the correct answer is to configure the application to asynchronously process the requests and change the invocation type of the Lambda function to Event.

### A developer is moving a legacy web application from their on-premises data center to AWS. The application is concurrently used by thousands of people and it stores the user session state in memory. Its on-premises server usually reaches 100% CPU Utilization every time there is a surge on the number of people accessing the application.  Which of the following is the best way to re-factor the performance and availability of the application's session management once it is migrated to AWS?
 
Amazon ElastiCache for Redis is a blazing fast in-memory data store that provides sub-millisecond latency to power internet-scale real-time applications. Built on open-source Redis and compatible with the Redis APIs, ElastiCache for Redis works with your Redis clients and uses the open Redis data format to store your data. Your self-managed Redis applications can work seamlessly with ElastiCache for Redis without any code changes. ElastiCache for Redis combines the speed, simplicity, and versatility of open-source Redis with manageability, security, and scalability from Amazon to power the most demanding real-time applications in Gaming, Ad-Tech, E-Commerce, Healthcare, Financial Services, and IoT.
 
 In order to address scalability and provide a shared data storage for sessions that can be accessible from any individual web server, you can abstract the HTTP sessions from the web servers themselves. A common solution to for this is to leverage an In-Memory Key/Value store such as Redis and Memcached. While Key/Value data stores are known to be extremely fast and provide sub-millisecond latency, the added network latency and added cost are the drawbacks. An added benefit of leveraging Key/Value stores is that they can also be utilized to cache any data, not just HTTP sessions, which can help boost the overall performance of your applications.

With Redis, you can keep your data on disk with a point in time snapshot which can be used for archiving or recovery. Redis also lets you create multiple replicas of a Redis primary. This allows you to scale database reads and to have highly available clusters. Hence, the correct answer for this scenario is to use an ElastiCache for Redis cluster to store the user session state of the application.
 
 
### A developer has deployed a Lambda function which will run in various environments such as DEV, TEST, UAT, and PROD. As part of its processing, the function also calls a set of external API services which varies based on the environment. The function must use different endpoints for these external services to properly complete the processing. Which of the following features in Lambda should the developer use to reference the appropriate external endpoint for each environment?
 
Environment variables for Lambda functions enable you to dynamically pass settings to your function code and libraries, without making changes to your code. Environment variables are key-value pairs that you create and modify as part of your function configuration, using either the AWS Lambda Console, the AWS Lambda CLI or the AWS Lambda SDK. AWS Lambda then makes these key-value pairs available to your Lambda function code using standard APIs supported by the language, like process.env for Node.js functions.

You can use environment variables to help libraries know what directory to install files in, where to store outputs, store connection and logging settings, and more. By separating these settings from the application logic, you don't need to update your function code when you need to change the function behavior based on different settings.
 
(Aliases is incorrect because this is just like a pointer to a specific Lambda function version. By using aliases, you can access the Lambda function which the alias is pointing to, without the caller knowing the specific version the alias is pointing to.)
 
### A developer needs to encrypt all objects being uploaded by their application to the S3 bucket to comply with the company's security policy. The bucket will use server-side encryption with Amazon S3-Managed encryption keys (SSE-S3) to encrypt the data using 256-bit Advanced Encryption Standard (AES-256) block cipher. Which of the following request headers should the developer use?
 
**Server-side encryption protects data at rest**. If you use Server-Side Encryption with Amazon S3-Managed Encryption Keys (SSE-S3), Amazon S3 will encrypt each object with a unique key and as an additional safeguard, it encrypts the key itself with a master key that it rotates regularly. Amazon S3 server-side encryption uses one of the strongest block ciphers available, 256-bit Advanced Encryption Standard (AES-256), to encrypt your data.
 
If you need server-side encryption for all of the objects that are stored in a bucket, use a bucket policy. For example, the following bucket policy denies permissions to upload an object unless the request includes the x-amz-server-side-encryption header to request server-side encryption:

![Screen Shot 2021-09-20 at 12 32 21 PM](https://user-images.githubusercontent.com/44325167/133988662-7fa439f2-2e9c-48c2-b76c-6e208007737c.png)
 
 
### An application hosted in an Auto Scaling group of On-Demand EC2 instances is used to process data polled from an SQS queue and the generated output is stored in an S3 bucket. To improve security, you were tasked to ensure that all objects in the S3 bucket are encrypted at rest using server-side encryption with AWS KMS–Managed Keys (SSE-KMS). Which of the following is required to properly implement this requirement?
 
 Server-side encryption is about protecting data at rest. AWS Key Management Service (AWS KMS) is a service that combines secure, highly available hardware and software to provide a key management system scaled for the cloud. AWS KMS uses customer master keys (CMKs) to encrypt your Amazon S3 objects. You use AWS KMS via the AWS Management Console or AWS KMS APIs to centrally create encryption keys, define the policies that control how keys can be used, and audit key usage to prove they are being used correctly. You can use these keys to protect your data in Amazon S3 buckets.

The first time you add an SSE-KMS–encrypted object to a bucket in a region, a default CMK is created for you automatically. This key is used for SSE-KMS encryption unless you select a CMK that you created separately using AWS Key Management Service. Creating your own CMK gives you more flexibility, including the ability to create, rotate, disable, and define access controls, and to audit the encryption keys used to protect your data.
 
Amazon S3 supports bucket policies that you can use if you require server-side encryption for all objects that are stored in your bucket. For example, you can set a bucket policy that denies permission to upload an object (s3:PutObject) to everyone if the request does not include the x-amz-server-side-encryption header requesting server-side encryption with SSE-KMS.

When you upload an object, you can specify the KMS key using the x-amz-server-side-encryption-aws-kms-key-id header which you can use to require a specific KMS key for object encryption. If the header is not present in the request, Amazon S3 assumes the default KMS key. Regardless, the KMS key ID that Amazon S3 uses for object encryption must match the KMS key ID in the policy, otherwise Amazon S3 denies the request.

Therefore, the correct answer is: **Add a bucket policy which denies any s3:PutObject action unless the request includes the x-amz-server-side-encryption header**.

### A serverless application composed of Lambda, API Gateway, and DynamoDB has been running without any issues for quite some time. As part of the IT compliance of the company, a developer was instructed to ensure that all of the new changes made to the items in DynamoDB are recorded and stored to another DynamoDB table in another region. In this scenario, which of the following is the MOST ideal way to comply with the given requirements?
 
**DynamoDB Streams** enables solutions such as these, and many others. DynamoDB Streams captures a time-ordered sequence of item-level modifications in any DynamoDB table, and stores this information in a log for up to 24 hours. Applications can access this log and view the data items as they appeared before and after they were modified, in near real time.

A DynamoDB stream is an ordered flow of information about changes to items in an Amazon DynamoDB table. When you enable a stream on a table, DynamoDB captures information about every modification to data items in the table.

Whenever an application creates, updates, or deletes items in the table, DynamoDB Streams writes a stream record with the primary key attribute(s) of the items that were modified. A stream record contains information about a data modification to a single item in a DynamoDB table. You can configure the stream so that the stream records capture additional information, such as the "before" and "after" images of modified items.
 
(Integrating CloudWatch Events to track the changes to DynamoDB is incorrect because the CloudWatch Events service is not ideal to use for tracking changes to your DynamoDB table. The most appropriate feature that you should use is DynamoDB Streams.)
 
### A serverless application, which is composed of Lambda functions integrated with API Gateway and DynamoDB, processes ad hoc requests that are sent by its users. Due to the recent spike in incoming traffic, some of your customers are complaining that they are getting HTTP 504 errors from time to time. Which of the following is the MOST likely cause of this issue?
 
 A gateway response is identified by a response type defined by API Gateway. The response consists of an HTTP status code, a set of additional headers that are specified by parameter mappings, and a payload that is generated by a non-VTL (Apache Velocity Template Language) mapping template.
 
You can set up a gateway response for a supported response type at the API level. Whenever API Gateway returns a response of the type, the header mappings and payload mapping templates defined in the gateway response are applied to return the mapped results to the API caller.

The following are the Gateway response types which are associated with the HTTP 504 error in API Gateway: 

INTEGRATION_FAILURE - The gateway response for an integration failed error. If the response type is unspecified, this response defaults to the DEFAULT_5XX type.

INTEGRATION_TIMEOUT - The gateway response for an integration timed out error. If the response type is unspecified, this response defaults to the DEFAULT_5XX type.

For the integration timeout, the range is from 50 milliseconds to 29 seconds for all integration types, including Lambda, Lambda proxy, HTTP, HTTP proxy, and AWS integrations.

In this scenario, there is an issue where the users are getting HTTP 504 errors in the serverless application. This means the Lambda function is working fine at times but there are instances when it throws an error. Based on this analysis, the most likely cause of the issue is the INTEGRATION_TIMEOUT error since you will only get an INTEGRATION_FAILURE error if your AWS Lambda integration does not work at all in the first place.

Hence, the root cause of this issue is that the API Gateway request has timed out because the underlying Lambda function has been running for more than 29 seconds. 

### Your application is processing one Kinesis data stream which has four shards, and each instance has one KCL worker. To scale up processing in your application, you reshard your stream to increase the number of open shards to six. What is the MAXIMUM number of EC2 instances that you should launch to achieve optimum performance?
 
Resharding enables you to increase or decrease the number of shards in a stream in order to adapt to changes in the rate of data flowing through the stream. The Kinesis Client Library (KCL) ensures that for every shard there is a record processor running and processing that shard. It also tracks the shards in the stream using an Amazon DynamoDB table.

Typically, when you use the KCL, you should ensure that the number of instances does not exceed the number of shards (except for failure standby purposes). Each shard is processed by exactly one KCL worker and has exactly one corresponding record processor, so you never need multiple instances to process one shard. However, one worker can process any number of shards, so it's fine if the number of shards exceeds the number of instances.

To scale up processing in your application, you should test a combination of these approaches:

 - Increasing the instance size (because all record processors run in parallel within a process)

 - Increasing the number of instances up to the maximum number of open shards (because shards can be processed independently)

 - Increasing the number of shards (which increases the level of parallelism)


Thus, the maximum number of instances you can launch is 6, to match the number of open shards in a ratio of 1:1.

Although you can launch 3 instances in which each instance handles 2 shards, this is not the maximum number of instances you can deploy for your application. Hence, this option is incorrect. Take note that the maximum number of your instances is not half the number of open shards.

Just like the above option, you can also launch 5 instances in which each instance handles 3 shards. However, this is not the maximum number of instances you can launch. Keep in mind that the maximum number of your instances can be equal to the number of open shards of the Kinesis stream. Therefore, this option is also incorrect.

Launching 12 instances is incorrect because you should ensure that the number of instances does not exceed the number of open shards. The maximum number of instances that you should deploy is 6.
 
### An application performs various workflows and processes long-running tasks that take a long time to complete. The users are complaining that the application is unresponsive since the workflow substantially increased the time it takes to complete a user request. Which of the following is the BEST way to improve the performance of the application?
 
If your application performs operations or workflows that take a long time to complete, you can offload those tasks to a dedicated worker environment. Decoupling your web application front end from a process that performs blocking operations is a common way to ensure that your application stays responsive under load.

A long-running task is anything that substantially increases the time it takes to complete a request, such as processing images or videos, sending email, or generating a ZIP archive. These operations can take only a second or two to complete, but a delay of a few seconds is a lot for a web request that would otherwise complete in less than 500 ms.
 
One option is to spawn a worker process locally, return success, and process the task asynchronously. This works if your instance can keep up with all of the tasks sent to it. Under high load, however, an instance can become overwhelmed with background tasks and become unresponsive to higher priority requests. If individual users can generate multiple tasks, the increase in load might not correspond to an increase in users, making it hard to scale out your web server tier effectively.

To avoid running long-running tasks locally, you can use the AWS SDK for your programming language to send them to an Amazon Simple Queue Service (Amazon SQS) queue, and run the process that performs them on a separate set of instances. You then design these worker instances to take items from the queue only when they have the capacity to run them, preventing them from becoming overwhelmed.

Elastic Beanstalk worker environments simplify this process by managing the Amazon SQS queue and running a daemon process on each instance that reads from the queue for you. When the daemon pulls an item from the queue, it sends an HTTP POST request locally to http://localhost/ on port 80 with the contents of the queue message in the body. All that your application needs to do is perform the long-running task in response to the POST. You can configure the daemon to post to a different path, use a MIME type other than application/JSON, connect to an existing queue, or customize connections (maximum concurrent requests), timeouts, and retries.

Hence, the best solution to meet the requirements of this scenario is to use an Elastic Beanstalk worker environment to process the tasks asynchronously.
 
### Your serverless AWS Lambda functions are integrated with Amazon API gateway using Lambda proxy integration. The API caching feature is enabled in the API Gateway with a TTL value of 300 seconds. A client would like to fetch the latest data from your endpoints every time a request is sent and invalidate the existing cache. What should the client do in order to get the latest data?
 
 A client of your API can invalidate an existing cache entry and reload it from the integration endpoint for individual requests. The client must send a request that contains the Cache-Control: max-age=0 header. 

The client receives the response directly from the integration endpoint instead of the cache, provided that the client is authorized to do so. This replaces the existing cache entry with the new response, which is fetched from the integration endpoint.

### You are deploying a serverless application composed of Lambda, API Gateway, CloudFront, and DynamoDB using CloudFormation. The AWS SAM syntax should be used to declare resources in your template which requires you to specify the version of the AWS Serverless Application Model (AWS SAM). Which of the following sections is required, aside from the Resources section, that should be in your CloudFormation template?
 
 For serverless applications (also referred to as Lambda-based applications), the optional Transform section specifies the version of the AWS Serverless Application Model (AWS SAM) to use. When you specify a transform, you can use AWS SAM syntax to declare resources in your template. The model defines the syntax that you can use and how it is processed.

This section specifies one or more macros that AWS CloudFormation uses to process your template. The Transform section builds on the simple, declarative language of AWS CloudFormation with a powerful macro system.

You can declare one or more macros within a template. AWS CloudFormation executes macros in the order that they are specified. When you create a change set, AWS CloudFormation generates a change set that includes the processed template content. You can then review the changes and execute the change set.

AWS CloudFormation also supports the AWS::Serverless and AWS::Include transforms, which are macros hosted by AWS CloudFormation. AWS CloudFormation treats these transforms the same as any macros you create in terms of execution order and scope.

Therefore, the Transform section should be the correct one to be added your template.
 
### An online stock trading platform is hosted in an Auto Scaling group of EC2 instances with an Application Load Balancer in front to evenly distribute the incoming traffic. The developer must capture information about the IP traffic going to and from network interfaces in your VPC to comply with financial regulatory requirements. Which of the following options should the developer do to meet the requirement?
 
**VPC Flow Logs** is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC. Flow log data can be published to Amazon CloudWatch Logs and Amazon S3. After you've created a flow log, you can retrieve and view its data in the chosen destination.

 ![image](https://user-images.githubusercontent.com/44325167/133995044-fe50fd48-0e5b-4aad-a9cd-60e1ca331b79.png)

Flow logs can help you with a number of tasks; for example, to troubleshoot why specific traffic is not reaching an instance, which in turn helps you diagnose overly restrictive security group rules. You can also use flow logs as a security tool to monitor the traffic that is reaching your instance. CloudWatch Logs charges apply when using flow logs, whether you send them to CloudWatch Logs or to Amazon S3.

Hence, you should create a flow log in your VPC to capture information about the IP traffic going to and from network interfaces in your VPC.

(Using CloudTrail logs to track all API calls and capture information about the IP traffic going to and from your VPC is incorrect because although you can indeed use CloudTrail to track the API call, it can't capture information about the IP traffic of your VPC.) 
 
### A developer is instructed to set up a new serverless architecture composed of AWS Lambda, API Gateway, and DynamoDB in a single stack. The new architecture should allow the developer to locally build, test, and debug serverless applications. Which of the following should the developer use to satisfy the above requirement?
 
 The AWS Serverless Application Model (AWS SAM) is an open-source framework that you can use to build serverless applications on AWS. It consists of the AWS SAM template specification that you use to define your serverless applications, and the AWS SAM command line interface (AWS SAM CLI) that you use to build, test, and deploy your serverless applications.

Because AWS SAM is an extension of AWS CloudFormation, you get the reliable deployment capabilities of AWS CloudFormation. You can define resources by using AWS CloudFormation in your AWS SAM template. Also, you can use the full suite of resources, intrinsic functions, and other template features that are available in AWS CloudFormation.

You can use AWS SAM with a suite of AWS tools for building serverless applications. The AWS SAM CLI lets you locally build, test, and debug serverless applications that are defined by AWS SAM templates. The CLI provides a Lambda-like execution environment locally. It helps you catch issues upfront by providing parity with the actual Lambda execution environment. To step through and debug your code to understand what the code is doing, you can use AWS SAM with AWS toolkits like the AWS Toolkit for JetBrains, AWS Toolkit for PyCharm, AWS Toolkit for IntelliJ, and AWS Toolkit for Visual Studio Code. This tightens the feedback loop by making it possible for you to find and troubleshoot issues that you might run into in the cloud.

Therefore, the most suitable service to use in this scenario is AWS SAM.
 
 (Elastic Beanstalk is incorrect because this service is not suitable for deploying serverless applications. In addition, it doesn't have the capability to locally build, test, and debug your serverless applications as effectively as what AWS SAM can do.) 
 
### A mission-critical application is required to have a monitoring system which can provide immediate insight into its sub-minute activity. You are required to collect the data of all of the users who are currently logged in to the system every 10 seconds.  Which of the following options is the MOST suitable solution that you should do to meet the above requirements?
 
You can publish your own metrics to CloudWatch using the AWS CLI or an API. You can view statistical graphs of your published metrics with the AWS Management Console. CloudWatch stores data about a metric as a series of data points. Each data point has an associated time stamp. You can even publish an aggregated set of data points called a statistic set.

![image](https://user-images.githubusercontent.com/44325167/133997326-408822a1-30de-45a9-a965-20119a10db59.png)
 
Each metric is one of the following:

- Standard resolution, with data having a one-minute granularity

- High resolution, with data at a granularity of one second

Metrics produced by AWS services are standard resolution by default. When you publish a custom metric, you can define it as either standard resolution or high resolution. When you publish a high-resolution metric, CloudWatch stores it with a resolution of 1 second, and you can read and retrieve it with a period of 1 second, 5 seconds, 10 seconds, 30 seconds, or any multiple of 60 seconds.

High-resolution metrics can give you more immediate insight into your application's sub-minute activity. Keep in mind that every PutMetricData call for a custom metric is charged, so calling PutMetricData more often on a high-resolution metric can lead to higher charges.

Therefore, the correct answer in this scenario is to publish a high-resolution custom metric to CloudWatch.
 
(The option that says: Enable detailed monitoring is incorrect because it will only store metric data in one-minute granularity. Moreover, you have to publish a custom metric for this scenario since the type of data that you have to monitor is specific only to your application.) 
 
### A programmer is developing a Node.js application which will be run in a Linux server on their on-premises data center. The application will access various AWS services such as S3, DynamoDB, and ElastiCache using the AWS SDK. Which of the following is the MOST suitable way to provide access to the developer in order to accomplish the specified task?
 
 If you have resources that are running inside AWS, that need programmatic access to various AWS services,then the best practice is to always use IAM roles. However, for applications running outside of an AWS environment, these will need access keys for programmatic access to AWS resources. For example, monitoring tools running on-premises and third-party automation tools will need access keys.

Access keys are long-term credentials for an IAM user or the AWS account root user. You can use access keys to sign programmatic requests to the AWS CLI or AWS API (directly or using the AWS SDK).
 
 In order to use the AWS SDK for your application, you have to create your credentials file first at ~/.aws/credentials for Linux servers or at C:\Users\USER_NAME\.aws\credentials for Windows users and then save your access keys.

Hence, the correct answer is: **Go to the AWS Console and create a new IAM user with programmatic access. In the application server, create the credentials file at ~/.aws/credentials with the access keys of the IAM user.**
 
### You are managing a distributed system which is composed of an Application Load Balancer, SQS queue, and an Auto Scaling group of EC2 instances. The system has been integrated with CloudFront to better serve their clients around the globe. To improve the security of your in-flight data, you were instructed to establish an end-to-end SSL connection between your origin and your end users. How can you meet this requirement using CloudFront? (Select TWO.)
 
For web distributions, you can configure CloudFront to require that viewers use HTTPS to request your objects, so connections are encrypted when CloudFront communicates with viewers. You can also configure CloudFront to use HTTPS to get objects from your origin so connections are encrypted when CloudFront communicates with your origin.

If you configure CloudFront to require HTTPS both to communicate with viewers and to communicate with your origin, here's what happens when CloudFront receives a request for an object. The process works basically the same way whether your origin is an Amazon S3 bucket or a custom origin such as an HTTP/S server:

1. A viewer submits an HTTPS request to CloudFront. There's some SSL/TLS negotiation here between the viewer and CloudFront. In the end, the viewer submits the request in an encrypted format.

2. If the object is in the CloudFront edge cache, CloudFront encrypts the response and returns it to the viewer, and the viewer decrypts it.

3. If the object is not in the CloudFront cache, CloudFront performs SSL/TLS negotiation with your origin and, when the negotiation is complete, forwards the request to your origin in an encrypted format.

4. Your origin decrypts the request, encrypts the requested object, and returns the object to CloudFront.

5. CloudFront decrypts the response, re-encrypts it, and forwards the object to the viewer. CloudFront also saves the object in the edge cache so that the object is available the next time it's requested.

6. The viewer decrypts the response.

 You can configure one or more cache behaviors in your CloudFront distribution to require HTTPS for communication between viewers and CloudFront. You also can configure one or more cache behaviors to allow both HTTP and HTTPS, so that CloudFront requires HTTPS for some objects but not for others.

To implement this setup, you have to change the Origin Protocol Policy setting for the applicable origins in your distribution. If you're using the domain name that CloudFront assigned to your distribution, such as dtut0rial5d0j0.cloudfront.net, you change the Viewer Protocol Policy setting for one or more cache behaviors to require HTTPS communication. With this configuration, CloudFront provides the SSL/TLS certificate.

Hence, configuring the Origin Protocol Policy as well as the Viewer Protocol Policy are the correct answers in this scenario.
 

### A developer uses AWS SAM templates to deploy a serverless application. He needs to embed the application from the AWS Serverless Application Repository or from an S3 bucket as a nested application. Which of the following resource type is the most SUITABLE one that the developer should use?
 
A serverless application can include one or more nested applications. You can deploy a nested application as a stand-alone artifact or as a component of a larger application.

As serverless architectures grow, common patterns emerge in which the same components are defined in multiple application templates. You can now separate out common patterns as dedicated applications, and then nest them as part of new or existing application templates. With nested applications, you can stay more focused on the business logic that's unique to your application.

To define a nested application in your serverless application, use the AWS::Serverless::Application resource type.
 
### You have created a Node.js Lambda function that updates a DynamoDB table and sends an email notification via Amazon SNS. However, upon testing, the function is not working as expected. Which of the following is the BEST way to troubleshoot this issue?

AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture. With X-Ray, you can understand how your application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors. X-Ray provides an end-to-end view of requests as they travel through your application, and shows a map of your application’s underlying components.

You can use X-Ray to analyze both applications in development and in production, from simple three-tier applications to complex microservices applications consisting of thousands of services.

AWS X-Ray works with Amazon EC2, Amazon EC2 Container Service (Amazon ECS), AWS Lambda, and AWS Elastic Beanstalk. You can use X-Ray with applications written in Java, Node.js, and .NET that are deployed on these services.
 
 ### A developer is building a new Docker application using ECS. She needs to allow containers to access ports on the host container instance to send or receive traffic using port mapping. Which component of ECS should the developer configure to properly implement this task?
 
Port mappings allow containers to access ports on the host container instance to send or receive traffic. Port mappings are specified as part of the container definition which can be configured in the task definition.

For task definitions that use the awsvpc network mode, you should only specify the containerPort. The hostPort can be left blank or it must be the same value as the containerPort.

Port mappings on Windows use the NetNAT gateway address rather than localhost. There is no loopback for port mappings on Windows, so you cannot access a container's mapped port from the host itself.

Hence, the correct component that the developer should configure is Task Definition.
 
### Your company uses Elastic Beanstalk to manage a web application. You were instructed to configure the Elastic Beanstalk environment's deployment policy to launch new EC2 instances, and then deploy the new version of your application only to these new resources. Which of the following deployment methods can you use to meet this required configuration? (Select TWO.)
 
In ElasticBeanstalk, you can choose from a variety of deployment methods: 

- All at once – Deploy the new version to all instances simultaneously. All instances in your environment are out of service for a short time while the deployment occurs.

- Rolling – Deploy the new version in batches. Each batch is taken out of service during the deployment phase, reducing your environment's capacity by the number of instances in a batch.

- Rolling with additional batch – Deploy the new version in batches, but first launch a new batch of instances to ensure full capacity during the deployment process.

- Immutable – Deploy the new version to a fresh group of instances by performing an immutable update.

- Blue/Green - Deploy the new version to a separate environment, and then swap CNAMEs of the two environments to redirect traffic to the new version instantly.
 
All at once is incorrect because this will deploy the new version to all existing instances only and will not create new EC2 instances. 

Rolling is incorrect because this will deploy the new version in batches only to existing instances, without provisioning new resources. 

Rolling with additional batch is incorrect because although it does deploy the new version to a new batch of instances, it also deploys the package to the existing instances.
 
 ### A mobile app is using a backend API hosted in AWS. You want to develop a push notification feature that can send messages directly to mobile apps whenever there is a new version of the app available. The notification message can include a link to download and install the update. Which of the following is the BEST service to use to develop this feature?
 
 Amazon Simple Notification Service (Amazon SNS) is a web service that coordinates and manages the delivery or sending of messages to subscribing endpoints or clients. In Amazon SNS, there are two types of clients —publishers and subscribers — also referred to as producers and consumers. Publishers communicate asynchronously with subscribers by producing and sending a message to a topic, which is a logical access point and communication channel. Subscribers (i.e., web servers, email addresses, Amazon SQS queues, AWS Lambda functions) consume or receive the message or notification over one of the supported protocols (i.e., Amazon SQS, HTTP/S, email, SMS, Lambda) when they are subscribed to the topic.

With Amazon SNS, you have the ability to send push notification messages directly to apps on mobile devices. Push notification messages sent to a mobile endpoint can appear in the mobile app as message alerts, badge updates, or even sound alerts.
 
 ![image](https://user-images.githubusercontent.com/44325167/134002325-e104dba4-3dac-4927-bd03-3c7f6b8cf3d3.png)
 
Push notification services such as APNS and FCM maintain a connection with each app and associated mobile device registered to use their service. When an app and mobile device register, the push notification service returns a device token. Amazon SNS uses the device token to create a mobile endpoint, to which it can send direct push notification messages. In order for Amazon SNS to communicate with the different push notification services, you submit your push notification service credentials to Amazon SNS to be used on your behalf.

Hence, the correct answer is SNS in this scenario.
 
### A web application is uploading large files, which are over 4 GB in size, in an S3 bucket called data.tutorialsdojo.com every 30 minutes. You want to minimize the time required to upload each file. Which of the following should you do to minimize upload time?
 
Multipart upload allows you to upload a single object as a set of parts. Each part is a contiguous portion of the object's data. You can upload these object parts independently and in any order. If transmission of any part fails, you can retransmit that part without affecting other parts. After all parts of your object are uploaded, Amazon S3 assembles these parts and creates the object. In general, when your object size reaches 100 MB, you should consider using multipart uploads instead of uploading the object in a single operation.
 
 ![image](https://user-images.githubusercontent.com/44325167/134002588-f3690085-3ef1-496a-ae81-7165e0947e74.png)
 
 Using multipart upload provides the following advantages:

    - Improved throughput - You can upload parts in parallel to improve throughput.

    - Quick recovery from any network issues - Smaller part size minimizes the impact of restarting a failed upload due to a network error.

    - Pause and resume object uploads - You can upload object parts over time. Once you initiate a multipart upload there is no expiry; you must explicitly complete or abort the multipart upload.

    - Begin an upload before you know the final object size - You can upload an object as you are creating it.

Hence, using the Multipart Upload API is the correct answer in this scenario.

### A Software Engineer is refactoring a Lambda function, which currently uses a public GraphQL API from the Internet as part of its processing. The new requirement states that the function should process the data and store the results to a database hosted in your VPC. The additional VPC-specific information has already been configured in the function and the database connection has been successfully established. However, after testing, he found that the function can't connect to the Internet anymore. Which of the following should the Software Engineer do to fix this issue? (Select TWO.)

 AWS Lambda uses the VPC information you provide to set up ENIs that allow your Lambda function to access VPC resources. Each ENI is assigned a private IP address from the IP address range within the subnets you specify but is not assigned any public IP addresses.

![image](https://user-images.githubusercontent.com/44325167/134155643-5a865799-9854-448a-8918-75165e57c38b.png)
 
 Therefore, if your Lambda function requires Internet access (for example, to access AWS services that don't have VPC endpoints ), you can configure a NAT instance inside your VPC or you can use the Amazon VPC NAT gateway. You cannot use an Internet gateway attached to your VPC, since that requires the ENI to have public IP addresses. 

If your Lambda function needs Internet access, just as described in this scenario, do not attach it to a public subnet or to a private subnet without Internet access. Instead, attach it only to private subnets with Internet access through a NAT instance or add a NAT gateway to your VPC. You should also ensure that the associated security group of the Lambda function allows outbound connections. 
 
### A web application is using an ElastiCache cluster that is suffering from cache churn, which means that a lot of cache data in the cluster are never read. There is a requirement to reconfigure the application to retrieve the data from the database only in the event that there is a cache miss. Which of the following caching strategy is the MOST suitable that the developer should implement?
 
Amazon ElastiCache is an in-memory key/value store that sits between your application and the data store (database) that it accesses. Whenever your application requests data, it first makes the request to the ElastiCache cache.

**Lazy Loading,** as its name implies, is a caching strategy that loads data into the cache only when necessary. Here is how it works:
 
 ![image](https://user-images.githubusercontent.com/44325167/134156063-fc26ec85-a4e9-403f-9cc5-8fd379c7c56c.png)
 
- If the data exists in the cache and is current, ElastiCache returns the data to your application. This event is also called "Cache Hit".

- If there is a "Cache Miss", or in other words, the data does not exist in the cache, or the data in the cache has expired, then your application requests the data from your data store which returns the data to your application. Your application then writes the data received from the store to the cache so it can be more quickly retrieved next time it is requested.
 
Since the Lazy Loading strategy satisfies the requirement described in the scenario, this option is correct.
 
### A Lambda function has been integrated with DynamoDB Streams as its event source. There has been a new version of the function that needs to be deployed using CodeDeploy where the traffic must be shifted in two increments. It should shift 10 percent of the incoming traffic to the new version in the first increment and then the remaining 90 percent should be deployed five minutes later. Which of the following deployment configurations is the MOST suitable to satisfy this requirement?
 
**CodeDeploy** is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS services. CodeDeploy can deploy application content that runs on a server and is stored in Amazon S3 buckets, GitHub repositories, or Bitbucket repositories. CodeDeploy can also deploy a serverless Lambda function. You do not need to make changes to your existing code before you can use CodeDeploy.

When you deploy to an AWS Lambda compute platform, the deployment configuration specifies the way traffic is shifted to the new Lambda function versions in your application.
 
In a **Canary** deployment configuration, the traffic is shifted in two increments. You can choose from predefined canary options that specify the percentage of traffic shifted to your updated Lambda function version in the first increment and the interval, in minutes, before the remaining traffic is shifted in the second increment. Hence, this is the correct answer which will satisfy the requirement for the given scenario.
 
### You want to update a Lambda function on your production environment and ensure that when you publish the updated version, you still have a quick way to roll back to the older version in case you encountered a problem. To prevent any sudden user interruptions, you want to gradually increase the traffic going to the new version. Which of the following implementation is the BEST option to use? 
 
By default, an alias points to a single Lambda function version. When the alias is updated to point to a different function version, incoming request traffic in turn instantly points to the updated version. This exposes that alias to any potential instabilities introduced by the new version. To minimize this impact, you can implement the routing-config parameter of the Lambda alias that allows you to point to two different versions of the Lambda function and dictate what percentage of incoming traffic is sent to each version.

For example, you can specify that only 2 percent of incoming traffic is routed to the new version while you analyze its readiness for a production environment, while the remaining 98 percent is routed to the original version. As the new version matures, you can gradually update the ratio as necessary until you have determined that the new version is stable. You can then update the alias to route all traffic to the new version.

You can point an alias to a maximum of two Lambda function versions. In addition:

- Both versions must have the same IAM execution role.

- Both versions must have the same AWS Lambda Function Dead Letter Queues configuration, or no DLQ configuration.

- When pointing an alias to more than one version, the alias cannot point to $LATEST.

Hence, using **Traffic Shifting** for Lambda Aliases is the correct answer. 
 
 
 ### A reporting application is hosted in Elastic Beanstalk and uses DynamoDB as its database. If a user requests for data, it scans the entire table and returns the requested data. In the coming weeks, it is expected that the table will grow due to the surge of new users and requested reports. Which of the following should be done as a preparation to improve the performance of the application with minimal cost? (Select TWO.)

In general, Scan operations are less efficient than other operations in DynamoDB. A Scan operation always scans the entire table or secondary index. It then filters out values to provide the result you want, essentially adding the extra step of removing data from the result set.

If possible, you should avoid using a Scan operation on a large table or index with a filter that removes many results. Also, as a table or index grows, the Scan operation slows. The Scan operation examines every item for the requested values and can use up the provisioned throughput for a large table or index in a single operation. For faster response times, design your tables and indexes so that your applications can use **Query** instead of Scan. For tables, you can also consider using the GetItem and BatchGetItem APIs.
 
Alternatively, you can refactor your application to use Scan operations in a way that minimizes the impact on your request rate.  Instead of using a large Scan operation, you can use the following techniques to minimize the impact of a scan on a table's provisioned throughput.

**Reduce page size** - Because a Scan operation reads an entire page (by default, 1 MB), you can reduce the impact of the scan operation by setting a smaller page size. The Scan operation provides a Limit parameter that you can use to set the page size for your request. Each Query or Scan request that has a smaller page size uses fewer read operations and creates a "pause" between each request. For example, suppose that each item is 4 KB and you set the page size to 40 items. A Query request would then consume only 20 eventually consistent read operations or 40 strongly consistent read operations. A larger number of smaller Query or Scan operations would allow your other critical requests to succeed without throttling.
 
 **Isolate scan operations** - DynamoDB is designed for easy scalability. As a result, an application can create tables for distinct purposes, possibly even duplicating content across several tables. You want to perform scans on a table that is not taking "mission-critical" traffic. Some applications handle this load by rotating traffic hourly between two tables—one for critical traffic, and one for bookkeeping. Other applications can do this by performing every write on two tables: a "mission-critical" table, and a "shadow" table.
 
Hence, **using Query operations instead of Scan and reducing the page size** are the correct answers.
 
### An application hosted in an Amazon ECS Cluster processes a large stream of data and stores the result to a DynamoDB table. There is an urgent requirement to detect new entries in the table then automatically trigger a Lambda function to run some tests to verify the processed data. Which of the following options can satisfy the requirement with minimal configuration?
 
Amazon DynamoDB is integrated with AWS Lambda so that you can create triggers—pieces of code that automatically respond to events in **DynamoDB Streams**. With triggers, you can build applications that react to data modifications in DynamoDB tables.

If you enable DynamoDB Streams on a table, you can associate the stream ARN with a Lambda function that you write. Immediately after an item in the table is modified, a new record appears in the table's stream. AWS Lambda polls the stream and invokes your Lambda function synchronously when it detects new stream records.
 
![image](https://user-images.githubusercontent.com/44325167/134159954-a325dbd2-7705-49c9-ac09-dd4af53ec02e.png)
 
You can create a Lambda function which can perform a specific action that you specify, such as sending a notification or initiating a workflow. For instance, you can set up a Lambda function to simply copy each stream record to persistent storage, such as EFS or S3, to create a permanent audit trail of write activity in your table.

Suppose you have a mobile gaming app that writes to a TutorialsDojoCourses table. Whenever the TopCourse attribute of the TutorialsDojoScores table is updated, a corresponding stream record is written to the table's stream. This event could then trigger a Lambda function that posts a congratulatory message on a social media network. (The function would simply ignore any stream records that are not updates to TutorialsDojoCourses or that do not modify the TopCourse attribute.)

Hence, the correct answer is to enable DynamoDB Streams to detect the new entries and automatically trigger the Lambda function.  In this way, the requirement can be met with minimal configuration change as DynamoDB streams can be used as an event source to automatically trigger Lambda functions whenever there is a new entry.

(Setting up a CloudWatch Alarm to automatically trigger the Lambda function whenever a new entry is created in the DynamoDB table is incorrect because CloudWatch Alarms only monitor service metrics, not changes in DynamoDB table data.)
 
 
### An application, which already uses X-Ray, generates thousands of trace data every hour. The developer wants to use a filter expression which will limit the results based on custom attributes or keys that he specifies. How should the developer refactor the application in order to filter the results in the X-Ray console?
 
Even with sampling, a complex application generates a lot of data. The AWS X-Ray console provides an easy-to-navigate view of the service graph. It shows health and performance information that helps you identify issues and opportunities for optimization in your application. For advanced tracing, you can drill down to traces for individual requests, or use filter expressions to find traces related to specific paths or users.

When you instrument your application, the X-Ray SDK records information about incoming and outgoing requests, the AWS resources used, and the application itself. You can add other information to the segment document as annotations and metadata.

Annotations are simple key-value pairs that are indexed for use with filter expressions. Use annotations to record data that you want to use to group traces in the console, or when calling the GetTraceSummaries API. X-Ray indexes up to 50 annotations per trace.

Metadata are key-value pairs with values of any type, including objects and lists, but that are not indexed. Use metadata to record data you want to store in the trace but don't need to use for searching traces. You can view annotations and metadata in the segment or subsegment details in the X-Ray console.

Hence, **adding the custom attributes as annotations in your segment document** is the correct answer.

 
### A recently deployed Lambda function has an intermittent issue in processing customer data. You enabled the active tracing option in order to detect, analyze, and optimize performance issues of your function using the X-Ray service. Which of the following environment variables are used by AWS Lambda to facilitate communication with X-Ray? (Select TWO.)

AWS X-Ray is an AWS service that allows you to detect, analyze, and optimize performance issues with your AWS Lambda applications. X-Ray collects metadata from the Lambda service and any upstream or downstream services that make up your application. X-Ray uses this metadata to generate a detailed service graph that illustrates performance bottlenecks, latency spikes, and other issues that impact the performance of your Lambda application.

AWS Lambda uses environment variables to facilitate communication with the X-Ray daemon and configure the X-Ray SDK.

_X_AMZN_TRACE_ID: Contains the tracing header, which includes the sampling decision, trace ID, and parent segment ID. If Lambda receives a tracing header when your function is invoked, that header will be used to populate the _X_AMZN_TRACE_ID environment variable. If a tracing header was not received, Lambda will generate one for you.

AWS_XRAY_CONTEXT_MISSING: The X-Ray SDK uses this variable to determine its behavior in the event that your function tries to record X-Ray data, but a tracing header is not available. Lambda sets this value to LOG_ERROR by default.
 
AWS_XRAY_DAEMON_ADDRESS: This environment variable exposes the X-Ray daemon's address in the following format: IP_ADDRESS:PORT. You can use the X-Ray daemon's address to send trace data to the X-Ray daemon directly, without using the X-Ray SDK.

Therefore, the correct answers for this scenario are the _X_AMZN_TRACE_ID and AWS_XRAY_CONTEXT_MISSING environment variables.


### A mobile game is using a DynamoDB table named GameScore that keeps track of users and scores. Each item in the table is identified by a partition key (UserId) and a sort key (GameTitle). The diagram below shows how the items in the table are organized:

![image](https://user-images.githubusercontent.com/44325167/134162562-f7726542-b106-4d0f-b8fc-ea6559e354ca.png)

 
### A developer wants to write a leaderboard application to display the top scores for each game. How can the developer meet the requirement in the MOST efficient manner?
 
Amazon DynamoDB provides fast access to items in a table by specifying primary key values. However, many applications might benefit from having one or more secondary (or alternate) keys available, to allow efficient access to data with attributes other than the primary key. To address this, you can create one or more secondary indexes on a table, and issue Query or Scan requests against these indexes.

A secondary index is a data structure that contains a subset of attributes from a table, along with an alternate key to support Query operations. You can retrieve data from the index using a Query, in much the same way as you use Query with a table. A table can have multiple secondary indexes, which gives your applications access to many different query patterns.

DynamoDB supports two types of secondary indexes:

Global secondary index — an index with a partition key and a sort key that can be different from those on the base table. A global secondary index is considered "global" because queries on the index can span all of the data in the base table, across all partitions.

Local secondary index — an index that has the same partition key as the base table, but a different sort key. A local secondary index is "local" in the sense that every partition of a local secondary index is scoped to a base table partition that has the same partition key value.

To speed up queries on non-key attributes, you can create a global secondary index. A global secondary index contains a selection of attributes from the base table, but they are organized by a primary key that is different from that of the table. The index key does not need to have any of the key attributes from the table; it doesn't even need to have the same key schema as a table.

In this scenario, you could create a global secondary index named GameTitleIndex, with a partition key of GameTitle and a sort key of TopScore. Since the base table's primary key attributes are always projected into an index, the UserId attribute is also present. The following diagram shows what GameTitleIndex index would look like:
 
 ![image](https://user-images.githubusercontent.com/44325167/134164057-83905ff6-695a-48f0-b0b1-201f01f20499.png)

Hence, the correct answer in this scenario is to: **Create a global secondary index. Assign the GameTitle attribute as the partition key and the TopScore attribute as the sort key**.
 
(Create a local secondary index. Assign the GameTitle attribute as the partition key and the TopScore attribute as the sort key is incorrect because you can't add this index to an already existing table. Additionally, a local secondary index has the same partition key as the base table, but has a different sort key. It is "local" in the sense that every partition of a local secondary index is scoped to a base table partition that has the same partition key value.)


### You developed a shell script which uses AWS CLI to create a new Lambda function. However, you received an InvalidParameterValueException after running the script. What is the MOST likely cause of this issue?
 
 To create a Lambda function, you need a deployment package and an execution role. The deployment package contains your function code. The execution role grants the function permission to use AWS services, such as Amazon CloudWatch Logs for log streaming and AWS X-Ray for request tracing. You can use the CreateFunction API via the AWS CLI or the AWS SDK of your choice.

A function has an unpublished version, and can have published versions and aliases. The unpublished version changes when you update your function's code and configuration. A published version is a snapshot of your function code and configuration that can't be changed. An alias is a named resource that maps to a version, and can be changed to map to a different version. 

The InvalidParameterValueException will be returned if one of the parameters in the request is invalid. For example, if you provided an IAM role in the CreateFunction API which AWS Lambda is unable to assume. Hence, this option is the most likely cause of the issue in this scenario.
 
### The users of a social media website must be authenticated using social identity providers such as Twitter, Facebook, and Google. Users can login to the site which will allow them to upload their selfies, memes, and other media files in an S3 bucket. As an additional feature, you should also enable guest user access to certain sections of the website. Which of the following should you do to accomplish this task?
 
Amazon Cognito provides authentication, authorization, and user management for your web and mobile apps. Your users can sign in directly with a user name and password, or through a third party such as Facebook, Amazon, or Google.

The two main components of Amazon Cognito are user pools and identity pools. User pools are user directories that provide sign-up and sign-in options for your app users. Identity pools enable you to grant your users access to other AWS services. You can use identity pools and user pools separately or together.
 
![image](https://user-images.githubusercontent.com/44325167/134166146-55c81d0c-05e1-4a63-9a2f-7f317b813497.png)
 
Amazon Cognito identity pools (federated identities) support user authentication through Amazon Cognito user pools, federated identity providers—including Amazon, Facebook, Google, and SAML identity providers—as well as unauthenticated identities. This feature also supports Developer Authenticated Identities (Identity Pools), which lets you register and authenticate users via your own back-end authentication process.

Hence, creating an Identity Pool in Amazon Cognito and enabling access to unauthenticated identities is the most suitable answer for this scenario.
 
 ### An API gateway with a Lambda proxy integration takes a long time to complete its processing. There were also occurrences where some requests timed out. You want to monitor the responsiveness of your API calls as well as the underlying Lambda function. Which of the following CloudWatch metrics should you use to troubleshoot this issue? (Select TWO.)

You can monitor API execution using CloudWatch, which collects and processes raw data from API Gateway into readable, near real-time metrics. These statistics are recorded for a period of two weeks, so that you can access historical information and gain a better perspective on how your web application or service is performing. By default, API Gateway metric data is automatically sent to CloudWatch in one-minute periods. 

The metrics reported by API Gateway provide information that you can analyze in different ways. The list below shows some common uses for the metrics. These are suggestions to get you started, not a comprehensive list.

 - Monitor the IntegrationLatency metrics to measure the responsiveness of the backend.

 - Monitor the Latency metrics to measure the overall responsiveness of your API calls.

 - Monitor the CacheHitCount and CacheMissCount metrics to optimize cache capacities to achieve a desired performance.

Hence, the correct metrics that you have to use in this scenario are Latency and IntegrationLatency.
 
 (Count is incorrect because this metric simply gets the total number of API requests in a given period.

CacheMissCount is incorrect because this metric just gets the number of requests served from the backend in a given period when API caching is enabled. The Sum statistic represents this metric, namely, the total count of the cache misses in the given period.

CacheHitCount is incorrect because this fetches the number of requests served from the API cache in a given period. The Sum statistic represents this metric, namely, the total count of the cache hits in the given period.)
 
 ### An augmented reality mobile game has a serverless backend composed of Lambda, DynamoDB, and API Gateway. Due to the surge of new players globally, there were a lot of delays in retrieving the player data. You are instructed by your manager to improve the game's performance by reducing the database response times down to microseconds. Which of the following is the BEST service to use that can satisfy this scenario?
 
**Amazon DynamoDB Accelerator (DAX**) is a fully managed, highly available, in-memory cache for DynamoDB that delivers up to a 10x performance improvement – from milliseconds to microseconds – even at millions of requests per second. DAX does all the heavy lifting required to add in-memory acceleration to your DynamoDB tables, without requiring developers to manage cache invalidation, data population, or cluster management.

This will enable you to focus on building great applications for your customers without worrying about performance at scale. You do not need to modify application logic, since DAX is compatible with existing DynamoDB API calls. You can enable DAX with just a few clicks in the AWS Management Console or using the AWS SDK. Just as with DynamoDB, you only pay for the capacity you provision.
 
 (ElastiCache is incorrect because even though you may use ElastiCache as your database cache, it will not reduce the DynamoDB response time to microseconds unlike DynamoDB DAX.)
 
### A serverless application is composed of several Lambda functions which reads data from RDS. These functions must share the same connection string that should be encrypted to improve data security. Which of the following is the MOST secure way to meet the above requirement?
 
AWS Systems Manager Parameter Store provides secure, hierarchical storage for configuration data management and secrets management. You can store data such as passwords, database strings, and license codes as parameter values. You can store values as plain text or encrypted data. You can then reference values by using the unique name that you specified when you created the parameter.

Parameter Store offers the following benefits and features:

- Use a secure, scalable, hosted secrets management service (No servers to manage).

- Improve your security posture by separating your data from your code.

- Store configuration data and secure strings in hierarchies and track versions.

- Control and audit access at granular levels.

- Configure change notifications and trigger automated actions.

- Tag parameters individually, and then secure access from different levels, including operational, parameter, Amazon EC2 tag, or path levels.

- Reference AWS Secrets Manager secrets by using Parameter Store parameters.

Hence, **creating a Secure String Parameter using the AWS Systems Manager Parameter Store** is the correct solution for this scenario.
 
### A Lambda-based application consists of several functions. Once triggered, these functions will call various downstream resources such as a DynamoDB table or an S3 bucket, or make other API calls. There is a requirement to allow the developers to trace the event source that invoked your Lambda functions and trace the downstream calls that your functions made. The number of requests and the execution duration per request should also be monitored. Which of the following services should you use to achieve this? (Select TWO.)
 
A typical Lambda-based application consists of one or more functions triggered by events such as object uploads to Amazon S3, Amazon SNS notifications, and API actions. Once triggered, those functions usually call downstream resources such as DynamoDB tables or Amazon S3 buckets, or make other API calls. AWS Lambda leverages Amazon CloudWatch to automatically emit metrics and logs for all invocations of your function. However, this mechanism might not be convenient for tracing the event source that invoked your Lambda function, or for tracing downstream calls that your function made.
 
AWS X-Ray is a service that collects data about requests that your application serves, and provides tools you can use to view, filter, and gain insights into that data to identify issues and opportunities for optimization. For any traced request to your application, you can see detailed information not only about the request and response, but also about calls that your application makes to downstream AWS resources, microservices, databases and HTTP web APIs.

Hence, the correct answers are: **AWS X-Ray and Amazon CloudWatch**.

### A programmer is developing a shell script which uses AWS CLI to list all objects of a given bucket. However, the script is timing out if the bucket has tens of thousands of objects. What is the BEST solution that the programmer should implement to rectify this issue?
 
For commands that can return a large list of items, the AWS CLI provides options that you can use to control the number of items included in the output when the AWS CLI calls a service's API to populate the list.

By default, the AWS CLI uses a page size of 1000 and retrieves all available items. If you see issues when running list commands on a large number of resources, the default page size of 1000 might be too high. This can cause calls to AWS services to exceed the maximum allowed time and generate a "timed out" error.
 
You can use the --page-size option to specify that the AWS CLI request a smaller number of items from each call to the AWS service. The CLI still retrieves the full list but performs a larger number of service API calls in the background and retrieves a smaller number of items with each call. This gives the individual calls a better chance of succeeding without a timeout.

Hence, the correct answer is to **add pagination parameters in the AWS CLI command which will avoid timeouts to the shell script**.
 
 ### An application hosted in a multicontainer Docker platform in Elastic Beanstalk uses DynamoDB to handle the session data of its users. These data are only used in a particular timeframe and the stale data can be deleted after the user logged out of the system. Which of the following is the most suitable way to delete the session data?
 
**Time To Live (TTL)** for DynamoDB allows you to define when items in a table expire so that they can be automatically deleted from the database.

TTL is provided at no extra cost as a way to reduce storage usage and reduce the cost of storing irrelevant data without using provisioned throughput. With TTL enabled on a table, you can set a timestamp for deletion on a per-item basis, allowing you to limit storage usage to only those records that are relevant.
 
TTL is useful if you have continuously accumulating data that loses relevance after a specific time period. For example: session data, event logs, usage patterns, and other temporary data. If you have sensitive data that must be retained only for a certain amount of time according to contractual or regulatory obligations, TTL helps you ensure that it is removed promptly and as scheduled.

Therefore, the correct answer in this scenario is to **enable TTL for the session data in the DynamoDB table**.  
 
### A Lambda function downloads a file, with a size of 55 MB, from an external repository every time it is invoked. This causes the function to time out intermittently which greatly affects your serverless application. How should you refactor the function to solve this issue?
 
When AWS Lambda executes your Lambda function, it provisions and manages the resources needed to run your Lambda function. When you create a Lambda function, you specify configuration information, such as the amount of memory and maximum execution time that you want to allow for your Lambda function. When a Lambda function is invoked, AWS Lambda launches an execution context based on the configuration settings you provide. The execution context is a temporary runtime environment that initializes any external dependencies of your Lambda function code, such as database connections or HTTP endpoints. This affords subsequent invocations better performance because there is no need to "cold-start" or initialize those external dependencies, as explained below.

It takes time to set up an execution context and do the necessary "bootstrapping", which adds some latency each time the Lambda function is invoked. You typically see this latency when a Lambda function is invoked for the first time or after it has been updated because AWS Lambda tries to reuse the execution context for subsequent invocations of the Lambda function.
 
After a Lambda function is executed, AWS Lambda maintains the execution context for some time in anticipation of another Lambda function invocation. In effect, the service freezes the execution context after a Lambda function completes, and thaws the context for reuse, if AWS Lambda chooses to reuse the context when the Lambda function is invoked again.

Each execution context provides 512 MB of additional disk space in the /tmp directory. The directory content remains when the execution context is frozen, providing transient cache that can be used for multiple invocations. You can add extra code to check if the cache has the data that you stored.

Hence, the correct answer in this scenario is to **store the file in the /tmp directory of the execution context and reuse it on succeeding invocations**.

### A developer has recently completed a new version of a serverless application that is ready to be deployed using AWS SAM. There is a requirement that the traffic should shift from the previous Lambda function to the new version in the shortest time possible, but you still don't want to shift traffic all-at-once immediately. Which deployment configuration is the MOST suitable one to use in this scenario?
 
If you use AWS SAM to create your serverless application, it comes built-in with CodeDeploy to help ensure safe Lambda deployments. There are various deployment preference types that you can choose from.

For example:

If you choose Canary10Percent10Minutes then 10 percent of your customer traffic is immediately shifted to your new version. After 10 minutes, all traffic is shifted to the new version.

However, if your pre-hook/post-hook tests fail, or if a CloudWatch alarm is triggered, CodeDeploy rolls back your deployment. The following table outlines other traffic-shifting options that are available:

- Canary: Traffic is shifted in two increments. You can choose from predefined canary options. The options specify the percentage of traffic that's shifted to your updated Lambda function version in the first increment, and the interval, in minutes, before the remaining traffic is shifted in the second increment.

- Linear: Traffic is shifted in equal increments with an equal number of minutes between each increment. You can choose from predefined linear options that specify the percentage of traffic that's shifted in each increment and the number of minutes between each increment.

- All-at-once: All traffic is shifted from the original Lambda function to the updated Lambda function version at once.
 
![image](https://user-images.githubusercontent.com/44325167/134170924-4cc4362a-923c-4dc4-bca0-0010fbc74e58.png)
 
Hence, the CodeDeployDefault.LambdaCanary10Percent5Minutes option is correct because 10 percent of your customer traffic is immediately shifted to your new version. After 5 minutes, all traffic is shifted to the new version. This means that the entire deployment time will only take 5 minutes

### An internal web application is hosted in a custom VPC with multiple private subnets only. Every EC2 instance that will be provisioned on this VPC will require access to an S3 bucket to pull configuration files as well as to push application logs. Which of the following options is the most suitable solution to use in this scenario?
 
In this scenario, the key point that you have to understand is that S3 is not part of your VPC, unlike your EC2 instances, EBS volumes, ELBs, and other services that typically reside within your private network. An EC2 instance needs to have access to the Internet, via the Internet Gateway or a NAT Instance/Gateway in order to access S3. Alternatively, you can also create a VPC endpoint so your private subnet would be able to connect to S3.

To visualize this, take a look at the diagram below:
 
![image](https://user-images.githubusercontent.com/44325167/134172258-ae78b39b-3bf8-4bd4-b5cb-8a41caf6ecfe.png)
 
Hence, creating a VPC endpoint for S3 is the correct answer.

### A DynamoDB table has several top-level attributes such as id, course_id, course_title, price, rating and many others. The database queries of your application returns all of the item attributes by default but you only want to fetch specific attributes such as the course_id and price per request. As the developer, how can you refactor your application to accomplish this requirement?
 
To read data from a table, you use operations such as GetItem, Query, or Scan. DynamoDB returns all of the item attributes by default. To get just some, rather than all of the attributes, use a **projection expression**.

**A projection expression is a string that identifies the attributes you want. To retrieve a single attribute, specify its name. For multiple attributes, the names must be comma-separated.**

The following AWS CLI example shows how to use a projection expression with a GetItemoperation. This projection expression retrieves a top-level scalar attribute (Description), the first element in a list (RelatedItems[0]), and a list nested within a map (ProductReviews.FiveStar).

You can use any attribute name in a projection expression, provided that the first character is a-z or A-Z and the second character (if present) is a-z, A-Z, or 0-9. If an attribute name does not meet this requirement, you will need to define an expression attribute name as a placeholder.

Therefore, using projection expression is the correct answer in this scenario.
