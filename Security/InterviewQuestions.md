![image](https://user-images.githubusercontent.com/33947539/157840120-ce50d89b-438e-4dbd-a84a-6bf8fccc6007.png)

Explanation: In this scenario, an inbound rule is required to allow traffic from any internet client to the web front-end on SSL/TLS port 443. The source should therefore be set to 0.0.0.0/0 to allow any inbound traffic.

To secure the connection from the web front-end to the database tier, an outbound rule should be created from the public EC2 security group with a destination of the private EC2 security group. The port should be set to 1433 for MySQL. The private EC2 security group will also need to allow inbound traffic on 1433 from the public EC2 security group.

This configuration can be seen in the diagram:

![image](https://user-images.githubusercontent.com/33947539/157840344-7c859d6e-bb44-4186-abc1-02ca7d3ce4bd.png)

CORRECT:“Configure the security group for the web tier to allow inbound traffic on port 443 from 0.0.0.0/0.” is a correct answer.

INCORRECT: “Configure the security group for the web tier to allow outbound traffic on port 443 from 0.0.0.0/0.” is incorrect as this is configured backwards.

CORRECT:“Configure the security group for the database tier to allow inbound traffic on port 1433 from the security group for the web tier.” is also a correct answer.

INCORRECT: “Configure the security group for the database tier to allow outbound traffic on ports 443 and 1433 to the security group for the web tier.” is incorrect as the MySQL database instance does not need to send outbound traffic on either of these ports.

INCORRECT: “Configure the security group for the database tier to allow inbound traffic on ports 443 and 1433 from the security group for the web tier.” is incorrect as the database tier does not need to allow inbound traffic on port 443.
