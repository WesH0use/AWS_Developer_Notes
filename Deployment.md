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


**A developer wants to package the code and dependencies for the application-specific Lambda functions as container images to be hosted on Amazon Elastic Container Registry (ECR). Which of the following options are correct for the given requirement? (Select two)**
**To deploy a container image to Lambda, the container image must implement the Lambda Runtime API** - To deploy a container image to Lambda, the container image must implement the Lambda Runtime API. The AWS open-source runtime interface clients implement the API. You can add a runtime interface client to your preferred base image to make it compatible with Lambda.

**You must create the Lambda function from the same account as the container registry in Amazon ECR** - You can package your Lambda function code and dependencies as a container image, using tools such as the Docker CLI. You can then upload the image to your container registry hosted on Amazon Elastic Container Registry (Amazon ECR). Note that you must create the Lambda function from the same account as the container registry in Amazon ECR.

**A developer in your company was just promoted to Team Lead and will be in charge of code deployment on EC2 instances via AWS CodeCommit and AWS CodeDeploy. Per the new requirements, the deployment process should be able to change permissions for deployed files as well as verify the deployment success. Which of the following actions should the new Developer take?**

**Define an appspec.yml file in the root directory**: An AppSpec file must be a YAML-formatted file named appspec.yml and it must be placed in the root of the directory structure of an application's source code.

**The AppSpec file is used to:**

Map the source files in your application revision to their destinations on the instance.

Specify custom permissions for deployed files.

Specify scripts to be run on each instance at various stages of the deployment process.

During deployment, the CodeDeploy agent looks up the name of the current event in the hooks section of the AppSpec file. If the event is not found, the CodeDeploy agent moves on to the next step. If the event is found, the CodeDeploy agent retrieves the list of scripts to execute. The scripts are run sequentially, in the order in which they appear in the file. The status of each script is logged in the CodeDeploy agent log file on the instance.

If a script runs successfully, it returns an exit code of 0 (zero). If the CodeDeploy agent installed on the operating system doesn't match what's listed in the AppSpec file, the deployment fails.


## CodeCommit 

AWS CodeCommit - AWS CodeCommit is a fully-managed Source Control service that hosts secure Git-based repositories. It makes it easy for teams to collaborate on code in a secure and highly scalable ecosystem. AWS CodeCommit helps you collaborate on code with teammates via pull requests, branching and merging. AWS CodeCommit keeps your repositories close to your build, staging, and production environments in the AWS cloud. You can transfer incremental changes instead of the entire application. AWS CodeCommit supports all Git commands and works with your existing Git tools. You can keep using your preferred development environment plugins, continuous integration/continuous delivery systems, and graphical clients with CodeCommit.

## Codebuild

A build represents a set of actions performed by AWS CodeBuild to create output artifacts (for example, a JAR file) based on a set of input artifacts (for example, a collection of Java class files).

The following rules apply when you run multiple builds:

When possible, builds run concurrently. The maximum number of concurrently running builds can vary.

Builds are queued if the number of concurrently running builds reaches its limit. The maximum number of builds in a queue is five times the concurrent build limit.

A build in a queue that does not start after the number of minutes specified in its time out value is removed from the queue. The default timeout value is eight hours. You can override the build queue timeout with a value between five minutes and eight hours when you run your build.

By setting the timeout configuration, the build process will automatically terminate post the expiry of the configured timeout.

## Advanced environment customization with configuration files (.ebextensions)

You can add AWS Elastic Beanstalk configuration files (.ebextensions) to your web application's source code to configure your environment and customize the AWS resources that it contains. Configuration files are YAML- or JSON-formatted documents with a .config file extension that you place in a folder named .ebextensions and deploy in your application source bundle.

The option_settings section of a configuration file defines values for configuration options. Configuration options let you configure your Elastic Beanstalk environment, the AWS resources in it, and the software that runs your application. Configuration files are only one of several ways to set configuration options.

# CodeDeploy

