![image](https://user-images.githubusercontent.com/33947539/155957360-703865f8-0cc2-4679-8dbb-cf9f8717dd2e.png)

**Explanation:**
To address scalability and provide a shared data storage for sessions that can be accessed from any individual web server, you can abstract the HTTP sessions from the web servers themselves. A common solution for this is to leverage an In-Memory Key/Value store such as Redis and Memcached.

Sticky sessions, also known as session affinity, allow you to route a site user to the particular web server that is managing that individual user’s session. The session’s validity can be determined by a number of methods, including a client-side cookie or via configurable duration parameters that can be set at the load balancer, which routes requests to the web servers. You can configure sticky sessions on Amazon ELBs.

👉 [**sticky-and-non-sticky-sessions**](https://stackoverflow.com/questions/10494431/sticky-and-non-sticky-sessions)

CORRECT: “Sticky sessions on an Elastic Load Balancer (ELB)” is the correct answer.

INCORRECT: “A block storage service such as Elastic Block Store (EBS)” is incorrect. In this case, the question states that a caching layer is being implemented. EBS volumes would not be suitable for creating an independent caching layer as they must be attached to EC2 instances.

INCORRECT: “A workflow service such as Amazon Simple Workflow Service (SWF)” is incorrect. Workflow services such as SWF are used for carrying out a series of tasks in a coordinated task flow. They are not suitable for storing session state data.**

INCORRECT: “A relational data store such as Amazon RDS” is incorrect. Relational databases are not typically used for storing session state data due to their rigid schema that tightly controls the format in which data is stored.

CORRECT: “A key/value store such as ElastiCache Redis” is the correct answer.


![image](https://user-images.githubusercontent.com/33947539/157815494-60edfe6d-8cb8-4c20-958d-fbdb731cc5d7.png)

**Explanation:**

High availability can be enabled for this architecture quite simply by modifying the existing Auto Scaling group to use multiple Availability Zones. The ASG will automatically balance the load, so you don’t actually need to specify the instances per AZ.

The architecture for the web tier will look like this:
![image](https://user-images.githubusercontent.com/33947539/157815595-401b17b8-b457-4395-b26f-521c5e74e8a0.png)

INCORRECT: “Create an Auto Scaling group that uses four instances across each of the two regions.” is incorrect as EC2 Auto Scaling does not support multiple regions.

CORRECT: “Modify the Auto Scaling group to use four instances across each of the two Availability Zones.” is the correct answer.

INCORRECT: “Create an Auto Scaling template that can be used to quickly create more instances in another region.” is incorrect as EC2 Auto Scaling does not support multiple regions.

INCORRECT: “Create an Auto Scaling group that uses four instances across each of the two subnets.” is incorrect as the subnets could be in the same AZ.

