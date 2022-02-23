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

