## What is a Placement Group in Amazon EC2?

Placement group is a way to impact the placement of interdependent EC2 instance groups in order to suit your workload requirements. AWS provides three placement strategies which you can use based on the type of your workload:

- Cluster Placement Groups: A logical grouping of instances within a single AZ.
- Partition Placement Groups: Logical partition of instance groups such that no two partitions within a placement group share the same underlying hardware.
- Spread Placement Groups: each instance within a spread placement group will be placed in a different rack.

## What are the benefits of using placement group?

### Cluster Placement group benefits:

- Recommended for low network latency, and/or high network throughput applications.
- Only specific to a single AZ
- Can span peered VPCs in the same Region

### Partition Placement Group benefits:

- Reduces the impact of correlated hardware failures for your application
- Mainly used to deploy large distributed and replicated workloads, such as HDFS, HBase, and Cassandra, across distinct racks.
- Can have partitions in multiple Availability Zones in the same Region.
- Offer visibility into the partitions using which you can check which instance is in which partition. Topology-aware applications, such as HDFS, HBase, and Cassandra use this information to make intelligent data replication decisions for increasing data availability and durability.

### Spread Placement Group benefits:

- Recommended for applications that have a small number of critical instances that should be kept separate from each other.
- Reduces the risk of simultaneous failures that might occur when instances share the same racks which is not the case in spread placement group
- Can span multiple Availability Zones in the same Region.

## Reference

https://dev.to/aws-builders/working-with-placement-groups-in-amazon-ec2-2eg3
