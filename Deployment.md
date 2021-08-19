# Deployment in AWS

## AWS 

Development Kit (AWS CDK)

The AWS Cloud Development Kit (AWS CDK) is an open-source software development framework to define your cloud application resources using familiar programming languages. 

Provisioning cloud applications can be a challenging process that requires you to perform manual actions, write custom scripts, maintain templates, or learn domain-specific languages. AWS CDK uses the familiarity and expressive power of programming languages such as JavaScript/TypeScript, Python, Java, and .NET for modeling your applications. It provides you with high-level components called constructs that preconfigure cloud resources with proven defaults, so you can build cloud applications without needing to be an expert. AWS CDK provisions your resources in a safe, repeatable manner through AWS CloudFormation. It also enables you to compose and share your own custom constructs that incorporate your organization's requirements, helping you start new projects faster.

#### Order of steps to be followed for creating an app using AWS CDK:

-> Create the app from a template provided by AWS CDK 
-> Add code to the app to create resources within stacks 
-> Build the app (optional) 
-> Synthesize one or more stacks in the app 
-> Deploy stack(s) to your AWS account

## AWS Serverless Application Model (SAM)

The AWS Serverless Application Repository is a managed repository for serverless applications. It enables teams, organizations, and individual developers to store and share reusable applications, and easily assemble and deploy serverless architectures in powerful new ways. Using the Serverless Application Repository, you don't need to clone, build, package, or publish source code to AWS before deploying it.

**AWS Serverless Application Model and AWS CDK both abstract AWS infrastructure as code making it easier for you to define your cloud infrastructure. If you prefer defining your serverless infrastructure in concise declarative templates, SAM is the better fit.** If you want to define your AWS infrastructure in a familiar programming language, as is the requirement in the current use case, AWS CDK is the right fit.

## AWS CodeDeploy

WS CodeDeploy is a fully managed deployment service that automates software deployments to a variety of compute services such as Amazon EC2, AWS Fargate, AWS Lambda, and your on-premises servers. AWS CodeDeploy makes it easier for you to rapidly release new features, helps you avoid downtime during application deployment, and handles the complexity of updating your applications. CodeDeploy can be used with AWS CDK for deployments.

**The blue/green deployment type uses the blue/green deployment model controlled by CodeDeploy.** This deployment type enables you to verify a new deployment of service before sending production traffic to it.


## Elastic Beanstalk 

AWS Elastic Beanstalk provides an environment to easily deploy and run applications in the cloud. It is integrated with developer tools and provides a one-stop experience for you to manage the lifecycle of your applications.

AWS Elastic Beanstalk lets you manage all of the resources that run your application as environments where each environment runs only a single application version at a time. When an environment is being created, Elastic Beanstalk provisions all the required resources needed to run the application version. You don't need to worry about server provisioning, configuration, and deployment as that's taken care of by Beanstalk.

When processing a batch, Elastic Beanstalk detaches all instances in the batch from the load balancer, deploys the new application version, and then reattaches the instances. If you enable connection draining, Elastic Beanstalk drains existing connections from the Amazon EC2 instances in each batch before beginning the deployment.

If a deployment fails after one or more batches completed successfully, the completed batches run the new version of your application while any pending batches continue to run the old version. You can identify the version running on the instances in your environment on the health page in the console. This page displays the deployment ID of the most recent deployment that was executed on each instance in your environment. If you terminate instances from the failed deployment, Elastic Beanstalk replaces them with instances running the application version from the most recent successful deployment.

Benefits of Elastic Beanstalk:

1) Elastic Beanstalk is the fastest and simplest way to deploy your application on AWS. You simply use the AWS Management Console, a Git repository, or an integrated development environment (IDE) such as Eclipse or Visual Studio to upload your application, and Elastic Beanstalk automatically handles the deployment details of capacity provisioning, load balancing, auto-scaling, and application health monitoring. 
2) Elastic Beanstalk provisions and operates the infrastructure and manages the application stack (platform) for you, so you don't have to spend the time or develop the expertise.
3) You have the freedom to select the AWS resources, such as Amazon EC2 instance type, that are optimal for your application.

### Elastic Beanstalk Deployment Types

**Deploy using 'Rolling with additional batch' deployment policy** - With this method, Elastic Beanstalk launches an extra batch of instances, then performs a rolling deployment. Launching the extra batch takes time, and ensures that the same bandwidth is retained throughout the deployment. This policy also avoids any reduced availability, although at a cost of an even longer deployment time compared to the Rolling method. Finally, this option is suitable if you must maintain the same bandwidth throughout the deployment.

**Deploy using 'Immutable' deployment policy** - A slower deployment method, that ensures your new application version is always deployed to new instances, instead of updating existing instances. It also has the additional advantage of a quick and safe rollback in case the deployment fails. With this method, Elastic Beanstalk performs an immutable update to deploy your application. In an immutable update, a second Auto Scaling group is launched in your environment and the new version serves traffic alongside the old version until the new instances pass health checks. Immutable deployments perform an immutable update to launch a full set of new instances running the new version of the application in a separate Auto Scaling group, alongside the instances running the old version. Immutable deployments can prevent issues caused by partially completed rolling deployments.

