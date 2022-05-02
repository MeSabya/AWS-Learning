## What is an AWS IAM Policy? 

An AWS IAM policy defines the permissions of an identity (users, groups, and roles) or resource within the AWS account.

IAM policies can either be identity-based or resource-based. Identity-based policies are attached to an identity (a user, group, or role) and dictate the permissions of that specific identity. In contrast, a resource-based policy defines the permissions around the specific resource


### Example of an AWS IAM Policy
An organization initiates a short-term project. Current and new employees will need specific access to specialized resources during the lifecycle of this project. By creating an AWS IAM policy, IT admins can ensure that members of a project will only have access to the exact resources they’ll need to complete the project. 

They can do this by creating a policy that enables access to a particular resource for a specific date range and applying the policy to each IAM identity (users, roles, or groups).

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "arn:aws:s3:::s3-test-policy-bucket",
            "Condition": {
                "DateGreaterThan": {"aws:CurrentTime": "2022-04-01T00:00:00Z"},
                "DateLessThan": {"aws:CurrentTime": "2022-06-30T23:59:59Z"}
            }
        }
    ]
}
```

## What is an AWS IAM Role?

An IAM role is a set of permissions that define what actions are allowed and denied by an entity in the AWS console

Roles are designed so that a set of permissions can easily be delegated to users on an individual basis. For example, instead of assigning an individual all their necessary permissions one at a time, they can be assigned a specific role that contains all the necessary permissions in a single step. 

For example, you might want to allow a mobile app to use AWS resources, but you do not want it to save the key, credential or password. Or you might want to give access to resources to a user who already has an identity defined outside of AWS, such as a user who already has Google or Facebook authentication. If you want to provide someone with a service or let someone access resources in your account, you can use roles for that purpose too. You also might want to grant temporary access to your account to a third party, such as a consultant or an auditor. They’re not permanent users, just users with temporary access to your environment



### Example of an AWS IAM Role


