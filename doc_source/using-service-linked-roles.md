# Using Service\-Linked Roles for AWS SSO<a name="using-service-linked-roles"></a>

AWS Single Sign\-On uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to AWS SSO\. It is predefined by AWS SSO and includes all the permissions that the service requires to call other AWS services on your behalf\. For more information, see [Service\-Linked Roles](slrconcept.md)\.

A service\-linked role makes setting up AWS SSO easier because you don’t have to manually add the necessary permissions\. AWS SSO defines the permissions of its service\-linked role, and unless defined otherwise, only AWS SSO can assume its role\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\.

For information about other services that support service\-linked roles, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes **in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-Linked Role Permissions for AWS SSO<a name="slr-permissions"></a>

AWS SSO uses the service\-linked role named **AWSServiceRoleForSSO** to grant AWS SSO permissions to manage AWS resources, including IAM roles, policies, and SAML IdP on your behalf\.

The AWSServiceRoleForSSO service\-linked role trusts the following services to assume the role:
+ `AWS SSO`

The AWSServiceRoleForSSO service\-linked role permissions policy allows AWS SSO to complete the following on roles on the path “/aws\-reserved/sso\.amazonaws\.com/” and with the name prefix “AWSReservedSSO\_”:
+ `iam:AttachRolePolicy`
+ `iam:CreateRole`
+ `iam:DeleteRole`
+ `iam:DeleteRolePolicy`
+ `iam:DetachRolePolicy`
+ `iam:GetRole`
+ `iam:ListRolePolicies`
+ `iam:PutRolePolicy`
+ `iam:ListAttachedRolePolicies`

The AWSServiceRoleForSSO service\-linked role permissions policy allows AWS SSO to complete the following on SAML providers with name prefix as “AWSSSO\_”:
+ `iam:CreateSAMLProvider`
+ `iam:GetSAMLProvider`
+ `iam:UpdateSAMLProvider`
+ `iam:DeleteSAMLProvider`

The AWSServiceRoleForSSO service\-linked role permissions policy allows AWS SSO to complete the following on all organizations:
+ `organizations:DescribeAccount`
+ `organizations:DescribeOrganization`
+ `organizations:ListAccounts`

The AWSServiceRoleForSSO service\-linked role permissions policy allows AWS SSO to complete the following on all IAM roles \(\*\):
+ `iam:listRoles`

The AWSServiceRoleForSSO service\-linked role permissions policy allows AWS SSO to complete the following on “arn:aws:iam::\*:role/aws\-service\-role/sso\.amazonaws\.com/AWSServiceRoleForSSO”:
+ `iam:GetServiceLinkedRoleDeletionStatus`
+ `iam:DeleteServiceLinkedRole`

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-Linked Role Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Creating a Service\-Linked Role for AWS SSO<a name="create-slr"></a>

You don't need to manually create a service\-linked role\. When a user who is signed in with the AWS organization’s master account assigns access to an AWS account for the first time, AWS SSO creates the service\-linked role automatically in that AWS account\. 

**Important**  
If you were using the AWS SSO service before December 7, 2017, when it began supporting service\-linked roles, then AWS SSO created the AWSServiceRoleForSSO role in your account\. To learn more, see [A New Role Appeared in My IAM Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_roles.html#troubleshoot_roles_new-role-appeared)\.

If you delete this service\-link role and then need to create it again, you can use the same process to recreate the role in your account\.

## Editing a Service\-Linked Role for AWS SSO<a name="edit-slr"></a>

AWS SSO does not allow you to edit the AWSServiceRoleForSSO service\-linked role\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting a Service\-Linked Role for AWS SSO<a name="delete-slr"></a>

You don't need to manually delete the AWSServiceRoleForSSO role\. When an AWS account is removed from an AWS organization, AWS SSO automatically cleans up the resources and deletes the service\-linked role from that AWS account\.

You can also use the IAM console, the IAM CLI, or the IAM API to manually delete the service\-linked role\. To do this, you must first manually clean up the resources for your service\-linked role and then you can manually delete it\.

**Note**  
If the AWS SSO service is using the role when you try to delete the resources, then the deletion might fail\. If that happens, wait for a few minutes and try the operation again\.

**To delete AWS SSO resources used by the AWSServiceRoleForSSO**

1. [Remove User Access](useraccess.md#howtoremoveaccess) for all users and groups that have access to the AWS account\.

1. [Delete Permission Sets](howtoremovepermissionset.md) that you have associated with the AWS account\.

1. [Remove the IAM Identity Provider](idp.md#removeidp) to delete the trust between AWS SSO and the AWS account\.

**To manually delete the service\-linked role using IAM**

Use the IAM console, the IAM CLI, or the IAM API to delete the AWSServiceRoleForSSO service\-linked role\. For more information, see [Deleting a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.