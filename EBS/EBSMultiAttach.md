# What you should know about EBS Multi-attach Volumes

1. Multi-attach EBS volume option is available only for Provisioned IPOPs SSD io1 & io2 Type EBS volumes.

![image](https://user-images.githubusercontent.com/33947539/166426964-04c815f7-cb69-4c32-952a-76566a547d09.png)

2. Multi-attach EBS does not support XFS, EXT2, EXT4, 
   and NTFSas these file systems are not designed for simultaneous read/write operations from multiple nodes. It supports only cluster-aware File systems like GFS2 & OCFS2.
3. To attach the multi-attach enabled EBS to multiple instances, the EBS volume should reside in the same availability zone as the instances.
4. You can attach up to 16 Nitro-based instances in the same Availability Zone.   
5. Multi-Attach enabled volumes can't be created as boot volumes.
6. Only for io1 and io2 family.


   
