## Replication: Redis (Cluster Mode Disabled) vs. Redis (Cluster Mode Enabled)

A Redis (cluster mode disabled) cluster always has a single shard (API/CLI: node group) with up to 5 read replica nodes. 
A Redis (cluster mode enabled) cluster has up to 500 shards with 1 to 5 read replica nodes in each.

![image](https://user-images.githubusercontent.com/33947539/163678215-7c195bfd-8e36-441d-886e-a916e8bf822d.png)

![image](https://user-images.githubusercontent.com/33947539/163678275-edfee6d3-8401-4bdc-9633-74ea94f382c9.png)
![image](https://user-images.githubusercontent.com/33947539/163678296-408ed7d8-6faa-4477-a785-1929492b6185.png)
![image](https://user-images.githubusercontent.com/33947539/163678316-6e5294d5-e50d-441f-8dd7-e4927aba3378.png)
