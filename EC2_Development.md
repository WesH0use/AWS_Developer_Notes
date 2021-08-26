## EC2

### Instance Purchasing Options

**Dedicated Instances** - Dedicated Instances are Amazon EC2 instances that run in a virtual private cloud (VPC) on hardware that's dedicated to a single customer. Dedicated Instances that belong to different AWS accounts are physically isolated at a hardware level, even if those accounts are linked to a single-payer account. However, Dedicated Instances may share hardware with other instances from the same AWS account that are not Dedicated Instances. A Dedicated Host is also a physical server that's dedicated for your use. With a Dedicated Host, you have visibility and control over how instances are placed on the server.

**Spot Instances** - A Spot Instance is an unused EC2 instance that is available for less than the On-Demand price. Your Spot Instance runs whenever capacity is available and the maximum price per hour for your request exceeds the Spot price. Any instance present with unused capacity will be allocated. Even though this is cost-effective, it does not fulfill the single-tenant hardware requirement of the client and hence is not the correct option.

**Dedicated Hosts** - An Amazon EC2 Dedicated Host is a physical server with EC2 instance capacity fully dedicated to your use. Dedicated Hosts allow you to use your existing software licenses on EC2 instances. With a Dedicated Host, you have visibility and control over how instances are placed on the server. This option is costlier than the Dedicated Instance.

**On-Demand Instances** - With On-Demand Instances, you pay for compute capacity by the second with no long-term commitments. You have full control over its lifecycle—you decide when to launch, stop, hibernate, start, reboot, or terminate it. Hardware isolation is not possible and on-demand has one of the costliest instance charges.

### EC2 Auto Scaling 

Amazon EC2 Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application. You create collections of EC2 instances, called Auto Scaling groups. You can specify the minimum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes below this size. You can specify the maximum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes above this size. If you specify the desired capacity, either when you create the group or at any time thereafter, Amazon EC2 Auto Scaling ensures that your group has this many instances. If you specify scaling policies, then Amazon EC2 Auto Scaling can launch or terminate instances as demand on your application increases or decreases.

**An Auto Scaling group can contain EC2 instances in one or more Availability Zones within the same Region**

**Amazon EC2 Auto Scaling attempts to distribute instances evenly between the Availability Zones that are enabled for your Auto Scaling group** - When one Availability Zone becomes unhealthy or unavailable, Auto Scaling launches new instances in an unaffected Availability Zone. When the unhealthy Availability Zone returns to a healthy state, Auto Scaling automatically redistributes the application instances evenly across all of the designated Availability Zones.

**For Auto Scaling groups in a VPC, the EC2 instances are launched in subnets** - For Auto Scaling groups in a VPC, the EC2 instances are launched in subnets. Customers can select the subnets for your EC2 instances when you create or update the Auto Scaling group.

--<br>
**Burstable performance instances**, which are T3, T3a, and T2 instances, are designed to provide a baseline level of CPU performance with the ability to burst to a higher level when required by your workload. Burstable performance instances are the only instance types that use credits for CPU usage.

**AWS states that, if your AWS account is less than 12 months old, you can use a t2.micro instance for free within certain usage limits.**

# Practice Questions 

## A startup with newly created AWS account is testing different EC2 instances. They have used Burstable performance instance - T2.micro - for 35 seconds and stopped the instance. At the end of the month, what is the instance usage duration that the company is charged for?

**0 seconds - AWS states that, if your AWS account is less than 12 months old, you can use a t2.micro instance for free within certain usage limits.**

## A company is looking at optimizing their Amazon EC2 instance costs. Few instances are sure to run for a few years, but the instance type might change based on business requirements. Which EC2 instance purchasing option should they opt to meet the reduced cost criteria?

Reserved Instances offer significant savings on Amazon EC2 costs compared to On-Demand Instance pricing. A Reserved Instance can be purchased for a one-year or three-year commitment, with the three-year commitment offering a bigger discount. Reserved instances come with two offering classes - Standard or Convertible.

**Convertible Reserved instances** - A Convertible Reserved Instance can be exchanged during the term for another Convertible Reserved Instance with new attributes including instance family, instance type, platform, scope, or tenancy. This is the best fit for the current requirement.

## An IT company is configuring Auto Scaling for its Amazon EC2 instances spread across different AZs and Regions. Which of the following scenarios are  correct about EC2 Auto Scaling? (Select three)

**An Auto Scaling group can contain EC2 instances in one or more Availability Zones within the same Region** - This is a valid statement. Auto Scaling groups can span across the availability Zones of a Region.

**Amazon EC2 Auto Scaling attempts to distribute instances evenly between the Availability Zones that are enabled for your Auto Scaling group** - When one Availability Zone becomes unhealthy or unavailable, Auto Scaling launches new instances in an unaffected Availability Zone. When the unhealthy Availability Zone returns to a healthy state, Auto Scaling automatically redistributes the application instances evenly across all of the designated Availability Zones.

**For Auto Scaling groups in a VPC, the EC2 instances are launched in subnets - For Auto Scaling groups in a VPC, the EC2 instances are launched in subnets. Customers can select the subnets for your EC2 instances when you create or update the Auto Scaling group.**

## A media publishing company is using Amazon EC2 instances for running their business-critical applications. Their IT team is looking at reserving capacity apart from savings plans for the critical instances. As a Developer Associate, which of the following reserved instance types you would select to provide capacity reservations?

When you purchase a Reserved Instance for a specific Availability Zone, it's referred to as a **Zonal Reserved Instance**. **Zonal Reserved Instances provide *capacity reservations* as well as discounts.**

**Zonal Reserved Instances** - A zonal Reserved Instance provides a capacity reservation in the specified Availability Zone. Capacity Reservations enable you to reserve capacity for your Amazon EC2 instances in a specific Availability Zone for any duration. This gives you the ability to create and manage Capacity Reservations independently from the billing discounts offered by Savings Plans or regional Reserved Instances.

Regional vs Zonal Reserved Instances:

**A zonal Reserved Instance reserves capacity in the specified Availability Zone. A regional on does not.** 



