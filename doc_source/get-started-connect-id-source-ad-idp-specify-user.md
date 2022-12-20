# Connect Active Directory or an external IdP and specify a user<a name="get-started-connect-id-source-ad-idp-specify-user"></a>

If you're already using Active Directory or an external identity provider \(IdP\), the following topics will help you connect your directory to IAM Identity Center\.

You can connect an AWS Managed Microsoft AD directory, a self\-managed directory in Active Directory, or an external IdP with IAM Identity Center\. If you plan to connect an AWS Managed Microsoft AD directory or a self\-managed directory in Active Directory, make sure that your Active Directory configuration meets the prerequisites in [Active Directory or an external IdP](get-started-prereqs-considerations.md#prereqs-active-directory-idp-identity-source)\.

**Note**  
As a security best practice, we strongly recommend that you enable multi\-factor authentication\. If you plan to connect an AWS Managed Microsoft AD directory or a self\-managed directory in Active Directory and you're not using RADIUS MFA with AWS Directory Service, enable MFA in IAM Identity Center\. If you plan to use an external identity provider, note that the external IdP, not IAM Identity Center, manages MFA settings\. MFA in IAM Identity Center is not supported for use by external IdPs\. For more information, see [Enable MFA](mfa-enable-how-to.md)\. 

**AWS Managed Microsoft AD**

1. Review the guidance in [Connect to a Microsoft AD directory](manage-your-identity-source-ad.md)\.

1. Follow the steps in [Connect a directory in AWS Managed Microsoft AD to IAM Identity Center](connectawsad.md)\.

1. Configure Active Directory to synchronize the user to whom you want to grant administrative permissions into IAM Identity Center\. For more information, see [Synchronize an administrative user into IAM Identity Center](#sync-admin-user-from-ad)\.

**Self\-managed directory in Active Directory**

1. Review the guidance in [Connect to a Microsoft AD directory](manage-your-identity-source-ad.md)\.

1. Follow the steps in [Connect a self\-managed directory in Active Directory to IAM Identity Center](connectonpremad.md)\.

1. Configure Active Directory to synchronize the user to whom you want to grant administrative permissions into IAM Identity Center\. For more information, see [Synchronize an administrative user into IAM Identity Center](#sync-admin-user-from-ad)\.

**External IdP**

1. Review the guidance in [Connect to an external identity provider](manage-your-identity-source-idp.md)\.

1. Follow the steps in [How to connect to an external identity provider](manage-your-identity-source-idp.md#how-to-connect-idp)\.

1. 

   Configure your IdP to provision users into IAM Identity Center\. 
**Note**  
Before you set up automatic, group\-based provisioning of all your workforce identities from your IdP into IAM Identity Center, we recommend that you sync the one user to whom you want to grant administrative permissions into IAM Identity Center\.

## Synchronize an administrative user into IAM Identity Center<a name="sync-admin-user-from-ad"></a>

After you connect your directory to IAM Identity Center, you can specify a user to whom you want to grant administrative permissions, and then synchronize that user from your directory into IAM Identity Center\.

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab, choose **Actions**, and then choose **Manage Sync**\.

1. On the **Manage Sync** page, choose the **Users** tab, and then choose **Add users and groups**\.

1. On the **Users** tab, under **User**, enter the exact user name and choose **Add**\.

1. Under **Added Users and Groups**, do the following:

   1. Confirm that the user to whom you want to grant administrative permissions is specified\.

   1. Select the check box to the left of the user name\.

   1. Choose **Submit**\.

1. In the **Manage sync** page, the user that you specified appears in the **Users in sync scope** list\.

1. In the navigation pane, choose **Users**\.

1. On the **Users** page, it might take some time for the user that you specified to appear in the list\. Choose the refresh icon to update the list of users\. 

**Next step: Create an administrative permission set** 

At this point, your user doesn't have access to the management account\. You will set up administrative access to this account by creating an administrative permission set and assigning the user to that permission set\. For more information, see [Step 3: Create an administrative permission set](get-started-create-an-administrative-permission-set.md)\.