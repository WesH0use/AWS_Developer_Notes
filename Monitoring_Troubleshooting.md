# Monitoring & Troubleshooting in AWS


## X-Ray

AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture. With X-Ray, you can understand how your application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors. X-Ray provides an end-to-end view of requests as they travel through your application, and shows a map of your application’s underlying components.

You can use X-Ray to collect data across AWS Accounts. The X-Ray agent can assume a role to publish data into an account different from the one in which it is running. This enables you to publish data from various components of your application into a central account.

How X-Ray works: 
![image](https://user-images.githubusercontent.com/44325167/129902551-e936e019-5e1f-48f4-bed8-806703e9e3a2.png)

### Recently in your organization, the AWS X-Ray SDK was bundled into each Lambda function to record outgoing calls for tracing purposes. When your team leader goes to the X-Ray service in the AWS Management Console to get an overview of the information collected, they discover that no data is available. What is the most likely reason for this issue?

**Fix the IAM Role**

**Create an IAM role with write permissions and assign it to the resources running your application.** You can use AWS Identity and Access Management (IAM) to grant X-Ray permissions to users and compute resources in your account. This should be one of the first places you start by checking that your permissions are properly configured before exploring other troubleshooting options.

## CloudFormation

CloudFormation currently supports the following parameter types:
String – A literal string
Number – An integer or float
List<Number> – An array of integers or floats
CommaDelimitedList – An array of literal strings that are separated by commas
AWS::EC2::KeyPair::KeyName – An Amazon EC2 key pair name
AWS::EC2::SecurityGroup::Id – A security group ID
AWS::EC2::Subnet::Id – A subnet ID
AWS::EC2::VPC::Id – A VPC ID
List<AWS::EC2::VPC::Id> – An array of VPC IDs
List<AWS::EC2::SecurityGroup::Id> – An array of security group IDs
List<AWS::EC2::Subnet::Id> – An array of subnet IDs

  
## Internet Gateway 
  
**While troubleshooting, a developer realized that the Amazon EC2 instance is unable to connect to the Internet using the Internet Gateway. Which conditions should be met for Internet connectivity to be established?**
  
1) **The network ACLs associated with the subnet must have rules to allow inbound and outbound traffic** - The network access control lists (ACLs) that are associated with the subnet must have rules to allow inbound and outbound traffic on port 80 (for HTTP traffic) and port 443 (for HTTPs traffic). This is a necessary condition for Internet Gateway connectivity. 
  
2) **The route table in the instance’s subnet should have a route to an Internet Gateway** - A route table contains a set of rules, called routes, that are used to determine where network traffic from your subnet or gateway is directed. The route table in the instance’s subnet should have a route defined to the Internet Gateway.


## VPC Flow Logs

VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC. Flow log data is used to analyze network traces and helps with network security. Flow log data can be published to Amazon CloudWatch Logs or Amazon S3. You cannot use VPC Flow Logs to debug and trace data across accounts.

## CloudWatch Events

Amazon CloudWatch Events delivers a near real-time stream of system events that describe changes in Amazon Web Services (AWS) resources. These help to trigger notifications based on changes happening in AWS services. You cannot use CloudWatch Events to debug and trace data across accounts.

## Cloudtrail 

With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. You can use AWS CloudTrail to answer questions such as - “Who made an API call to modify this resource?”. CloudTrail provides event history of your AWS account activity thereby enabling governance, compliance, operational auditing, and risk auditing of your AWS account. You cannot use CloudTrail to maintain a history of resource configuration changes.

