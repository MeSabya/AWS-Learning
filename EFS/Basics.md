# Amazon Elastic File System (EFS)

- Amazon Elastic File System (Amazon EFS) provides a simple, serverless, set-and-forget, elastic file system that lets you share file data without provisioning or managing storage
- It is Good for big data and analytics, media processing workflows, content management, web serving, home directories, etc. The EFS uses the NFS protocol and can scale up to petabytes.

- The main advantage of EFS is it can be accessed from multiple EC2 instances. 
- Can concurrently connect 1 to 1000s of EC2 instances, from multiple AZs. 
- The file system can be accessed concurrently from all AZs in the region where it is located. 
- Your On-premises system can access EFS via Direct Connect or AWS VPN.

![image](https://user-images.githubusercontent.com/33947539/157826184-148ee38f-4796-4f26-9aef-1bd3b92e5a79.png)

## What’s the Difference between EBS and EFS 

- EBS volumes are limited to a single instance and more importantly, it can only be accessed by one instance at a time. With EFS, you can have hundreds or thousands of instances accessing the file system simultaneously. This makes AWS EFS a great fit for any use that requires a decent performing centralized shared storage — uses like media processing or shared code repositories.
- You can also use AWS EFS to serve web content, keep various backups, and reduce storage spending. While EFS does cost more than EBS ($0.30 per GB for EFS vs. $0.10 per GB for EBS), you only pay once per EFS file system. This means that if you attach a dozen instances to it, you will still pay the same amount as if you only had one instance attached to it. With EBS volumes, you pay for each volume. Therefore, to save money on storage, EFS can sometimes serve as a replacement for EBS.


```
EFS may be used whenever you need a shared file storage option for multiple EC2 instances with automatic, high-performance scaling. 

This makes it a great candidate for file storage for content management systems; for lift and shift operations, 
as its autoscaling potential means you do not need to re-architect; for application development, as EFS’s shareable 
file storage is ideal for storing code and media files.
```

