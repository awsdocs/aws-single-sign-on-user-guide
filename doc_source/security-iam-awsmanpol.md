# AWS managed policies for AWS Single Sign\-On<a name="security-iam-awsmanpol"></a>

To [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need takes time and expertise\. To get started quickly, you can use AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the **ReadOnlyAccess** AWS managed policy provides read\-only access to all AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.

## AWS managed policy: AWSSSOMasterAccountAdministrator<a name="security-iam-awsmanpol-AWSSSOMasterAccountAdministrator"></a>

The `AWSSSOMasterAccountAdministrator` policy provides required administrative actions to principals\. The policy is intended for principals who perform the job role of an AWS SSO administrator\. Over time the list of actions provided will be updated to match the existing functionality of AWS SSO and the actions that are required as an administrator\.

You can attach the `AWSSSOMasterAccountAdministrator` policy to your IAM identities\. When you attach the `AWSSSOMasterAccountAdministrator` policy to an identity, you grant administrative AWS Single Sign\-On permissions\. Principals with this policy can access AWS SSO within the AWS Organizations management account and all member accounts\. This principal can fully manage all AWS SSO operations, including the ability to create an SSO instance, users, permission sets, and assignments\. The principal can also instantiate those assignments throughout the AWS organization member accounts and establish connections between AWS Directory Service managed directories and AWS SSO\. As new administrative features are released, the account administrator will be granted these permissions automatically\.

**Permissions groupings**

This policy is grouped into statements based on the set of permissions provided\.
+ `AWSSSOMasterAccountAdministrator` – Allows AWS SSO to [pass the service role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_passrole.html) named `AWSServiceRoleforSSO` to SSO so that it can later assume the role and perform actions on their behalf\. This is necessary when the person or application attempts to enable SSO\. For more information, see [Manage SSO to your AWS accounts](manage-your-accounts.md)\.
+ `AWSSSOMemberAccountAdministrator` – Allows AWS SSO to perform account administrator actions in a multi\-account AWS environment\. For more information, see [AWS managed policy: AWSSSOMemberAccountAdministrator](#security-iam-awsmanpol-AWSSSOMemberAccountAdministrator)\.

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
            "sso:*",
            "sso-directory:*",
            "ds:CreateAlias"
         ],
         "Resource":"*"
      }
   ]
}
```

### Additional information about this policy<a name="security-iam-awsmanpol-additional-info"></a>

When AWS SSO is enabled for the first time, the SSO service creates a [service linked role](https://docs.aws.amazon.com/singlesignon/latest/userguide/using-service-linked-roles.html) in the AWS Organizations management account \(formerly master account\) so that AWS SSO can manage the resources in your account\. The actions required are `iam:CreateServiceLinkedRole` and `iam:PassRole` which are shown below\.

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

The `AWSSSOMemberAccountAdministrator` policy provides required administrative actions to principals\. The policy is intended for principals who perform the job role of an AWS SSO administrator\. Over time the list of actions provided will be updated to match the existing functionality of AWS SSO and the actions that are required as an administrator\.

You can attach the `AWSSSOMemberAccountAdministrator` policy to your IAM identities\. When you attach the `AWSSSOMemberAccountAdministrator` policy to an identity, you grant administrative AWS Single Sign\-On permissions\. Principals with this policy can access AWS SSO within the AWS Organizations management account and all member accounts\. This principal can fully manage all AWS SSO operations, including the ability to create users, permission sets, and assignments\. The principal can also instantiate those assignments throughout the AWS organization member accounts and establish connections between AWS Directory Service managed directories and AWS SSO\. As new administrative features are released, the account administrator will be granted these permissions automatically\.

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
        "sso:*",
        "sso-directory:*",
        "ds:CreateAlias"
      ],
      "Resource": "*"
    }
  ]
}
```

### Additional information about this policy<a name="security-iam-awsmanpol-additional-info-AWSSSOMemberAccountAdministrator"></a>

AWS SSO administrators manage users, groups, and passwords in their SSO directory store \(sso\-directory\)\. The account admin role includes permissions for the following actions:
+ `"sso:*"`
+ `"sso-directory:*"`

AWS SSO administrators need limited permissions to the following AWS Directory Service actions to perform daily tasks\.
+ `"ds:DescribeTrusts"`
+ `"ds:UnauthorizeApplication"`
+ `"ds:DescribeDirectories"`
+ `"ds:AuthorizeApplication"`
+ `“ds:CreateAlias”`

These permissions allow AWS SSO administrators to identify existing directories and manage applications so that they can be configured for use with AWS SSO\. For more information about each of these actions, see [AWS Directory Service API permissions: Actions, resources, and conditions reference](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/UsingWithDS_IAM_ResourcePermissions.html)\.

