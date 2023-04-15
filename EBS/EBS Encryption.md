👉 Amazon EBS automatically creates a unique AWS managed key **in each Region** where you store AWS resources. 
This KMS key has the alias alias/aws/ebs. By default, Amazon EBS uses this KMS key for encryption. 
Alternatively, you can specify a symmetric customer managed encryption key that you created as the default KMS key for EBS encryption. 
Using your own KMS key gives you more flexibility, including the ability to create, rotate, and disable KMS keys.

👉 Amazon EBS does not support asymmetric encryption KMS keys.

👉 You can encrypt both the boot and data volumes of an EC2 instance.

👉 You can attach both encrypted and unencrypted volumes to an instance simultaneously.

👉 Encryption is supported by all EBS volume types.


