# Routing policies

Routing policies determine how Route 53 responds to queries. The following table highlights the key function of each type of routing policy:

👉 Simple Routing: redirect to single resource, can’t attach health check, If multiple records are attached, random one will be selected.

👉 Weighted Routing: Weighted Routing Policy controls the what percentage % of the requests that go to specific endpoint. It’s helpful to test 1% of traffic on new app version. It is also helpful to split traffic between two regions. We can associate Health checks with it.

![image](https://user-images.githubusercontent.com/33947539/153134032-708f8e53-0acb-4014-a63c-91f66bc4c4ce.png)

👉 Latency Routing: redirect to the server that has the least latency close to us, latency is calculated in terms to AWS Region, health check attached.

👉 Failover Routing: If primary resource is not working, traffic is redirect to secondary instance/resource. Health check is mandatory.

👉 Geo-location Routing: routing is based on user location. Specify that, traffic from XYZ location should go always to particular instance/resource, if it doesn’t match, should go to default policy(We define this also).

👉 Multi-Value: Use when, traffic needs to go to multiple resources, health check mandatory. It’s not substitute for having an ELB.

![image](https://user-images.githubusercontent.com/33947539/153134170-13e5112f-528a-480e-a9aa-fda4a876f552.png)
