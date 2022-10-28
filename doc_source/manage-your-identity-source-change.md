# Change your identity source<a name="manage-your-identity-source-change"></a>

The following procedure describes how to change from a directory that IAM Identity Center provides \(the default Identity Center directory\) to Active Directory or an external identity provider, or the other way around\. Before you proceed, review the information in [Considerations for changing your identity source](manage-your-identity-source-considerations.md)\. Depending on your current deployment, this change might remove any user and group assignments that you configured in IAM Identity Center\. If this occurs, all users, including the administrative user in IAM Identity Center, will lose single sign\-on access to their AWS accounts and applications\.

**To change your identity source**

1. Open the [IAM Identity Center console](https://console.aws.amazon.com/singlesignon)\.

1. Choose **Settings**\.

1. On the **Settings** page, choose the **Identity source** tab\. Choose **Actions**, and then choose **Change identity source**\.

1. Under **Choose identity source**, select the source that you want to change to, and then choose **Next**\. 

   If you are changing to Active Directory, choose the available directory from the menu on the next page\. 
**Important**  
Changing your identity source to or from Active Directory deletes users and groups from the Identity Center directory\. This change also removes any assignments that you configured in IAM Identity Center\.

   If you are switching to an external identity provider, we recommend that you follow the steps in [How to connect to an external identity provider](manage-your-identity-source-idp.md#how-to-connect-idp)\.

1. After you read the disclaimer and are ready to proceed, type **ACCEPT**\.

1. Choose **Change identity source**\. If you are changing your identity source to Active Directory, proceed to the next step\.

1. Changing your identity source to Active Directory takes you to the **Settings** page\. On the **Settings** page, do either of the following:
   + Choose **Start guided setup**\. For information about how to complete the guided setup process, see [Guided setup](provision-users-from-ad-configurable-ADsync.md#manage-sync-guided-setup-configurable-ADsync)\.
   + In the **Identity source **section, choose **Actions**, and then choose **Manage sync** to configure your *sync scope*, the list of users and groups to sync\.