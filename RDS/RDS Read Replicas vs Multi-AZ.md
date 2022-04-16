 ![image](https://user-images.githubusercontent.com/33947539/163659643-8ecb172e-69cc-4f2a-a714-234ff22637e1.png)

# What is Amazon RDS Read Replicas?

- Read Replicas helps in decreasing load on the primary DB by serving read-only traffic.
- You can create Read Replicas within AZ, Cross-AZ or Cross-Region.
- Read Replica can be manually promoted as a standalone database instance.
- Read Replicas support Multi-AZ deployments.
- You can use Read Replicas to take logical backups, if you want to store the backups externally to RDS.
- You can have Read Replicas of Read Replicas.
- Read Replica helps to maintain a copy of databases in a different region for disaster recovery.
- You can have up to five Read Replicas per master, each with own DNS endpoint. Unlike a Multi-AZ standby replica, you can connect to each Read Replica and use them for read scaling.
- Amazon enables you to create one or more read-only copies of your database instance.
- Replication can be within the same AWS Region or in a different AWS Region.
- Read replicas are implemented using asynchronous replication, so reads are eventually consistent.
- Applications must update the connection string to leverage read replicas.

![image](https://user-images.githubusercontent.com/33947539/163660156-84dcfca5-418e-46aa-a028-2e52d424ea96.png)

## RDS Read Replicas — Use Cases

![image](https://user-images.githubusercontent.com/33947539/163659723-0b7c2d6c-4926-4c41-955a-b42508db5441.png)

- You have a production database that is taking on normal load
- You want to run a reporting application to run some analytics
- You create a Read Replica to run the new workload there
- The production application is unaffected
- Read replicas are used for SELECT (=read) the only kind of statements (not INSERT, UPDATE, DELETE)
- Read-heavy database workloads. This excess read traffic can be directed to one or more read replicas.
- Business reporting or data warehousing scenarios - you may want business reporting queries to run against a read replica, rather than your primary, production DB Instance.

## RDS Read Replicas Pricing

![image](https://user-images.githubusercontent.com/33947539/163659755-f830b94c-2944-4b5d-bcf7-0c44a3f8c965.png)

A read replica is billed as a standard DB Instance and at the same rates

👉 **You are not charged for the data transfer incurred in replicating data between your source DB instance and read replica within the same AWS Region but need to change the data 
    transfer charge for cross-region.**

![image](https://user-images.githubusercontent.com/33947539/163660034-7c77309e-ff1e-4119-a163-3f1d90050521.png)

# What is Amazon RDS Multi-AZ (Disaster Recovery)?

![image](https://user-images.githubusercontent.com/33947539/163659831-79438c97-930d-42c7-a0de-68706b5fbd85.png)

- AWS Provides high availability for database instances within a single AWS Region.
- With Multi-AZ, your data is synchronously (at the same time) replicated to standby in a different AZ.
- One DNS name — Endpoint of DB instance remains the same after a failover, the application can resume database operations without manual intervention.
- Not used for scaling
- ***Note: The Read Replicas can be set up as Multi-AZ for Disaster Recovery (DR)***

![image](https://user-images.githubusercontent.com/33947539/163660118-1154a403-d8b7-4296-9d12-569544fe04ee.png)

## RDS Multi-AZ — Failover Conditions

**When a problem is detected on the primary instance, it will automatically failover to the standby in the following conditions:**

- The primary DB instance fails
- Unreachable due to loss of network connectivity
- An Availability Zone outage or busy and unresponsive
- Modified (eg. The DB instance server type is changed)
- The operating system of the DB instance is undergoing software patching.
- A manual failover of the DB instance was initiated using Reboot with failover.

## RDS — From Single-AZ to Multi-AZ

To Create multi-AZ from the primary instance, we need to just click on “modify” for the database and select Multi-AZ
It is a zero-downtime operation meaning we don’t have to stop the DB.

![image](https://user-images.githubusercontent.com/33947539/163659995-a9f02c83-0390-4fb6-b62d-f1c9e2a06484.png)

It is important to understand what happened internally behind the scenes when you changed the DB instance from single AZ to multi-AZ

1. A snapshot is taken by RDS automatically
2. A new DB is restored from the snapshot in a new AZ
3. Synchronization is established between the two databases