How Cloudtrail works:
![image](https://user-images.githubusercontent.com/44325167/129903569-511c8d9f-59e3-4aa4-981e-3b00a66608f3.png)

# Config 

AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources. With Config, you can review changes in configurations and relationships between AWS resources, dive into detailed resource configuration histories, and determine your overall compliance against the configurations specified in your internal guidelines. You can use Config to answer questions such as - “What did my AWS resource look like at xyz point in time?”. Config cannot help determine the source for KMS API calls.
  
 # CodeDeploy
  
**A company uses AWS CodeDeploy to deploy applications from GitHub to EC2 instances running Amazon Linux. The deployment process uses a file called appspec.yml for specifying deployment hooks. A final lifecycle event should be specified to verify the deployment success. Which of the following hook events should be used to verify the success of the deployment?**
  
AWS CodeDeploy is a fully managed deployment service that automates software deployments to a variety of compute services such as Amazon EC2, AWS Fargate, AWS Lambda, and your on-premises servers. AWS CodeDeploy makes it easier for you to rapidly release new features, helps you avoid downtime during application deployment, and handles the complexity of updating your applications.

**ValidateService:** ValidateService is the last deployment lifecycle event. It is used to verify the deployment was completed successfully.

An EC2/On-Premises deployment hook is executed once per deployment to an instance. You can specify one or more scripts to run in a hook.

## Practice Question

# A financial services company is undergoing a compliance audit by the regulator. The company has hundreds of IAM users that make API calls but specifically it needs to be determined who is making KMS API calls. Which of the following services should the audit team use?

# A multi-national company has multiple business units with each unit having its own AWS account. The development team at the company would like to debug and trace data across accounts and visualize it in a centralized account. As a Developer Associate, which of the following solutions would you suggest for the given use-case?




# EC2

## User Data 

User Data is generally used to perform common automated configuration tasks and even run scripts after the instance starts. When you launch an instance in Amazon EC2, you can pass two types of user data - shell scripts and cloud-init directives. You can also pass this data into the launch wizard as plain text or as a file.

**By default, scripts entered as user data are executed with root user privileges** - Scripts entered as user data are executed as the root user, hence do not need the sudo command in the script. Any files you create will be owned by root; if you need non-root users to have file access, you should modify the permissions accordingly in the script.

**By default, user data runs only during the boot cycle when you first launch an instance** - By default, user data scripts and cloud-init directives run only during the boot cycle when you first launch an instance. You can update your configuration to ensure that your user data scripts and cloud-init directives run every time you restart your instance.

## Load Balancers

You must ensure that your load balancer can communicate with registered targets on both the listener port and the health check port. Whenever you add a listener to your load balancer or update the health check port for a target group used by the load balancer to route requests, you must verify that the security groups associated with the load balancer allow traffic on the new port in both directions.

Application Load Balancer Configuration for Security Groups and Health Check Routes:
![image](https://user-images.githubusercontent.com/44325167/129904758-a8c5c0ff-c26b-4bf6-b4cc-8e4a554bd3d1.png)

**ALB access logs** - Elastic Load Balancing provides access logs that capture detailed information about requests sent to your load balancer. Each log contains information such as the time the request was received, the client's IP address, latencies, request paths, and server responses. You can use these access logs to analyze traffic patterns and troubleshoot issues. Access logging is an optional feature of Elastic Load Balancing that is disabled by default.

Access logs for your Application Load Balancer:
![image](https://user-images.githubusercontent.com/44325167/129908289-80f38787-9de1-4b31-8095-2c1319f65542.png)



## Practice Questions
  
# An e-commerce company uses AWS CloudFormation to implement Infrastructure as Code for the entire organization. Maintaining resources as stacks with CloudFormation has greatly reduced the management effort needed to manage and maintain the resources. However, a few teams have been complaining of failing stack updates owing to out-of-band fixes running on the stack resources.Which of the following is the best solution that can help in keeping the CloudFormation stack and its resources in sync with each other?

**Use Drift Detection feature of CloudFormation**

**Drift detection enables you to detect whether a stack's actual configuration differs, or has drifted, from its expected configuration**. Use CloudFormation to detect drift on an entire stack, or individual resources within the stack. A resource is considered to have drifted if any of its actual property values differ from the expected property values. This includes if the property or resource has been deleted. A stack is considered to have drifted if one or more of its resources have drifted.

To determine whether a resource has drifted, CloudFormation determines the expected resource property values, as defined in the stack template and any values specified as template parameters. CloudFormation then compares those expected values with the actual values of those resource properties as they currently exist in the stack. A resource is considered to have drifted if one or more of its properties have been deleted, or had their value changed.

You can then take corrective action so that your stack resources are again in sync with their definitions in the stack template, such as updating the drifted resources directly so that they agree with their template definition. Resolving drift helps to ensure configuration consistency and successful stack operations.

# A firm runs its technology operations on a fleet of Amazon EC2 instances. The firm needs a certain software to be available on the instances to support their daily workflows. The developer team has been told to use the user data feature of EC2 instances. Which of the following are true about the user data EC2 configuration? ( Select two)

# Your company has stored all application secrets in SSM Parameter Store. The audit team has requested to get a report to better understand when and who has issued API calls against SSM Parameter Store. Which of the following options can be used to produce your report?

Explanation
Correct option:

Use AWS CloudTrail to get a record of actions taken by a user

AWS Systems Manager Parameter Store provides secure, hierarchical storage for configuration data management and secrets management. You can store data such as passwords, database strings, Amazon Machine Image (AMI) IDs, and license codes as parameter values. You can store values as plain text or encrypted data.

AWS CloudTrail provides a record of actions taken by a user, role, or an AWS service in Systems Manager. Using the information collected by AWS CloudTrail, you can determine the request that was made to Systems Manager, the IP address from which the request was made, who made the request, when it was made, and additional details.

# You have created an Elastic Load Balancer that has marked all the EC2 instances in the target group as unhealthy. Surprisingly, when you enter the IP address of the EC2 instances in your web browser, you can access your website. What could be the reason your instances are being marked as unhealthy? (Select two)

# An organization has offices across multiple locations and the technology team has configured an Application Load Balancer across targets in multiple Availability Zones. The team wants to analyze the incoming requests for latencies and the client's IP address patterns. Which feature of the Load Balancer will help collect the required information?
  
# You are a development team lead setting permissions for other IAM users with limited permissions. On the AWS Management Console, you created a dev group where new developers will be added, and on your workstation, you configured a developer profile. You would like to test that this user cannot terminate instances. Which of the following options would you execute?
  
**Use the AWS CLI --dry-run option**: The --dry-run option checks whether you have the required permissions for the action, without actually making the request, and provides an error response. If you have the required permissions, the error response is **DryRunOperation**, otherwise, it is **UnauthorizedOperation**.



# You have deployed a Java application to an EC2 instance where it uses the X-Ray SDK. When testing from your personal computer, the application sends data to X-Ray but when the application runs from within EC2, the application fails to send data to X-Ray. Which of the following does NOT help with debugging the issue?

## X-Ray Sampling
## EC2 X-Ray Daemon
## Cloudtrail
## EC2 Instance Role 

Explanation
Correct option:

**X-Ray sampling**

By customizing sampling rules, you can control the amount of data that you record, and modify sampling behavior on the fly without modifying or redeploying your code. Sampling rules tell the X-Ray SDK how many requests to record for a set of criteria. X-Ray SDK applies a sampling algorithm to determine which requests get traced however because our application is failing to send data to X-Ray it does not help in determining the cause of failure.

X-Ray Overview:
![image](https://user-images.githubusercontent.com/44325167/129905921-ba6176f8-f051-4e88-8b0b-c073b233bf35.png)

Incorrect options:

EC2 X-Ray Daemon - The AWS X-Ray daemon is a software application that listens for traffic on UDP port 2000, gathers raw segment data, and relays it to the AWS X-Ray API. The daemon logs could help with figuring out the problem.

EC2 Instance Role - The X-Ray daemon uses the AWS SDK to upload trace data to X-Ray, and it needs AWS credentials with permission to do that. On Amazon EC2, the daemon uses the instance's instance profile role automatically. Eliminates API permission issues (in case the role doesn't have IAM permissions to write data to the X-Ray service)

CloudTrail - With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. You can use AWS CloudTrail to answer questions such as - “Who made an API call to modify this resource?”. CloudTrail provides event history of your AWS account activity thereby enabling governance, compliance, operational auditing, and risk auditing of your AWS account. You can check CloudTrail to see if any API call is being denied on X-Ray.


