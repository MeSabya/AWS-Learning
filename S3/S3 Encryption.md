# S3 Encryption

Server Side Encryption (SSE): It is the simplest encryption provided by AWS. SSE performs heavy encryption. The are three types of it viz SSE-S3, SSE-KMS and SSE-C.

- SSE-S3: Here encryption keys are managed and handled by AWS to encrypt the data. We cannot see the key directly or use this key manually to encrypt or decrypt the data. AWS has developed an algorithm to encrypt data, called Advanced Encryption Standard (AES-256).
- SSE-C: Here encryption keys are provided by customers and AWS doesn’t store it. User have to passed their keys to AWS to handle each encryption/decryption request.
- SSE-KMS: SSE-KMS is somewhere in mid of SSE-S3 and SSE-C. Here data key is managed by AWS but user manages the customer master key (CMK).

- When we set up server-side encryption on the S3 bucket, it only affects new objects uploaded to that bucket. Any unencrypted objects already in the S3 bucket will stay encrypted.

- To encrypt the existing object we need to copy object back to itself using a customer managed key by adding the encryption argument. 

