# What is Amazon S3 Replication?

Amazon Simple Storage Service (S3) Replication is an elastic, fully managed, low-cost feature that replicates objects between buckets.

- Replication enables automatic, asynchronous copying of objects across Amazon S3 buckets. 
- Buckets that are configured for object replication can be owned by the same AWS account or by different accounts.
- You can copy objects between different AWS Regions or within the same Region.
- Amazon S3 Replication now provides detailed metrics and notifications to monitor the status of object replication between buckets.
- Using cloudwatch we can monitor replication progress by tracking bytes pending, operations pending, and replication latency between your source and destination buckets.
- Using S3 Event Notifications we can easily receive replication failure notifications to quickly diagnose and correct configuration issues.

## Types of Replication:

- **SAME REGION REPLICATION**: The source and destination buckets will be in the same region and the S3 objects are copied within the region.
- **CROSS REGION REPLICATION**: It is used to copy across the S3 buckets in the different AWS Region.

## When to use S3 Replication:

**Data redundancy** — If you need to maintain multiple copies of your data in the same, or different AWS Regions, with different encryption types, or across different accounts. S3 Replication powers your global content distribution needs, compliant storage needs, and data sharing across accounts.

**Replicate objects while retaining metadata** — If you need to ensure your replica copies are identical to the source data, you can use S3 Replication to make copies of your objects that retain all metadata, such as the original object creation time, object access control lists (ACLs), and version IDs.

**Replicate objects to more cost-effective storage classes** — You can use S3 Replication to put objects into S3 Glacier, S3 Glacier Deep Archive, or another storage class in the destination buckets. You can also replicate your data to the same storage class and then use S3 Lifecyle policies to move your objects to a more cost-effective storage.

**Maintain object copies under a different account** — Regardless of who owns the source object, you can tell Amazon S3 to change replica ownership to the AWS account that owns the destination bucket to restrict access to object replicas.

**Replicate your objects within 15 minutes** — You can use Amazon S3 Replication Time Control (S3 RTC) to replicate your data in a predictable time frame. S3 RTC replicates 99.99 percent of new objects stored in Amazon S3 within 15 minutes of upload and is backed by a Service Level Agreement (SLA).

## Requirements for Replication:

- versioning should be enabled in both the source and the destination buckets.
- Amazon S3 must have the permission to copy the objects from one region to another.
- The source bucket owner must have the source and destination AWS Regions enabled for their account. The destination bucket owner must have the destination Region-enabled for their account.
- If the source bucket has Amazon S3 object lock enabled, the destination bucket must also have object lock enabled.
- If the owner of the source bucket doesn’t own the object in the bucket, the object owner must grant the bucket owner READ and READ_ACP permissions with the object access control list.

> Amazon S3 events are available through Amazon Simple Queue Service (Amazon SQS), Amazon Simple Notification Service (Amazon SNS), or AWS Lambda.


