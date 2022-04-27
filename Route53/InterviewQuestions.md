```python
A company has created a duplicate of its environment in another AWS Region. 
The application is running in warm standby mode. There is an Application Load Balancer (ALB) in front of the application. 
Currently, failover is manual and requires updating a DNS Alias record to point to the secondary ALB.

How can a solutions architect automate the failover process?

Enable an ALB health check.
Enable an Amazon Route 53 health check.
Create a CNAME record on Amazon Route 53 pointing to the ALB endpoint.
Create a latency based routing policy on Amazon Route 53.
```

Explanation: You can use Route 53 to check the health of your resources and only return healthy resources in response to DNS queries. There are three types of DNS failover configurations:

- **Active-passive:** Route 53 actively returns a primary resource. In case of failure, Route 53 returns the backup resource. Configured using a failover policy.

- **Active-active:** Route 53 actively returns more than one resource. In case of failure, Route 53 fails back to the healthy resource. Configured using any routing policy besides failover.

- **Combination:** Multiple routing policies (such as latency-based, weighted, etc.) are combined into a tree to configure more complex DNS failover.


In this case, an alias already exists for the secondary ALB. Therefore, the solutions architect just needs to enable a failover configuration with an Amazon Route 53 health check.

Answer is 2

