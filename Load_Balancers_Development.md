## Load Balancers

<u>A load balancer accepts incoming traffic from clients and routes requests to its registered targets (such as EC2 instances) in one or more Availability Zones</u>. The load balancer also monitors the health of its registered targets and ensures that it routes traffic only to healthy targets. **When the load balancer detects an unhealthy target, it stops routing traffic to that target**. It then resumes routing traffic to that target when it detects that the target is healthy again.

Elastic Load Balancing supports three types of load balancers:
1) Application Load Balancers
2) Network Load Balancers
3) Classic Load Balancers

**Load balancers separate public traffic from private traffic** - The nodes of an internet-facing load balancer have public IP addresses. Load balancers route requests to your targets using private IP addresses. Therefore, your targets do not need public IP addresses to receive requests from users over the internet.

**Load balancers build a highly available system**- Elastic Load Balancing provides fault tolerance for your applications by automatically balancing traffic across targets – Amazon EC2 instances, containers, IP addresses, and Lambda functions – in multiple Availability Zones while ensuring only healthy targets receive traffic.

A load balancer accepts incoming traffic from clients and routes requests to its registered targets (such as EC2 instances) in one or more Availability Zones.

The nodes for a load balancer distribute requests from clients to registered targets. When cross-zone load balancing is enabled, each load balancer node distributes traffic across the registered targets in all enabled Availability Zones. When cross-zone load balancing is disabled, each load balancer node distributes traffic only across the registered targets in its Availability Zone. With Application Load Balancers, cross-zone load balancing is always enabled.

Cross Zone Load Balancing

The nodes for your load balancer distribute requests from clients to registered targets. When cross-zone load balancing is enabled, each load balancer node distributes traffic across the registered targets in all enabled Availability Zones. When cross-zone load balancing is disabled, each load balancer node distributes traffic only across the registered targets in its Availability Zone.

The following diagrams demonstrate the effect of cross-zone load balancing. There are two enabled Availability Zones, with two targets in Availability Zone A and eight targets in Availability Zone B. Clients send requests, and Amazon Route 53 responds to each request with the IP address of one of the load balancer nodes. This distributes traffic such that each load balancer node receives 50% of the traffic from the clients. Each load balancer node distributes its share of the traffic across the registered targets in its scope.

If cross-zone load balancing is enabled, each of the 10 targets receives 10% of the traffic. This is because each load balancer node can route its 50% of the client traffic to all 10 targets.

![image](https://user-images.githubusercontent.com/44325167/129888959-d1c9fe8e-eae3-44ed-8723-2b1257973c49.png)

If cross-zone load balancing is disabled:

Each of the two targets in Availability Zone A receives 25% of the traffic.

Each of the eight targets in Availability Zone B receives 6.25% of the traffic.

This is because each load balancer node can route its 50% of the client traffic only to targets in its Availability Zone.

![image](https://user-images.githubusercontent.com/44325167/129889011-d7c77a06-5553-4c0f-bb8f-d6fb82a69497.png)


## Practice Questions 

# An E-commerce business, has its applications built on a fleet of Amazon EC2 instances, spread across various Regions and AZs. The technical team has suggested using Elastic Load Balancers for better architectural design. What characteristics of an Elastic Load Balancer make it a winning choice? (Select two)

## Improve vertical scalability of the system

## Deploy EC2 instances across multiple WS regions

## Build a highly available sytem

## Seperate public traffic from private traffic


# An organization has hosted its EC2 instances in two AZs. AZ1 has two instances and AZ2 has 8 instances. The Elastic Load Balancer managing the instances in the two AZs has cross-zone load balancing enabled in its configuration. What percentage traffic will each of the instances in AZ1 receive?


## 25

## 10

## 15

## 20


### You have a popular three-tier web application that is used by users throughout the globe receiving thousands of incoming requests daily. You have AWS Route 53 policies to automatically distribute weighted traffic to the API resources located at URL api.global.com. What is an alternative way of distributing traffic to a web application?

**_ELB_**

Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions. Route 53 failover policy is similar to an ELB in that when using failover routing, it lets you route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy.
