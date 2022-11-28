## What is the difference between partition key and sort key in amazon dynamodb?

The partition key is used for partitioning the data. Data with the same partition key is stored together, which allows you to query data with the same partition key in 1 query.

The (optional) sort key determines the order of how data with the same partition key is stored. Using a clever sort key allows you to query many items in 1 query.

An example: let's say I'm storing logging data for several applications. My partition key could be the Application Name, and the sort key the timestamp of the log. This allows me to query all logs of a particular application of the last hour in 1 query, using the BEGINS WITH operator, or even all the logs of last Wednesday for an application, by using the BETWEEN operator.

The partition key + the optional sort key form the primary key of the table, so they must be unique. Additionally, they are immutable.

The choice of your partition key and sort key should be based on your most important access pattern. If you have other access patterns, you can accommodate for them by using Global Secondary Indexes, but this comes with a cost.


## You are building an application that will collect information about user behavior. The application will rapidly ingest large amounts of dynamic data and requires very low latency. The database must be scalable without incurring downtime. Which database would you recommend in this scenario?

              RDS with MySQL
              DynamoDB
              RedShift
              RDS with Microsoft SQL
              
**Explanation:**

Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. Push-button scaling means that you can scale the DB at any time without incurring downtime. DynamoDB provides low read and write latency.

INCORRECT: “RDS with MySQL” is incorrect. RDS uses EC2 instances so you have to change your instance type/size in order to scale and compute vertically.

CORRECT: “DynamoDB” is the correct answer.

INCORRECT: “RedShift” is incorrect. RedShift uses EC2 instances as well, so you need to choose your instance type/size for scaling compute vertically, but you can also scale horizontally by adding more nodes to the cluster.

INCORRECT: “RDS with Microsoft SQL” is incorrect. Rapid ingestion of dynamic data is not an ideal use case for RDS or RedShift.

## A company wishes to restrict access to their Amazon DynamoDB table to specific, private source IP addresses from their VPC. What should be done to secure access to the table?

            Create an interface VPC endpoint in the VPC with an Elastic Network Interface (ENI).
            Create a gateway VPC endpoint and add an entry to the route table.
            Create the Amazon DynamoDB table in the VPC.
            Create an AWS VPN connection to the Amazon DynamoDB endpoint
            
**Explanation:**
There are two different types of VPC endpoints: interface endpoint and gateway endpoint. With an interface endpoint, you use an ENI in the VPC. With a gateway endpoint, you configure your route table to point to the endpoint. Amazon S3 and DynamoDB use gateway endpoints. This solution means that all traffic will go through the VPC endpoint straight to DynamoDB using private IP addresses.           

![image](https://user-images.githubusercontent.com/33947539/155985781-07f013e2-3e13-4a4b-9227-89183e461cfd.png)

INCORRECT: “Create an interface VPC endpoint in the VPC with an Elastic Network Interface (ENI).” is incorrect. As mentioned above, an interface endpoint is not used for DynamoDB. You must use a gateway endpoint.

CORRECT: “Create a gateway VPC endpoint and add an entry to the route table.” is the correct answer.

INCORRECT: “Create the Amazon DynamoDB table in the VPC.” is incorrect. You cannot create a DynamoDB table in a VPC. To connect securely using private addresses, you should use a gateway endpoint instead.

INCORRECT: “Create an AWS VPN connection to the Amazon DynamoDB endpoint.” is incorrect. You cannot create an AWS VPN connection to the Amazon DynamoDB endpoint.
