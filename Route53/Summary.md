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
