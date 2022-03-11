- Auto Scaling dynamically adds and removes EC2 instances, while Elastic Load Balancing manages incoming requests by optimally routing traffic so that no one instance is overwhelmed
- Auto Scaling helps to automatically increase the number of EC2 instances when the user demand goes up, and decrease the number of EC2 instances when demand goes down.
- ELB service helps to distribute the incoming web traffic (called the load) automatically among all the running EC2 instances.
- ELB uses load balancers to monitor traffic and handle requests that come through the Internet.
- Using ELB & Auto Scaling
      
      makes it easy to route traffic across a dynamically changing fleet of EC2 instances
      
      load balancer acts as a single point of contact for all incoming traffic to the instances in an Auto Scaling group.


![image](https://user-images.githubusercontent.com/33947539/157819415-ab5a876c-6be3-435a-8433-d427cdeee1b8.png)

## High Availability & Redundancy

- Auto Scaling can span across multiple AZs, within the same region.
- When one AZ becomes unhealthy or unavailable, Auto Scaling launches new instances in an unaffected AZ
- When the unhealthy AZs recovers, Auto Scaling redistributes the traffic across all the healthy AZs
- Elastic Load balancer can be setup to distribute incoming requests across EC2 instances in a single AZ or multiple AZs within a region
- Using Auto Scaling & ELB by spanning Auto Scaling groups across multiple AZs within a region and then setting up ELB to distribute incoming traffic across those AZs helps take advantage of the safety and reliability of geographic redundancy
- Incoming traffic is load balanced equally across all the AZs enabled for ELB

## Health Checks
- Auto Scaling group determines the health state of each instance by periodically checking the results of EC2 instance status checks
- Auto Scaling marks the instance as unhealthy and replaces the instance, if the instance fails the EC2 instance status check
- ELB also performs health checks on the EC2 instances that are registered with the it for e.g. application is available by pinging an health check page
- Auto Scaling, by default, does not replace the instance, if the ELB health check fails
- ELB health check with the instances should be used to ensure that traffic is routed only to the healthy instances
- After a load balancer is registered with an Auto Scaling group, it can be configured to use the results of the ELB health check in addition to the EC2 instance status checks to determine the health of the EC2 instances in the Auto Scaling group.

## Monitoring
- Elastic Load Balancing sends data about the load balancers and EC2 instances to Amazon CloudWatch. CloudWatch collects data about the performance of your resources and presents it as metrics.
- After registering one or more load balancers with the Auto Scaling group, Auto Scaling group can be configured to use ELB metrics (such as request latency or request count) to scale the application automatically
- 

