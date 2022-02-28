
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

## An organization wants to share regular updates about their charitable work using static web pages. The pages are expected to generate a large number of views from around the world. The files are stored in an Amazon S3 bucket. Which action should the solutions architect take to accomplish this?

1. Generate pre-signed URLs for the files.
2. Use Cross-Region Replication to all Regions.
3. Use the geoproximity feature of Amazon Route 53.
4. Use Amazon CloudFront with the S3 bucket as its origin.

**Explanation:** 

Using Amazon CloudFront to cache the files in edge locations around the world will improve the performance of the webpages.

To serve a static website hosted on Amazon S3, you can deploy a CloudFront distribution using one of these configurations:

Using a REST API endpoint as the origin with access restricted by an origin access identity (OAI)
Using a website endpoint as the origin with anonymous (public) access allowed
Using a website endpoint as the origin with access restricted by a Referer header
INCORRECT: “Generate presigned URLs for the files.” is incorrect as this is used to restrict access, which is not a requirement.

INCORRECT: “Use Cross-Region Replication to all Regions.” is incorrect as this does not provide a mechanism for directing users to the closest copy of the static web pages.

INCORRECT: “Use the geoproximity feature of Amazon Route 53.” is incorrect as this does not include a solution for having multiple copies of the data in different geographic locations.

CORRECT: “Use Amazon CloudFront with the S3 bucket as its origin.” is the correct answer.

## An application receives images uploaded by customers and stores them on Amazon S3. An AWS Lambda function then processes the images to add graphical elements. The processed images need to be available for users to download for 30 days, after which they can be deleted. Processed images can be easily recreated from original images. The original images need to be immediately available for 30 days in addition to being accessible within 24 hours for another 90 days.Which combination of Amazon S3 storage classes is most cost-effective for the original and processed images? (Select TWO)

1. Store the original images in STANDARD for 30 days, transition to GLACIER for 90 days, and then expire the data.
2. Store the original images in STANDARD_IA for 30 days, and then transition to DEEP_ARCHIVE.
3. Store the processed images in ONEZONE_IA, and then expire the data after 30 days.
4. Store the processed images in STANDARD, and then transition to GLACIER after 30 days.
5. Store the original images in STANDARD for 30 days, transition to DEEP_ARCHIVE for 90 days, and then expire the data.

Explanation: The key requirements for the original images are that they must be immediately available for 30 days (STANDARD), available within 24 hours for 90 days (GLACIER), after which they will not be needed (expire them).

The key requirements for the processed images are that they must be immediately available for 30 days (ONEZONE_IA as they can be recreated from the originals), after which they are not needed (expire them).

CORRECT: “Store the original images in STANDARD for 30 days, transition to GLACIER for 90 days, and then expire the data.” is a correct answer.

INCORRECT: “Store the original images in STANDARD_IA for 30 days and then transition to DEEP_ARCHIVE.” is incorrect. DEEP_ARCHIVE has a minimum storage duration of 180 days.

CORRECT: “Store the processed images in ONEZONE_IA, and then expire the data after 30 days.” is also a correct answer.

INCORRECT: “Store the processed images in STANDARD, and then transition to GLACIER after 30 days.” is incorrect. There is no need to transition the processed images to GLACIER as they are not needed after 30 days and they can be recreated from the originals if needed.

INCORRECT: “Store the original images in STANDARD for 30 days, transition to DEEP_ARCHIVE for 90 days, then expire the data.” is incorrect. DEEP_ARCHIVE has a minimum storage duration of 180 days.


