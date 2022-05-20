# Delegated administration<a name="delegated-admin"></a>

Delegated administration provides a convenient way for assigned users in a registered member account to perform most AWS SSO administrative tasks\. When you enable AWS SSO, your SSO instance is created in the management account in AWS Organizations by default\. This was originally designed this way so that AWS SSO can provision, de\-provision, and update roles across all your organization's member accounts\. Even though your SSO instance must always reside in the management account, you can choose to delegate administration of AWS SSO to a member account in AWS Organizations, thereby extending the ability to manage AWS SSO from outside the management account\.

Enabling delegated administration provides the following benefits:
+ Minimizes the number of people who require access to the management account to help mitigate security concerns
+ Allows select administrators to assign users and groups to applications and to your organization's member accounts

For more information about how AWS SSO works with AWS Organizations, see [Manage SSO access to your AWS accounts](manage-your-accounts.md)\. For additional information and to review an example company scenario showing how to configure delegated administration, see [Getting started with AWS SSO delegated administration](https://aws.amazon.com/blogs/security/getting-started-with-aws-sso-delegated-administration/) in the *AWS Security Blog*\.

## What tasks can be performed in the delegated administrator account<a name="delegated-admin-tasks-member-account"></a>

To configure delegated administration you must first register a member account in your AWS organization as a delegated administrator, users in that member account who have sufficient permissions will have administrative access to AWS SSO\. After a member account has been successfully registered for delegated administration, it can then be referred to as the delegated administrator account\.

The following table describes the administrative tasks available for a delegated administrator account compared to a management account\. 


| AWS SSO administrative tasks |  **Delegated administrator account**  | Management account | 
| --- | --- | --- | 
|  Add, edit, or delete users or groups  | X | X | 
|  Enable or disable user access  | X | X | 
| Enable, disable, or manage incoming attributes | X | X | 
| Change or manage identity sources | X | X | 
| Create, edit, or delete applications | X | X | 
| Configure MFA | X | X | 
| Manage permission sets not provisioned in the management account | X | X | 
| Manage permission sets provisioned in the management account |  | X | 
| Enable AWS SSO |  | X | 
| Delete AWS SSO configuration |  | X | 
| Enable or disable user access in the management account |  | X | 
| Register or deregister a member account as a delegated administrator |  | X | 

## Best practices<a name="delegated-admin-best-practices"></a>

Here are some best practices to consider before you configure delegated administration\.
+ **Grant least privilege to the management account** – Knowing that the management account is a highly privileged account and to adhere to the principal of least privilege, we highly recommend that you restrict access to the management account to as few people as possible\. The delegated administrator feature is intended to minimize the number of people who require access to the management account\. 
+ **Create permission sets for use only in the management account** – This makes it easier to administer permission sets tailored just for users accessing your management account and helps to differentiate them from permission sets managed by your delegated administrator account\. 
+ **Consider your Active Directory location** – If you plan on using Active Directory as your AWS SSO identity source, locate the directory in the member account where you have enabled the AWS SSO delegated administrator feature\. If you decide to change the AWS SSO identity source from any other source to Active Directory, or change it from Active Directory to any other source, the directory must reside in \(be owned by\) the AWS SSO delegated administrator member account if one exists; otherwise, it must be in the management account\.

## Prerequisites<a name="delegated-admin-prereqs"></a>

Before you can register an account as a delegated administrator you must first have the following environment deployed:
+ AWS Organizations must be enabled and configured with at least one member account in addition to your default management account\. 
+ If your identity source is set to Active Directory, the [AWS SSO configurable AD sync](provision-users-from-ad-configurable-ADsync.md) feature must be enabled\.

**Note**  
If your AWS SSO configuration was enabled prior to November 2019 and you have not yet enabled access to other accounts in AWS Organizations, you might see an info alert in the console to enable access to AWS SSO for a member account in your organization\. To provide a registered delegated administrator access to the users/groups and to setup entitlements you have to [Enable AWS SSO\-integrated applications in AWS accounts](app-enablement.md#enable-app-enablement)\. If your AWS SSO configuration was enabled after November 2019, there is nothing more for you to do because access to accounts in your organization were automatically enabled by AWS\.

## Register a member account<a name="delegated-admin-how-to-register"></a>

AWS SSO only supports registering one member account as a delegated administrator at a time\. You can only register a member account while signed in with credentials from the management account\.

Use the following procedure to grant administrative access to AWS SSO by registering a specific member account in your AWS organization as a delegated administrator\.

**Important**  
This operation delegates AWS SSO administrative access to admin users in this member account\. All users who have sufficient permissions to this delegated administrator account can perform all AWS SSO administrative tasks from the account, except for: enabling AWS SSO, deleting AWS SSO configurations, managing permission sets provisioned in the management account, registering or deregistering other member accounts as delegated administrators, or enabling or disabling user access in the management account\.

**To register a member account**

1. Sign in to the AWS Management Console using the credentials of your management account in AWS Organizations\. Management account credentials are required to run the [RegisterDelegatedAdministrator](https://docs.aws.amazon.com/organizations/latest/APIReference/API_RegisterDelegatedAdministrator.html) API\.

1. Select the Region where AWS SSO is enabled, and then open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**, and then select the **Management** tab\.

1. In the **Delegated administrator** section, choose **Register account**\.

1. On the **Register delegated administrator** page, select the AWS account you want to register, and then choose **Register account**\.

## Deregister a member account<a name="delegated-admin-how-to-deregister"></a>

You can only deregister a member account while signed in with credentials from the management account\.

Use the following procedure to remove administrative access from AWS SSO by deregistering a member account in your AWS organization that had previously been designated as a delegated administrator\.

**Important**  
When you deregister an account, you effectively remove the ability for all admin users to manage AWS SSO from that account\. As a result, they can no longer administer AWS SSO identities, access management, authentication, or application access from this account\. This operation will not affect any permissions or assignments configured in AWS SSO and therefore will have no impact on your end users as they will continue to have access to their apps and AWS accounts from within the user portal\.

**To deregister a member account**

1. Sign in to the AWS Management Console using the credentials of your management account in AWS Organizations\. Management account credentials are required to run the [DeregisterDelegatedAdministrator](https://docs.aws.amazon.com/organizations/latest/APIReference/API_DeregisterDelegatedAdministrator.html) API\.

1. Select the Region where AWS SSO is enabled, and then open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**, and then select the **Management** tab\.

1. In the **Delegated administrator** section, choose **Deregister account**\.

1. In the **Deregister account** dialog, review the security implications, and then enter the name of the member account to confirm that you understand\. 

1. Choose **Deregister account**\.

## View which member account has been registered as the delegated administrator<a name="delegated-admin-how-to-view-member-account"></a>

Use the following procedure to find which member account in your AWS Organizations has been configured as the delegated administrator for AWS SSO\.

**To view your registered member account**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\. 

1. In the **Details** section, locate the registered account name under **Delegated administrator**\. You can also locate this information by selecting the **Management** tab, and viewing it under the **Delegated administrator** section\.