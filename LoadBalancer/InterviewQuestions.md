## The company you work for is currently transitioning its infrastructure and applications into the AWS cloud. You are planning to deploy an Elastic Load Balancer (ELB) that distributes traffic for a web application running on EC2 instances. You still have some application servers running on-premise, and you would like to distribute application traffic across both your AWS and on-premises resources.

**Explanation:**

The ALB (and NLB) supports IP addresses as well as instance IDs as targets. When you create a target group, you specify its target type, which determines how you specify its targets. After you create a target group, you cannot change its target type.

Using IP addresses as targets allows load balancing any application hosted in AWS or on-premises using IP addresses of the application back-ends as targets.

You must have a VPN or Direct Connect connection to enable this configuration to work.

CORRECT: “Provision a Direct Connect connection between your on-premises location and AWS. Create a target group on an ALB to use IP based targets for both your EC2 instances and on-premises servers.” is the correct answer.

INCORRECT: “Provision a Direct Connect connection between your on-premises location and AWS. Create a target group on an ALB to use Instance ID-based targets for both your EC2 instances and on-premises servers.” is incorrect. You cannot use instance ID-based targets for on-premises servers, and you cannot mix instance ID and IP address target types in a single target group.

INCORRECT: “Provision an IPSec VPN connection between your on-premises location and AWS. Create a CLB that uses cross-zone load balancing to distribute traffic across EC2 instances and on-premises servers.” is incorrect. The CLB does not support IP addresses as targets.

INCORRECT: “This cannot be done; ELBs are an AWS service and can only distribute traffic within the AWS cloud.” is incorrect as this statement is false.

![image](https://user-images.githubusercontent.com/33947539/157821705-b34941ef-e091-42db-8acc-7441c308aa73.png)

Explanation: To increase the resiliency of the application, the solutions architect can use Auto Scaling groups to launch and terminate instances across multiple Availability Zones based on demand. An Application Load Balancer (ALB) can be used to direct traffic to the web application running on the EC2 instances. Lastly, the Amazon Elastic File System (EFS) can assist with increasing the resiliency of the application by providing a shared file system that can be mounted by multiple EC2 instances from multiple Availability Zones.

INCORRECT: “Launch the application on EC2 instances in each Availability Zone. Attach EBS volumes to each EC2 instance.” is incorrect as the EBS volumes are single points of failure that are not shared with other instances.

INCORRECT: “Create an Application Load Balancer with Auto Scaling groups across multiple Availability Zones. Mount an instance store on each EC2 instance.” is incorrect as instance stores are ephemeral data stores, which means data is lost when powered down. Also, instance stores cannot be shared between instances.

CORRECT: “Create an Application Load Balancer with Auto Scaling groups across multiple Availability Zones. Store data on Amazon EFS, and mount a target on each instance.” is the correct answer.

INCORRECT: “Create an Application Load Balancer with Auto Scaling groups across multiple Availability Zones. Store data using Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA).” is incorrect as there are data retrieval charges associated with this S3 tier. It is not a suitable storage tier for application files.

