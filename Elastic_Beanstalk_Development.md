
# Elastic Beanstalk 

When processing a batch, Elastic Beanstalk detaches all instances in the batch from the load balancer, deploys the new application version, and then reattaches the instances. If you enable connection draining, Elastic Beanstalk drains existing connections from the Amazon EC2 instances in each batch before beginning the deployment.

**If a deployment fails after one or more batches completed successfully, the completed batches run the new version of your application while any pending batches continue to run the old version.** You can identify the version running on the instances in your environment on the health page in the console. This page displays the deployment ID of the most recent deployment that was executed on each instance in your environment. **If you terminate instances from the failed deployment, Elastic Beanstalk replaces them with instances running the application version from the most recent successful deployment.**

When creating configuration files for AWS Elastic Beanstalk which naming convention should you follow?

**.ebextensions/<my_settings>.config**

.ebextensions/<mysettings>.config : You can add AWS Elastic Beanstalk configuration files (.ebextensions) to your web application's source code to configure your environment and customize the AWS resources that it contains. Configuration files are YAML or JSON formatted documents with a .config file extension that you place in a folder named .ebextensions and deploy in your application source bundle.
  
## Practice Questions 
  
# You have chosen AWS Elastic Beanstalk to upload your application code and allow it to handle details such as provisioning resources and monitoring. When creating configuration files for AWS Elastic Beanstalk which naming convention should you follow?
