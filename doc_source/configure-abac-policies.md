# Create permission policies for ABAC in IAM Identity Center<a name="configure-abac-policies"></a>

You can create permissions policies that determine who can access your AWS resources based on the configured attribute value\. When you enable ABAC and specify attributes, IAM Identity Center passes the attribute value of the authenticated user into IAM for use in policy evaluation\.

## aws:PrincipalTag condition key<a name="abac-principaltag"></a>

You can use access control attributes in your permission sets using the `aws:PrincipalTag` condition key for creating access control rules\. For example, in the following trust policy you can tag all the resources in your organization with their respective cost centers\. You can also use a single permission set that grants developers access to their cost center resources\. Now, whenever developers federate into the account using single sign\-on and their cost center attribute, they only get access to the resources in their respective cost centers\. As the team adds more developers and resources to their project, you only have to tag resources with the correct cost center\. Then you pass cost center information in the AWS session when developers federate into AWS accounts\. As a result, as the organization adds new resources and developers to the cost center, developers can manage resources aligned to their cost centers without needing any permission updates\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeInstances"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:StartInstances",
                "ec2:StopInstances"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "ec2:ResourceTag/CostCenter": "${aws:PrincipalTag/CostCenter}"
                }
            }
        }
    ]
}
```

For more information, see [aws:PrincipalTag](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-principaltag) and [EC2: Start or stop instances based on matching principal and resource tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_examples_ec2-start-stop-match-tags.html) in the *IAM User Guide*\.

If policies contain invalid attributes in their conditions, then the policy condition will fail and access will be denied\. For more information, see [Error 'An unexpected error has occurred' when a user tries to sign in using an external identity provider](troubleshooting.md#issue8)\.