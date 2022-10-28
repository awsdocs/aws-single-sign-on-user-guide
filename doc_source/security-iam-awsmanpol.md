# AWS managed policies for IAM Identity Center<a name="security-iam-awsmanpol"></a>

To [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need takes time and expertise\. To get started quickly, you can use AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the **ReadOnlyAccess** AWS managed policy provides read\-only access to all AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.

New actions that allow you to list and delete user sessions are available under the new namespace `identitystore-auth`\. Any additional permissions for actions in this namespace will be updated on this page\. When creating your custom IAM policies, avoid using `*` after `identitystore-auth` because this applies to all actions that exist in the namespace today or in the future\.

## AWS managed policy: AWSSSOMasterAccountAdministrator<a name="security-iam-awsmanpol-AWSSSOMasterAccountAdministrator"></a>

The `AWSSSOMasterAccountAdministrator` policy provides required administrative actions to principals\. The policy is intended for principals who perform the job role of an AWS IAM Identity Center \(successor to AWS Single Sign\-On\) administrator\. Over time the list of actions provided will be updated to match the existing functionality of IAM Identity Center and the actions that are required as an administrator\.

You can attach the `AWSSSOMasterAccountAdministrator` policy to your IAM identities\. When you attach the `AWSSSOMasterAccountAdministrator` policy to an identity, you grant administrative AWS IAM Identity Center \(successor to AWS Single Sign\-On\) permissions\. Principals with this policy can access IAM Identity Center within the AWS Organizations management account and all member accounts\. This principal can fully manage all IAM Identity Center operations, including the ability to create an IAM Identity Center instance, users, permission sets, and assignments\. The principal can also instantiate those assignments throughout the AWS organization member accounts and establish connections between AWS Directory Service managed directories and IAM Identity Center\. As new administrative features are released, the account administrator will be granted these permissions automatically\.

**Permissions groupings**

This policy is grouped into statements based on the set of permissions provided\.
+ `AWSSSOMasterAccountAdministrator` – Allows IAM Identity Center to [pass the service role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_passrole.html) named `AWSServiceRoleforSSO` to IAM Identity Center so that it can later assume the role and perform actions on their behalf\. This is necessary when the person or application attempts to enable IAM Identity Center\. For more information, see [Multi\-account permissions](manage-your-accounts.md)\.
+ `AWSSSOMemberAccountAdministrator` – Allows IAM Identity Center to perform account administrator actions in a multi\-account AWS environment\. For more information, see [AWS managed policy: AWSSSOMemberAccountAdministrator](#security-iam-awsmanpol-AWSSSOMemberAccountAdministrator)\.
+ `AWSSSOManageDelegatedAdministrator` – Allows IAM Identity Center to register and deregister a delegated administrator for your organization\. 

```
{
   "Version":"2012-10-17",
   "Statement":[
     {
         "Sid": "AWSSSOCreateSLR",
         "Effect": "Allow",
         "Action": "iam:CreateServiceLinkedRole",
         "Resource": "arn:aws:iam::*:role/aws-service-role/sso.amazonaws.com/AWSServiceRoleForSSO",
         "Condition": {
            "StringLike": {
               "iam:AWSServiceName": "sso.amazonaws.com"
            }
         }
     },
     {
         "Sid":"AWSSSOMasterAccountAdministrator",
         "Effect":"Allow",
         "Action":"iam:PassRole",
         "Resource":"arn:aws:iam::*:role/aws-service-role/sso.amazonaws.com/AWSServiceRoleForSSO",
         "Condition":{
             "StringLike":{
               "iam:PassedToService":"sso.amazonaws.com"
             }
         }
      },
      {
         "Sid":"AWSSSOMemberAccountAdministrator",
         "Effect":"Allow",
         "Action":[
            "ds:DescribeTrusts",
            "ds:UnauthorizeApplication",
            "ds:DescribeDirectories",
            "ds:AuthorizeApplication",
            "iam:ListPolicies",
            "organizations:EnableAWSServiceAccess",
            "organizations:ListRoots",
            "organizations:ListAccounts",
            "organizations:ListOrganizationalUnitsForParent",
            "organizations:ListAccountsForParent",
            "organizations:DescribeOrganization",
            "organizations:ListChildren",
            "organizations:DescribeAccount",
            "organizations:ListParents",
            "organizations:ListDelegatedAdministrators",
            "sso:*",
            "sso-directory:*",
            "identitystore:*",
            "identitystore-auth:*",
            "ds:CreateAlias",
            "access-analyzer:ValidatePolicy"
         ],
         "Resource":"*"
      },
      {
         "Sid": "AWSSSOManageDelegatedAdministrator",
         "Effect": "Allow",
         "Action": [
            "organizations:RegisterDelegatedAdministrator",
            "organizations:DeregisterDelegatedAdministrator"
         ],
         "Resource": "*",
         "Condition": {
            "StringEquals": { 
               "organizations:ServicePrincipal": "sso.amazonaws.com"
        }
            }
        }

   ]
}
```

### Additional information about this policy<a name="security-iam-awsmanpol-additional-info"></a>

When IAM Identity Center is enabled for the first time, the IAM Identity Center service creates a [service linked role](https://docs.aws.amazon.com/singlesignon/latest/userguide/using-service-linked-roles.html) in the AWS Organizations management account \(formerly master account\) so that IAM Identity Center can manage the resources in your account\. The actions required are `iam:CreateServiceLinkedRole` and `iam:PassRole`, which are shown in the following snippets\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Sid": "AWSSSOCreateSLR",
         "Effect": "Allow",
         "Action": "iam:CreateServiceLinkedRole",
         "Resource": "arn:aws:iam::*:role/aws-service-role/sso.amazonaws.com/AWSServiceRoleForSSO",
         "Condition": {
            "StringLike": {
               "iam:AWSServiceName": "sso.amazonaws.com"
            }
         }
      },
      {
         "Sid":"AWSSSOMasterAccountAdministrator",
         "Effect":"Allow",
         "Action":"iam:PassRole",
         "Resource":"arn:aws:iam::*:role/aws-service-role/sso.amazonaws.com/AWSServiceRoleForSSO",
         "Condition":{
             "StringLike":{
               "iam:PassedToService":"sso.amazonaws.com"
             }
         }
      },
   ]
}
```

## AWS managed policy: AWSSSOMemberAccountAdministrator<a name="security-iam-awsmanpol-AWSSSOMemberAccountAdministrator"></a>

The `AWSSSOMemberAccountAdministrator` policy provides required administrative actions to principals\. The policy is intended for principals who perform the job role of an IAM Identity Center administrator\. Over time the list of actions provided will be updated to match the existing functionality of IAM Identity Center and the actions that are required as an administrator\.

You can attach the `AWSSSOMemberAccountAdministrator` policy to your IAM identities\. When you attach the `AWSSSOMemberAccountAdministrator` policy to an identity, you grant administrative AWS IAM Identity Center \(successor to AWS Single Sign\-On\) permissions\. Principals with this policy can access IAM Identity Center within the AWS Organizations management account and all member accounts\. This principal can fully manage all IAM Identity Center operations, including the ability to create users, permission sets, and assignments\. The principal can also instantiate those assignments throughout the AWS organization member accounts and establish connections between AWS Directory Service managed directories and IAM Identity Center\. As new administrative features are released, the account administrator is granted these permissions automatically\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AWSSSOMemberAccountAdministrator",
      "Effect": "Allow",
      "Action": [
        "ds:DescribeDirectories",
        "ds:AuthorizeApplication",
        "ds:UnauthorizeApplication",
        "ds:DescribeTrusts",
        "iam:ListPolicies",
        "organizations:EnableAWSServiceAccess",
        "organizations:DescribeOrganization",
        "organizations:DescribeAccount",
        "organizations:ListRoots",
        "organizations:ListAccounts",
        "organizations:ListAccountsForParent",
        "organizations:ListParents",
        "organizations:ListChildren",
        "organizations:ListOrganizationalUnitsForParent",
        "organizations:ListDelegatedAdministrators",
        "sso:*",
        "sso-directory:*",
        "identitystore:*",
        "identitystore-auth:*",
        "ds:CreateAlias",
        "access-analyzer:ValidatePolicy"
      ],
      "Resource": "*"
    },
    {
      "Sid": "AWSSSOManageDelegatedAdministrator",
      "Effect": "Allow",
      "Action": [
        "organizations:RegisterDelegatedAdministrator",
        "organizations:DeregisterDelegatedAdministrator"
      ],
      "Resource": "*",
        "Condition": {
           "StringEquals": { 
              "organizations:ServicePrincipal": "sso.amazonaws.com"
        }
            }
        }
  ]
}
```

