## AWS S3 Overview — Buckets
Amazon S3 allows people to store objects (files) in “buckets” (directories).
Buckets must have a globally unique name.

👉 Buckets are defined at the region level.

Files can be 0 bytes to 5TB.
Unlimited storage, Files are stored in buckets.
When you upload a file to S3, will recieve a HTTP code 200 if upload successful.

Naming convention:
- No uppercase
- No underscore
- 3–63 characters long
- Not an IP
- Must start with lowercase letter or number

## AWS S3 Overview — Objects

**Characterstics of Objects**:

- Objects (files) have a **Key**. The key is the FULL path: <my_bucket>/my_file.txt , <my_bucket>/my_folder1/another_folder/my_file.txt

There’s no concept of “directories” within buckets (although the UI will trick you to think otherwise).
Just keys with very long names that contain slashes (“/”)

👉 **Object Values are the content of the body**

👉 **Max Size is 5TB. If uploading more than 5GB, must use “multi-part upload”**

- **Metadata** (list of text key / value pairs — system or user metadata).
- **Tags** (Unicode key / value pair — up to 10) — useful for security / lifecycle.
- **Version ID** (if versioning is enabled).

## AWS S3 -Versioning
- You can version your files in AWS S3.
- 👉 **It is enabled at the bucket level**.
- Same key overwrite will increment the “version”: 1, 2, 3….
- It is best practice to version your buckets.
- Protect against unintended deletes (ability to restore a version).
- Easy roll back to previous version.
- Any file that is not versioned prior to enabling versioning will have version “null”.

## AWS S3 Encryption for Objects

There are 4 methods of encrypting objects in S3:
        1. SSE-S3: encrypts S3 objects using keys handled & managed by AWS.
        2. SSE-KMS: leverage AWS Key Management Service to manage encryption keys.
        3. SSE-C: when you want to manage your own encryption keys.
        4. Client Side Encryption.
        
### SSE-S3
SSE-S3: encryption using keys handled & managed by AWS S3. Object is encrypted server side
AES-256 encryption type
Must set header: “x-amz-server-side-encryption”: “AES256”

### SSE-KMS
SSE-KMS: encryption using keys handled & managed by KMS
KMS Advantages: user control + audit trail
Object is encrypted server side
Must set header: “x-amz-server-side-encryption”: ”aws:kms”

### SSE-C
SSE-C: server-side encryption using data keys fully managed by the customer outside of AWS. 
Amazon S3 does not store the encryption key you provide. 
HTTPS must be used
Encryption key must provided in HTTP headers, for every HTTP request made

### Client Side Encryption
- Client library such as the Amazon S3 Encryption Client
- Clients must encrypt data themselves before sending to S3
- Clients must decrypt data themselves when retrieving from S3
- Customer fully manages the keys and encryption cycle

## S3- Storage Tiers/Classes:

![image](https://user-images.githubusercontent.com/33947539/150803859-b7a21127-c488-4f4b-8fdb-8d69d76866b5.png)

![image](https://user-images.githubusercontent.com/33947539/150803932-ef947579-495e-4d27-9774-b3fab43834b3.png)

## Encryption in transit (SSL)
AWS S3 exposes:
- HTTP endpoint: non encrypted
- HTTPS endpoint: encryption in flight. You’re free to use the endpoint you want, but HTTPS is recommended.
-  HTTPS is mandatory for SSE-C.
-  Encryption in flight is also called SSL / TLS

## S3 Security
#### User based 
• IAM policies — which API calls should be allowed for a specific user from IAM console
#### Resource Based
• Bucket Policies — bucket wide rules from the S3 console — allows cross account
• Object Access Control List (ACL) — finer grain
• Bucket Access Control List (ACL) — less common

## Amazon S3 data consistency model
👉 **Read after write consistency for PUTS of new objects**

As soon as an object is written, we can retrieve it  ex: (PUT 200 -> GET 200)
This is true, except if we did a GET before to see if the object existed ex: (GET 404 -> PUT 200 -> GET 404) - eventually consistent

👉 **Eventual Consistency for DELETES and PUTS of existing objects**

If we read an object after updating, we might get the older version ex: (PUT 200 -> PUT 200 -> GET 200 (might be older version))
If we delete an object, we might still be able to retrieve it for a short time ex: (DELETE 200 -> GET 200)

## S3 Replication
S3 replication allows objects of one bucket to be copied to another bucket with the same or a different AWS account and within the same or a different region. We configure object replication by providing a replication configuration to the source bucket consists of at least the destination bucket and IAM role for S3 to copy the objects.

This feature of S3 is helpful when we want to make a real-time copy of the bucket. This can be created in different AWS regions.

>We can create the copy in:
a. Different Region: Cross-Region Replication (CRR)
b. Same Region: Same Region Replication (SRR)

![image](https://user-images.githubusercontent.com/33947539/150811818-73fd4686-d17b-4797-9e45-b5eed9837001.png)

### Use of Replication

**Replicate objects while retaining metadata**: 

You can use replication to make copies of your objects that retain all metadata, such as the original object creation time and version IDs. This capability is important if you need to ensure that your replica is identical to the source object.

**Replicate objects into different storage classes**:

You can use replication to directly put objects into S3 Glacier, S3 Glacier Deep Archive, or another storage class in the destination buckets

**Maintain object copies under different ownership**:

Regardless of who owns the source object, you can tell Amazon S3 to change replica ownership to the AWS account that owns the destination bucket. This is referred to as the owner override option.

**Keep objects stored over multiple AWS Regions**:

You can set multiple destination buckets across different AWS Regions to ensure geographic differences in where your data is kept.

**Replicate objects within 15 minutes**:

You can use S3 Replication Time Control (S3 RTC) to replicate your data in the same AWS Region or across different Regions in a predictable time frame. S3 RTC replicates 99.99 percent of new objects stored in Amazon S3 within 15 minutes (backed by a service level agreement).

## S3 popular use cases
**Some really popular use case which AWS S3 can be used for can be**:

- Data backups, data storage, and hybrid cloud storage.
- Media such as images, music and videos, application hosting, and Static Website Hosting.
- Data archiving.
- Data Lakes building and data analytics on data lakes.
- Disaster recovery.

