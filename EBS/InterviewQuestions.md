![image](https://user-images.githubusercontent.com/33947539/157813677-947e10d5-2216-40a4-9c8c-8c1a4b532761.png)

**Explanation:**

An instance store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer. An instance store is ideal for the temporary storage of information that frequently changes (such as buffers, caches, scratch data) and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

![image](https://user-images.githubusercontent.com/33947539/157813743-bbd61213-b6d2-49ae-bf70-3fb641d4da0c.png)

Some instance types use NVMe or SATA-based solid-state drives (SSD) to deliver high random I/O performance. This is a good option when you need storage with very low latency, but you don’t need the data to persist when the instance terminates.

In this scenario, the data is replicated and fault-tolerant, so the best option to provide the level of performance required is to use instance store volumes.

INCORRECT: “Amazon EBS” is incorrect. The Elastic Block Store (EBS) is a block storage device but because the data is distributed and fault-tolerant, a better option for performance would be to use instance stores.

CORRECT: “Amazon EC2 instance store” is the correct answer.

INCORRECT: “Amazon EFS” is incorrect as EFS is a file system that is accessed using the NFS protocol, not a block device.

INCORRECT: “Amazon S3” is incorrect as S3 is an object-based storage system, not a block-based storage system.

![image](https://user-images.githubusercontent.com/33947539/166435561-2f1a2bb4-655c-4e60-a7e5-6e402634212f.png)

![image](https://user-images.githubusercontent.com/33947539/166435753-b7a929f9-0a24-4c69-9c6d-f8e846f6c8ac.png)
