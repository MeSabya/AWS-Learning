
## Your company shares some HR videos stored in an Amazon S3 bucket via CloudFront. You need to restrict access to the private content so users coming from specific IP addresses can access the videos and also to ensure that direct access via the Amazon S3 bucket is not possible.How can this be achieved?

1. Configure CloudFront to require users to access the files using signed cookies, create an Origin Access Identity (OAI), and instruct users to login with the OAI.
2. Configure CloudFront to require users to access the files using a signed URL, create an Origin Access Identity (OAI), and restrict access to the files in the Amazon S3 bucket to the OAI.
3. Configure CloudFront to require users to access the files using signed cookies, and move the files to an encrypted EBS volume.
4. Configure CloudFront to require users to access the files using a signed URL, and configure the S3 bucket as a website endpoint.

**Correct Answer: 2**

**Explanation:**

A signed URL includes additional information (for example, expiration date and time) that gives you more control over access to your content. You can also specify the IP address (or range of IP addresses) of the users who can access your content.

If you use CloudFront signed URLs (or signed cookies) to limit access to files in your Amazon S3 bucket, you may also want to prevent users from directly accessing your S3 files by using Amazon S3 URLs. To achieve this, you can create an Origin Access Identity (OAI), which is a special CloudFront user, and associate the OAI with your distribution.

You can then change the permissions either on your Amazon S3 bucket or on the files in your bucket so that only the OAI has read permission (or read and download permission).

INCORRECT: “Configure CloudFront to require users to access the files using signed cookies, create an Origin Access Identity (OAI), and instruct users to login with the OAI.” is incorrect. Users cannot login with an OAI.

CORRECT: “Configure CloudFront to require users to access the files using a signed URL, create an Origin Access Identity (OAI), and restrict access to the files in the Amazon S3 bucket to the OAI.” is the correct answer.

INCORRECT: “Configure CloudFront to require users to access the files using signed cookies, and move the files to an encrypted EBS volume.” is incorrect. You cannot use CloudFront and an OAI when your S3 bucket is configured as a website endpoint.

INCORRECT: “Configure CloudFront to require users to access the files using a signed URL, and configure the S3 bucket as a website endpoint.” is incorrect. You cannot use CloudFront to pull data directly from an EBS volume.

## An application you are designing receives and processes files. The files are typically around 4 GB in size, and the application extracts metadata from the files, which typically takes a few seconds for each file. The pattern of updates is highly dynamic, with times of little activity and then multiple uploads within a short period of time.What architecture will address this workload in the most cost-efficient manner?

1. Use a Kinesis data stream to store the file, and use Lambda for processing.
2. Store the file in an EBS volume, which can then be accessed by another EC2 instance for processing.
3. Upload files into an S3 bucket, and use the Amazon S3 event notification to invoke a Lambda function to extract the metadata.
4. Place the files in an SQS queue, and use a fleet of EC2 instances to extract the metadata.

**Explanation:**

Storing the file in an S3 bucket is the most cost-efficient solution, and using S3 event notifications to invoke a Lambda function works well for this unpredictable workload.

The following diagram depicts a similar architecture where users upload documents to an Amazon S3 bucket, and an event notification triggers a Lambda function that resizes the image.

![image](https://user-images.githubusercontent.com/33947539/155976057-2ccfa0e5-3785-434d-8212-52119e0752d4.png)

INCORRECT: “Use a Kinesis data stream to store the file, and use Lambda for processing.” is incorrect. Kinesis data streams run on EC2 instances, and therefore, you must provision some capacity even when the application is not receiving files. This is not as cost-efficient as storing them in an S3 bucket prior to using Lambda for the processing.

INCORRECT: “Store the file in an EBS volume, which can then be accessed by another EC2 instance for processing.” is incorrect. Storing the file in an EBS volume and using EC2 instances for processing is not cost efficient.

CORRECT: “Upload files into an S3 bucket, and use the Amazon S3 event notification to invoke a Lambda function to extract the metadata.” is the correct answer.

INCORRECT: “Place the files in an SQS queue, and use a fleet of EC2 instances to extract the metadata.” is incorrect. SQS queues have a maximum message size of 256 KB. You can use the extended client library for Java to use pointers to a payload on S3, but the maximum payload size is 2 GB.
