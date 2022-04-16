# RDS Security — Encryption

##  Encryption of Data In-Rest
- Amazon RDS encrypts your databases using keys you manage with the AWS Key Management Service (KMS).
- Data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots.
- RDS encryption uses the industry standard AES-256 encryption algorithm to encrypt your data on the server that hosts your RDS instance.
- With TDE, the database server automatically encrypts data before it is written to storage and automatically decrypts data when it is read from storage.
- Encryption has to be defined at launch time
- Transparent Data Encryption (TDE) available for (SQL Server Enterprise Edition) and Oracle (Oracle Advanced Security option in Oracle Enterprise Edition).

## Encryption of Data In-flight

![image](https://user-images.githubusercontent.com/33947539/163663947-aa84bfa3-ca6b-4d8c-9cc3-95ba7e40e7dc.png)

- You can encrypt connections between your application and your DB Instance using SSL certificates.
- Amazon RDS creates an SSL certificate and installs the certificate on the DB instance when Amazon RDS provisions the instance.
- These certificates are signed by a certificate authority.
- The public key is stored at https://s3.amazonaws.com/rds-downloads/rds-combined-ca-bundle.pem
- Provide SSL options with trust certificate when connecting to database
- To enforce SSL

PostgreSQL: rds.force_ssl=1 in the AWS RDS Console (Parameter Groups)

MySQL: Within the DB: GRANT USAGE ON *.* TO ‘mysqluser’@’%’ REQUIRE SSL.

```
You can only enable encryption for an Amazon RDS DB instance when you create it, not after the DB instance is created. 
However, because you can encrypt a copy of an unencrypted DB snapshot, you can effectively add encryption to an unencrypted DB instance. 
That is, you can create a snapshot of your DB instance, and then create an encrypted copy of that snapshot. 
You can then restore a DB instance from the encrypted snapshot, and thus you have an encrypted copy of your original DB instance.
```

👉 DB instances that are encrypted can’t be modified to disable encryption.

👉 You can’t have an encrypted Read Replica of an unencrypted DB instance or an unencrypted Read Replica of an encrypted DB instance.

👉 Encrypted Read Replicas must be encrypted with the same key as the source DB instance.

👉 You can’t restore an unencrypted backup or snapshot to an encrypted DB instance.

👉 To copy an encrypted snapshot from one AWS Region to another, you must specify the KMS key identifier of the destination AWS Region. 
   This is because KMS encryption keys are specific to the AWS Region that they are created in.

👉 The source snapshot remains encrypted throughout the copy process. AWS Key Management Service uses envelope encryption to protect data during the copy process.


### How to encrypt
So, if you already have an unencrypted database you can encrypt it in the next way:

- Stop writes on the RDS instance
- Create a manual snapshot of the unencrypted RDS instance
- Go to Snapshots and choose the snapshot just created
- Copy snapshot and enable encryption
- Select the new encrypted snapshot
- Restore encrypted snapshot

## Network and IAM

![image](https://user-images.githubusercontent.com/33947539/163667493-3a24b3ef-7276-49a7-83c7-752205e981a6.png)


## Reference :
[How to Secure RDS on AWS](https://medium.com/swlh/how-to-secure-rds-on-aws-b46b15b7c7c6)

