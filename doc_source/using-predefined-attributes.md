# Using predefined attributes from the AWS SSO identity store for access control in AWS<a name="using-predefined-attributes"></a>

Each user in the AWS SSO Identity Store is assigned a unique `UserId`\. You can view the `UserId` for your users using the AWS SSO console by navigating to each user or calling the [DescribeUser](https://docs.aws.amazon.com/singlesignon/latest/IdentityStoreAPIReference/API_DescribeUser.html) API\. AWS SSO allows you to use this `UserId` in permissions sets or resource based policies for making access control decisions in AWS\. For example, the permissions policy below will allow a user with <UserId> to call read operations against all SSM Incident Manager resources\. This permission allows the user to read the object data from *mybucket*\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "ssmincidents:List*",
                "ssmincidents:Get*"
            ],
            "Resource": [
                "*"
            ],
            "Condition": {
                "StringEquals": {
                    "identitystore:UserId": [
                        "<UserId>"
                    ]
                },
                "Null": {
                    "identitystore:UserId": "false"
                }
            }
        }
    ]
}
```