**Deploy using 'All at once' deployment policy** - This is the quickest deployment method. Suitable if you can accept a short loss of service, and if quick deployments are important to you. With this method, Elastic Beanstalk deploys the new application version to each instance. Then, the web proxy or application server might need to restart. As a result, your application might be unavailable to users (or have low availability) for a short time.

**Deploy using 'Rolling' deployment policy** - With this method, your application is deployed to your environment one batch of instances at a time. Most bandwidth is retained throughout the deployment. Avoids downtime and minimizes reduced availability, at a cost of a longer deployment time. Suitable if you can't accept any period of completely lost service. The cost remains the same as the number of EC2 instances does not increase.

Traffic-splitting deployments let you perform canary testing as part of your application deployment. In a traffic-splitting deployment, Elastic Beanstalk launches a full set of new instances just like during an immutable deployment. It then forwards a specified percentage of incoming client traffic to the new application version for a specified evaluation period.

### Some policies replace all instances during the deployment or update. This causes all accumulated Amazon EC2 burst balances to be lost. It happens in the following cases:

- Managed platform updates with instance replacement enabled
- Immutable updates
- Deployments with immutable updates or traffic splitting enabled


## .ebextensions 

Any resources created as part of your .ebextensions is part of your Elastic Beanstalk template and will get deleted if the environment is terminated.


## Cloudformation

AWS CloudFormation is a service that gives developers and businesses an easy way to create a collection of related AWS and third-party resources and provision them in an orderly and predictable fashion.

How CloudFormation Works:
![image](https://user-images.githubusercontent.com/44325167/130060920-856a507e-50c0-4568-ab30-cc50fa34facc.png)

AWS Elastic Beanstalk provides an environment to easily deploy and run applications in the cloud. It is integrated with developer tools and provides a one-stop experience for you to manage the lifecycle of your applications.

**Elastic Beanstalk uses AWS CloudFormation to launch the resources in your environment and propagate configuration changes. AWS CloudFormation supports Elastic Beanstalk application environments as one of the AWS resource types.** This allows you, for example, to create and manage an AWS Elastic Beanstalk–hosted application along with an RDS database to store the application data.

 For each AWS account, EXPORT NAMES must be unique within a region. 


## ECR

Amazon Elastic Container Registry (Amazon ECR) is a fully managed container registry that makes it easy to store, manage, share, and deploy your container images and artifacts anywhere. Amazon ECR eliminates the need to operate your own container repositories or worry about scaling the underlying infrastructure. Amazon ECR hosts your images in a highly available and high-performance architecture, allowing you to deploy images for your container applications reliably. You can share container software privately within your organization or publicly worldwide for anyone to discover and download. 

How ECR Works:
![image](https://user-images.githubusercontent.com/44325167/130061523-7af2ec48-ebcd-473d-b90f-7651f845be49.png)

## ECS 

Amazon Elastic Container Service (Amazon ECS) is a highly scalable, fast, container management service that makes it easy **to run, stop, and manage Docker containers** on a cluster. You can host your cluster on a serverless infrastructure that is managed by Amazon ECS by launching your services or tasks using the Fargate launch type. For more control over your infrastructure, you can host your tasks on a cluster of Amazon Elastic Compute Cloud (Amazon EC2) instances that you manage by using the EC2 launch type.

**You cannot use ECS to store and deploy Docker images.**

![image](https://user-images.githubusercontent.com/44325167/130063466-ed6c5a06-7209-452b-9d57-8755a0529a4d.png)

## Codebuild

A build represents a set of actions performed by AWS CodeBuild to create output artifacts (for example, a JAR file) based on a set of input artifacts (for example, a collection of Java class files).

The following rules apply when you run multiple builds:

When possible, builds run concurrently. The maximum number of concurrently running builds can vary.

Builds are queued if the number of concurrently running builds reaches its limit. The maximum number of builds in a queue is five times the concurrent build limit.

A build in a queue that does not start after the number of minutes specified in its time out value is removed from the queue. The default timeout value is eight hours. You can override the build queue timeout with a value between five minutes and eight hours when you run your build.

By setting the timeout configuration, the build process will automatically terminate post the expiry of the configured timeout.

## AWS Serverless Application Model (SAM)

The AWS Serverless Application Model (SAM) is an open-source framework for building serverless applications. It provides shorthand syntax to express functions, APIs, databases, and event source mappings. With just a few lines per resource, you can define the application you want and model it using YAML.

SAM supports the following resource types:

**AWS::Serverless::Api**

**AWS::Serverless::Application**

**AWS::Serverless::Function**

**AWS::Serverless::HttpApi**

**AWS::Serverless::LayerVersion**

**AWS::Serverless::SimpleTable**

**AWS::Serverless::StateMachine**
