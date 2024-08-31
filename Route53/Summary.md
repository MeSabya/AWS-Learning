## Root DNS server Vs TLD server Vs authorative server in route 53

### 1. Root DNS Server
- Role: The root DNS servers are the top of the DNS hierarchy. They are the first step in translating (resolving) human-readable domain names (like www.example.com) into IP addresses.

- Function: When a DNS resolver doesn't know the IP address of a domain, it starts by querying a root DNS server. The root DNS server doesn't know the IP address either but knows where to find the TLD servers for each top-level domain (like .com, .org, etc.).

- Location in Hierarchy: Top-most level in the DNS hierarchy.

### 2. TLD DNS Server (Top-Level Domain Server)

- Role: TLD servers manage information for all domains within a specific top-level domain (TLD), like .com, .org, or country-code TLDs like .uk.
- Function: After receiving a query from a root DNS server, the TLD server directs the query to the authoritative name servers responsible for the specific domain. For example, if you’re querying www.example.com, the .com TLD server would direct you to the authoritative name server for example.com.
- Location in Hierarchy: Just below the root DNS servers in the DNS hierarchy.

### 3. Authoritative DNS Server
- Role: The authoritative DNS server holds the DNS records for a specific domain name (like example.com). These records include the IP address associated with the domain and other information like mail server addresses (MX records).

- Function: When the DNS resolver reaches the authoritative DNS server for a domain, it provides the final answer to the DNS query, such as the IP address of the web server for www.example.com.

- Location in Hierarchy: Below the TLD servers in the DNS hierarchy.

- Route 53 in Context
Route 53: In AWS Route 53, you can configure it to act as an authoritative DNS server for your domains. When someone queries your domain, Route 53 provides the DNS records you’ve set up (e.g., A records, CNAME records) just like any other authoritative DNS server.

### Query Process Flow
- Query sent to a Root DNS Server: If the resolver doesn't have a cached record, it starts here.
- Root DNS Server directs to TLD Server: The root server returns the IP of the TLD server (e.g., for .com).
- TLD Server directs to Authoritative DNS Server: The TLD server returns the IP of the authoritative server for the domain in question.
- Authoritative DNS Server provides the DNS record: The authoritative server responds with the final answer (e.g., the IP address for www.example.com).

## DNS Records 

Here's a brief overview of the key DNS record types and their purpose:

### A Record (Address Record):

- Purpose: Maps a domain name to an IPv4 address.
- Example: example.com → 192.0.2.1
- Stored In: Authoritative DNS Server

### AAAA Record (IPv6 Address Record):
- Purpose: Maps a domain name to an IPv6 address.
- Example: example.com → 2001:0db8:85a3:0000:0000:8a2e:0370:7334
- Stored In: Authoritative DNS Server

### CNAME Record (Canonical Name Record):

- Purpose: Maps a domain name to another domain name (an alias). Useful for pointing multiple domain names to the same IP address.
- Example: www.example.com → example.com
- Stored In: Authoritative DNS Server

### MX Record (Mail Exchange Record):
- Purpose: Specifies the mail server responsible for receiving email on behalf of a domain.
- Example: example.com → mail.example.com
- Stored In: Authoritative DNS Server

### NS Record (Name Server Record):
- Purpose: Specifies the authoritative DNS servers for a domain.
- Example: example.com → ns1.example.com
- Stored In: Authoritative DNS Server

### TXT Record (Text Record):

- Purpose: Allows domain administrators to insert arbitrary text into a DNS record. Commonly used for verification and security purposes (e.g., SPF records for email).
- Example: example.com → "v=spf1 include:_spf.example.com ~all"

These DNS records are stored and managed by the Authoritative DNS Server for the domain. 
The authoritative DNS server is the definitive source of information for a domain and responds to DNS queries with these records.

In the context of AWS Route 53:

When you configure Route 53 as the authoritative DNS server for your domain, you input these DNS records (A, AAAA, CNAME, etc.) 
into Route 53’s hosted zone for your domain.
Route 53 then responds to DNS queries with the appropriate records based on what you've configured.

## Hosted zone in route 53 and its significance 

A hosted zone in Amazon Route 53 is a container for DNS records that define how you want to route traffic for a specific domain (e.g., example.com) and its subdomains (e.g., www.example.com, blog.example.com).

Key Aspects and Significance of a Hosted Zone:

### 1. Container for DNS Records
The hosted zone holds various DNS records, such as A, AAAA, CNAME, MX, and TXT records, that determine how DNS queries for your domain are resolved.
When someone types your domain name in a browser or when an email is sent to your domain, the DNS records in the hosted zone direct the traffic to the appropriate IP address or service.

### 2. Types of Hosted Zones

#### Public Hosted Zone:
Used to manage the DNS settings for a public domain that is accessible over the internet.
Example: You create a public hosted zone for example.com, and it includes records like A, CNAME, MX, etc., which are publicly accessible.

#### Private Hosted Zone:
Used for managing DNS settings within a specific VPC (Virtual Private Cloud) in AWS.
Example: You create a private hosted zone for example.internal that is only accessible within your private network (e.g., a VPC), not from the public internet.

### 3. DNS Routing Policies

- Simple routing policy
- Failover routing policy
- Weighted routing policy
- Latency routing policy
- Geolocation routing policy
- Geoproximity routing policy
- Multivalue routing policy
- IP-based routing policy

Within a hosted zone, Route 53 allows you to define various routing policies for DNS queries:

- Simple Routing: Maps a domain to a single resource, like an EC2 instance or an S3 bucket.
- Weighted Routing: Distributes traffic across multiple resources based on weights you assign.
- Latency-Based Routing: Routes traffic to the resource that provides the lowest latency for the user.
- Failover Routing: Routes traffic to a backup resource if the primary one becomes unavailable.
- Geolocation and Geoproximity Routing: Routes traffic based on the geographic location of the user or resources.

## How does Route 53 integrate with CloudFront?
Route 53 can be used to route traffic to a CloudFront distribution by creating an alias record that points to the CloudFront distribution. 
This enables you to use a custom domain name for your CloudFront distribution and leverage Route 53's DNS features, 
such as latency-based routing or geolocation routing. 

## alias vs CNAME in route53

### Alias Record
- Purpose: Alias records are Route 53-specific DNS records that map a domain name to an AWS resource, 
such as an Amazon S3 bucket, CloudFront distribution, Elastic Load Balancer (ELB), or another Route 53 DNS record.

- Usage: You can use alias records to point to AWS resources such as:
S3 static websites
Elastic Load Balancers (ELBs)
CloudFront distributions
Route 53 records (in the same hosted zone)

### CNAME Record (Canonical Name Record)
Purpose: A CNAME record maps one domain name to another domain name (not an IP address). It essentially creates an alias for a domain.


## Practical Examples

### a. Using a CNAME Record
Suppose you have a website hosted on an external platform, and you want www.example.com to point to it.

DNS Record:
www.example.com.   CNAME   example.externalplatform.com.

Behavior:
DNS resolver queries www.example.com and is directed to example.externalplatform.com, which then resolves to the appropriate IP address.

### b. Using an Alias Record
Suppose you have an AWS Elastic Load Balancer (ELB) serving your application, and you want both example.com and www.example.com to point to it.

DNS Records in Route 53:
example.com.       A      Alias → ELB

www.example.com.   A      Alias → ELB

Behavior:
DNS resolver queries example.com or www.example.com and Route 53 directly resolves these to the ELB’s IP addresses without additional lookups.
