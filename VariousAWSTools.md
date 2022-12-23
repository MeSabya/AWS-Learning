### AWS Migration Tools
**AWS Server Migration Service (SMS)**:   To migrate the server to Amazon EC2.

**AWS Database Migration Service (DMS)**: To directly migrate the database to RDS.

**AWS DataSync** is used for migrating data, not databases.

**CloudFront**
is a content delivery network (CDN) that caches content closer to users. You can cache the static content on CloudFront using the EC2 instances as origins for the content. This will improve performance (as the content is closer to the users) and reduce the need for the ASG to scale (as you don’t need the processing power of the EC2 instances to serve the static content).

