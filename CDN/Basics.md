# AWS CloudFront Architecture

## Content Delivery Network (CDN)
A Content Delivery Network (CDN) is a global cache that stores copies of your data on Edge Location caches, which are positioned close to your customers as possible.
A better way to solve the web latency issues for very remote servers in the Internet can be solved having a CDN.

## AWS CloudFront:
**CloudFront is the AWS CDN and it is a Global (not Regional) service**. 
It consists of a global network of Edge Locations, that are distributed across the globe. It is complaint with both PCI DSS (except storing credit card information in the cache) and HIPAA standards.
To deliver content to end users with lower latency, Amazon CloudFront uses a global network of 225+ Points of Presence (215+ Edge locations and 13 regional mid-tier caches) in 90 cities across 47 countries. (Updated — May 2021, Source: AWS Documentation) 

## What files should be served from a CDN

- Images
- Javascript files
- CSS files
- Small static files

## CloudFront Components
There are multiple components in AWS CloudFront:

- CF Origin — The source location of your content
- CF Distribution — The configurable unit of CloudFormation
- Edge Locations — The local cache of your data
- Regional Edge Caches — A larger version of an Edge location, which sits between the origin and an typical Edge location primarily to improve the performance.

### Origins

An origin is the origin of the files that the CDN will distribute. Origins can be either an S3 bucket, an EC2 instance, an Elastic Load Balancer, or Route 53. They can also be external (non-AWS).

👉 When using Amazon S3 as an origin, you place all of your objects within the bucket. You can use an existing bucket, and the bucket is not modified in any way. By default, all newly created buckets are private. You can make objects publicly available or use CloudFront signed URLs.

👉 A custom origin server is an HTTP server, which can be an EC2 instance or an on-premise/non-AWS-based web server. When using an on-premise or non-AWS-based web server, you must specify the DNS name, ports, and protocols that you want CloudFront to use when fetching objects from your origin. Most CloudFront features are supported for custom origins except RTMP distributions (must be an S3 bucket).

### Distributions

To distribute content with CloudFront, you need to create a distribution.

The distribution includes the configuration of the CDN, including:

- Content origins.
- Access (public or restricted).
- Security (HTTP or HTTPS).
- Cookie or query-string forwarding.
- Geo-restrictions.
- Access logs (record viewer activity).

There are two types of distributions, web distribution and RTMP.

```Lua
Web Distribution

Static and dynamic content including .html, .css, .php, and graphics files
Distributes files over HTTP and HTTPS
Add, update, or delete objects, and submit data from web forms. Add, update, or delete objects, and submit data from web forms.
Use live streaming to stream an event in real-time.


RTMP

Distribute streaming media files using Adobe Flash Media Server’s RTMP protocol.
It allows an end-user to begin playing a media file before the file has finished downloading from a CloudFront edge location.
Files must be stored in an S3 bucket.
To use CloudFront live streaming, create a web distribution.
```
![image](https://user-images.githubusercontent.com/33947539/154664723-099692ac-9f08-4811-88c0-b50bebcaddbd.png)

## CloudFront Caching Process
![image](https://user-images.githubusercontent.com/33947539/154657912-113cff6f-3a39-4207-9a6c-810110c67967.png)

**Step 1**: The user request is landed on the closest Edge location. The process checks the requested resource (image) is available at the Edge location.

**Step 2**: If the content is available, it returns the successful response with the requested image. This is a “Cache Hit” scenario.

**Step 3**: If it is not available at the Edge location, the process requests it from the Regional Edge location. This is a “Cache Miss” scenario. If it is available it sends the image back to the requester.

**Step 4**: If not, it requests it from the AWS origin

**Step 5 and 6**: The process returns the image back to the requester.

**Step 7**: Another user tries to retrieve the same image, which the first user tried. The second user gets it from a different Edge location close to his access.

**Step 8**: Since the second Edge location does not have the image file (since it was copied only to the first Edge location before), it tries to get it from the Regional Edge location, which the first user also used. (Remember that multiple Edge location can share the same Regional Edge location).

**Step 9 and 10**: Since the Regional Edge location already has it, it returns the image file back to the second user.


## WAF, Security, and Charges for CloudFront

### AWS WAF
AWS WAF is a web application firewall that lets you monitor HTTP and HTTPS requests that are forwarded to CloudFront. It also lets you control access to your content.

With AWS WAF, you can shield access to content based on conditions in a web access control list (web ACL) such as:

- Origin IP address.- Values in query strings.

CloudFront responds 
to requests with the requested content or an HTTP 403 status code (forbidden). CloudFront can also be configured to deliver a custom error page. 

### Security
CloudFront is PCI DSS compliant, but it is not recommended to cache credit card information at edge locations. It is also HIPAA compliant as a HIPAA eligible service.

Distributed Denial of Service (DDoS) protection

CloudFront distributes traffic across multiple edge locations and filters requests to ensure that only valid HTTP(S) requests will be forwarded to back-end hosts. CloudFront also supports geo-blocking, which you can use to prevent requests from particular geographic locations from being served.


### Restrictions
Blacklists and whitelists can be used for geography. You can only use one at a time.

There are two options available for geo-restriction (geo-blocking):

👉 Use the CloudFront geo-restriction feature (use for restricting access to all files in a distribution and at the country level).

👉 Use a 3rd party geo-location service (use it for restricting access to a subset of the files in a distribution and for finer granularity at the country level).

### Amazon CloudFront - Signed URLs, Cookies and OAI
https://cloud.in28minutes.com/aws-certification-amazon-cloudfront-signed-urls-cookies-oai-s3


## Reference 
https://kumargaurav1247.medium.com/aws-cdn-content-delivery-network-cloudfront-with-hands-on-e074b0e77166#:~:text=Amazon%20S3%20is%20designed%20for,close%20to%20users%20as%20possible.
