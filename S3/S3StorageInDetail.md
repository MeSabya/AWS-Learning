# Amazon Web Service S3 Storage Classes

The different storage classes provided are:

- S3 Standard
- S3 Standard-IA
- S3 One Zone-IA
- S3 Glacier
- S3 Glacier Deep Archive

## S3 Standard (General purpose)
- S3 Standard is the default storage class, if nothing is specified during upload.
- S3 Standard offers high durability, availability, and performance object storage for frequently accessed data.
- S3 Standard is the most expensive storage class among all others.
- Designed for durability of 99.999999999% of objects across multiple Availability Zones.
- Data is stored in multiple locations. S3 standard is Resilient against events that impact an entire Availability Zone and is designed to sustain the loss of data in a two facilities.
- Designed for 99.99% availability over a given year
- Supports SSL for data in transit and encryption of data at rest.

## S3 Standard-IA ( Infrequent access)
- S3 Standard-Infrequent Access storage class is optimized for long-lived and less frequently accessed data. for e.g. for backups and older data where access is limited, but the use case still demands high performance.
- Designed for durability of 99.999999999% of objects across multiple Availability Zones.
- The S3 Standard-IA is ideal for backups, long-term storage, and as a data store for disaster recovery.
- Data stored redundantly across multiple geographically separated AZs and are resilient to the loss of an Availability Zone.
- Suitable for larger objects greater than 128 KB (smaller objects are charged for 128 KB only) kept for at least 30 days (charged for minimum 30 days)
- Designed for 99.999999999% i.e. 11 9’s Durability of objects across AZs
- Designed for 99.9% availability over a given year.

## S3 One Zone-Infrequent Access (S3 One Zone-IA)
- One Zone-Infrequent Access storage class is as durable as Standard-Infrequent Access, but it is less available and less resilient.
- Designed for 99.999999999% i.e. 11 9’s Durability of objects in a single AZ
- Designed for 99.5% availability over a given year

## S3 Glacier (Archive)
- GLACIER storage class is suitable for low cost data archiving where data access is infrequent and retrieval time of minutes to hours is acceptable.
- Storage class has a minimum storage duration period of 90 days
- Provides configurable retrieval times, from minutes to hours.
- Designed for 99.999999999% i.e. 11 9’s Durability of objects across AZs
- Designed for 99.9% availability over a given year

## S3 Glacier Deep Archive
- Glacier Deep Archive storage class provides lowest cost data archiving where data access is infrequent and retrieval time of hours is acceptable.
- Has a minimum storage duration period of 180 days and can be accessed in at a default retrieval time of 12 hours.
- Supports long-term retention and digital preservation for data that may be accessed once or twice in a year
- Designed for 99.999999999% i.e. 11 9’s Durability of objects across AZs
- Designed for 99.9% availability over a given year
