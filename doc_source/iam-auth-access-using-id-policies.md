# Using Identity\-Based Policies \(IAM Policies\) for AWS SSO<a name="iam-auth-access-using-id-policies"></a>

This topic provides examples of permissions policies that an account administrator can attach to IAM identities \(that is, users, groups, and roles\)\. 

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your AWS SSO resources\. For more information, see [Overview of Managing Access Permissions to Your AWS SSO Resources](iam-auth-access-overview.md)\.

The sections in this topic cover the following:
+ [Permissions Required to Use the AWS SSO Console](#requiredpermissionsconsole)
+ [AWS Managed \(Predefined\) Policies for AWS SSO](#accesscontrolmanagedpolicies)
+ [Customer Managed Policy Examples](#policyexample)

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

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

## Customer Managed Policy Examples<a name="policyexample"></a>

In this section, you can find example user policies that grant permissions for various AWS SSO actions\. 

**Topics**
+ [Example 1: Allow a User to Set Up and Enable AWS SSO](#policyexamplesetupenable)
+ [Example 2: Allow a User to Manage Your AWS SSO Connected Directory](#policyexamplemanageconnecteddirectory)
+ [Example 3: Allow a User to Manage Applications in AWS SSO](#policyexamplemanageapplication)
+ [Example 4: Allow a User to Manage Permissions for Your AWS Accounts in AWS SSO](#policyexamplemanageaccount)
+ [Example 5: Allow a User to Manage Access for Your Applications in AWS SSO](#policyexamplemanageapplicationaccess)
+ [Example 6: Allow a User to Find Which Cloud Applications Are Preintegrated with AWS SSO](#policyexamplefindapplication)

### Example 1: Allow a User to Set Up and Enable AWS SSO<a name="policyexamplesetupenable"></a>

The following permissions policy grants permissions to allow a user to open the AWS SSO console and enable the service\. In order to do so, permissions such as those granted to the AWS Organizations master account are also required\.

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action": [
 7.                 sso:StartSSO,
 8.                 sso:GetSSOStatus
 9.                   ],
10.          "Resource":"*"
11.       }, 
12.       {
13.          "Effect":"Allow",
14.          "Action": [
15.                 organizations:DescribeAccount,
16.                 organizations:EnableAWSServiceAccess
17.                   ],
18.          "Resource":"*"
19. 
20.       }
21.    ]
22. }
```

### Example 2: Allow a User to Manage Your AWS SSO Connected Directory<a name="policyexamplemanageconnecteddirectory"></a>

The following permissions policy grants permissions to a user to manage your connected directory\. 

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action": [
 7.                 sso:AssociateDirectory,
 8.                 sso:DisassociateDirectory,
 9.                 sso:ListDirectoryAssociations,
10.                 sso:UpdateDirectoryAssociation
11.                   ],
12.          "Resource":"*"
13.       },
14.       {
15.          "Effect":"Allow",
16.          "Action": [
17.                 ds:DescribeDirectories
18.                   ],
19.          "Resource":"*"
20.       }
21.    ]
22. }
```

### Example 3: Allow a User to Manage Applications in AWS SSO<a name="policyexamplemanageapplication"></a>

The following permissions policy grants permissions to allow a user to create and manage application instances, profiles, and certificates in the AWS SSO console\.

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action": [
 7.                 sso:ListApplicationTemplates,
 8.                 sso:GetApplicationTemplate
 9.                 sso:ListApplicationInstances,
10.                 sso:GetApplicationInstance,
11.                 sso:CreateApplicationInstance,
12.                 sso:UpdateApplicationInstanceStatus,
13.                 sso:UpdateApplicationInstanceDisplayData,
14.                 sso:UpdateApplicationInstanceServiceProviderConfiguration,
15.                 sso:UpdateApplicationInstanceResponseConfiguration,
16.                 sso:UpdateApplicationInstanceResponseSchemaConfiguration,
17.                 sso:UpdateApplicationInstanceSecurityConfiguration,
18.                 sso:DeleteApplicationInstance,
19.                 sso:ImportApplicationInstanceServiceProviderMetadata,
20.                 sso:CreateProfile,
21.                 sso:UpdateProfile,
22.                 sso:DeleteProfile,
23.                 sso:GetProfile,
24.                 sso:ListProfiles,
25.                 sso:ListApplicationInstanceCertificates,
26.                 sso:CreateApplicationInstanceCertificate,
27.                 sso:UpdateApplicationInstanceActiveCertificate,
28.                 sso:DeleteApplicationInstanceCertificate
29.                   ],
30.          "Resource":"*"
31.       }
32.    ]
33. }
```

### Example 4: Allow a User to Manage Permissions for Your AWS Accounts in AWS SSO<a name="policyexamplemanageaccount"></a>

The following permissions policy grants permissions to allow a user to create and manage permission sets for your AWS accounts in the AWS SSO console\.

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action": [
 7.                 sso:ListApplicationInstances,
 8.                 sso:GetApplicationInstance,
 9.                 sso:CreateApplicationInstance,
10.                 sso:UpdateApplicationInstanceStatus,
11.                 sso:UpdateApplicationInstanceDisplayData,
12.                 sso:UpdateApplicationInstanceServiceProviderConfiguration,
13.                 sso:UpdateApplicationInstanceResponseConfiguration,
14.                 sso:UpdateApplicationInstanceResponseSchemaConfiguration,
15.                 sso:UpdateApplicationInstanceSecurityConfiguration,
16.                 sso:DeleteApplicationInstance,
17.                 sso:ImportApplicationInstanceServiceProviderMetadata,
18.                 sso:CreateProfile,
19.                 sso:UpdateProfile,
20.                 sso:DeleteProfile,
21.                 sso:GetProfile,
22.                 sso:ListProfiles,
23.                 sso:ListApplicationInstanceCertificates,
24.                 sso:CreateApplicationInstanceCertificate,
25.                 sso:UpdateApplicationInstanceActiveCertificate,
26.                 sso:DeleteApplicationInstanceCertificate,
27.                 sso:CreatePermissionSet,
28.                 sso:GetPermissionSet,
29.                 sso:ListPermissionSets,
30.                 sso:DeletePermissionSet,
31.                 sso:PutPermissionsPolicy,
32.                 sso:DeletePermissionsPolicy,
33.                 sso:DescribePermissionsPolicies,
34.                 sso:GetTrust,
35.                 sso:CreateTrust,
36.                 sso:UpdateTrust,
37.                 sso:DeleteTrust
38.                   ],
39.          "Resource":"*"
40.       }, 
41.       {
42.          "Effect":"Allow",
43.          "Action": [
44.                 organizations:DescribeOrganization
45.                   ],
46.          "Resource":"*"
47.       }
48.    ]
49. }
```

### Example 5: Allow a User to Manage Access for Your Applications in AWS SSO<a name="policyexamplemanageapplicationaccess"></a>

The following permissions policy grants permissions to allow a user to manage who can access your applications in the AWS SSO console\.

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action": [
 7.                 sso:ListApplicationInstances,
 8.                 sso:ListProfileAssociations,
 9.                 sso:AssociateProfile,
10.                 sso:DisassociateProfile
11.                   ],
12.          "Resource":"*"
13.       },
14.       {
15.          "Effect":"Allow",
16.          "Action": [
17.                 ds:DescribeDirectories
18.                   ],
19.          "Resource":"*"
20.       }
21.    ]
22. }
```

### Example 6: Allow a User to Find Which Cloud Applications Are Preintegrated with AWS SSO<a name="policyexamplefindapplication"></a>

The following permissions policy grants permissions to allow a user to locate what cloud applications are preintegrated with AWS SSO using the Add Application wizard\.

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action": [
 7.                 sso:ListApplicationTemplates,
 8.                 sso:GetApplicationTemplate
 9.                   ],
10.          "Resource":"*"
11.       }
12.    ]
13. }
```