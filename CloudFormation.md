## A team lead has asked you to create an AWS CloudFormation template that creates EC2 instances and RDS databases. The template should be reusable by allowing the user to input a parameter value for an Amazon EC2 AMI ID. Which of the following intrinsic function should you choose to reference the parameter?

**!Ref**

The intrinsic function Ref returns the value of the specified parameter or resource. When you specify a parameter's logical name, it returns the value of the parameter, when you specify a resource's logical name, it returns a value that you can typically use to refer to that resource such as a physical ID. Take a look at this YAML sample template:
![Screen Shot 2021-08-26 at 10 12 00 AM](https://user-images.githubusercontent.com/44325167/130926350-9b47a9db-a9b1-4d0a-b37a-82e94b55c6c5.png)
