# Amazon Aurora

Amazon Aurora is a fully managed MySQL- and PostgreSQL-compatible relational database.

An Amazon Aurora DB cluster consists of one or more DB instances and a cluster volume that manages the data for those DB instances. 

An Aurora cluster volume is a **virtual database storage volume** that spans multiple Availability Zones, 
with each Availability Zone having a copy of the DB cluster data. 

#### Two types of DB instances make up an Aurora DB cluster:

**Primary DB instance** – Supports read and write operations, and performs all of the data modifications to the cluster volume. Each Aurora DB cluster has one primary DB instance.

**Aurora Replica** – 
Connects to the same storage volume as the primary DB instance and supports only read operations. 
Each Aurora DB cluster can have up to 15 Aurora Replicas in addition to the primary DB instance. 
Maintain high availability by locating Aurora Replicas in separate Availability Zones. 
Aurora automatically fails over to an Aurora Replica in case the primary DB instance becomes unavailable. 
You can specify the failover priority for Aurora Replicas. Aurora Replicas can also offload read workloads from the primary DB instance.

![image](https://user-images.githubusercontent.com/33947539/166449429-07ea7241-935b-412b-be82-eb4de44e122a.png)


## Features

- Fully managed service
- High performance, low price
- Scales in 10 GB increments
- Scales up to 32 vCPUs and 244 GB RAM -2 copies of data kept in each AZ with a minimum of 3 AZs (6 copies)
- Can handle the loss of up to two copies of data without affecting DB write availability and up to three copies without affecting read availability.
- Aurora’s database storage is separate from the instances. In Aurora, data has 6 copies (as 10GB chunks distributed) to three Availability Zones. 
  Hence, even if you have only one Aurora instance, your data will still have 6 copies.
- Aurora Serverless
  Aurora Serverless lets you run Aurora without having to guess how many compute nodes you need. 
  It automatically starts and stops nodes to match the needs of your application. 
  It scales up to meet a spike in demand and scales down when things are quiet. 
  The data remains in the shared storage volume, independent of any scaling.

![image](https://user-images.githubusercontent.com/33947539/166447931-d6b8208a-5790-446e-bfaf-153f27e3680e.png)

![image](https://user-images.githubusercontent.com/33947539/166448015-5e7d57af-a17f-47b5-b501-5c2ceacc5635.png)


## Aurora Replicas
There are two types of replication: Aurora Replica (up to 15) and MySQL Read Replica (up to 5).

![image](https://user-images.githubusercontent.com/33947539/166448316-1c699f27-06e6-4517-8e85-92ecac38c1fd.png)

## Cross-region read replicas

![image](https://user-images.githubusercontent.com/33947539/166448925-7502e9ca-d105-4dd2-8764-5876a80d0437.png)

## Aurora Global Database

For globally distributed applications, you can use Global Database, 
where a single Aurora database can span multiple AWS Regions to enable fast local reads and quick disaster recovery.

Global Database uses storage-based replication to replicate a database across multiple AWS Regions, with a typical latency of less than 1 second.
You can use a secondary region as a backup option in case you need to recover quickly from a regional degradation or outage.
A database in a secondary region can be promoted to full read/write capabilities in less than 1 minute.
The following table depicts the Aurora Global Database topology:

![image](https://user-images.githubusercontent.com/33947539/166450331-159494ae-f649-468f-8bb6-8ba284c57e4e.png)

