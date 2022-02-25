![image](https://user-images.githubusercontent.com/33947539/155714758-5166a2e2-6a99-4b6d-84f2-717d9831de5a.png)

**Explanation:**

The Amazon S3 notification feature enables you to receive notifications when certain events happen in your bucket. To enable notifications, you must first add a notification configuration that identifies the events you want Amazon S3 to publish and the destinations where you want Amazon S3 to send the notifications. You store this configuration in the notification subresource that is associated with a bucket.

AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for customers to prepare and load their data for analytics.

With this solution, S3 event notifications triggering a Lambda function is completely serverless and cost-effective, and AWS Glue can trigger ETL jobs that will transform that data and load it into a data store such as S3.

INCORRECT: “Configure a CloudWatch alarm to send a notification to CloudFormation when data is uploaded.” is incorrect. Using event notifications is the best solution.

CORRECT: “Configure S3 event notifications to trigger a Lambda function when data is uploaded, and use the Lambda function to trigger the ETL job.” is a correct answer.

INCORRECT: “Configure CloudFormation to provision a Kinesis data stream to transform the data and load it into S3.” is incorrect. Kinesis Data Streams is used for processing data rather than extracting and transforming it. Kinesis consumers are EC2 instances that are not as cost-effective as serverless solutions.

CORRECT: “Use AWS Glue to extract, transform and load the data into the target data store.” is also a correct answer.

INCORRECT: “Configure CloudFormation to provision AWS Data Pipeline to transform the data.” is incorrect. AWS Data Pipeline can be used to automate the movement and transformation of data; it relies on other services to actually transform the data.

![image](https://user-images.githubusercontent.com/33947539/155716326-3ff8abd0-f3ba-4f52-8663-7592af4fc98b.png)

**Explanation:**

In this scenario, you need to connect the EC2 instances to the SaaS application with a source address of one of two whitelisted public IP addresses to ensure authentication works.

A NAT gateway is created in a specific AZ and can have a single Elastic IP address associated with it. NAT gateways are deployed in public subnets. The route tables of the private subnets where the EC2 instances reside are configured to forward Internet-bound traffic to the NAT gateway. You pay for using a NAT gateway based on hourly usage and data processing; however, this is still a cost-effective solution.

The diagram below depicts an instance in a private subnet using a NAT gateway to connect to the Internet via an Internet gateway.

![image](https://user-images.githubusercontent.com/33947539/155716384-efc7a117-46fd-4b93-9e84-b8d1d1106e0a.png)

INCORRECT: “Use a Network Load Balancer, and configure a static IP for each AZ.” is incorrect. A Network Load Balancer can be configured with a single static IP address (the other types of ELB cannot) for each AZ. However, using an NLB is not an appropriate solution as the connections are being made outbound from the EC2 instances to the SaaS app, and ELBs are used for distributing inbound connection requests to EC2 instances (only the return traffic goes back through the ELB).

INCORRECT: “Use multiple Internet-facing Application Load Balancers with Elastic IP addresses.” is incorrect. An ALB does not support static IP addresses and is not suitable for a proxy function.

INCORRECT: “Configure redundant Internet gateways, and update the routing tables for each subnet.” is incorrect as you cannot create multiple Internet gateways. An IGW is already redundant.

CORRECT: “Configure a NAT gateway for each AZ with an Elastic IP address.” is the correct answer.

![image](https://user-images.githubusercontent.com/33947539/155717054-faf965e0-9edd-4106-80e3-a1cc9b4f6761.png)

**Explanation:**

An Application Load Balancer is a type of Elastic Load Balancer that can use layer 7 (HTTP/HTTPS) protocol data to make forwarding decisions. An ALB supports both path-based (e.g., /images or /orders) and host-based routing (e.g., example.com).

In this scenario, a single EC2 instance is listening for traffic for each application on a different port. You can use a target group that listens on a single port (HTTP or HTTPS) and then uses listener rules to selectively route to a different port on the EC2 instance based on the information in the URL path. So you might have example.com/images going to one backend port and example.com/orders going to a different backend port.

INCORRECT: “Amazon Route 53” is incorrect. Amazon Route 53 is a DNS service. It can be used to load balance; however, it does not have the ability to route based on information in the incoming request path.

INCORRECT: “Amazon CloudFront” is incorrect. Amazon CloudFront is used for caching content. It can route based on request path to custom origins; however, the question is not requesting a content caching service, so it’s not the best fit for this use case.

CORRECT: “Application Load Balancer (ALB)” is the correct answer.

INCORRECT: “Classic Load Balancer (CLB)” is incorrect. You cannot use host-based or path-based routing with a CLB.

