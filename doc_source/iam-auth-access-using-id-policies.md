# Using Identity\-Based Policies \(IAM Policies\) for AWS SSO<a name="iam-auth-access-using-id-policies"></a>

This topic provides examples of permissions policies that an account administrator can attach to IAM identities \(that is, users, groups, and roles\)\. 

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your AWS SSO resources\. For more information, see [Overview of Managing Access Permissions to Your AWS SSO Resources](iam-auth-access-overview.md)\.

The sections in this topic cover the following:
+ [Permissions Required to Use the AWS SSO Console](#requiredpermissionsconsole)
+ [AWS Managed \(Predefined\) Policies for AWS SSO](#accesscontrolmanagedpolicies)

The following shows an example of a permissions policy\.

```
{
  "Version" : "2012-10-17",
  "Statement" : [
    {
      "Action" : [
        "sso:CreateApplicationInstance",
        "sso:UpdateResponseConfig",
        "sso:UpdateResponseSchemaConfig",
        "sso:UpdateSecurityConfig",
        "sso:UpdateServiceProviderConfig",
        "sso:UpdateApplicationInstanceStatus",
        "sso:UpdateApplicationInstanceDisplay",
        "sso:CreateProfile",
        "sso:SetupTrust"
      ],
      "Effect" : "Allow",
      "Resource" : "*"
    },
    
    {
      "Action" : [
        "organizations:xxx", 
        "organizations:yyy"
       ],
      "Effect" : "Allow",
      "Resource" : "*"
    },
    
    {
      "Action" : [
        "ds:AuthorizeApplication"
      ],
      "Effect" : "Allow",
      "Resource" : "*"
    }
  ]
}
```

The policy includes the following:
+ The first statement grants permission to manage profile associations to users and groups within your directory\. It also grants permission to read all of the AWS SSO resources\.
+ The second statement grants permissions to search the directory for users and groups\. This is required before you can create profile associations\. 

The policy doesn't specify the `Principal` element because in an identity\-based policy you don't specify the principal who gets the permission\. When you attach a policy to a user, the user is the implicit principal\. When you attach a permission policy to an IAM role, the principal identified in the role's trust policy gets the permissions\.

## Permissions Required to Use the AWS SSO Console<a name="requiredpermissionsconsole"></a>

For a user to work with the AWS SSO console, that user must have permissions listed in the preceding policy\.

If you create an IAM policy that is more restrictive than the minimum required permissions, the console won't function as intended for users with that IAM policy\. 

## AWS Managed \(Predefined\) Policies for AWS SSO<a name="accesscontrolmanagedpolicies"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.