# Security with AWS

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

## IAM Access Analyzer

 AWS IAM Access Analyzer **helps you identify the resources in your organization and accounts, such as Amazon S3 buckets or IAM roles, that are shared with an external entity.** **This lets you identify unintended access to your resources and data, which is a security risk.**

You can set the scope for the analyzer to an organization or an AWS account. This is your zone of trust. The analyzer scans all of the supported resources within your zone of trust. When Access Analyzer finds a policy that allows access to a resource from outside of your zone of trust, it generates an active finding.

## Access Advisor feature on IAM console

To help identify the unused roles, IAM reports the last-used timestamp that represents when a role was last used to make an AWS request. Your security team can use this information to identify, analyze, and then confidently remove unused roles. This helps improve the security posture of your AWS environments. Additionally, by removing unused roles, you can simplify your monitoring and auditing efforts by focusing only on roles that are in use.

## Secrets Manager

AWS Secrets Manager enables you to easily rotate, manage, and retrieve database credentials, API keys, and other secrets throughout their lifecycle. Users and applications retrieve secrets with a call to Secrets Manager APIs, eliminating the need to hardcode sensitive information in plain text. Secrets Manager offers secret rotation with built-in integration for Amazon RDS, Amazon Redshift, and Amazon DocumentDB.

## Key Pairs

Key pairs consist of a public key and a private key. You use the private key to create a digital signature, and then AWS uses the corresponding public key to validate the signature. **Key pairs are used only for Amazon EC2 and Amazon CloudFront**. AWS does not provide key pairs for your account; you must create them. You can create Amazon EC2 key pairs from the Amazon EC2 console, CLI, or API. Key pairs make a robust combination for accessing an instance securely, a better option than using passwords.


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

## Permissions & Policy Types 

**Permissions boundary** - Permissions boundary is a managed policy that is used for an IAM entity (user or role). The policy defines the maximum permissions that the identity-based policies can grant to an entity, but does not grant permissions.

**AWS Organizations Service Control Policy (SCP)** – Use an AWS Organizations Service Control Policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU). SCPs limit permissions that identity-based policies or resource-based policies grant to entities (users or roles) within the account, but do not grant permissions.

**Access control list (ACL)** - Use ACLs to control which principals in other accounts can access the resource to which the ACL is attached. ACLs are similar to resource-based policies, although they are the only policy type that does not use the JSON policy document structure. ACLs are cross-account permissions policies that grant permissions to the specified principal.

**Resource-based policy** - Resource-based policies grant permissions to the principal that is specified in the policy. Principals can be in the same account as the resource or in other accounts. The most common examples of resource-based policies are Amazon S3 bucket policies and IAM role trust policies.

**Identity-based policy** - Help attach managed and inline policies to IAM identities (users, groups to which users belong, or roles). Identity-based policies grant permissions to an identity.

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







