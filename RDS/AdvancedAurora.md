# Multi-Master and Aurora Serverless

## Multi-Master

It adds the ability to scale out write performance across multiple Availability Zones, allowing applications to direct read/write workloads to multiple instances in a database cluster and operate with higher availability.

Aurora Multi-Master is designed to achieve high availability and ACID transactions across a cluster of database nodes with configurable read after write consistency.

### Architecture
- An Aurora cluster consists of a set of compute (database) nodes and a shared storage volume.
- The storage volume consists of six storage nodes placed in three Availability Zones for high availability and durability of user data.
- Every database node in the cluster is a writer node that can run read and write statements.
- Applications can use any writer node for their read/write and DDL needs. 
- A database change made by a writer node is written to six storage nodes in three Availability Zones. 
- This provides data durability and resilience against storage node and Availability Zone failures.

The writer nodes are all functionally equal. A failure of one writer node does not affect the availability of the other writer nodes in the cluster. 
There is no single point of failure in the cluster.

### High availability

Aurora Multi-Master improves upon the high availability of the single-master version of Amazon Aurora because all of the nodes in the cluster are read/write nodes.

With single-master Aurora, a failure of the single writer node requires the promotion of a Read Replica to be the new writer. In the case of Aurora Multi-Master, 
the failure of a writer node merely requires the application to use the writer to open connections to another writer.

## Aurora Serverless

Amazon Aurora Serverless is an on-demand, auto-scaling configuration for the MySQL-compatible and PostgreSQL-compatible editions of Amazon Aurora. The database automatically starts up, shuts down, and scales capacity up or down based on application needs.

It enables you to run a database in the cloud without managing any database instances. It is a simple and cost-effective option for infrequent, intermittent, or unpredictable workloads. You simply create a database endpoint and optionally specify the desired database capacity range and connect applications.

You can migrate between standard and serverless configurations with a few clicks in the Amazon RDS Management Console.

