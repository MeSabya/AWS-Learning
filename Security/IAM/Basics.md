## IAM Identities 
are the constructs used to define who has access to AWS resources and what they can do. These include IAM users, groups, and roles.

## IAM Entities 
are the actual actors (like users, services, or federated identities) that perform actions within AWS, authenticated and authorized by the policies attached to their identities.

## IAM Users and Groups

- An IAM user is an identity we can use to provide account access to an individual entity. It is used when we want to provide long-term credentials to an entity.
- Using the IAM user credentials, the principal entity can authenticate itself with AWS and log in to the account.
- However, by default, the IAM users cannot perform any function besides logging into the account.
- To authorize the user to perform the required actions, we attach the IAM policy with the IAM user.
- The policy defines the scope of permissions of the user. So, the IAM user identity handles user authentication, while the attached policy is responsible for authorization.

## Why to use IAM users

### Secure the root account
The main account that we create on AWS is a root account. It has all the privileges and can perform all sorts of operations.
Using this account for day-to-day operations is not recommended, as it can be used to change the account settings. So, to start off, we should create an IAM user with administrative access and use that account instead of the root account.

### Provide access to principal entities
An organization usually consists of different operational units. For example, there can be admins, developers, QA, and many other departments. We can provide each of them with an IAM account with permission to perform only their respective tasks. By doing so, not only are we providing them with the required access but also making sure that they do not have permission to do anything out of their scope of work.

## IAM user workflow
When creating an IAM user, we provide a username and a password for the user. The specific entity can then use these credentials to log in to the AWS account. Along with these basic credentials, we can use some other credentials for authentication. The choice of authentication credentials depends upon the type of access required. Aside from the username and password that we use to log in to the AWS console, the other credentials are as follows:

- Access keys: These credentials are useful when we make programmatic calls to AWS. They consist of AWS ACCESS ID and AWS SECRET KEY.
- SSH keys for use with CodeCommit: This is a public SSH key that can be used to authenticate with CodeCommit.
- Server certificates: These are SSL/TLS certificates that we can use to authenticate with some AWS services.

  
