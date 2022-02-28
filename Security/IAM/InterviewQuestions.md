## Q: What is IAM service in AWS Cloud?

- IAM is abbreviation of Identity Access Management. 
- It’s a service offered by AWS Cloud that helps one to create user account and groups and manage their access to AWS services and resources securely. 
- IAM is a global service and has no additional fees associated to it. 

## Q: Explain different types of user accounts in AWS Cloud?

**Root User** is the Owner Account (administrator) and is created with the creation of AWS Account. 
It has full access by default to all services and resources in the AWS account. 
This user cannot be explicitly denied access to AWS resources or services with IAM Policies. 
In order to limit permissions to this user account, one has to do so with AWS Organization Service Control Policy (SCP). 
Some specific tasks such as closing an AWS Account can only be accomplished by the AWS Account Root User only. 

**IAM User** is a standard user account that has no permission to any AWS service or resource. This account is either created by root user or an IAM administrator. 
IAM Policies are used to define permissions to this user account. 
All the user, that require to login in AWS Management Console, or configure services or access resources programmatically, can have their individual IAM user account with different set of policies associated to them. 
Certain tasks such as closing an AWS Account cannot be accomplished by this user account.

## Q: Describe the key elements used in the JSON schema of an IAM policy?

![image](https://user-images.githubusercontent.com/33947539/155366058-92c3578d-0c71-46eb-8201-77b2ab515ab4.png)

## Q: What are some best practices to manage access to AWS resources?
 
Following are some best practices to manage access to AWS resources.

**Do not use root account** - Your root account has access to all your AWS resources and services, hence it is a best practice to not share or use it.

**Use Groups** - Instead of giving access to AWS resources and services for individual users - create groups, give needed access to the groups, and add users to the groups - so that all users within a group has the same access.

**Enable Multi-factor Authentication (MFA)** - It is a best practice to enable MFA for privileged users such as admins. MFA adds an extra layer of protection on top of basic user-id and password based authentication.

**Grant least privileges** - Grant only the minimum required permissions for the user or group.

## Q: A solutions architect is developing an encryption solution. The solution requires that data keys are encrypted using envelope protection before they are written to the disk.Which solution option can assist with this requirement?

      API Gateway with STS
      IAM Access Key
      AWS Certificate Manager
      AWS KMS API

**Correct Answer: 4**
Explanation: When you encrypt your data, your data is protected, but you still have to protect your encryption key. One strategy is to encrypt it. Envelope encryption is the practice of encrypting plaintext data with a data key and then encrypting the data key under another key.

![image](https://user-images.githubusercontent.com/33947539/155972087-d341439d-b6aa-41dc-9c38-e37ca9d5ef20.png)

##### Envelope encryption offers several benefits:

Protecting data keys: When you encrypt a data key, you don’t have to worry about storing the encrypted data key because the data key is inherently protected by encryption. You can safely store the encrypted data key alongside the encrypted data.

Encrypting the same data under multiple master keys: Encryption operations can be time-consuming, particularly when the data being encrypted are large objects. Instead of re-encrypting raw data multiple times with different keys, you can re-encrypt only the data keys that protect the raw data.

Combining the strengths of multiple algorithms: In general, symmetric key algorithms are faster and produce smaller ciphertexts than public-key algorithms. But public-key algorithms provide inherent separation of roles and easier key management. Envelope encryption lets you combine the strengths of each strategy.

INCORRECT: “API Gateway with STS” is incorrect. The AWS Security Token Service (STS) is a web service that enables you to request temporary, limited-privilege credentials for AWS Identity and Access Management (IAM) users or for users that you authenticate (federated users).

INCORRECT: “IAM Access Key” is incorrect. IAM access keys are used for signing programmatic requests that you make to AWS.

INCORRECT: “AWS Certificate Manager” is incorrect. AWS Certificate Manager is a service that lets you easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with AWS services and your internal connected resources.

CORRECT: “AWS KMS API” is the correct answer.