### Additional information about this policy<a name="security-iam-awsmanpol-additional-info-AWSSSOMemberAccountAdministrator"></a>

IAM Identity Center administrators manage users, groups, and passwords in their Identity Center directory store \(sso\-directory\)\. The account admin role includes permissions for the following actions:
+ `"sso:*"`
+ `"sso-directory:*"`

IAM Identity Center administrators need limited permissions to the following AWS Directory Service actions to perform daily tasks\.
+ `"ds:DescribeTrusts"`
+ `"ds:UnauthorizeApplication"`
+ `"ds:DescribeDirectories"`
+ `"ds:AuthorizeApplication"`
+ `“ds:CreateAlias”`

These permissions allow IAM Identity Center administrators to identify existing directories and manage applications so that they can be configured for use with IAM Identity Center\. For more information about each of these actions, see [AWS Directory Service API permissions: Actions, resources, and conditions reference](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/UsingWithDS_IAM_ResourcePermissions.html)\.

IAM Identity Center uses IAM policies to grant permissions to IAM Identity Center users\. IAM Identity Center administrators create permission sets and attach polices to them\. The IAM Identity Center administrator must have the permissions to list the existing policies so that they can choose which polices to use with the permission set they are creating or updating\. To set secure and functional permissions, the IAM Identity Center administrator must have permissions to run the IAM Access Analyzer policy validation\.
+ `"iam:ListPolicies"`
+ `"access-analyzer:ValidatePolicy"`

