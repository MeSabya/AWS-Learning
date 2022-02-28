# EBS (Elastic Block Store) vs Instance Store in AWS

![image](https://user-images.githubusercontent.com/33947539/155942646-db5524fc-8316-4df7-8836-ec43b3742799.png)


👉 EBS volume is network attached drive which results in slow performance but data is persistent meaning even if you reboot the instance data will be there.

👉 Instance store instance store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer.

## EC2 Storage Overview
EC2 instances support two types for block level storage: 

- EC2 Instances can be launched using either Elastic Block Store (EBS) or Instance Store volume as root volumes and additional volumes.
- EC2 instances can be launched by choosing between AMIs backed by EC2 instance store and AMIs backed by EBS. However, AWS recommends use of EBS backed AMIs, because they launch faster and use persistent storage

## Instance Store
![image](https://user-images.githubusercontent.com/33947539/155943553-08043040-8941-4f7e-92c7-7e7c57802e33.png)

- These storage devices physically lie on the same host that provides the EC2 instance and are essentially useful to store temporary data associated with the EC2 instances. 

### Features of EC2 instance storage:

**Temporary storage**: EC2 instance storage provides temporary storage for EC2 instances.

**Cost**: The cost of these storage volumes is included in the cost of the EC2 instance. Different instances may have different storage volumes capacity, but the cost is always included in the price of the EC2 instance.

**Data Transfer Rate**: Since these storage volumes physically reside on the same host as the EC2 server, the I/O speed offered by these storage volumes in extremely high. I/O speeds offered by these volumes far exceed other storage options on AWS.

**Security**: Security on instance store volumes is the same as the security on the EC2 associated with them. The roles, users, and policies which have access to an EC2 instance will have access to the associated Instance Storage Volumes.

**Not backed up as AMI**: If the user takes an AMI snapshot of an existing EC2 instance, and launches a new instance from that AMI, the instance storage data is not replicated onto the new EC2 instance machine.

### Limitations of EC2 instance storage:

- EC2 instance storage, being a temporary storage service, is not suitable for storing important/critical data.
- In case, the EC2 instance associated with this storage is stopped or terminated, all data on the storage is lost with no possible means for data recovery.
- In case, the host device that provided the EC2 instance fails/crashes due to internal errors, all data on EC2 instance storage is lost.
- Not all instance types in EC2 service support Instance Storage Volumes.
- Instance Store Volumes can only be specified for an instance during its launch. Users cannot add new storage volumes as a later update to the same EC2.

## Key points for Instance store backed Instance
1. Boot time is slower then EBS backed volumes and usually less then 5 min
2. Instance store backed Instances can be of maximum 10GiB volume size
3. Instance store volume can be attached as additional volumes only when the instance is being launched and cannot be attached once the Instance is up and running
4. Instance store backed Instances cannot be stopped, as when stopped and started AWS does not guarantee the instance would be launched in the same host and hence the data is lost
5. Instance store backed Instances cannot be upgraded
6. Data on Instance store volume is LOST in following scenarios:

          1. Underlying disk drive fails
          2. Instance stops
          3. Instance terminates
          4. Instance hibernates
          Therefore, do not rely on instance store for valuable, long-term data.

## Key points for EBS backed Instance
1. Boot time is very fast usually less then a min.
2. EBS backed Instances can be of maximum 16TiB volume size depending upon the OS.
3. EBS volume can be attached as additional volumes when the Instance is launched and even when the Instance is up and running.
4. When EBS-backed instance is in a stopped state, various instance– and volume-related tasks can be done for e.g. you can modify the properties of the instance, you can change the size of your instance or update the kernel it is using, or you can attach your root volume to a different running instance for debugging or any other purpose.
5. EBS volumes are AZ scoped and tied to a single AZ in which created.
6. EBS volumes are automatically replicated within that zone to prevent data loss due to failure of any single hardware component.
7. EBS backed Instances can be upgraded for instance type, Kernel, RAM disk and user data.
8. Data on EBS volume is NOT LOST in following scenarios:

          1. Reboot on the Instance.
          2. Stopping an EBS-backed instance.
          3. Termination of the Instance for the additional EBS volumes. Additional EBS volumes are detached with their data intact.

9. Data on the EBS volume is LOST:

          1. For EBS Root volume, if Delete on termination flag is enabled (enabled, by default).
          2. For attached EBS volumes, if the Delete on termination flag is enabled (disabled, by default).