AWS SSO uses IAM policies to grant permissions to AWS SSO users\. AWS SSO administrators create permission sets and attach polices to them\. The AWS SSO administrator needs to have the following permissions to list the existing policies so that they can choose which polices to use with the permission set they are creating or updating\.
+ `"iam:ListPolicies"`

AWS SSO administrators need limited access to the following AWS Organizations actions to perform daily tasks:
+ `"organizations:EnableAWSServiceAccess"`
+ `"organizations:ListRoots"`
+ `"organizations:ListAccounts"`
+ `"organizations:ListOrganizationalUnitsForParent"`
+ `"organizations:ListAccountsForParent"`
+ `"organizations:DescribeOrganization"`
+ `"organizations:ListChildren"`
+ `"organizations:DescribeAccount"`
+ `"organizations:ListParents"`

These permissions allow AWS SSO administrators the ability to work with organization resources \(accounts\) for basic SSO administrative tasks such as the following:
+ Identifying the management account that belongs to the organization
+ Identifying the member accounts that belong to the organization
+ Enabling AWS service access for accounts

For more information about how these permissions are used with AWS Organizations, see [Using AWS Organizations with other AWS services](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_integrate_services.html)

## AWS managed policy: AWSSSODirectoryAdministrator<a name="security-iam-awsmanpol-AWSSSODirectoryAdministrator"></a>

You can attach the `AWSSSODirectoryAdministrator` policy to your IAM identities\.

This policy grants administrative permissions over AWS SSO users and groups\. Principals with this policy attached can make any updates to AWS SSO users and groups\. The content of this policy statement is shown in the following snippet\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AWSSSODirectoryAdministrator",
            "Effect": "Allow",
            "Action": [
                "sso-directory:*",
                "sso:ListDirectoryAssociations"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSSSOReadOnly<a name="security-iam-awsmanpol-AWSSSOReadOnly"></a>

You can attach the `AWSSSOReadOnly` policy to your IAM identities\.

This policy grants read\-only permissions that allow users to view information in AWS SSO\. Principals with this policy attached cannot view the AWS SSO users or groups directly\. Principals with this policy attached cannot make any updates in AWS SSO\. For example, principals with these permissions can view AWS SSO settings, but cannot change any of the setting values\. The content of this policy statement is shown in the following snippet\.

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
                "sso:Describe*",
                "sso:Get*",
                "sso:List*",
                "sso:Search*",
                "sso-directory:DescribeDirectory"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSSSODirectoryReadOnly<a name="security-iam-awsmanpol-AWSSSODirectoryReadOnly"></a>

You can attach the `AWSSSODirectoryReadOnly` policy to your IAM identities\.

This policy grants read\-only permissions that allow users to view users and groups in AWS SSO\. Principals with this policy attached cannot view AWS SSO assignments, permission sets, applications or settings\. Principals with this policy attached cannot make any updates in AWS SSO\. For example, principals with these permissions can view AWS SSO users, but cannot change any of the user attributes or assign MFA devices\. The content of this policy statement is shown in the following snippet\.

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
                "sso-directory:Get*"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS SSO updates to AWS managed policies<a name="security-iam-awsmanpol-updates"></a>

View details about updates to AWS managed policies for AWS SSO since August 4, 2021\. For automatic alerts about changes to this page, subscribe to the RSS feed on the AWS SSO Document history page\.


| Change | Description | Date | 
| --- | --- | --- | 
| [AWSSSOMasterAccountAdministrator](#security-iam-awsmanpol-AWSSSOMasterAccountAdministrator) |  Add Organizations permissions that allow AWS SSO to create the AWS SSO service\-linked role in the organization's management account so that administrators can fully enable AWS SSO within the organization\. This policy also allows full access to sso\-directory permissions\.  | August 4, 2021 | 
| [AWSSSOMemberAccountAdministrator](#security-iam-awsmanpol-AWSSSOMemberAccountAdministrator) |  This policy also allows full access to sso\-directory permissions\.  | August 4, 2021 | 
| [AWSSSODirectoryAdministrator](#security-iam-awsmanpol-AWSSSODirectoryAdministrator) |  Add permissions that allow a principal to fully administer all AWS SSO configuration settings\.   | August 4, 2021 | 
| [AWSSSOReadOnly](#security-iam-awsmanpol-AWSSSOReadOnly) |  Add read\-only permissions that allow a principal to view AWS SSO configuration settings\.   | August 4, 2021 | 
| [AWSSSODirectoryReadOnly](#security-iam-awsmanpol-AWSSSODirectoryReadOnly) |  Add read\-only permissions that allow a principal to get individual AWS SSO directory resources\.  | August 4, 2021 | 
| AWS SSO started tracking changes | AWS SSO started tracking changes for AWS managed policies\. | August 4, 2021 | 