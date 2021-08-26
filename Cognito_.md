## The development team at a multi-national retail company wants to support trusted third-party authenticated users from the supplier organizations to create and update records in specific DynamoDB tables in the company's AWS account. As a Developer Associate, which of the following solutions would you suggest for the given use-case?

**Use Cognito Identity pools to enable trusted third-party authenticated users to access DynamoDB**

Amazon Cognito identity pools (federated identities) enable you to create unique identities for your users and federate them with identity providers. With an identity pool, you can obtain temporary, limited-privilege AWS credentials to access other AWS services. Amazon Cognito identity pools support the following identity providers:

Public providers: Login with Amazon (Identity Pools), Facebook (Identity Pools), Google (Identity Pools), Sign in with Apple (Identity Pools).

# Cognito User Pools vs Cognito Identity Pools 

## User pools are user directories that provide sign-up and sign-in options for your app users.

A user pool is a user directory in Amazon Cognito. With a user pool, your users can sign in to your web or mobile app through Amazon Cognito, or federate through a third-party identity provider (IdP). Whether your users sign in directly or through a third party, all members of the user pool have a directory profile that you can access through an SDK.

## Identity pools enable you to grant your users access to other AWS services.

With an identity pool, your users can obtain temporary AWS credentials to access AWS services, such as Amazon S3 and DynamoDB. Identity pools support anonymous guest users, as well as the following identity providers that you can use to authenticate users for identity pools:

Amazon Cognito user pools

Social sign-in with Facebook, Google, Login with Amazon, and Sign in with Apple

OpenID Connect (OIDC) providers

SAML identity providers

Developer authenticated identities

To save user profile information, your identity pool needs to be integrated with a user pool.