**A developer needs to automate software package deployment to both Amazon EC2 instances and virtual servers running on-premises, as part of continuous integration and delivery that the business has adopted. Which AWS service should he use to accomplish this task?**

**Continuous integration** is a DevOps software development practice where developers regularly merge their code changes into a central repository, after which automated builds and tests are run.

Continuous delivery is a software development practice where code changes are automatically prepared for a release to production. A pillar of modern application development, continuous delivery expands upon continuous integration by deploying all code changes to a testing environment and/or a production environment after the build stage.

**AWS CodeDeploy** - AWS CodeDeploy is a fully managed "deployment" service that automates software deployments to a variety of compute services such as Amazon EC2, AWS Fargate, AWS Lambda, and your on-premises servers. AWS CodeDeploy **makes it easier for you to rapidly release new features, helps you avoid downtime during application deployment, and handles the complexity of updating your applications**. This is the right choice for the current use case.

## Serverless Application Model (SAM)

The AWS Serverless Application Model (AWS SAM) is an open-source framework that you can use to build serverless applications on AWS.

A serverless application is a combination of Lambda functions, event sources, and other resources that work together to perform tasks. Note that a serverless application is more than just a Lambda function—it can include additional resources such as APIs, databases, and event source mappings.

Serverless Application Model (SAM) Templates include several major sections. **Transform and Resources** are the only required sections.

SAM supports the following resource types:

**AWS::Serverless::Api**

**AWS::Serverless::Application**

**AWS::Serverless::Function**

**AWS::Serverless::HttpApi**

**AWS::Serverless::LayerVersion**

**AWS::Serverless::SimpleTable**

**AWS::Serverless::StateMachine**

## The development team at an e-commerce company completed the last deployment for their application at a reduced capacity because of the deployment policy. The application took a performance hit because of the traffic spike due to an on-going sale.Which of the following represents the BEST deployment option for the upcoming application version such that it maintains at least the FULL capacity of the application and MINIMAL impact of failed deployment?

With Elastic Beanstalk, you can quickly deploy and manage applications in the AWS Cloud without having to learn about the infrastructure that runs those applications. Elastic Beanstalk reduces management complexity without restricting choice or control. You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring.