IAM Identity Center administrators need limited access to the following AWS Organizations actions to perform daily tasks:
+ `"organizations:EnableAWSServiceAccess"`
+ `"organizations:ListRoots"`
+ `"organizations:ListAccounts"`
+ `"organizations:ListOrganizationalUnitsForParent"`
+ `"organizations:ListAccountsForParent"`
+ `"organizations:DescribeOrganization"`
+ `"organizations:ListChildren"`
+ `"organizations:DescribeAccount"`
+ `"organizations:ListParents"`
+ `"organizations:ListDelegatedAdministrators"`
+  `"organizations:RegisterDelegatedAdministrator"` 
+  `"organizations:DeregisterDelegatedAdministrator"` 

These permissions allow IAM Identity Center administrators the ability to work with organization resources \(accounts\) for basic IAM Identity Center administrative tasks such as the following:
+ Identifying the management account that belongs to the organization
+ Identifying the member accounts that belong to the organization
+ Enabling AWS service access for accounts
+ Setting up and managing a delegated administrator

For more information about using a delegated administrator with IAM Identity Center, see [Delegated administration](delegated-admin.md)\. For more information about how these permissions are used with AWS Organizations, see [Using AWS Organizations with other AWS services](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_integrate_services.html)\.

## AWS managed policy: AWSSSODirectoryAdministrator<a name="security-iam-awsmanpol-AWSSSODirectoryAdministrator"></a>

You can attach the `AWSSSODirectoryAdministrator` policy to your IAM identities\.

