![image](https://user-images.githubusercontent.com/33947539/157835768-4c55186c-85d1-41ab-9850-f7e65d2e9ece.png)

**Explanation:**

The problem given in this question is that the users are uploading the documents to an individual EC2 instance with a local EBS volume. Therefore, as EBS volumes cannot be shared across AZs, the data is stored separately, and the ALB will be distributing incoming connections to different instances/data sets.

The simple solution is to implement a shared storage layer for the documents so that they can be stored in one place and maybe seen by any user who connects, no matter which instance they connect to.

INCORRECT: “Run a script to synchronize the data between Amazon EBS volumes.” is incorrect. This is a complex and messy approach. A better solution is to use a shared storage layer.

INCORRECT: “Use Sticky Sessions with the ALB to ensure users are directed to the same EC2 instance in a session.” is incorrect as this will just “stick” a user to the same instance. They won’t see documents uploaded to other instances/EBS volumes.

CORRECT: “Copy the data from all EBS volumes to Amazon EFS. Modify the application to save new documents to Amazon EFS.” is the correct answer.

INCORRECT: “Configure the Application Load Balancer to send the request to all servers. Return each document from the correct server.” is incorrect as there is no mechanism here for selecting a specific document. The requirement also requests that all documents be visible.