![image](https://user-images.githubusercontent.com/44325167/131115116-8f39a31c-49a2-4a79-8e82-384e7f1685d1.png)

The **'Immutable'** deployment policy ensures that your new application version is always deployed to new instances, instead of updating existing instances. It also has the additional advantage of a quick and safe rollback in case the deployment fails. In an immutable update, a second Auto Scaling group is launched in your environment and the new version serves traffic alongside the old version until the new instances pass health checks. In case of deployment failure, the new instances are terminated, so the impact is minimal.


## ECS 

**Your company has embraced cloud-native microservices architectures. New applications must be dockerized and stored in a registry service offered by AWS. The architecture should support dynamic port mapping and support multiple tasks from a single service on the same container instance. All services should run on the same EC2 instance.Which of the following options offers the best-fit solution for the given use-case?**

**Amazon Elastic Container Service (Amazon ECS)** is a highly scalable, fast, container management service that makes it easy to run, stop, and manage Docker containers on a cluster. You can host your cluster on a serverless infrastructure that is managed by Amazon ECS by launching your services or tasks using the Fargate launch type. For more control over your infrastructure, you can host your tasks on a cluster of Amazon Elastic Compute Cloud (Amazon EC2) instances that you manage by using the EC2 launch type.

**An Application load balancer** distributes incoming application traffic across multiple targets, such as EC2 instances, in multiple Availability Zones. A listener checks for connection requests from clients, using the protocol and port that you configure. The rules that you define for a listener determine how the load balancer routes requests to its registered targets. Each rule consists of a priority, one or more actions, and one or more conditions.

![image](https://user-images.githubusercontent.com/44325167/131115461-d1c7e0ba-797b-4d58-95c5-4924df902d09.png)

When you deploy your services using Amazon Elastic Container Service (Amazon ECS), you can use dynamic port mapping to support multiple tasks from a single service on the same container instance. Amazon ECS manages updates to your services by automatically registering and deregistering containers with your target group using the instance ID and port for each container.

![image](https://user-images.githubusercontent.com/44325167/131115983-9f821992-f535-4cb5-a5b3-557148a6c368.png)

## API 

**A company follows collaborative development practices. The engineering manager wants to isolate the development effort by setting up simulations of API components owned by various development teams. Which API integration type is best suited for this requirement?**

**MOCK**

This type of integration lets API Gateway return a response without sending the request further to the backend. This is useful for API testing because it can be used to test the integration setup without incurring charges for using the backend and to enable collaborative development of an API.

In collaborative development, a team can isolate their development effort by setting up simulations of API components owned by other teams by using the MOCK integrations. It is also used to return CORS-related headers to ensure that the API method permits CORS access. In fact, the API Gateway console integrates the OPTIONS method to support CORS with a mock integration.

### Your AWS CodeDeploy deployment to T2 instances succeed. The new application revision makes API calls to Amazon S3 however the application is not working as expected due to authorization exceptions and you were assigned to troubleshoot the issue. Which of the following should you do?

**Fix the IAM permissions for the EC2 instance role**

You should use an IAM role to manage temporary credentials for applications that run on an EC2 instance. When you use a role, you don't have to distribute long-term credentials (such as a user name and password or access keys) to an EC2 instance. Instead, the role supplies temporary permissions that applications can use when they make calls to other AWS resources. In this case, make sure your role has access to the S3 bucket.


### You have a Java-based application running on EC2 instances loaded with AWS CodeDeploy agents. You are considering different options for deployment, one is the flexibility that allows for incremental deployment of your new application versions and replaces existing versions in the EC2 instances. The other option is a strategy in which an Auto Scaling group is used to perform a deployment. Which of the following options will allow you to deploy in this manner? (Select two)

**In-place Deployment**

The application on each instance in the deployment group is stopped, the latest application revision is installed, and the new version of the application is started and validated. You can use a load balancer so that each instance is deregistered during its deployment and then restored to service after the deployment is complete.

**Blue/green Deployment**

With a blue/green deployment, you provision a new set of instances on which CodeDeploy installs the latest version of your application. CodeDeploy then re-routes load balancer traffic from an existing set of instances running the previous version of your application to the new set of instances running the latest version. After traffic is re-routed to the new instances, the existing instances can be terminated.

### An IT company is using AWS CloudFormation to manage its IT infrastructure. It has created a template to provision a stack with a VPC and a subnet. The output value of this subnet has to be used in another stack. As a Developer Associate, which of the following options would you suggest to provide this information to another stack?

**Use 'Export' field in the Output section of the stack's template**

To share information between stacks, export a stack's output values. Other stacks that are in the same AWS account and region can import the exported values.

To export a stack's output value, use the Export field in the Output section of the stack's template. To import those values, use the Fn::ImportValue function in the template for the other stacks.


### An e-commerce company has implemented AWS CodeDeploy as part of its AWS cloud CI/CD strategy. The company has configured automatic rollbacks while deploying a new version of its flagship application to Amazon EC2. What occurs if the deployment of the new version fails?

**A new deployment of the last known working version of the application is deployed with a new deployment ID**

AWS CodeDeploy is a service that automates code deployments to any instance, including Amazon EC2 instances and instances running on-premises. AWS CodeDeploy makes it easier for you to rapidly release new features, helps you avoid downtime during deployment, and handles the complexity of updating your applications.

CodeDeploy rolls back deployments by redeploying a previously deployed revision of an application as a new deployment. These rolled-back deployments are technically new deployments, with new deployment IDs, rather than restored versions of a previous deployment.

To roll back an application to a previous revision, you just need to deploy that revision. AWS CodeDeploy keeps track of the files that were copied for the current revision and removes them before starting a new deployment, so there is no difference between redeploy and rollback. However, you need to make sure that the previous revisions are available for rollback.

### A communication platform serves millions of customers and deploys features in a production environment on AWS via CodeDeploy. You are reviewing scripts for the deployment process located in the AppSec file. Which of the following options lists the correct order of lifecycle events?

**DownloadBundle => BeforeInstall => ApplicationStart => ValidateService**

AWS CodeDeploy is a fully managed deployment service that automates software deployments to a variety of compute services such as Amazon EC2, AWS Fargate, AWS Lambda, and your on-premises servers. AWS CodeDeploy makes it easier for you to rapidly release new features, helps you avoid downtime during application deployment, and handles the complexity of updating your applications.

You can specify one or more scripts to run in a hook. Each hook for a lifecycle event is specified with a string on a separate line.


### Your company is in the process of building a DevOps culture and is moving all of its on-premise resources to the cloud using serverless architectures and automated deployments. You have created a CloudFormation template in YAML that uses an AWS Lambda function to pull HTML files from GitHub and place them into an Amazon Simple Storage Service (S3) bucket that you specify. Which of the following AWS CLI commands can you use to upload AWS Lambda functions and AWS CloudFormation templates to AWS?

**cloudformation package and cloudformation deploy**

AWS CloudFormation gives developers and businesses an easy way to create a collection of related AWS and third-party resources and provision them in an orderly and predictable fashion.

### A development team is considering Amazon ElastiCache for Redis as its in-memory caching solution for its relational database. Which of the following options are correct while configuring ElastiCache? (Select two)

**All the nodes in a Redis cluster must reside in the same region**

All the nodes in a Redis cluster (cluster mode enabled or cluster mode disabled) must reside in the same region.

**While using Redis with cluster mode enabled, you cannot manually promote any of the replica nodes to primary**

While using Redis with cluster mode enabled, there are some limitations:

You cannot manually promote any of the replica nodes to primary.

Multi-AZ is required.

You can only change the structure of a cluster, the node type, and the number of nodes by restoring from a backup.


### You have been hired at a company that needs an experienced developer to help with a continuous integration/continuous delivery (CI/CD) workflow on AWS. You configure the company’s workflow to run an AWS CodePipeline pipeline whenever the application’s source code changes in a repository hosted in AWS Code Commit and compiles source code with AWS Code Build. You are configuring ProjectArtifacts in your build stage. Which of the following should you do?

**Give AWS CodeBuild permissions to upload the build output to your Amazon S3 bucket**

If you choose ProjectArtifacts and your value type is S3 then the build project stores build output in Amazon Simple Storage Service (Amazon S3). For that, you will need to give AWS CodeBuild permissions to upload.


### A data analytics company with its IT infrastructure on the AWS Cloud wants to build and deploy its flagship application as soon as there are any changes to the source code. As a Developer Associate, which of the following options would you suggest to trigger the deployment? (Select two)

**Keep the source code in an AWS CodeCommit repository and start AWS CodePipeline whenever a change is pushed to the CodeCommit repository**

**Keep the source code in an Amazon S3 bucket and start AWS CodePipeline whenever a file in the S3 bucket is updated**

AWS CodePipeline is a fully managed continuous delivery service that helps you automate your release pipelines for fast and reliable application and infrastructure updates. CodePipeline automates the build, test, and deploy phases of your release process every time there is a code change, based on the release model you define.

Using change detection methods that you specify, you can make your pipeline start when a change is made to a repository. You can also make your pipeline start on a schedule.

When you use the console to create a pipeline that has a CodeCommit source repository or S3 source bucket, CodePipeline creates an Amazon CloudWatch Events rule that starts your pipeline when the source changes. This is the recommended change detection method.

If you use the AWS CLI to create the pipeline, the change detection method defaults to starting the pipeline by periodically checking the source (CodeCommit, Amazon S3, and GitHub source providers only). AWS recommends that you disable periodic checks and create the rule manually.
