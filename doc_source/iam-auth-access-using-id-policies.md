# Identity\-based policy examples for IAM Identity Center<a name="iam-auth-access-using-id-policies"></a>

This topic provides examples of permissions policies that you can attach to AWS identities, including IAM users, groups, and roles, and IAM Identity Center users \(as part of a custom permissions policy\), for administration of IAM Identity Center\. 

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your IAM Identity Center resources\. For more information, see [Overview of managing access permissions to your IAM Identity Center resources](iam-auth-access-overview.md)\.

The sections in this topic cover the following:
+ [Custom policy examples](#policyexample)
+ [Permissions required to use the IAM Identity Center console](#requiredpermissionsconsole)

## Custom policy examples<a name="policyexample"></a>

This section provides examples of common use cases that require a custom IAM policy\. These example policies are identity\-based policies, which do not specify the Principal element\. This is because with an identity\-based policy, you don't specify the principal who gets the permission\. Instead, you attach the policy to the principal\. When you attach an identity\-based permission policy to an IAM role, the principal identified in the role's trust policy gets the permissions\. You can create identity\-based policies in IAM and attach them to users, groups, and/or roles\. You can also apply these policies to IAM Identity Center users when you create a permission set in IAM Identity Center\.

**Note**  
Use these examples when you create policies for your environment and make sure to test for both positive \(“access granted”\) and negative \(“access denied”\) test cases before you deploy these policies in your production environment\. For more information about testing IAM policies, see [Testing IAM policies with the IAM policy simulator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

**Topics**
+ [Example 1: Allow a user to view IAM Identity Center](#policyexamplesetupenable)
+ [Example 2: Allow a user to manage permissions to AWS accounts in IAM Identity Center](#policyexamplemanageconnecteddirectory)
+ [Example 3: Allow a user to manage applications in IAM Identity Center](#policyexamplemanageapplication)
+ [Example 4: Allow a user to manage users and groups in your Identity Center directory](#policyexamplemanageusersgroups)
+ [Example 5: Allow a user to administer IAM Identity Center for specific accounts](#policyexamplemanageaccount)

### Example 1: Allow a user to view IAM Identity Center<a name="policyexamplesetupenable"></a>

The following permissions policy grants read\-only permissions to a user so they can view all the settings and directory information configured in IAM Identity Center\. 

**Note**  
This policy is provided for example purposes only\. In a production environment, we recommend that you use the `ViewOnlyAccess` AWS managed policy for IAM Identity Center\.

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

### Example 2: Allow a user to manage permissions to AWS accounts in IAM Identity Center<a name="policyexamplemanageconnecteddirectory"></a>

The following permissions policy grants permissions to allow a user to create, manage, and deploy permission sets for your AWS accounts\. 

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

### Example 3: Allow a user to manage applications in IAM Identity Center<a name="policyexamplemanageapplication"></a>

The following permissions policy grants permissions to allow a user to view and configure applications in IAM Identity Center, including pre\-integrated SaaS applications from within the IAM Identity Center catalog\. 

**Note**  
The `sso:AssociateProfile` operation used in the following policy example is required for management of user and group assignments to applications\. It also allows a user to assign users and groups to AWS accounts by using existing permission sets\. If a user must manage AWS account access within IAM Identity Center, and requires permissions necessary to manage permission sets, see [Example 2: Allow a user to manage permissions to AWS accounts in IAM Identity Center](#policyexamplemanageconnecteddirectory)\.

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

### Example 4: Allow a user to manage users and groups in your Identity Center directory<a name="policyexamplemanageusersgroups"></a>

The following permissions policy grants permissions to allow a user to create, view, modify, and delete users and groups in IAM Identity Center\. 

In some cases, direct modifications to users and groups in IAM Identity Center are restricted\. For example, when Active Directory, or an external identity provider with Automatic Provisioning enabled, is selected as the identity source\.

```
 1. {
 2.     "Version": "2012-10-17",
 3.     "Statement": [
 4.         {
 5.             "Effect": "Allow",
 6.             "Action": [
 7.                 "sso-directory:ListGroupsForUser",
 8.                 "sso-directory:DisableUser",
 9.                 "sso-directory:EnableUser",
10.                 "sso-directory:SearchGroups",
11.                 "sso-directory:DeleteGroup",
12.                 "sso-directory:AddMemberToGroup",
13.                 "sso-directory:DescribeDirectory",
14.                 "sso-directory:UpdateUser",
15.                 "sso-directory:ListMembersInGroup",
16.                 "sso-directory:CreateUser",
17.                 "sso-directory:DescribeGroups",
18.                 "sso-directory:SearchUsers",
19.                 "sso:ListDirectoryAssociations",
20.                 "sso-directory:RemoveMemberFromGroup",
21.                 "sso-directory:DeleteUser",
22.                 "sso-directory:DescribeUsers",
23.                 "sso-directory:UpdateGroup",
24.                 "sso-directory:CreateGroup"
25.             ],
26.             "Resource": "*"
27.         }
28.     ]
29. }
```

### Example 5: Allow a user to administer IAM Identity Center for specific accounts<a name="policyexamplemanageaccount"></a>

As your team grows, consider implementing a delegation model that enables AWS account administrators to manage their users' single sign\-on access to their resources\. By using this model and the following example policy, you can delegate permissions for administering AWS accounts\. After you create this policy, you can select the same policy any time you need to delegate the same permissions to other administrative users\.

**Account\-based delegation**

The following policy grants permissions that allow you to delegate access for each of the AWS accounts under `Resource`\.

```
 1. {
 2.     "Version": "2012-10-17",
 3.     "Statement": [
 4.         {
 5.             "Sid":"DelegateAccountsAdminAccess",
 6.             "Effect":"Allow",
 7.             "Action":[
 8.                 "sso:ProvisionPermissionSet",
 9.                 "sso:CreateAccountAssignment",
10.                 "sso:DeleteInlinePolicyFromPermissionSet",
11.                 "sso:UpdateInstanceAccessControlAttributeConfiguration",
12.                 "sso:PutInlinePolicyToPermissionSet",
13.                 "sso:DeleteAccountAssignment",
14.                 "sso:DetachManagedPolicyFromPermissionSet",
15.                 "sso:DeletePermissionSet",
16.                 "sso:AttachManagedPolicyToPermissionSet",
17.                 "sso:CreatePermissionSet",
18.                 "sso:UpdatePermissionSet",
19.                 "sso:CreateInstanceAccessControlAttributeConfiguration",
20.                 "sso:DeleteInstanceAccessControlAttributeConfiguration"
21.            ],
22.            "Resource":[
23.                 "arn:aws:sso:::account/112233445566",
24.                 "arn:aws:sso:::account/223344556677",
25.                 "arn:aws:sso:::account/334455667788",
26.                 "arn:aws:sso:::permissionSet/*/*",
27.                 "arn:aws:sso:::instance/ssoins-xxxxxxxxx"
28.            ]
29.         }
30.    ]  
31. }
```

**More information**

For an example walkthrough that covers how to delegate administration of user identities in an IAM environment, see [How to delegate management of identity in AWS IAM Identity Center \(successor to AWS Single Sign\-On\)](https://aws.amazon.com/blogs/security/how-to-delegate-management-of-identity-in-aws-single-sign-on/) on the AWS Security Blog\.

## Permissions required to use the IAM Identity Center console<a name="requiredpermissionsconsole"></a>

For a user to work with the IAM Identity Center console without errors, additional permissions are required\. If an IAM policy has been created that is more restrictive than the minimum required permissions, the console won't function as intended for users with that policy\. The following example lists the set of permissions that might be needed to ensure error\-free operation within the IAM Identity Center console\.

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