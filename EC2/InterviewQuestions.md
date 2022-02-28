## Amazon EC2 instances in a development environment run between 9 am and 5 pm Monday-Friday. Production instances run 24/7. Which pricing models should be used? (Select TWO)

        Spot instances for the development environment
        Reserved instances for the development environment
        Scheduled reserved instances for the development environment
        Reserved instances for the production environment
        On-Demand instances for the production environment
        
**Explanation:** 

Scheduled Instances are a good choice for workloads that do not run continuously but do run on a regular schedule. This is ideal for the development environment. Reserved Instances are a good choice for workloads that run continuously. This is a good option for the production environment.

INCORRECT: “Spot instances for the development environment” is incorrect. Spot instances are a cost-effective choice if you can be flexible about when your applications run and if your applications can be interrupted. Spot instances are not suitable for the development environment as important work may be interrupted.

INCORRECT: “Reserved instances for the development environment” is incorrect as they should be used for the production environment.

CORRECT: “Scheduled reserved instances for the development environment” is a correct answer.

CORRECT: “Reserved instances for the production environment” is also a correct answer.

INCORRECT: “On-Demand instances for the production environment” is incorrect. There is no long-term commitment required when you purchase On-Demand Instances. However, you do not get any discount, and therefore this is a very expensive option.    

## A company’s application is running on Amazon EC2 instances in a single Region. In the event of a disaster, a solutions architect needs to ensure that the resources can also be deployed to a second Region. Which combination of actions should the solutions architect take to accomplish this? (Select TWO)

        Detach a volume on an EC2 instance, and copy it to an Amazon S3 bucket in the second Region.
        Launch a new EC2 instance from an Amazon Machine Image (AMI) in the second Region.
        Launch a new EC2 instance in the second Region, and copy a volume from Amazon S3 to the new instance.
        Copy an Amazon Machine Image (AMI) of an EC2 instance, and specify the second Region for the destination.
        Copy an Amazon Elastic Block Store (Amazon EBS) volume from Amazon S3, and launch an EC2 instance in the second Region using that EBS volume.
        
**Explanation:**

You can copy an Amazon Machine Image (AMI) within or across AWS Regions using the AWS Management Console, the AWS Command Line Interface or SDKs, or the Amazon EC2 API. All of these support the CopyImage action.

Using the copied AMI, the solutions architect would be able to launch an instance from the same EBS volume in the second Region.

Note: the AMIs are stored on Amazon S3; however, you cannot view them in the S3 management console or work with them programmatically using the S3 API.

INCORRECT: “Detach a volume on an EC2 instance, and copy it to an Amazon S3 bucket in the second Region.” is incorrect. You cannot copy EBS volumes directly from EBS to Amazon S3.

CORRECT: “Launch a new EC2 instance from an Amazon Machine Image (AMI) in the second Region.” is a correct answer.

INCORRECT: “Launch a new EC2 instance in the second Region, and copy a volume from Amazon S3 to the new instance.” is incorrect. You cannot create an EBS volume directly from Amazon S3.

CORRECT: “Copy an Amazon Machine Image (AMI) of an EC2 instance, and specify the second Region for the destination.” is the second correct answer.

INCORRECT: “Copy an Amazon Elastic Block Store (Amazon EBS) volume from Amazon S3, and launch an EC2 instance in the second Region using that EBS volume.” is incorrect. You cannot create an EBS volume directly from Amazon S3.
