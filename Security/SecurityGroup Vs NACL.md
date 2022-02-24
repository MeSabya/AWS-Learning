# Deep Dive into Security Groups and N
ACL in AWS

Let’s start with the basic definitions

👉 **Security Group** — Security Group is a stateful firewall to the instances. Here stateful means, security group keeps a track of the State. Operates at the instance level.

👉 **Network Access Control List** — NACL is stateless, it won’t keep any track of the state. Operates at Subnet level.

![image](https://user-images.githubusercontent.com/33947539/155372566-5ebbcdb4-742b-4874-be95-e49d49cc6823.png)

## Security Group:

- Security Group is a stateful firewall which can be associated with Instances. 
- **Security Group acts like a Firewall to Instance or Instances**. 
- Security Group will always have a hidden Implicit Deny in both Inbound and Outbound Rules. 
- So we can only allow something explicitly, but not deny something explicitly in Security Groups.
- Security Group is applied to an instance only when you specify a security group while launching an instance.

![image](https://user-images.githubusercontent.com/33947539/155377410-a1ef8c53-2b8c-4291-beb8-6c0e3fe29ab7.png)

When we talk about the default Security Group, there are two things to discuss — 
              1. AWS created Default SG, 
              2. User Created Default SG.

AWS creates a default SG when it creates a default VPC — in this security group they will add an inbound rule which says all Instances in this Security Group can talk to each other.
Any Security Group created by a User explicitly, wouldn’t contain this Inbound Rule which would allow communication between the Instances, we should explicitly add it if required.

Both in the AWS created SG and User Created Custom SG , the Outbound Rules would be the same — which allows ALL TRAFFIC out.

### Security Group Features:

              Stateful Firewall
              Connection Tracking

#### Stateful Firewall:
Why its called Stateful trafic ?

It is a stateful means that any changes made in the inbound rule will be automatically reflected in the outbound rule. 
*If your instance sends traffic to another host (host B), and host B initiates the same type of traffic to your instance in a separate request within 600 seconds of the original request or response, your instance accepts it regardless of inbound security group rules. Your instance accepts it because it’s regarded as response traffic.*

#### Connection Tracking:
Security Groups use Connection Tracking to keep track of connection information that flows in and out of an instance, 
this information includes — IP address, Port number and some other information(for some specific protocols).

![image](https://user-images.githubusercontent.com/33947539/155377699-3bb747a8-2849-489e-aa8e-178c45d67e61.png)


## NACL — Network Access Control List:

- NACLs are stateless firewalls which work at Subnet Level, meaning NACLs act like a Firewall to an entire subnet or subnets. 
- It is a stateless means that any changes made in the inbound rule will not reflect the outbound rule.
- A default NACL allows everything both Inbound and Outbound Traffic. Unlike Security Groups, in NACLs we have to explicitly tell what to deny in Inbound and Outbound Rules. 
- There’s no Implicit Deny in NACL.
- When we create a VPC, a default NACL will be created which will allow ALL Inbound Traffic and Outbound Traffic.
- If we don’t associate a Subnet to NACL, the default NACL in that VPC will be associated to that Subnet.

## Security Group and NACL Key Differences:

![image](https://user-images.githubusercontent.com/33947539/155376083-4a431979-9d53-49da-b9fd-025d9f2d01b8.png)

### NACL & SG Default Quota:

#### NACL :
NACLs Per VPC — 200
Rules per NACL — 20

Key Points:

👉 *Single NACL can be associated with multiple Subnets, however single Subnet cannot be associated with multiple NACLs at same time as there can be multiple Deny Rules which contradict each other.*

#### Security Groups:
VPC Security Groups per Region — 2500
Rules Per Security Group — 60 Inbound and 60 Outbound.

![image](https://user-images.githubusercontent.com/33947539/155377158-96a0178c-066f-46c7-9d3f-53e74a43df6c.png)


