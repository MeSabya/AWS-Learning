```Lua
Your company shares some HR videos stored in an Amazon S3 bucket via CloudFront. 
You need to restrict access to the private content so users coming from specific IP addresses can access the videos 
and also to ensure that direct access via the Amazon S3 bucket is not possible.

How can this be achieved?

1. Configure CloudFront to require users to access the files using signed cookies, create an Origin Access Identity (OAI), and instruct users to login with the OAI.
2. Configure CloudFront to require users to access the files using a signed URL, create an Origin Access Identity (OAI), and restrict access to the files in the Amazon S3 bucket to the OAI.
3. Configure CloudFront to require users to access the files using signed cookies, and move the files to an encrypted EBS volume.
4. Configure CloudFront to require users to access the files using a signed URL, and configure the S3 bucket as a website endpoint.
```
**Correct Answer: 2**

**Explanation:**

A signed URL includes additional information (for example, expiration date and time) that gives you more control over access to your content. You can also specify the IP address (or range of IP addresses) of the users who can access your content.

If you use CloudFront signed URLs (or signed cookies) to limit access to files in your Amazon S3 bucket, you may also want to prevent users from directly accessing your S3 files by using Amazon S3 URLs. To achieve this, you can create an Origin Access Identity (OAI), which is a special CloudFront user, and associate the OAI with your distribution.

You can then change the permissions either on your Amazon S3 bucket or on the files in your bucket so that only the OAI has read permission (or read and download permission).

INCORRECT: “Configure CloudFront to require users to access the files using signed cookies, create an Origin Access Identity (OAI), and instruct users to login with the OAI.” is incorrect. Users cannot login with an OAI.

CORRECT: “Configure CloudFront to require users to access the files using a signed URL, create an Origin Access Identity (OAI), and restrict access to the files in the Amazon S3 bucket to the OAI.” is the correct answer.

INCORRECT: “Configure CloudFront to require users to access the files using signed cookies, and move the files to an encrypted EBS volume.” is incorrect. You cannot use CloudFront and an OAI when your S3 bucket is configured as a website endpoint.

INCORRECT: “Configure CloudFront to require users to access the files using a signed URL, and configure the S3 bucket as a website endpoint.” is incorrect. You cannot use CloudFront to pull data directly from an EBS volume.
