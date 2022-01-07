# Identity\-based policy examples for AWS SSO<a name="iam-auth-access-using-id-policies"></a>

This topic provides examples of permissions policies that an account administrator can attach to AWS identities, including IAM users, groups, and roles, and AWS SSO users \(as part of a custom permissions policy\), for administration of AWS SSO\. 

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your AWS SSO resources\. For more information, see [Overview of managing access permissions to your AWS SSO resources](iam-auth-access-overview.md)\.

The sections in this topic cover the following:
+ [Custom policy examples](#policyexample)
+ [Permissions required to use the AWS SSO console](#requiredpermissionsconsole)

## Custom policy examples<a name="policyexample"></a>

In this section, you can find examples of common use cases which require a custom IAM policy\. The example policies below are identity\-based policies, which do not specify the Principal element\. This is because with an identity\-based policy, you don't specify the principal who gets the permission\. Instead, you attach the policy to the principal\. When you attach an identity\-based permission policy to an IAM role, the principal identified in the role's trust policy gets the permissions\. Identity\-based policies can be created in IAM and are attached to users, groups, and/or roles, or can be applied to AWS SSO users as part of a custom permissions policy in an AWS SSO permission set\. 

**Note**  
Use these examples when crafting policies for your environment and make sure to test for both positive \(“access granted”\) and negative \(“access denied”\) test cases prior to deploying in your production deployment\. For more information about testing IAM policies, see [Testing IAM policies with the IAM policy simulator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

**Topics**
+ [Example 1: Allow a user to view AWS SSO](#policyexamplesetupenable)
+ [Example 2: Allow a user to manage permissions to AWS accounts in AWS SSO](#policyexamplemanageconnecteddirectory)
+ [Example 3: Allow a user to manage applications in AWS SSO](#policyexamplemanageapplication)
+ [Example 4: Allow a user to manage users and groups in your AWS SSO directory](#policyexamplemanageaccount)
+ [Example 5: Allow a user to administer AWS SSO for specific permission sets, accounts, or OUs](#policyexamplemanageaccount)

### Example 1: Allow a user to view AWS SSO<a name="policyexamplesetupenable"></a>

The following permissions policy grants read\-only permissions to a user so they can view all of the settings and directory information configured within AWS SSO\. 

**Note**  
This example policy is provided purely for illustrative purposes\. In a production environment, we recommend that you use the AWS Managed Policy for Read\-Only access to AWS SSO\.

```
 1. {
 2.     "Version": "2012-10-17",
 3.     "Statement": [
 4.         {
 5.             "Sid": "VisualEditor0",
 6.             "Effect": "Allow",
 7.             "Action": [
 8.                 "ds:DescribeDirectories",
 9.                 "ds:DescribeTrusts",
10.                 "iam:ListPolicies",
11.                 "organizations:DescribeOrganization",
12.                 "organizations:DescribeAccount",
13.                 "organizations:ListParents",
14.                 "organizations:ListChildren",
15.                 "organizations:ListAccounts",
16.                 "organizations:ListRoots",
17.                 "organizations:ListAccountsForParent",
18.                 "organizations:ListOrganizationalUnitsForParent",
19.                 "sso:ListManagedPoliciesInPermissionSet",
20.                 "sso:ListPermissionSetsProvisionedToAccount",
21.                 "sso:ListAccountAssignments",
22.                 "sso:ListAccountsForProvisionedPermissionSet",
23.                 "sso:ListPermissionSetsProvisionedToAccount",
24.                 "sso:ListPermissionSets",
25.                 "sso:DescribePermissionSet",
26.                 "sso:GetInlinePolicyForPermissionSet",
27.                 "sso-directory:DescribeDirectory",
28.                 "sso-directory:SearchUsers",
29.                 "sso-directory:SearchGroups"
30.             ],
31.             "Resource": "*"
32.         }
33.     ]
34. }
```

### Example 2: Allow a user to manage permissions to AWS accounts in AWS SSO<a name="policyexamplemanageconnecteddirectory"></a>

The following permissions policy grants permissions to allow a user to create, manage and deploy permission sets for your AWS accounts\. 

```
 1. {
 2.     "Version": "2012-10-17",
 3.     "Statement": [
 4.         {
 5.             "Effect": "Allow",
 6.             "Action": [
 7.                 "sso:AttachManagedPolicyToPermissionSet",
 8.                 "sso:CreateAccountAssignment",
 9.                 "sso:CreatePermissionSet",
10.                 "sso:DeleteAccountAssignment",
11.                 "sso:DeleteInlinePolicyFromPermissionSet",
12.                 "sso:DeletePermissionSet",
13.                 "sso:DetachManagedPolicyFromPermissionSet",
14.                 "sso:ProvisionPermissionSet",
15.                 "sso:PutInlinePolicyToPermissionSet",
16.                 "sso:UpdatePermissionSet"
17.             ],
18.             "Resource": "*"
19.         },
20.         {
21.             "Sid": "IAMListPermissions",
22.             "Effect": "Allow",
23.             "Action": [
24.                 "iam:ListRoles",
25.                 "iam:ListPolicies"
26.             ],
27.             "Resource": "*"
28.         },
29.         {
30.             "Sid": "AccessToSSOProvisionedRoles",
31.             "Effect": "Allow",
32.             "Action": [
33.                 "iam:AttachRolePolicy",
34.                 "iam:CreateRole",
35.                 "iam:DeleteRole",
36.                 "iam:DeleteRolePolicy",
37.                 "iam:DetachRolePolicy",
38.                 "iam:GetRole",
39.                 "iam:ListAttachedRolePolicies",
40.                 "iam:ListRolePolicies",
41.                 "iam:PutRolePolicy",
42.                 "iam:UpdateRole",
43.                 "iam:UpdateRoleDescription"
44.             ],
45.             "Resource": "arn:aws:iam::*:role/aws-reserved/sso.amazonaws.com/*"
46.         },
47.         {
48.             "Effect": "Allow",
49.             "Action": [
50.                 "iam:GetSAMLProvider"
51.             ],
52.             "Resource": "arn:aws:iam::*:saml-provider/AWSSSO_*_DO_NOT_DELETE"
53.         }
54.     ]
55. }
```

**Note**  
The additional permissions listed under the `"Sid": "IAMListPermissions"`, and `"Sid": "AccessToSSOProvisiondRoles"` sections are required only to enable the user to create assignments in the AWS Organizations management account\.

### Example 3: Allow a user to manage applications in AWS SSO<a name="policyexamplemanageapplication"></a>

The following permissions policy grants permissions to allow a user to view and configure applications in AWS SSO, including pre\-integrated SaaS applications from within the AWS SSO catalog\. 

**Note**  
The `sso:AssociateProfile` operation used in the policy example below is required for management of user and group assignments to applications\. It also allows a user to assign users and groups to AWS accounts, using existing permission sets\. If a user needs to manage AWS account access within AWS SSO, and requires permissions necessary to manage permission sets, see [Example 2: Allow a user to manage permissions to AWS accounts in AWS SSO](#policyexamplemanageconnecteddirectory)\.

As of October 2020, many of these operations are available only through the AWS console\. This example policy includes “read” actions such as list, get, and search, which are relevant to the error\-free operation of the console for this case\.

```
 1. {
 2.     "Version": "2012-10-17",
 3.     "Statement": [
 4.         {
 5.             "Effect": "Allow",
 6.             "Action": [
 7.                 "sso:AssociateProfile",
 8.                 "sso:CreateApplicationInstance",
 9.                 "sso:ImportApplicationInstanceServiceProviderMetadata",
10.                 "sso:DeleteApplicationInstance",
11.                 "sso:DeleteProfile",
12.                 "sso:DisassociateProfile",
13.                 "sso:GetApplicationTemplate",
14.                 "sso:UpdateApplicationInstanceServiceProviderConfiguration",
15.                 "sso:UpdateApplicationInstanceDisplayData",
16.                 "sso:DeleteManagedApplicationInstance",
17.                 "sso:UpdateApplicationInstanceStatus",
18.                 "sso:GetManagedApplicationInstance",
19.                 "sso:UpdateManagedApplicationInstanceStatus",
20.                 "sso:CreateManagedApplicationInstance",
21.                 "sso:UpdateApplicationInstanceSecurityConfiguration",
22.                 "sso:UpdateApplicationInstanceResponseConfiguration",
23.                 "sso:GetApplicationInstance",
24.                 "sso:CreateApplicationInstanceCertificate",
25.                 "sso:UpdateApplicationInstanceResponseSchemaConfiguration",
26.                 "sso:UpdateApplicationInstanceActiveCertificate",
27.                 "sso:DeleteApplicationInstanceCertificate",
28.                 "sso:ListApplicationInstanceCertificates",
29.                 "sso:ListApplicationTemplates",
30.                 "sso:ListApplications",
31.                 "sso:ListApplicationInstances",
32.                 "sso:ListDirectoryAssociations",
33.                 "sso:ListProfiles",
34.                 "sso:ListProfileAssociations",
35.                 "sso:ListInstances",
36.                 "sso:GetProfile",
37.                 "sso:GetSSOStatus",
38.                 "sso:GetSsoConfiguration",
39.                 "sso-directory:DescribeDirectory",
40.                 "sso-directory:DescribeUsers",
41.                 "sso-directory:ListMembersInGroup",
42.                 "sso-directory:SearchGroups",
43.                 "sso-directory:SearchUsers"
44.             ],
45.             "Resource": "*"
46.         }
47.     ]
48. }
```

### Example 4: Allow a user to manage users and groups in your AWS SSO directory<a name="policyexamplemanageaccount"></a>

The following permissions policy grants permissions to allow a user to create, view, modify, and delete users and groups in AWS SSO\. 

Note that in some cases direct modifications to users and groups in AWS SSO are restricted\. For example, when Active Directory, or an external identity provider with Automatic Provisioning enabled, is selected as the identity source\.

```
 1. {
 2.     "Version": "2012-10-17",
 3.     "Statement": [
 4.         {
 5.             "Sid": "VisualEditor0",
 6.             "Effect": "Allow",
 7.             "Action": [
 8.                 "sso-directory:ListGroupsForUser",
 9.                 "sso-directory:DisableUser",
10.                 "sso-directory:EnableUser",
11.                 "sso-directory:SearchGroups",
12.                 "sso-directory:DeleteGroup",
13.                 "sso-directory:AddMemberToGroup",
14.                 "sso-directory:DescribeDirectory",
15.                 "sso-directory:UpdateUser",
16.                 "sso-directory:ListMembersInGroup",
17.                 "sso-directory:CreateUser",
18.                 "sso-directory:DescribeGroups",
19.                 "sso-directory:SearchUsers",
20.                 "sso:ListDirectoryAssociations",
21.                 "sso-directory:RemoveMemberFromGroup",
22.                 "sso-directory:DeleteUser",
23.                 "sso-directory:DescribeUsers",
24.                 "sso-directory:UpdateGroup",
25.                 "sso-directory:CreateGroup"
26.             ],
27.             "Resource": "*"
28.         }
29.     ]
30. }
```

### Example 5: Allow a user to administer AWS SSO for specific permission sets, accounts, or OUs<a name="policyexamplemanageaccount"></a>

As your team grows, an AWS SSO administrator may want to consider implementing a delegation model that enables AWS account and application administrators to manage their users SSO access to their resources\. Using this model and the example policies below, permissions can be delegated for administering AWS accounts, permission sets, or OUs\. Once any of these policies have been created, that same policy can be selected anytime the same permissions need to be delegated to other administrative users\.

**Account\-based delegation**

The following policy grants permissions that allow an administrator to delegate access for each of the AWS accounts noted under `Resource`\.

```
 1. {
 2.    "Sid":"DelegateAccountsAdminAccess",
 3.    "Effect":"Allow",
 4.    "Action":[
 5.       "sso:ProvisionPermissionSet",
 6.       "sso:CreateAccountAssignment",
 7.       "sso:DeleteInlinePolicyFromPermissionSet",
 8.       "sso:UpdateInstanceAccessControlAttributeConfiguration",
 9.       "sso:PutInlinePolicyToPermissionSet",
10.       "sso:DeleteAccountAssignment",
11.       "sso:DetachManagedPolicyFromPermissionSet",
12.       "sso:DeletePermissionSet",
13.       "sso:AttachManagedPolicyToPermissionSet",
14.       "sso:CreatePermissionSet",
15.       "sso:UpdatePermissionSet",
16.       "sso:CreateInstanceAccessControlAttributeConfiguration",
17.       "sso:DeleteInstanceAccessControlAttributeConfiguration"
18.    ],
19.    "Resource":[
20.       "arn:aws:sso:::account/112233445566",
21.       "arn:aws:sso:::account/223344556677",
22.       "arn:aws:sso:::account/334455667788"
23.    ]
24. }
```

**Permission\-based delegation**

The following permissions policy grants permissions that allow an administrator to delegate access for a given AWS SSO instance ID ARN \(in this case, `ssoins-1111111111`\) or permission set ARN \(`ssoins-1111111111/ps-112233abcdef123`\)\.

For more information about finding the ARNs associated with an AWS SSO instance ID or permission set, see [Identify your permission set and AWS SSO Instance IDs](https://aws.amazon.com/blogs/security/how-to-delegate-management-of-identity-in-aws-single-sign-on/#Identify) on the AWS Security blog\.

```
 1. {
 2.    "Sid":"DelegatePermissionsAdminAccess",
 3.    "Effect":"Allow",
 4.    "Action":[
 5.       "sso:ProvisionPermissionSet",
 6.       "sso:CreateAccountAssignment",
 7.       "sso:DeleteInlinePolicyFromPermissionSet",
 8.       "sso:UpdateInstanceAccessControlAttributeConfiguration",
 9.       "sso:PutInlinePolicyToPermissionSet",
10.       "sso:DeleteAccountAssignment",
11.       "sso:DetachManagedPolicyFromPermissionSet",
12.       "sso:DeletePermissionSet",
13.       "sso:AttachManagedPolicyToPermissionSet",
14.       "sso:CreatePermissionSet",
15.       "sso:UpdatePermissionSet",
16.       "sso:CreateInstanceAccessControlAttributeConfiguration",
17.       "sso:DeleteInstanceAccessControlAttributeConfiguration",
18.       "sso:ProvisionApplicationInstanceForAWSAccount"
19.    ],
20.    "Resource":[
21.       "arn:aws:sso:::instance/ssoins-1111111111",
22.       "arn:aws:sso:::permissionSet/ssoins-1111111111/ps-112233abcdef123"
23.    ]
24. }
```

**OU\-based delegation**

OU\-based delegation requires two policy statements within the same permission set and the ability for [Tagging AWS Single Sign\-On resources](tagging.md)\. 

The following permissions policy grants permissions that allow an administrator to delegate access for an OU\. In the first policy statement, we filter the permission sets by both the `Environment` and `OU` tags\. In the second policy statement, we filter the accounts that are tagged for the `Development` OU\. 

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Sid":"DelegateOUsAdminAccess",
 6.          "Effect":"Allow",
 7.          "Action":[
 8.             "sso:ProvisionPermissionSet",
 9.             "sso:CreateAccountAssignment",
10.             "sso:DeleteInlinePolicyFromPermissionSet",
11.             "sso:UpdateInstanceAccessControlAttributeConfiguration",
12.             "sso:PutInlinePolicyToPermissionSet",
13.             "sso:DeleteAccountAssignment",
14.             "sso:DetachManagedPolicyFromPermissionSet",
15.             "sso:DeletePermissionSet",
16.             "sso:AttachManagedPolicyToPermissionSet",
17.             "sso:CreatePermissionSet",
18.             "sso:UpdatePermissionSet",
19.             "sso:CreateInstanceAccessControlAttributeConfiguration",
20.             "sso:DeleteInstanceAccessControlAttributeConfiguration",
21.             "sso:ProvisionApplicationInstanceForAWSAccount"
22.          ],
23.          "Resource":"arn:aws:sso:::permissionSet/*/*",
24.          "Condition":{
25.             "StringEquals":{
26.                "aws:ResourceTag/Environment":"Development",
27.                "aws:ResourceTag/OU":"Test"
28.             }
29.          }
30.       },
31.       {
32.          "Sid":"Instance",
33.          "Effect":"Allow",
34.          "Action":[
35.             "sso:ProvisionPermissionSet",
36.             "sso:CreateAccountAssignment",
37.             "sso:DeleteInlinePolicyFromPermissionSet",
38.             "sso:UpdateInstanceAccessControlAttributeConfiguration",
39.             "sso:PutInlinePolicyToPermissionSet",
40.             "sso:DeleteAccountAssignment",
41.             "sso:DetachManagedPolicyFromPermissionSet",
42.             "sso:DeletePermissionSet",
43.             "sso:AttachManagedPolicyToPermissionSet",
44.             "sso:CreatePermissionSet",
45.             "sso:UpdatePermissionSet",
46.             "sso:CreateInstanceAccessControlAttributeConfiguration",
47.             "sso:DeleteInstanceAccessControlAttributeConfiguration",
48.             "sso:ProvisionApplicationInstanceForAWSAccount"
49.          ],
50.          "Resource":[
51.             "arn:aws:sso:::instance/ssoins-82593a6ed92c8920",
52.             "arn:aws:sso:::account/112233445566",
53.             "arn:aws:sso:::account/223344556677",
54.             "arn:aws:sso:::account/334455667788"
55.          ]
56.       }
57.    ]
58. }
```

**More information**

To see an example walkthrough that covers how to delegate administration of user identities in an IAM environment, see [How to delegate management of identity in AWS Single Sign\-On](https://aws.amazon.com/blogs/security/how-to-delegate-management-of-identity-in-aws-single-sign-on/) on the AWS Security Blog\.

## Permissions required to use the AWS SSO console<a name="requiredpermissionsconsole"></a>

For a user to work with the AWS SSO console without errors, additional permissions are required\. If an IAM policy has been created that is more restrictive than the minimum required permissions, the console won't function as intended for users with that policy\. The following example lists the set of permissions that may be needed to ensure error\-free operation within the AWS SSO console\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "sso:DescribeAccountAssignmentCreationStatus",
                "sso:DescribeAccountAssignmentDeletionStatus",
                "sso:DescribePermissionSet",
                "sso:DescribePermissionSetProvisioningStatus",
                "sso:DescribePermissionsPolicies",
                "sso:DescribeRegisteredRegions",
                "sso:GetApplicationInstance",
                "sso:GetApplicationTemplate",
                "sso:GetInlinePolicyForPermissionSet",
                "sso:GetManagedApplicationInstance",
                "sso:GetMfaDeviceManagementForDirectory",
                "sso:GetPermissionSet",
                "sso:GetPermissionsPolicy",
                "sso:GetProfile",
                "sso:GetSharedSsoConfiguration",
                "sso:GetSsoConfiguration",
                "sso:GetSSOStatus",
                "sso:GetTrust",
                "sso:ListAccountAssignmentCreationStatus",
                "sso:ListAccountAssignmentDeletionStatus",
                "sso:ListAccountAssignments",
                "sso:ListAccountsForProvisionedPermissionSet",
                "sso:ListApplicationInstanceCertificates",
                "sso:ListApplicationInstances",
                "sso:ListApplications",
                "sso:ListApplicationTemplates",
                "sso:ListDirectoryAssociations",
                "sso:ListInstances",
                "sso:ListManagedPoliciesInPermissionSet",
                "sso:ListPermissionSetProvisioningStatus",
                "sso:ListPermissionSets",
                "sso:ListPermissionSetsProvisionedToAccount",
                "sso:ListProfileAssociations",
                "sso:ListProfiles",
                "sso:ListTagsForResource",
                "sso-directory:DescribeDirectory",
                "sso-directory:DescribeGroups",
                "sso-directory:DescribeUsers",
                "sso-directory:ListGroupsForUser",
                "sso-directory:ListMembersInGroup",
                "sso-directory:SearchGroups",
                "sso-directory:SearchUsers"
            ],
            "Resource": "*"
        }
    ]
}
```