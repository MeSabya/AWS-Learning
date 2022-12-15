## References:
1. https://nimishgoel056.medium.com/aws-top-interview-questions-4e15be0de2cf

#### What Is an Amazon Resource Name(ARN) ?

https://www.cloudsavvyit.com/1979/what-is-an-amazon-resource-name-arn-and-how-do-i-find-mine/

#### Cloud Front Vs Global Acclerator
https://jayendrapatil.com/aws-cloudfront-vs-global-accelerator/

#### An application running video-editing software is using significant memory on an Amazon EC2 instance. How can a user track memory usage on the Amazon EC2 instance?
There is no standard metric in CloudWatch for collecting EC2 memory usage. However, you can use the CloudWatch agent to collect both system metrics and log files from Amazon EC2 instances and on-premises servers. The metrics can be pushed to a CloudWatch custom metric.

#### A mobile client requires data from several application-layer services to populate its user interface. What can the application team use to decouple the client interface from the underlying services behind them?

Amazon API Gateway decouples the client application from the back-end application-layer services by providing a single endpoint for API requests.

#### Security Group vs NACL 
https://medium.com/awesome-cloud/aws-difference-between-security-groups-and-network-acls-adc632ea29ae

#### Follow up question from the above discussion is : A company hosts a popular web application that connects to an Amazon RDS MySQL DB instance running in a private VPC subnet. The subnet was created with default ACL settings. The web servers must be accessible only to customers on an SSL connection. The database should only be accessible to web servers in a public subnet.Which solution meets these requirements without impacting other running applications?

A VPC automatically comes with a modifiable default network ACL. By default, it allows all inbound and outbound IPv4 traffic. Custom network ACLs deny everything inbound and outbound by default, but in this case, a default network ACL is being used. Inbound connections to web servers will be coming in on port 443 from the Internet, so creating a security group to allow this port from 0.0.0.0/0 and applying it to the web servers will allow this traffic.

#### Cloud Trail vs Cloud watch 
https://medium.com/awesome-cloud/aws-difference-between-cloudwatch-and-cloudtrail-16a486f8bc95

#### Follow up question from above discussion: The security team in your company is defining new policies for enabling security analysis, resource change tracking, and compliance auditing. They would like to gain visibility into user activity by recording API calls made within the company’s AWS account. The information that is logged must be encrypted. This requirement applies to all AWS Regions in which your company has services running.How will you implement this request?

CloudTrail is used for recording API calls (auditing), whereas CloudWatch is used for recording metrics (performance monitoring). The solution can be deployed with a single trail that is applied to all regions. A single KMS key can be used to encrypt log files for trails applied to all regions. CloudTrail log files are encrypted using S3 Server Side Encryption (SSE), and you can also enable encryption SSE KMS for additional security.



