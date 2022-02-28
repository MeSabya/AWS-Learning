# What is Amazon Elastic Block Store (EBS)

- Amazon EBS is like a hard drive in the cloud that provides persistent block storage volumes for use with Amazon EC2 instances.
- These volumes can be attached to your EC2 instances and allow you to create a file system on top of these volumes, run a database, server or use them in any other way you would use a block device.
- An EBS volume can only be mounted to a single EC2 instance at a time. If you want to assign a volume to multiple EC2 instances, check out Amazon Elastic File System (EFS).

### Few Points for EBS Volume:
- It’s a network drive (i.e. not a physical drive).
- It uses the network to communicate the instance, which means there might be a bit of latency.
- It can be detached from an EC2 instance and attached to another one quickly.
- It’s locked to an Availability Zone (AZ).
- An EBS Volume in us-east-1a cannot be attached to us-east-1b.
- To move a volume across, you first need to snapshot it.
- Have a provisioned capacity (size in GBs, and IOPS).
- You get billed for all the provisioned capacity.
- You can increase the capacity of the drive over time.

###  What is a block storage volume?
- A block storage volume works similarly to a hard drive. You can store any type of files on it or even install a whole Operating System on it.
- **EBS volumes are placed in an availability zone, where they are automatically replicated to protect data loss from the failure of a single component.**
- But since they are replicated only across a single availability zone you may lose data if the whole availability zone goes down, which is really rare.

## EBS Volume Types

![image](https://user-images.githubusercontent.com/33947539/155940024-2b1b9b5f-cc14-4513-b116-e64c81677f8c.png)

![image](https://user-images.githubusercontent.com/33947539/155939996-7a602383-8695-4093-b987-d3521ba416ce.png)

## EBS Snapshots:
>Snapshot: The snapshot is simply the AMI. A snapshot is a backup of an EC2 volume that’s stored in S3. 
>You can create a new volume using data stored in a snapshot by entering the snapshot’s ID. You can search for public snapshots by typing text in the Snapshot field.

### Points about EBS Snapshot:
- Incremental — only backup changed blocks.
- EBS backups use IO and you shouldn’t run them while your application is handling a lot of traffic.
- Snapshots will be stored in S3 (but you won’t directly see them).
- Not necessary to detach volume to do snapshot, but recommended.
- Max 100,000 snapshots.
- Can copy snapshots across AZ or Region.
- Can make Image (AMI) from Snapshot.
- Snapshots can be automated using Amazon Data LifeCycle Manager.

### EBS Migration
EBS Volumes are only locked to a specific AZ.
To migrate it to a different AZ (or region):
Snapshot the volume.
Copy the volume to a different region.
Create a volume from the snapshot in the AZ of your choice.

## EBS Encryption:
- EBS Encryption leverages keys from KMS (AES-256)
- Snapshots of encrypted volumes are encrypted.
- Data at rest is encrypted inside the volume
- All the data in flight moving between the instance and the volume is encrypted



