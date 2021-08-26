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



