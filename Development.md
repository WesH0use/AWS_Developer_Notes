# Development with AWS Services

## Load Balancers

<u>A load balancer accepts incoming traffic from clients and routes requests to its registered targets (such as EC2 instances) in one or more Availability Zones</u>. The load balancer also monitors the health of its registered targets and ensures that it routes traffic only to healthy targets. **When the load balancer detects an unhealthy target, it stops routing traffic to that target**. It then resumes routing traffic to that target when it detects that the target is healthy again.

Elastic Load Balancing supports three types of load balancers:
1) Application Load Balancers
2) Network Load Balancers
3) Classic Load Balancers

**Load balancers separate public traffic from private traffic** - The nodes of an internet-facing load balancer have public IP addresses. Load balancers route requests to your targets using private IP addresses. Therefore, your targets do not need public IP addresses to receive requests from users over the internet.

**Load balancers build a highly available system**- Elastic Load Balancing provides fault tolerance for your applications by automatically balancing traffic across targets – Amazon EC2 instances, containers, IP addresses, and Lambda functions – in multiple Availability Zones while ensuring only healthy targets receive traffic.

