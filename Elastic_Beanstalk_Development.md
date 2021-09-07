
# Elastic Beanstalk 

When processing a batch, Elastic Beanstalk detaches all instances in the batch from the load balancer, deploys the new application version, and then reattaches the instances. If you enable connection draining, Elastic Beanstalk drains existing connections from the Amazon EC2 instances in each batch before beginning the deployment.

**If a deployment fails after one or more batches completed successfully, the completed batches run the new version of your application while any pending batches continue to run the old version.** You can identify the version running on the instances in your environment on the health page in the console. This page displays the deployment ID of the most recent deployment that was executed on each instance in your environment. **If you terminate instances from the failed deployment, Elastic Beanstalk replaces them with instances running the application version from the most recent successful deployment.**

When creating configuration files for AWS Elastic Beanstalk which naming convention should you follow?

**.ebextensions/<my_settings>.config**

.ebextensions/<mysettings>.config : You can add AWS Elastic Beanstalk configuration files (.ebextensions) to your web application's source code to configure your environment and customize the AWS resources that it contains. Configuration files are YAML or JSON formatted documents with a .config file extension that you place in a folder named .ebextensions and deploy in your application source bundle.
  
## Practice Questions 
  
# You have chosen AWS Elastic Beanstalk to upload your application code and allow it to handle details such as provisioning resources and monitoring. When creating configuration files for AWS Elastic Beanstalk which naming convention should you follow?
  
  
# The development team at a social media company is considering using Amazon ElastiCache to boost the performance of their existing databases. As a Developer Associate, which of the following use-cases would you recommend as the BEST fit for ElastiCache? 
  
**Use ElastiCache to improve latency and throughput for read-heavy application workloads**
  
**Use ElastiCache to improve performance of compute-intensive workloads**

Amazon ElastiCache allows you to run in-memory data stores in the AWS cloud. Amazon ElastiCache is a popular choice for real-time use cases like Caching, Session Stores, Gaming, Geospatial Services, Real-Time Analytics, and Queuing.

Amazon ElastiCache can be used to significantly improve latency and throughput for many read-heavy application workloads (such as social networking, gaming, media sharing, and Q&A portals) or compute-intensive workloads (such as a recommendation engine) by allowing you to store the objects that are often read in the cache.
  
![image](https://user-images.githubusercontent.com/44325167/131362722-38decc12-89dc-4800-8a05-59c39d94e516.png)

  
### A .NET developer team works with many ASP.NET web applications that use EC2 instances to host them on IIS. The deployment process needs to be configured so that multiple versions of the application can run in AWS Elastic Beanstalk. One version would be used for development, testing, and another version for load testing. Which of the following methods do you recommend?
  
**Define a dev environment with a single instance and a 'load test' environment that has settings close to production environment**

AWS Elastic Beanstalk makes it easy to create new environments for your application. You can create and manage separate environments for development, testing, and production use, and you can deploy any version of your application to any environment. Environments can be long-running or temporary. When you terminate an environment, you can save its configuration to recreate it later.

It is common practice to have many environments for the same application. You can deploy multiple environments when you need to run multiple versions of an application. So for the given use-case, you can set up 'dev' and 'load test' environment.
