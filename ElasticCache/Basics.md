## Replication: Redis (Cluster Mode Disabled) vs. Redis (Cluster Mode Enabled)

A Redis (cluster mode disabled) cluster always has a single shard (API/CLI: node group) with up to 5 read replica nodes. 
A Redis (cluster mode enabled) cluster has up to 500 shards with 1 to 5 read replica nodes in each.

![image](https://user-images.githubusercontent.com/33947539/163678215-7c195bfd-8e36-441d-886e-a916e8bf822d.png)

![image](https://user-images.githubusercontent.com/33947539/163678275-edfee6d3-8401-4bdc-9633-74ea94f382c9.png)
![image](https://user-images.githubusercontent.com/33947539/163678296-408ed7d8-6faa-4477-a785-1929492b6185.png)
![image](https://user-images.githubusercontent.com/33947539/163678316-6e5294d5-e50d-441f-8dd7-e4927aba3378.png)

## Which should I choose?

When choosing between Redis (cluster mode disabled) or Redis (cluster mode enabled), consider the following factors:

### Scaling v. partitioning –

Redis (cluster mode disabled) supports scaling. You can scale read capacity by adding or deleting replica nodes, or you can scale capacity by scaling up to a larger node type.

Redis (cluster mode enabled) supports partitioning your data across up to 500 node groups. You can dynamically change the number of shards as your business needs change. One advantage of partitioning is that you spread your load over a greater number of endpoints, which reduces access bottlenecks during peak demand.

### Node size v. number of nodes – 
Because a Redis (cluster mode disabled) cluster has only one shard, the node type must be large enough to accommodate all the cluster's data plus necessary overhead. On the other hand, because you can partition your data across several shards when using a Redis (cluster mode enabled) cluster, the node types can be smaller, though you need more of them.

### Reads v. writes – 
If the primary load on your cluster is applications reading data, you can scale a Redis (cluster mode disabled) cluster by adding and deleting read replicas. However, there is a maximum of 5 read replicas. If the load on your cluster is write-heavy, you can benefit from the additional write endpoints of a Redis (cluster mode enabled) cluster with multiple shards.