This policy grants administrative permissions over IAM Identity Center users and groups\. Principals with this policy attached can make any updates to IAM Identity Center users and groups\. The content of this policy statement is shown in the following snippet\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AWSSSODirectoryAdministrator",
            "Effect": "Allow",
            "Action": [
                "sso-directory:*",
                "identitystore:*",
                "identitystore-auth:*",
                "sso:ListDirectoryAssociations"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSSSOReadOnly<a name="security-iam-awsmanpol-AWSSSOReadOnly"></a>

You can attach the `AWSSSOReadOnly` policy to your IAM identities\.

This policy grants read\-only permissions that allow users to view information in IAM Identity Center\. Principals with this policy attached cannot view the IAM Identity Center users or groups directly\. Principals with this policy attached cannot make any updates in IAM Identity Center\. For example, principals with these permissions can view IAM Identity Center settings, but cannot change any of the setting values\. The content of this policy statement is shown in the following snippet\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AWSSSOReadOnly",
            "Effect": "Allow",
            "Action": [
                "ds:DescribeDirectories",
                "ds:DescribeTrusts",
                "iam:ListPolicies",
                "organizations:DescribeOrganization",
                "organizations:DescribeAccount",
                "organizations:ListParents",
                "organizations:ListChildren",
                "organizations:ListAccounts",
                "organizations:ListRoots",
                "organizations:ListAccountsForParent",
                "organizations:ListOrganizationalUnitsForParent",
                "organizations:ListDelegatedAdministrators",
                "sso:Describe*",
                "sso:Get*",
                "sso:List*",
                "sso:Search*",
                "sso-directory:DescribeDirectory",
                "access-analyzer:ValidatePolicy"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSSSODirectoryReadOnly<a name="security-iam-awsmanpol-AWSSSODirectoryReadOnly"></a>

You can attach the `AWSSSODirectoryReadOnly` policy to your IAM identities\.

This policy grants read\-only permissions that allow users to view users and groups in IAM Identity Center\. Principals with this policy attached cannot view IAM Identity Center assignments, permission sets, applications, or settings\. Principals with this policy attached can't make any updates in IAM Identity Center\. For example, principals with these permissions can view IAM Identity Center users, but they can't change any user attributes or assign MFA devices\. The content of this policy statement is shown in the following snippet\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AWSSSODirectoryReadOnly",
            "Effect": "Allow",
            "Action": [
                "sso-directory:Search*",
                "sso-directory:Describe*",
                "sso-directory:List*",
                "sso-directory:Get*",
                "identitystore:Describe*",
                "identitystore:List*"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSIdentitySyncFullAccess<a name="security-iam-awsmanpol-AWSIdentitySyncFullAccess"></a>

You can attach the `AWSIdentitySyncFullAccess` policy to your IAM identities\.

Principals with this policy attached have full access permissions to create and delete sync profiles, associate or update a sync profile with a sync target, create, list and delete sync filters, and start or stop synchronization\.

**Permission details**

This policy includes the following permissions when accessing Active Directory\.
+ `ds:AuthorizeApplication` – Allows identity\-sync to grant access to the application during the sync profile creation process\.
+ `ds:UnauthorizeApplication` – Allows identity\-sync to remove access to the application during the sync profile deletion process\.

The content of this policy statement is shown in the following snippet\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ds:AuthorizeApplication",
                "ds:UnauthorizeApplication"
            ],
            "Resource": "*"
        },  
        {
            "Effect": "Allow",
            "Action": [
                "identity-sync:DeleteSyncProfile",
                "identity-sync:CreateSyncProfile",
                "identity-sync:GetSyncProfile",
                "identity-sync:StartSync",
                "identity-sync:StopSync",
                "identity-sync:CreateSyncFilter",
                "identity-sync:DeleteSyncFilter",
                "identity-sync:ListSyncFilters",
                "identity-sync:CreateSyncTarget",
                "identity-sync:DeleteSyncTarget",
                "identity-sync:GetSyncTarget",
                "identity-sync:UpdateSyncTarget"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSIdentitySyncReadOnlyAccess<a name="security-iam-awsmanpol-AWSIdentitySyncReadOnlyAccess"></a>

You can attach the `AWSIdentitySyncReadOnlyAccess` policy to your IAM identities\.

This policy grants read\-only permissions that allow users to view information about the identity synchronization profile, filters, and target settings\. Principals with this policy attached can't make any updates to synchronization settings\. For example, principals with these permissions can view identity synchronization settings, but can't change any of the profile or filter values\. The content of this policy statement is shown in the following snippet\.

```
{
    "Version": "2012-10-17",
    "Statement": [ 
        {
            "Effect": "Allow",
            "Action": [
                "identity-sync:GetSyncProfile",
                "identity-sync:ListSyncFilters",
                "identity-sync:GetSyncTarget",
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSSSOServiceRolePolicy<a name="security-iam-awsmanpol-AWSSSOServiceRolePolicy"></a>

You can't attach the `AWSSSOServiceRolePolicy` policy to your IAM identities\.

This policy is attached to a service\-linked role that allows IAM Identity Center to delegate and enforce which users have single sign\-on access to specific AWS accounts in AWS Organizations\. When you enable IAM, a service\-linked role is created in all of the AWS accounts within your organization\. IAM Identity Center also creates the same service\-linked role in every account that is subsequently added to your organization\. This role allows IAM Identity Center to access each account's resources on your behalf\. Service\-linked roles that are created in each AWS account are named `AWSServiceRoleForSSO`\. For more information, see [Using service\-linked roles for IAM Identity Center](using-service-linked-roles.md)\.

## IAM Identity Center updates to AWS managed policies<a name="security-iam-awsmanpol-updates"></a>

The following table describes the updates to AWS managed policies for IAM Identity Center since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the IAM Identity Center Document history page\.


| Change | Description | Date | 
| --- | --- | --- | 
| [AWSSSOServiceRolePolicy](#security-iam-awsmanpol-AWSSSOServiceRolePolicy) |  This policy now allows the`[UpdateSAMLProvider](https://docs.aws.amazon.com/IAM/latest/APIReference/API_UpdateSAMLProvider.html)` action to be taken on the management account\.  | October 20, 2022 | 
| [AWSSSOMasterAccountAdministrator](#security-iam-awsmanpol-AWSSSOMasterAccountAdministrator) |  This policy now includes the new namespace `identitystore-auth` with new permissions to allow the admin to list and delete sessions for a user\.  |  October 20, 2022  | 
| [AWSSSOMemberAccountAdministrator](#security-iam-awsmanpol-AWSSSOMemberAccountAdministrator) |  This policy now includes the new namespace `identitystore-auth` with new permissions to allow the admin to list and delete sessions for a user\.  |  October 20, 2022  | 
| [AWSSSODirectoryAdministrator](#security-iam-awsmanpol-AWSSSODirectoryAdministrator) |  This policy now includes the new namespace `identitystore-auth` with new permissions to allow the admin to list and delete sessions for a user\.  |  October 20, 2022  | 
| [AWSSSOMasterAccountAdministrator](#security-iam-awsmanpol-AWSSSOMasterAccountAdministrator) |  This policy now includes new permissions to call `[ListDelegatedAdministrators](https://docs.aws.amazon.com/organizations/latest/APIReference/API_ListDelegatedAdministrators.html)` in AWS Organizations\. This policy also now includes a subset of permissions `AWSSSOManageDelegatedAdministrator` that includes permissions to call `[RegisterDelegatedAdministrator](https://docs.aws.amazon.com/organizations/latest/APIReference/API_RegisterDelegatedAdministrator.html)` and `[DeregisterDelegatedAdministrator](https://docs.aws.amazon.com/organizations/latest/APIReference/API_DeregisterDelegatedAdministrator.html)`\.   |  August 16, 2022  | 
| [AWSSSOMemberAccountAdministrator](#security-iam-awsmanpol-AWSSSOMemberAccountAdministrator) |  This policy now includes new permissions to call `[ListDelegatedAdministrators](https://docs.aws.amazon.com/organizations/latest/APIReference/API_ListDelegatedAdministrators.html)` in AWS Organizations\. This policy also now includes a subset of permissions `AWSSSOManageDelegatedAdministrator` that includes permissions to call `[RegisterDelegatedAdministrator](https://docs.aws.amazon.com/organizations/latest/APIReference/API_RegisterDelegatedAdministrator.html)` and `[DeregisterDelegatedAdministrator](https://docs.aws.amazon.com/organizations/latest/APIReference/API_DeregisterDelegatedAdministrator.html)`\.   |  August 16, 2022  | 
| [AWSSSOReadOnly](#security-iam-awsmanpol-AWSSSOReadOnly) |  This policy now includes new permissions to call `[ListDelegatedAdministrators](https://docs.aws.amazon.com/organizations/latest/APIReference/API_ListDelegatedAdministrators.html)` in AWS Organizations\.  |  August 11, 2022  | 
| [AWSSSOServiceRolePolicy](#security-iam-awsmanpol-AWSSSOServiceRolePolicy) |  This policy now includes new permissions to call `[DeleteRolePermissionsBoundary](https://docs.aws.amazon.com/IAM/latest/APIReference/API_DeleteRolePermissionsBoundary.html)` and `[PutRolePermisionsBoundary](https://docs.aws.amazon.com/IAM/latest/APIReference/API_PutRolePermissionsBoundary.html)`\.  | July 14, 2022 | 
| [AWSSSOServiceRolePolicy](#security-iam-awsmanpol-AWSSSOServiceRolePolicy) | This policy now includes new permissions that allow calls to [ListAWSServiceAccessForOrganization](https://docs.aws.amazon.com/organizations/latest/APIReference/API_ListAWSServiceAccessForOrganization.html) and [ListDelegatedAdministrators](https://docs.aws.amazon.com/organizations/latest/APIReference/API_ListDelegatedAdministrators.html) in AWS Organizations\. | May 11, 2022 | 
|  [AWSSSOMasterAccountAdministrator](#security-iam-awsmanpol-AWSSSOMasterAccountAdministrator) [AWSSSOMemberAccountAdministrator](#security-iam-awsmanpol-AWSSSOMemberAccountAdministrator) [AWSSSOReadOnly](#security-iam-awsmanpol-AWSSSOReadOnly)  | Add IAM Access Analyzer permissions that allow a principal to use the policy checks for validation\. | April 28, 2022 | 
| [AWSSSOMasterAccountAdministrator](#security-iam-awsmanpol-AWSSSOMasterAccountAdministrator) |  This policy now allows all IAM Identity Center Identity Store service actions\. For information about the actions available in the IAM Identity Center Identity Store service, see the [IAM Identity Center Identity Store API Reference](https://docs.aws.amazon.com/singlesignon/latest/IdentityStoreAPIReference/welcome.html)\.  | March 29, 2022 | 
| [AWSSSOMemberAccountAdministrator](#security-iam-awsmanpol-AWSSSOMemberAccountAdministrator) |  This policy now allows all IAM Identity Center Identity Store service actions\.  | March 29, 2022 | 
| [AWSSSODirectoryAdministrator](#security-iam-awsmanpol-AWSSSODirectoryAdministrator) |  This policy now allows all IAM Identity Center Identity Store service actions\.  | March 29, 2022 | 
| [AWSSSODirectoryReadOnly](#security-iam-awsmanpol-AWSSSODirectoryReadOnly) |  This policy now grants access to the IAM Identity Center Identity Store service read actions\. This access is required to retrieve user and group information from the IAM Identity Center Identity Store service\.  | March 29, 2022 | 
| [AWSIdentitySyncFullAccess](#security-iam-awsmanpol-AWSIdentitySyncFullAccess) |  This policy allows full access to identity\-sync permissions\.  | March 3, 2022 | 
| [AWSIdentitySyncReadOnlyAccess](#security-iam-awsmanpol-AWSIdentitySyncReadOnlyAccess) |  This policy grants read\-only permissions that allow a principal to view identity\-sync settings\.  | March 3, 2022 | 
| [AWSSSOReadOnly](#security-iam-awsmanpol-AWSSSOReadOnly) |  This policy grants read\-only permissions that allow a principal to view IAM Identity Center configuration settings\.   | August 4, 2021 | 
| IAM Identity Center started tracking changes | IAM Identity Center started tracking changes for AWS managed policies\. | August 4, 2021 | 