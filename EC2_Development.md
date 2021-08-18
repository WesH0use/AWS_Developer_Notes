## EC2

### Instance Purchasing Options

**On-Demand Instances** – Pay, by the second, for the instances that you launch.

**Reserved Instances** – Reserved Instances offer significant savings on Amazon EC2 costs compared to On-Demand Instance pricing. A Reserved Instance can be purchased for a one-year or three-year commitment, with the three-year commitment offering a bigger discount. Reserved instances come with two offering classes - Standard or Convertible.

**Convertible Reserved instances** - A Convertible Reserved Instance can be exchanged during the term for another Convertible Reserved Instance with new attributes including instance family, instance type, platform, scope, or tenancy. 

**Spot Instances** – Request unused EC2 instances, which can reduce your Amazon EC2 costs significantly.

**Dedicated Hosts** – Pay for a physical host that is fully dedicated to running your instances, and bring your existing per-socket, per-core, or per-VM software licenses to reduce costs.

**Dedicated Instances** – Pay, by the hour, for instances that run on single-tenant hardware.

**Scheduled Reserved instances** - Scheduled Reserved Instances (Scheduled Instances) enable you to purchase capacity reservations that recur on a daily, weekly, or monthly basis, with a specified start time and duration, for a one-year term. You reserve the capacity in advance so that you know it is available when you need it.

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

