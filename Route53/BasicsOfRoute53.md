# Amazon Route 53

*A DNS service such as Amazon Route 53 is a globally distributed service that translates human readable names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other. The Internet’s DNS system works much like a phone book by managing the mapping between names and numbers. DNS servers translate requests for names into IP addresses, controlling which server an end user will reach when they type a domain name into their web browser. These requests are called queries.*

## Why the name Route 53
AWS Route 53 takes its name from the Port 53, which handles DNS for both the TCP and UDP traffic requests.

## Types of DNS Service

1. **Authoritative DNS**: 

It answers DNS queries, translating domain names into IP address so computers can communicate with each other. 
Authoritative DNS has the final authority over a domain and is responsible for providing answers to recursive DNS servers with the IP address information. Amazon Route 53 is an authoritative DNS system.
An authoritative Name Server is a nameserver (DNS Server) that holds the actual DNS records (A, AAAA, TXT, etc) for a particular domain/ address. Authoritative Name Servers need to be set up at the domain registrar and they only respond to DNS queries for the domain names that they host.

2. **Recursive DNS**: 

Clients typically do not make queries directly to authoritative DNS services. Instead, they generally connect to another type of DNS service known a resolver, or a recursive DNS service
it doesn't own any DNS records, it acts as an intermediary who can get the DNS information on your behalf. If a recursive DNS has the DNS reference cached, or stored for a period of time, then it answers the DNS query by providing the source or IP information. If not, it passes the query to one or more authoritative DNS servers to find the information.
Basically its a cache before authorative DNS.


## Before going deep into understanding Amazon Route 53, We should be aware of some useful terminology :

**Domain Name System (DNS)**: They are used to convert human readable domain names into IP addresses.

**Domain Registrars**: A authority that can assign domain names. Some popular ones are Domain.com, Bluehost, Network Solutions, HostGator, GoDaddy and Amazon Route 53 itself.

**Root server**: Root servers are DNS nameservers that operate in the root zone. These servers can directly answer queries for records stored or cached within the root zone, and they can also refer other requests to the appropriate Top Level Domain (TLD) server.

**Top Level Domain** : The TLD servers are the DNS server group one step below root servers in the DNS hierarchy, and they are an integral part of resolving DNS queries. Ex : .com, .net, .in and .org.

![image](https://user-images.githubusercontent.com/33947539/153127625-ccbb3e02-6f0f-4257-af71-5170ac1f3f56.png)

**Domain** : Domains are your standard URLs like amazon.com and google.com.

**Subdomains** : Subdomains are a unique URL that lives on your purchased domain as an extension in front of your regular domain like www.google.com and docs.google.com.

**Hosted Zone or Zone file**: A hosted zone is a container for records, and records contain information about how you want to route traffic for a specific domain, such as example.com, and its subdomains (web.example.com, admin.example.com). A hosted zone and the corresponding domain have the same name. When we create public hosted zone it automatically create a SOA and NS that are unique to each hosted zone.
This is how DNS system finally find out which IP should contact when a user requests a certain domain name.

A zone might include these things:

One domain name

One domain name and several subdomains

Multiple domain names

**What are DNS records?**:
The Domain Name System (DNS) is the phone book of the Internet. People access information online through easy-to-remember domain names. Computers communicate through Internet Protocol (IP) addresses. DNS translates domain names to IP addresses so browsers can load Internet resources.

DNS records are instructions that are created in authoritative DNS servers or name servers and provide information about a domain such as what IP address it is mapping to and where the emails for the domain name should go. All the DNS records constitute the domain's DNS zone which is stored in a text file called a zone file on the authoritative DNS servers.

**What does an SOA record look like (Start of authorative record)**: 

👉 A DNS SOA record contains a great deal of information about a zone, all packed into a recognized format that browsers and servers can understand.

👉 Every DNS zone must have a single SOA record and it is the first record in the zone. The DNS hosting provider will normally create a default SOA record for each domain added into their system and usually you do not need to make changes to this record.


👉 Each record contains these:
![image](https://user-images.githubusercontent.com/33947539/153130279-b14c08a7-93c2-4e42-8c33-198a7aa4f021.png)

![image](https://user-images.githubusercontent.com/33947539/153130374-442c325c-06a0-4c7c-8961-000a0452e120.png)

**What is an NS record?**:
An NS record or name server record identify which name servers are authoritative for a zone. DNS resolvers will query the servers listed in the NS records of a domain name for specific DNS records such as A, AAAA, MX, TXT. 


## Summary 

**Route53 can use basically:**

Public domain names you own (or buy) or Private domain names that can be resolved by your instances in your VPCs.
Route53 has many features such as Load balancing, Health checks, Routing policy like Simple, Failover, Geolocation, Latency, Weighted, Multi value.
You pay $0.50 per month per hosted zone.
