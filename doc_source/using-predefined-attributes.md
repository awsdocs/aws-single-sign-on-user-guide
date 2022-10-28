# Using predefined attributes from the IAM Identity Center directory for access control in AWS<a name="using-predefined-attributes"></a>

Each user in the IAM Identity Center directory is assigned a unique `UserId`\. You can view the `UserId` for your users by using the IAM Identity Center console and navigating to each user or by using the [DescribeUser](https://docs.aws.amazon.com/singlesignon/latest/IdentityStoreAPIReference/API_DescribeUser.html) API action\. IAM Identity Center allows you to use this `UserId` in permissions sets or resource\-based policies for making access control decisions in AWS\. For example, the following permissions policy allows a user with <UserId> to call get operations against all of their Amazon S3 resources\. This permission allows the user to read the object data from *mybucket*\. 

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Principal":"*",
         "Action":[
            "s3:GetObject",
            "s3:GetObjectVersion"
         ],
         "Resource":[
            "arn:aws:s3:::mybucket/*"
         ],
         "Condition":{
            "StringEquals":{
               "identitystore:UserId":[
                  "<UserId>"
               ]
            }
         }
      }
   ]
}
```

If you want to confirm that the caller is an IAM Identity Center user, you can specify a `Null` clause as a condition, as follows:

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Condition":{
            "Null":{
               "identitystore:UserId":"false"
            }
         }
      }
   ]
}
```