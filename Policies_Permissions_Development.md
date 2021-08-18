# Identity Based vs Resource Based policies 

Identity-based policies are the easier of the two, as some variation of it is present in most systems. They define what an identity can do, such as a user has access to an S3 bucket.

There are two types of identities in AWS: users and roles. By attaching a policy to an identity you can give it permissions to access resources.

Since the policy is attached to an identity, a user in this case, there is no Principal element in the policy. On the other hand, the Resource defines the object in the bucket that the user can access.

**Users**

There is only one type of user that can be created, but depending on how they are used we can distinguish natural and technical users.

Natural users are created for people. Bob, who is responsible for the S3 buckets, gets a user with the permissions needed to do his work. These type of users usually have a password to sign in to the console and sometimes access keys to allow programmatic access to the account. Since the user is created and managed by a single person, that person is responsible for it. Also, it’s likely that multiple people have the same job, so permissions are usually attached to groups instead of the users themselves.

![Screen Shot 2021-08-18 at 1 36 28 PM](https://user-images.githubusercontent.com/44325167/129891359-52ca3044-65b0-4018-a858-203b1d347143.png)


Technical users allow other services access to resources inside the account. For example, a web application hosted outside of AWS where users can send notifications to an SNS topic. In this case, you can create a new user, generate an access key and include that in the web application’s backend. Then you attach a policy so that it can publish a notification to the topic.
![Screen Shot 2021-08-18 at 1 37 05 PM](https://user-images.githubusercontent.com/44325167/129891474-c20fdbcc-c502-4856-b4bd-2f2dc7fe769f.png)

**Roles**

Roles are temporary credentials that other identities (users and roles) can assume to gain access to the permissions the role has. For example, when a bucket can only be accessed by a role then if a user can assume that role he then can access the bucket indirectly.

There are many use-cases for roles inside AWS. To give access to your account, you can use a role that can be used by identities in another account. This way you don’t need to create users and transfer secrets (passwords or access keys) to grant cross-account access. Another use-case is users logging in via SAML or Cognito. Instead of creating a user for every single person who can log in, you define a role and all users assume it. Then you can give permissions to the role and all users signed in this way will gain those permissions.

## Resource Based Policies 

What if there is no identity to attach the policies to? This is the case for anonymous access, and also when an AWS service does not use a service role, such as an API Gateway. When there is no identity, identity-based policies can not be used.

Many, but not all, AWS services support resource-based policies. These are policies attached to the resource and these can give access when there is no identity.

S3 buckets support bucket policies which can be used to give anonymous access to the bucket:

![Screen Shot 2021-08-18 at 1 41 38 PM](https://user-images.githubusercontent.com/44325167/129891999-b8d51eef-f7bf-46a3-a029-590862f634c9.png)

The * Principal means “everybody” that includes non-users.

Similarly, the role’s trust policy is a resource-based policy. This allows services and identities to assume the role. 

You manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources. **A policy is an object in AWS that, when associated with an identity or resource, defines their permissions.** Resource-based policies are JSON policy documents that you attach to a resource such as an Amazon S3 bucket. These policies grant the specified principal permission to perform specific actions on that resource and define under what conditions this applies.
 
**Trust policy** - Trust policies define which principal entities (accounts, users, roles, and federated users) can assume the role. An IAM role is both an identity and a resource that supports resource-based policies. For this reason, you must attach both a trust policy and an identity-based policy to an IAM role. **The IAM service supports only one type of resource-based policy called a role trust policy, which is attached to an IAM role.**
 
**AWS Organizations Service Control Policies (SCP)** - If you enable all features of AWS organization, then you can apply service control policies (SCPs) to any or all of your accounts. SCPs are JSON policies that specify the maximum permissions for an organization or organizational unit (OU). The SCP limits permissions for entities in member accounts, including each AWS account root user. An explicit deny in any of these policies overrides the allow.

**Access control list (ACL)** - Access control lists (ACLs) are service policies that allow you to control which principals in another account can access a resource. ACLs cannot be used to control access for a principal within the same account. Amazon S3, AWS WAF, and Amazon VPC are examples of services that support ACLs.

**Permissions boundary** - AWS supports permissions boundaries for IAM entities (users or roles). **A permissions boundary is an advanced feature for using a managed policy to set the maximum permissions that an identity-based policy can grant to an IAM entity.** An entity's permissions boundary allows it to perform only the actions that are allowed by both its identity-based policies and its permissions boundaries.

## Practice Questions

# As part of his development work, an AWS Certified Developer Associate is creating policies and attaching them to IAM identities. After creating necessary Identity-based policies, he is now creating Resource-based policies. Which is the only resource-based policy that the IAM service supports?

You manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources. A policy is an object in AWS that, when associated with an identity or resource, defines their permissions. Resource-based policies are JSON policy documents that you attach to a resource such as an Amazon S3 bucket. These policies grant the specified principal permission to perform specific actions on that resource and define under what conditions this applies.

**Trust policy** - Trust policies define which principal entities (accounts, users, roles, and federated users) can assume the role. An IAM role is both an identity and a resource that supports resource-based policies. For this reason, you must attach both a trust policy and an identity-based policy to an IAM role. The IAM service supports only one type of resource-based policy called a role trust policy, which is attached to an IAM role.
