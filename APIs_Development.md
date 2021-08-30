Amazon API Gateway is an AWS service for creating, publishing, maintaining, monitoring, and securing REST, HTTP, and WebSocket APIs at any scale. API developers can create APIs that access AWS or other web services, as well as data stored in the AWS Cloud.
  
A usage plan specifies who can access one or more deployed API stages and methods—and also how much and how fast they can access them. The plan uses API keys to identify API clients and meters access to the associated API stages for each key.

You can configure usage plans and API keys to allow customers to access selected APIs at agreed-upon request rates and quotas that meet their business requirements and budget constraints.
  
  ![image](https://user-images.githubusercontent.com/44325167/129881859-4a5697e0-f0e7-41f0-9be2-24771572c44e.png)

![image](https://user-images.githubusercontent.com/44325167/129897918-39b8189e-ff0f-4e31-8506-d99e239a7c0b.png)


# Practice Questions

# A SaaS company runs a HealthCare web application that is used worldwide by users. There have been requests by mobile developers to expose public APIs for the application-specific functionality. You decide to make the APIs available to mobile developers as product offerings. Which of the following options will allow you to do that?

# As a Senior Developer, you are tasked with creating several API Gateway powered APIs along with your team of developers. The developers are working on the API in the development environment, but they find the changes made to the APIs are not reflected when the API is called. As a Developer Associate, which of the following solutions would you recommend for this use-case?

**Redeploy the API to an existing stage or to a new stage**

After creating your API, you must deploy it to make it callable by your users. **To deploy an API, you create an API deployment and associate it with a stage. A stage is a logical reference to a lifecycle state of your API (for example, dev, prod, beta, v2)**. API stages are identified by the API ID and stage name. **Every time you update an API, you must redeploy the API to an existing stage or to a new stage**. **Updating an API includes modifying routes, methods, integrations, authorizers, and anything else other than stage settings**.

**A development team has created a new IAM user that has s3:putObject permission to write to an S3 bucket. This S3 bucket uses server-side encryption with AWS KMS managed keys (SSE-KMS) as the default encryption. Using the access key ID and the secret access key of the IAM user, the application received an access denied error when calling the PutObject API. As a Developer Associate, how would you resolve this issue?**

_Correct the policy of the IAM user to allow the kms:GenerateDataKey action_

You can protect data at rest in Amazon S3 by using three different modes of server-side encryption: 
SSE-S3 <br>
SSE-C <br>
SSE-KMS <br>

**SSE-KMS requires that AWS manage the data key but you manage the customer master key (CMK) in AWS KMS.**

The error message indicates that your IAM user or role needs permission for the kms:GenerateDataKey action. This permission is required for buckets that use default encryption with a custom AWS KMS key.

In the JSON policy documents, look for policies related to AWS KMS access. Review statements with "Effect": "Allow" to check if the user or role has permissions for the kms:GenerateDataKey action on the bucket's AWS KMS key. If this permission is missing, then add the permission to the appropriate policy.

In the JSON policy documents, look for statements with "Effect": "Deny". Then, confirm that those statements don't deny the s3:PutObject action on the bucket. The statements must also not deny the IAM user or role access to the kms:GenerateDataKey action on the key used to encrypt the bucket. Additionally, make sure the necessary KMS and S3 permissions are not restricted using a VPC endpoint policy, service control policy, permissions boundary, or session policy.

**You have a three-tier web application consisting of a web layer using AngularJS, an application layer using an AWS API Gateway and a data layer in an Amazon Relational Database Service (RDS) database. Your web application allows visitors to look up popular movies from the past. The company is looking at reducing the number of calls made to endpoint and improve latency to the API. What can you do to improve performance?**

_**Enable API Gateway Caching**_ 

You can enable API caching in Amazon API Gateway to cache your endpoint's responses. With caching, you can reduce the number of calls made to your endpoint and also improve the latency of requests to your API. When you enable caching for a stage, API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period, in seconds. API Gateway then responds to the request by looking up the endpoint response from the cache instead of making a request to your endpoint. The default TTL value for API caching is 300 seconds. The maximum TTL value is 3600 seconds. TTL=0 means caching is disabled.

