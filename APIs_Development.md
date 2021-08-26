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
