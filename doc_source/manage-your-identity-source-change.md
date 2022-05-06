# Change your identity source<a name="manage-your-identity-source-change"></a>

You can change where you store users at any time\. Use the following procedure to switch from a directory that AWS SSO provides \(the default\) to an external identity provider, AWS Managed Microsoft AD directory, or the other way around\. Before you proceed, review the information in [Considerations for changing your identity source](manage-your-identity-source-considerations.md)\.

**To change your identity source**

1. Open the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab\. Choose **Actions**, and then choose **Change identity source**\.

1. Under **Choose identity source**, select the source that you want to switch to, and then choose **Next**\. 

   If you are switching to a Microsoft AD directory, you must choose the available directory from the menu on the next page\. 
**Important**  
Changing your identity source to or from Active Directory removes all existing user and group assignments\. After you change your identity source, you must manually reapply assignments\.

   If you are switching to an external identity provider, we recommend that you follow the steps in [How to connect to an external identity provider](manage-your-identity-source-idp.md#how-to-connect-idp)\.

1. After you read the disclaimer and are ready to proceed, type **ACCEPT**\.

1. Choose **Change identity source**\. If you are changing your identity source to Active Directory, proceed to the next step\.

1. Changing your identity source to Active Directory takes you to the **Settings** page\. On the **Settings** page, do either of the following:
   + Choose **Start guided setup**\. For information about how to complete the guided setup process, see [Guided setup](provision-users-from-ad-configurable-ADsync.md#manage-sync-guided-setup-configurable-ADsync)\.
   + In the **Identity source **section, choose **Actions**, and then choose **Manage sync** to configure your *sync scope*, the list of users and groups to sync\.